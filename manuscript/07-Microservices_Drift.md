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
