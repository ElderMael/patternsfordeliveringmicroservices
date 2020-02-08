# Microservices Drift

As you reach a certain scale of projects using microservices,
complexity of deploying and maintaining pipelines and project
kickstarters starts to build up. Even though you try to have a well
oiled infrastructure, the paved road pipelines and new features need to
be updated or refactored constantly.

Microservices themselves also need to be updated due to the organic
nature of software. At some point some services will be more stable
and will be less  updated less than others yet drift will make them
eventually unable to be built and deployed.

This poses a huge challenge to platform development and developer
productivity teams because the same tooling that allowed developers to
adopt their platforms is the same tooling that keeps new features from
being introduced because of the friction created by new features.

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

## Drift Slows Down Development

Policies such as template pipelines allow many microservices to be
deployed due to consistent codebase structures and build automation
tools. On the other hand, introducing new features to the same
codebases will eventually make different aspects differ from other
microservices.

This moment is when widely applied policies will need to change or will
require updating code. Libraries once stable will eventually have bugs
found on them or will have new vulnerabilities appear due to research.
If you have similar types of microservices with similar configurations,
dependencies and infrastructure around them, you will need to update
all of them due to these problems.

This creates technical debt that has to be managed in a scale that was
not present during the monolith era. Changes will be required to be
applied in different codebases and by consequence it will take more
time.


## Generated Code Still Needs To Be Updated

Project kickstarters, as its name implies, only help teams to early
adopt the platform but after that they do not provide updates unless
that is your strategy.

Code generators such as Yeoman provide sub-generators that could be
used to generate specific integrations and new features on already
existing projects.

### Configuration Drift

Having many services share configurations is a situation common while
deploying microservices. Sharing settings such as URLs of core
services or certificates created configuration drift when they require
updates.

### Versioning Drift

Software dependencies are also a source of drift. Library versions and
container base images are one of the main sources of drift within a
microservices deployment.

Keeping any type of dependency up to date is a task that is unavoidable
from a security perspective because sooner or later vulnerabilites are
discovered.

### Delivery Drift

While some services might be changed more often than others, the code
that deploys these services is also being integrated every day to
accomodate policies accross the platform. With enough time, if
pipelines are not kept up to date, some services won't be deployable
anymore.

Deployment code usually lives within the repositories of each
microservice and needs to be updated to avoid ossification i.e. the
inability to deploy or pass construction stages.

## Driving Change Can Be Overwhelming

Consolidation of the three type of Drift through governance is a good
starting point to drive change within all the microservices but quickly
becomes unwielding.

Security scans are an example of tools that alert developers when
change is required but alerting can become an overwhelming strategy
if it comes from many directions and repeating too frequently such
as when there are many microservices sharing common dependencies such
as frameworks or libraries.

## Conclusion

This chapter described what is drift on microservices architectures and
explained the different types of drift and their causes. Patterns to
drive consolidation and avoid drift were also described. The chapter
about Distributed Refactoring will follow on this topic and how to
tackle this problem.
