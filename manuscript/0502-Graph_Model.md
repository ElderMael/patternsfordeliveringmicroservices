# Graph Model To Build And Deliver Software

## Why Using Graphs?

A pipeline model can be seen as a series of inputs and outputs.
Earlier stages give inputs to later stages and the final product, the
artifact, is taken to different environments and finally, after some
minor manual intervention, it is deployed to a production environment.

A graph model for delivering software can be seen as a series of events
triggered that will trigger some kind of processing. An event could be
a commit on a distributed version-control system (e.g. Git), a specific
date happening (e.g. ever day, 12 PM). The processing that happens when
and event occurs can be similar to an stage of a CI/CD pipeline, for
example, building a binary.

A benefit of the graph model to build and delivery software is that
it is parallel by default while pipeline stages usually are not.
Events can trigger multiple processing taks at a time and can be
audited or even reproduced while most pipeline models and technologies
rely on webhooks which are usually fire and forget.

Graphs allow flexibility on the type of processing tasks that can be
triggered at a time and this benefits individual teams to pick or add
new processing tasks dependind on the event. Pipelines on the other
hand, are usually prescribed and lack the required flexibility out of
the box. While this flexibility can be added with some paradigms as
explained on the Pipelines chapter, it is not the default in most
CI/CD servers/technologies.

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
parallelized until the creation of the required container images,
compiling, testing, security scanning, linting, etc.

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

## Optionally Skip Processing Of Events

On a graph model, event processors can be designed to skip events or
skip processing after inspecting the event. Event processors can also
inspect the codebase even if the event they are interested in has been
triggered.

For example, an event processor interested in building a repository
binary can skip processing if the event triggered is a git commit
that did not changed any code e.g. editing the README file of the
repository had no impact on the code.

This is very useful to avoid wasting processing power usually seen on
pipelines where any webhook trigger usually means processing all stages
even when the commit only changed documentation.

## Tradeoffs

### Traceability Becomes Hard

Correlating events that trigger builds and deployments or releases
becomes troublesome when not everything is concentrated on a pipeline
definition and a server displaying the results. Event correlation can
be achieved by creating or using custom tools that keep the logs of
such events and their outcomes.

Nonetheless, separating construction, deployment and delivery on
microservices (or any software for that matter) still mandates that
you have a way to trace where artifacts come from and approvals for
deployment and delivery.


## Conclusion

A graph model to build and deliver software is beneficial to the
microservice architecture because it adds the necessary flexibility
to the paved road model provided by pipelines. It also can provide
policies as with the pipeline model but giving the individual teams
power to add or remove tasks as required.
