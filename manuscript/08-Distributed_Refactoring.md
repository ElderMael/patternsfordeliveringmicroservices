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
