---
layout: post
title:  "Improving RSpec Test Clarity With YAML Expectations"
date:   2014-11-28 12:13:26
categories: ruby testing rspec
meta: "An experiment using YAML instead of nested contexts to test a method with many corner cases."
---
We've been working on a new text matching module that takes any user-supplied address
(`'123 Madeup Lane'`) and determines whether it matches against any given sample
text (`'<b>123</b> Madeup Ln'`). Our class is called `AddressToTextMatcher`
and the initializer accepts strings `address` and `sample_text`, then provides
a public `exact_match?` that returns a boolean value.

What makes this module interesting after going through a few rounds of Ping Pong
Pairing is that the magnitude of test code is vastly outpacing the production
code, because the matcher is mostly taking advantage of `gsub` and regex logic that can be
condensed into concise single lines whereas the tests are accounting for lots of
corner cases that we want to test discretely. The raw test code (no refactoring
yet) looks like this:

{% highlight ruby %}
describe AddressToTextMatcher do
  describe "#exact_match?" do
    context 'the address matches the text exactly' do
      it 'returns true' do
        address = "123 Madeup Lane"
        text = "123 Madeup Lane"
        match_result = AddressToTextMatcher.new(address, text).exact_match?
        expect(match_result).to be true
      end
    end
    context 'the address differs from text by one number' do
      context 'the number is internal to the address' do
        it 'returns false' do
        address = "123 Madeup Lane"
        text = "124 Madeup Lane"
        match_result = AddressToTextMatcher.new(address, text).exact_match?
        expect(match_result).to be false
      end
    end
    context 'the number is part of the surrounding text' do
      it 'returns false' do
        address = "23 Madeup Lane"
        text = "123 Madeup Lane"
        match_result = AddressToTextMatcher.new(address, text).exact_match?
        expect(match_result).to be false
      end
    end
  end
  context 'abbreviations are present' do
    context 'the text contains an abbreviated form of the address' do
      it 'returns true' do
        address = '123 Madeup Lane'
        text = '123 Madeup Ln'
        match_result = AddressToTextMatcher.new(address, text).exact_match?
        expect(match_result).to be true
      end
    end
 ...
{% endhighlight %}

So far we have about 20 lines of production code and 150 lines of test code.
Generally you expect the two to more or less to approach each other over time as
the tests start benefiting from reuse opportunities, but in this case
my sense is that the gap will only widen as we discover and add corner cases
to the tests that only require minor changes to the matching logic. We could
try to condense the tests, accounting for multiple cases in each
one and adding shared examples to clean up the repetitive exercise/expect
lines at the end of every `it` block.

But I like having each case tested in relative isolation, so what I really want is a
more organized, succinct way to add a bunch of corner cases/contexts and keep
them organized easily without scrolling through piles of nested `context` blocks.
I want something like this:

{% highlight yaml %}
'the address matches the text exactly':
  text: '123 Madeup Lane'
  address: '123 Madeup Lane'
  result: true

'the address differs from text by one number':
  'the number is internal to the address':
    address: '123 Madeup Lane'
    text: '124 Madeup Lane'
    result: false
  'the number is part of the surrounding text':
    address: '23 Madeup Lane'
    text: '123 Madeup Lane'
    result: false

'abbreviations are present':
  'the text contains an abbreviated form of the address':
    address: '123 Madeup Lane'
    text: '123 Madeup Ln'
    result: true
...
{% endhighlight %}

So I set about hacking together something that would read YAML in this format
and generate the necessary RSpec contexts/expectations. This is what I came up
with:

{% highlight ruby %}
class YamlExpector

  def initialize(yaml_expectations_filename, describe_instance)
    @expectations = YAML.load_file(yaml_expectations_filename)
    @file_lines = File.readlines(yaml_expectations_filename)
    @describe_instance = describe_instance
  end

  def expect_all!
    @expectations.each do |top_level_context, within_context|
      expectation_from_yaml(top_level_context, within_context)
    end
  end

  def expectation_from_yaml(context_description, within_context)
    this = self
    if within_context['result'].nil?
      @describe_instance.context context_description do
        within_context.each do |subcontext_description, within_subcontext|
          this.expectation_from_yaml(subcontext_description, within_subcontext)
        end
      end
    else
      @describe_instance.context context_description do
        it "returns #{within_context['result']}" do
          address, sample_text = within_context['address'], within_context['text']
          result = AddressToTextMatcher.new(address, sample_text).exact_match?
          expected_result = within_context['result']
          expect(result).to be(expected_result), lambda {
            line = this.line_of_context_in_file(self.class.description)
            %Q{
              Failure in YAML expectation on line #{line}:
                Expected #{expected_result} and got #{result}
            }
          }
        end
      end
    end
  end

  def line_of_context_in_file(context)
    @file_lines.each_with_index do |line, i|
      return i + 1 if line =~ Regexp.new(context)
    end
  end

end
{% endhighlight %}

Here's the retrospective:

### The Good

The obvious win here is twofold. First, the spec for the matcher class now
looks like this:


{% highlight ruby %}
require_relative 'yaml_expector'

describe AddressToTextMatcher do
  describe '#exact_match?' do
    yaml_expector = YamlExpector.new('exact_match_expectations.yaml', self)
    yaml_expector.expect_all!
  end
end
{% endhighlight %}

That is great, and I get to use the YAML format described above to articulate
all of the test cases I want in a super readable and extendible format.

### The Bad

There are a few things that immediately come to mind as inherent setbacks.
First, I like using my vim-rspec plugin to run individual tests, which isn't
possible without further modifications to `YamlExpector`. It also
isn't an obvious win from a code magnitude perspective, since the new class is
around 50 lines and the YAML definitions still require 80 lines of (albeit much
more readable) declarations. And this non-traditional approach adds some
complexity and DSL where it isn't absolutely necessary.

### The Ugly

Obviously, the `YamlExpector` class will need some further
refactoring/abstraction/optimization to be reusable. Right now it is very
closely coupled with testing expectations of a single method on a single class,
so there is significant work yet to be done if we want to keep this strategy in
our test suite.

Overall I'm going to relish the new expectation declaration format and keep an
eye out for unintended consequences as we move forward with the module.
