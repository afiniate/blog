---
layout: post
title: On Why Common Smartphones Have "Better" Cameras Than Curiosity and the Design and Engineering of Systems
---

{{ page.title }}
================

We viewed the landing of Curiosity on Mars with awe and pride, just as
everyone around the the world has. As engineers ourselves, we may have
a perspective into this accomplishment that the general public
doesn't. Whoever thought to culminate the
[Entry, Descent, and Landing (EDL)](http://mars.jpl.nasa.gov/msl/mission/timeline/edl/)
with that [hovering sky crane maneuver](http://youtu.be/_KLxmGLZQSY)
had to be *absolutely crazy*! We mean that as the best possible
engineering compliment. Complicated requirements - such as the need to
land with precision and to protect the instruments from dust - drove
the development of that design, not an unnecessary flair for the
fanciful.

Unfortunately, there is a meme floating around, explaining that common
smartphones have a "better" cameras than Curiosity because of
government incompetence. This appears to be due to a misunderstanding
of a
[DPReview article](http://www.dpreview.com/news/2012/08/08/Curiosity-interview-with-Malin-Space-Science-Systems-Mike-Ravine),
where Mark Raving from Malin Space Science *Systems* (emphasis ours -
you'll see why) is quoted to have said, "These designs were proposed
in 2004, and you don't get to propose one specification and then go
off and develop something else".

A natural question is "Why not go develop something else, if 'better'
options become available?" Some have asserted the inability to put
up-to-date cameras on Curiosity is evidence of unresponsive
governmental processes and wasteful bureaucratic incompetence. In this
case, that explanation in incorrect, indicating a inadequate
understanding of the challenges behind designing, building, and
operating highly reliable systems.

##Because, it's about SYSTEMS, silly!##

10io is fortunate to have people how have been involved in the design,
development, and building of:

- high frequency trading *systems*
- financial exchange *system*
- large scale build *systems*
- fleet deployment *systems*
- interactive television *systems*
- digital media distribution *systems*
- logistics management *systems*
- healthcare management information *systems*
- semi-autonomous spaced-based tele-robotic *systems* (It's true!)
- real-time data stream analysis *systems*
- complex event processing *systems*

Why do we keep emphasizing *system*? Because it's the key to
understanding why Curiosity was sent to another planet with a 2MP
camera while 8MP cameras sit in our pockets here on Earth.

So, what is a system? To quote
["Thinking in Systems: A Primer"](http://www.chelseagreen.com/bookstore/item/thinking_in_systems:paperback/)
by Donella H. Meadows,

> A system isn't just any old collection of things. A system is an
> interconnected set of elements that is coherently organized in a way
> that achieves something. If you look at that definition for a
> minute, you can see that a system must consist of three kinds of
> things: elements, interconnections, and a function or purpose.

Designing and building systems that work reliably here on Earth is
challenging. One need not look any further than recent system failures
like that experience by Amazon.com's East Coast data centers, or
Knights Capital's algorithmic trading systems. Designing *systems*
that work in space? That's not rocket science. That's HARDER than
rocket science.

##No rover is an island##

Consider that the
[Mars Science Laboratory (MSL)](http://mars.jpl.nasa.gov/msl/mission/overview/)
program required
[five major subsystems](http://en.wikipedia.org/wiki/Mars_Science_Laboratory)
to be launched into space:

- [Launch vehicle](http://mars.jpl.nasa.gov/msl/mission/launchvehicle/)
- [Spacecraft](http://mars.jpl.nasa.gov/msl/mission/spacecraft/)
- [Entry, Descent, and Landing (EDL) Configuration](http://mars.jpl.nasa.gov/msl/mission/spacecraft/edlconfig/)
- [Rover (i.e., "Curiosity")](http://mars.jpl.nasa.gov/msl/mission/rover/)
- [Instruments (i.e., cameras, et al)](http://mars.jpl.nasa.gov/msl/mission/instruments/)
- [Communications with Earth](http://mars.jpl.nasa.gov/msl/mission/communicationwithearth/)

This list is just what was required to get Curiosity to Mars, and
doesn't include the NASA systems that support MSL here on Earth (like
the [Deep Space Network](http://deepspace.jpl.nasa.gov/dsn/)). A
camera is just one component of the many subsystems required for MSL
to successfully complete it's mission.

So, when Ravine is quoted as saying, "These designs were proposed in
2004, and you don't get to propose one specification and then go off
and develop something else", he's not referring to the strictures of
some "laboriously approved government spec", as has been contended in
other forums. It's an acknowledgment of a truism of implementing
systems: That even small, seemingly innocuous changes in one subsystem
can have an out-sized - usually catastrophic - effect on the entire
system.

When one spends $2.5B to send hardware 350 million miles away to
another planet, to operate at the end of a noisy, unreliable wireless
tether of limited bandwidth that can take as long as
80-minutes-round-trip, without hope of repair, one must ensure the
entire system is
tested... validated... retested... revalidated... retested... revalidated... retested... revalidated... retested... revalidated... retested... revalidated... retested... revalidated... retested... revalidated...

And, retested and revalidated, again.

##Constrained by an Iron Triangle##

Every engineer knows the three dimensions that form the
"[iron triangle](http://en.wikipedia.org/wiki/Project_management_triangle)"
in the development of every project: Resources, Schedule, and
Specification. These three dimensions are interdependent. If you want
to manage for Quality, you have manage all three. If you're developing
Mars Science Laboratory, with fixed Resources (budget), and fixed
Schedule (a set launch window), you *have* to fix the Specification,
or else lose control of its Quality, and introduce quantifiable risk
to the budget (overruns; cancellation) and to the schedule (missing
the launch window; cancellation), and unknowable, unquantifiable risks
to MSL itself (i.e. failure modes).

The only inexcusable waste would be spend $2.5B to send hardware 350
million miles away to another planet, to operate at the end of a
noisy, unreliable wireless tether of limited bandwidth that can take
as long as 80-minutes-round-trip, without hope of repair... and have
it not work.

It *is* interesting that NASA explored movie director (and MSL team
member, apparently) James Cameron's notion to ""re-start the zoom
project", but not surprising that it was shelved in the end. Cameron
is a beast, and we love that he's so involved in pushing the
boundaries of both Earth and space exploration with both his technical
experience and financial resources, even if this 3D camera on
Curiosity business smells a bit of a vanity project for
him. Introducing that big a change, that late in development, meant
that the 3D cameras would not have undergone all required system level
retesting and re-validations. NASA should be commended, not vilified,
for not shortcutting the process.

Whether you are here on Earth providing IT services, or executing
financial transactions, or driving sales and managing customer
relationships, or monitoring healthcare outcomes, or sending probes
out to explore space, remember that your business and your technology
are complicated systems that need to be carefully design, built,
deployed and operated - and continually tested and validated - for its
interconnection to, and interdependence of, other complicated systems.

No system - even a rover sent to explore other planets - is an
island. Don't think about, or treat them, like they are.

## Other viewpoints ##

Eric has a viewpoint differs on this subject, better to say it agrees
at the tactical level and differs at the meta level. He will be
posting about that next week.
