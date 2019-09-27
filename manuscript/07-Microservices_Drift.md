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



### Versioning Drift

Software dependencies are also a source of drift.


### Delivery Drift
