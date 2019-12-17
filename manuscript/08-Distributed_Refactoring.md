# Distributed Refactoring To Ease Drift

Microservices made the monolith crumble into many different services,
but with this division many cross-cutting concerns that were in the
same codebase now require to interact with more codebases at the same
time possibly creating duplication and drift. This chapter will
describe ways to discover the state of the codebases and drift along
techniques and patterns to tackle these problems.

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
