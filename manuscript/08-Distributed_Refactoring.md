# Distributed Refactoring To Ease Drift

Microservices made the monolith crumble into many different services,
but with this division many cross-cutting concerns that were in the
same codebase now require to interact with more codebases at the same
time possibly creating duplication and drift. This chapter will
describe ways to discover the state of the codebases and drift along
techniques and patterns to tackle these problems.

## Typical Drift Scenario

The most common scenario for microservice drift is any form of shared
library. In the chapter about Pipelines you can find that paved road
to production pipelines are very useful to standarize microservices
deployments. But they come with drawbacks such as Drift. Over time,
pipeline versions pinned to each microservice will start to differ
unless you are on a tag pointing always to latest.

Once the shared pipeline library starts to incorporate more features,
services that stay on a particular version won't be deployable over
time. For example, if the pipeline introduced security scanning, many
projects will fail the first time or eventually if they do not update
their dependencies due to new security vulnerabilities. This is a
form of _distributed technical debt_.

Other microservices will become more stable over time and while
development may have halted, they still need to incorporate
cross-cutting concerns over time to accomodate new platform features.
There are two commonly accepted approaches on these kind of scenarios:

1. The "If it's not broken, don't fix it" approach.
1. Deal with the pain and update everything as soon as possible
1. Share nothing
1. Use distributed refactoring

The first approach is basically a ticking time bomb waiting to happen.
Due to the organic nature of software, mainteinance will keep
microservices from being continuously delivered over time.

The second approach is also possible but with dozens of microservices,
teams and products being developed on parallel, many times schedules
and releases are not options. For example, having pipelines enforcing
policies and applied them from one day to another will cause havok
on many organizations. Imagine if releasing a pipeline version will
crash all the microservices unless they all fix the problem. This
might be a minor problem on some services but it would take various
hours of development on most of them and I have seen this happen many
times.

The third approach could guarantee that services share nothing or very
little among them but it will lead to a lot of teams trying to solve
the same problem on different ways. Promoting this approach would be
troublesome to say the least because many implementations of the same
solving strategy will lead to more drift.

Finally, the fourth approach is to make refactoring available to all
projects at once but allowing teams to be independently updated over
time without forcing the update at once. Possibly many teams can take
the change quickly wihtout problems but other teams might delay it.
This is alright as long as they are aware of the change.




## Measure Drift To Drive Consolidation

The first recommended step to drive convergence is to measure Drift.
But drift is an all-encompassing concept that is also very hard to
measure if you do not divide it on various types of drift.

### Measure Configuration Drift


## Conclusion

The chapter described the reasoning to apply distributed refactoring
and how to measure drift to drive consolidation. The chapter also
explained some of the tools available to apply distributed refactoring
to existing codebases.

[1]: https://en.wikipedia.org/wiki/Single_responsibility_principle
