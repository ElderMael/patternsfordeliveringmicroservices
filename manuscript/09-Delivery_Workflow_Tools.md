# Delivery Workflow Tools

The flexibility of the microservices architecture allows different
types of technology stacks. It's tempting to reuse parts of the paved
road pipelines to deploy the new set of technologies. While it would
be convenient to create another set of tools and pipeline templates to
manage the new technology stack, another approach is to create a
Delivery Workflow Tool that manages the required or duplicated steps
and stages for all sets of tech stacks.

The advantage of a Delivery Workflow Tool is that you are not tied to
a CI/CD server and you will probably get more testability due to this.
The reason for the loss of testability is that CI/CD servers usually
delegate pipeline configuration to YAML files or restricted subsets
of scripting languages.

While there could be an argument for using a scripting language for
pipeline configuration, YAML configuration usually embed scripts too!
This leads to a lot of duplication unless you are externalizing scripts
but at this point you are already creating a Delivery Workflow Tool.
YAML embedded scripts usually mean that you have created duplication
across many pipeline definitions but you have in reality one or two
templates.

As stated in the chapter about pipelines, templates try to aleviate
the problem of duplication across delivery code for microservices but
there is a trade-off regarding these templates and it's that they are
usually harder to test because many CI/CD servers provide very
rudimentary ways to test pipelines without instantiate a test pipeline.

## Why Not Stick To CI/CD Scripting?

The most significat trade-off observed is that the loss of testability
of the pipeline code. While many servers allow some kind of plugin
architecture or directly embedding shell scripts into tasks, they do
not provide very mature tools to test each step, stage or pipeline.

In order to have more control over the tools and steps used on
pipelines, Delivery Workflow Tools in forms of CLIs that allow
encapsulating entire stages or specific steps of a pipelineon them.

Initially, implementations could be as simple as shell scripts for each
stage but this quickly becomes complicated because of the nature of the
majority of shell scripting languages. They do not provide modularity,
most functions are global, testing tools are limited, and all the
conundrums related to these tools.

Some CI/CD servers also allow the use of DSLs or fully blown
programming languages through plugins and shared libraries. While
these tools are more sofisticated, they still remain harder to test
except with a good plugin architecture. This is because plugins
usually can be built as separate libraries to be incorporated to
pipelines thus the isolation from the main CI/CD server engine is
beneficial for testing porposes.

Opinionated workflows keep consistency between microservices pipelines
and Delivery Workflow Tools are a good pattern to implement such
opinions. They can also be programmed to benefit from the Convention
Over Configuration paradigm and can be parametrizable with command
line arguments or configuration files analogous to npm or gradle.

## Using Different Technology Stacks

Another benefit of developing Delivery Workflow Tools is the posibility
of using different technology stacks. Abstractions can be set on top
of existing build automation systems to avoid duplicating steps on
pipelines such as dependency installations or creating container images
depending on the project type e.g. gradle projects, maven, npm, etc.

## Avoiding Over Dependency On CI/CD Servers

As stated before, Delivery Workflow Tools could potentially be executed
outside the CI/CD servers helping developers to debug and develop
easily but it also will help application developers to test their code
without pushing to the pipeline, accelerating their feedback loop.
