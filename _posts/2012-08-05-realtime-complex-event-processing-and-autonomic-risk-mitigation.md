---
layout: post
title: Real-time Complex Event Processing And Autonomic Risk Mitigation
---

{{ page.title }}
================

  People have been watching the events at Knights Capital unfold over
the past week. A loss of $440M and the potential failure of yet
another financial services firm is both mesmerizing and
vexing. Mainstream media attributes this, perhaps simplistically, to
"software error". It is worth noting, however, that catastrophic
failures like this are almost never attributable to a single bug, but
rather a string of compounding systemic failures.

Those of us on the outside will probably never know the details of the
business and technical decisions that resulted in Knight Capital's
predicament. But we can make some educated guesses based on failures
of other similarly complex systems. In this case, there were at least
three areas of failure: a bug in the high frequency trading software
that caused the run away trading; the lack of an obvious "kill switch"
to stop trading once it got out of hand; and, perhaps most critically,
the lack of position management and risk controls.

It is impossible to develop bullet-proof trading software. The
non-correlated nature of the data makes it difficult to manage
position and risk to determine when to employ the "kill switch". In
addition, while it is necessary to building adequate controls into the
algorithms of trading software, this may not be sufficient to prevent
unacceptably risky scenarios from developing. If multiple trading
platforms are running different algorithms in parallel, each can
manage its internal risk properly and still expose the firm to high
levels of risk across trading systems.

However, it is not impossible to mitigate risk across algorithms and
trading platforms.  John Bates, CTO at Progress Software, recently
said, "You need an algorithm to monitor the trading algorithm."
(http://articles.chicagotribune.com/2012-08-03/business/sns-rt-us-knightcapital-loss-dealerresponsebre87300h-20120803_1_bats-global-markets-glitches-systems)

We agree. That's why we built Autonomic I/O.

[Warning: Start of obligatory tech talk!]

We developed Autonomic I/O to address a fundamental "Big Data"
requirement: create a complex event processing/datastream analysis
solution that can scale to handle arbitrarily large amounts of data
and arbitrarily complex events with little need for human
intervention. These are the characteristics of a risk engine that
financial services and trading firms need.

Autonomic I/O is very different from what is standard in the
industry. Autonomic I/O is a system of homogeneous nodes that self
distribute and self manage according to a small set of simple rules.
This gives us an emergent behavior that enables the system to grow and
shrink automatically to meet the demands placed upon it. That is, it
can take advantage of all the hardware you throw at it to get faster
and, to some extent smarter. On top of this, we built our complex
event processing Engine that follows and builds on these same
principles: Simple rules applied consistently on each node in the
cloud produces an emergent desirable result.

[End of obligatory tech talk - Whew!]

All of that was to say that Autonomic I/O has the ability to extract
meaningful knowledge from large amounts of data in real time, and act
on them automagically; exactly what was needed to avoid the events at
Knights Capital.

Well, almost but not quite. We have been building Autonomic I/O to
address specific needs in other industries (healthcare management,
customer relationship management, IT operations). The one trading
platform-specific piece we need to add to our system is an algorithmic
component. Autonomic I/O looks for patterns in real-time data streams,
but it doesn't (yet) do financial calculations to augment the raw
data. Combining the complex event processing/data stream analysis
engine with an algorithmic component is exactly what is needed for a
trading platform risk engine.

Fortunately, we did our work well. We have a very good basis to build
distributed systems on. We are designing and building a algorithm
engine that fits in our existing framework.  When combined with our
compliance engine, trading firms will have the tools they need to
manage all kinds of risk across all their business units and all their
trading platforms.
