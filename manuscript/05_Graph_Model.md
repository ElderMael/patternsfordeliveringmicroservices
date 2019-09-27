# Graph Model To Build And Deliver Software

## Pipelines Vs Graphs

The pipeline pattern to deliver software has been very useful for
Continuous Integration and Continuous Delivery but one of the trade-off
with it is that pipeline can be seen as a linear model.

Pipelines can be designed to parallelize as many stages as possible
but this is an optimization but not a change in the way that the
pattern works i.e. taking inputs for one or multiple stages and then
take the outputs of these to other stages.

While deploying microservices is important to understand that there
needs to be a policy across all of the services that allow reuse of
particular stages to enforce some aspects of the platform or policies
required for deployment. Examples of these are mandatory code analysis,
security scanning, etc. but also, pipeline flexibility for developers
is also an aspect that sooner or later needs to be addressed while
working with microservices. An example of this is optional stages,
different quirks required to deploy a specific microservice,
introduction of new tools used in the building process that are
technology-specific, etc.

Graphs represent a pattern that can be used to add flexibility to a
rigid pipeline concept while at the same time apply organizationally
wide policies to builds.

## Using Graphs And Events To Add Flexibility

In contrast with pipelines, graphs not only work with inputs and
outputs but also with events. This is a powerful tool as it allows
reacting on particular events such as git commits, security scanning
results, creation of docker images, etc.

The main difference between a pipeline and a graph-based CI/CD pattern
is that pipelines are more linear in nature and once the need to
deviate from this model they become more difficult to work with.

For example, a pipeline might contain the whole path to production by
promoting container images from lower to higher environments. While
this can work at the beginning, many times production environments have
more restrictions than the lower environments have. In this case, a
single pipeline might be divided to take into account CI into a set
of stages and another pipeline could take care of CD by promoting the
resulting artifacts from the CI pipeline.

If you model the previous example with a graph, the first event that
happens might be a commit on git. Everything from there can be
parallelized until the creation of the required container images.
Compiling, testing, security scanning, linting, etc.

A new event can be created that will promote the container image from
all of the required environments without having to have a pipeline
awaiting for promotion.

Another advantage is that graph nodes can trigger different types and
multiple events at a time so they are not constrained to trigger the
same linear stages but they can trigger more than one node at a time
or none at all. For example, a git commit can be inspected to only
update documentation instead of triggering a whole build.

## Model Different Workflows By Using Graphs

Another advantage of using graphs and events is that modeling different
workflows become easier. For example, a cross-cutting concern of
application policy is security scans and while they could be integrated
into the same pipeline, it may have more drawbacks than benefits.

A security scan may seem like a mandatory step but many times there is
no much the programmer can do about it. Vulnerabilities from known
databases may require updating to the latest library version but they
can also be found on it. Failing a pipeline because a security scan
finds such problems adds no value because there is no way to update
and the only action to not to block deployments is to suppress the
vulnerability.

With a graph model, triggering security scans can be yet another
process triggered by the same event but be independent of the main
pipeline policy and only trigger messaging warnings. While this can
be modeled in a pipeline too, the event can make trigger a different
set of events or be triggered on specific times without triggering the
complete pipeline.
