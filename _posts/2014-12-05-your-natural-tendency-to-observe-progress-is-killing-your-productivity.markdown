---
layout: post
title:  "Your Natural Tendency to Observe Progress is Killing Your Productivity"
date:   2014-12-05 12:13:26
categories: vim productivity
meta: "Humans seem predisposed to observe movement and progression, so we actively fight great productivity strategies in daily work"
---
I recently watched a [talk by Ben Orenstein][ben] about bringing your Vim
proficiency to the next level. A quick poll of the audience revealed that many
(if not most) of the Vim users present self-identified at a low-intermediate skill
level with the editor, and Ben went on to discuss several habits that prevent
many developers from advancing further:

- Navigation with the arrow keys/mouse
- Slow file selection (e.g. using visual file trees)
- Scrolling within files by holding "down"
- Editing text using incremental character movements and visual mode instead of
  text objects and verbs

These suboptimal strategies all seem closely related to me in that each
represents a form of visual movement (Progress) towards the end goal
where a faster search-based Jump option is available.

To take the scrolling example, we seem predisposed to this physically analogous "walking"
through the file even when we know the exact sequence of characters we want and
could execute a Vim string match must faster. I think many would argue that the
process of navigating to our target location here is more or less the same,
with the former strategy simply being a slower version of the latter since it
doesn't take advantage of a speed enhancement tool (Vim's character matching).
But these strategies are undertaken with fundamentally different states of
mind.

The first strategy is an example of a **Progress-driven approach**. You are
undertaking an exploratory endeavor that allows your brain to process the
topology of the document and the context in which you will ultimately find
yourself, and to put all of this contextual information along a timeline of
events (you were here, then you were here, and that's how you got here).

The second strategy is an example of an information-driven **Jump approach**. You
incorporate knowledge of your environment (in this case the document) and the
tools at hand (Vim) to circumvent the progression altogether. The result is
landing in the same place without witnessing the transition state.

### Ok so what, who cares?

The more I thought about this idea of a Progress vs Jump mindset, the more its
relevance seemed to expand out of Vim into other daily work-flows. Take a
Google search for example. If you know what you are looking for generally it is
the first search result (and in many cases I know for a fact it will be).
Yet how often do I use the "I'm feeling lucky" button? Never. It's not like
using that button has never occurred to me, but something in my psychology
prefers navigating to the first result through the results page. At the risk of
over-extrapolating, consider how distrustful we are of snap
judgements (see Malcom Gladwell's "Blink") and how often you peruse the entire
menu of your favorite restaurant despite already knowing your order.

My point isn't that the Jump mindset is always better, but rather that it is
necessary if productivity is the goal. And we appear to be naturally inclined against
it. So what makes us unconsciously shy away from Jump strategies?

- **Distrust in tools.** I don't use the search bar in the OSX Finder; instead I
  navigate folder by folder (if I find myself in the Finder at all).
  Why? I've lost faith in the Finder search bar's ability to find what
  I'm looking for, since it never seems to work. Jump strategies require a lot
  of trust in the tools enabling the jump, and the pervasiveness of crappy tools
  has created a culture of distrust with respect to software at large.
- **Uncertain information.** There is a certain amount of contextual
  information you need to have in your working memory for a Jump strategy to
  work: You need prior exposure to the context and confidence in your
  recollection of it. There is a comforting surety in the Progress approach that
  trumps the productivity benefits of Jump in unconscious thought almost every
  time due to a lack of confidence in your own memory (the chicken wraps are
  the lunch special on Tuesdays right? Or was it fish tacos...better check).
- **Preference for deferred effort.** A Jump strategy requires more thought up front (e.g.
  figuring out line numbers in a relative Vim command vs. highlighting in visual
  mode). We tend to favor the easier immediate path even if the end result will
  be more work.
- **Concern about personal limitation.** Maybe this one is just me, but for some
  reason I intuitively feel like there is an upper bound on the number of hotkeys
  and shortcuts I can remember. I think this is related to general inertia in
  the learning process; we tend to shy away from things we don't currently know
  in favor of the things we do, so learning alternative ways of doing things
  requires conscious effort.

When I'm trying to maximize productivity I've been making a conscious effort to
identify those four hurdles, and recognize if I'm making Progress decisions
when a Jump option is available---I've sped up a good number of my daily
processes already.

[ben]: https://www.youtube.com/watch?v=SkdrYWhh-8s
