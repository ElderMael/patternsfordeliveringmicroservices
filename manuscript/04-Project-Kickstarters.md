# Project Kickstarters

Project kickstarters are not really a new concept. Most build
automation tools such as npm, gradle, or maven provide a way to
generate new projects using a simple command with some parameters to
customize the output.

But the focus of project kickstarters in this book is that these tools
need to be created specifically for the platform that is going to be
the target of the project i.e. the Digital Platform on which the new
microservice is going to be delivered.

## Reference Architecture

Project templates are a form of reference architecture for other
microservices. Because they are not tied to any specific business
capability they can be evolved with new platform capabilities without
the fear to break any production application and thus they can be
kept up to date with the latest developments.

Software architects can dictate microservice tooling and technology
stacks using project kickstarters as references and prove that they
are suitable for the platform through research and implementation. This
implies that the patterns and research works with the current Digital
Platform without clashing with its design.

The benefits of using project templates as reference architecture is
that they avoid having different teams solving the same problems many
times. They provide a common vocabulary and technology stack for
new microservices to use.

## Project Templates

Over most microservice platforms, when the first microservices are
deployed they are green field projects
and they evolve along the tools and pipelines that work in tandem to
provision them to platforms such as Kubernetes or Cloud Virtual Machine
Templates. These projects usually are hand crafted and developers pour
all the best practices they know and can be utilized.

Eventually, these projects  need to be duplicated in order to create
more and more microservices. The duplication is also usually done by
hand too. This is an error prone task because many things have to be
changed and the possibility of making mistakes happen whenever the
structure of a template has to change.

Examples of these errors are innumerable: changing package structures
usually break dependency injection, renaming certain files or classes
breaking configurations that depend on those fully qualified names,
requiring to change database URLs (because sharing databases is a
no-no on any microservice deployment).

Unfortunately, project templates do not avoid the pain of having to
modify things to create a new service without errors and manual
processes.

## Project Generators

As stated before, most build automation software already provides
commands to generate new generic services with little or almost no
parametrization. New technologies such as Yeoman or Atomist allow more
sofistication for project scaffolding and provide capabilities for
customization.

This is when project generators customized for the business Digital
Platform become a necesity for the microservice architectures because
they become an excellent way to bootstrap new business capabilities
right away and have them deployed in a matter of minutes with little
or no manual modifications.

### Transform Projects Instead Of Templating

A pattern that comes from project generators is that they should
transform projects instead of using template engines to produce them.

A project generator coded using template engines is more difficult to
develop because the feedback loop takes more time than a generator
that only applies transformations to already existing projects which
are kept up to date independently and are already in a good shape. With
template engines rendering is a required step to know if the resulting
new microservice is going to be functional and error-free.

Another aspect to keep in mind about project generators is that they
do require maintenance along the project templates they generate. New
features on templates will probably require some degree of
customization during the code generation. This will require modify
names, variables or parameters in the project generator itself.

Typical flow of a project generator I have implemented is:

1. Clone base architecture project
1. Remove version control files (make it a new project)
1. Apply common transformations
   1. Rename required files
   1. Replace project name or references
   1. Replace configuration according to parameters
   1. Replace code references
1. Remove unnecessary features
   1. Remove related code
   1. Remove related configurations
1. Test new application builds correctly with build automation system
1. Push new project to source control
1. Trigger build pipeline and wait for lower environment deployment

##### Modularize Reference Architecture Early

Per the flow of a project generator, it's important to modularize
features in order to remove them without recurring to
[shotgun surgery][1] i.e. removing features by touching many code units
scattered across several source code files. Ideally, when a feature
is introduced to a reference architecture project, it should be
contained within a obviously apparent set of files such as a package
or a directory if the programming language does not use namespaces
for classes.

### Generator Downsides And Tradeoffs

#### Coupling With Pipeline Templates

Project generators using paved road pipeline templates usually couple
their lifecycle. This is because when releasing new versions of the
pipeline, project generators do require an update too to get the
benefits of the change.

Unless using always the latest version of the pipeline template, this
represents an opportunity for automation because releasing new
pipeline template versions should automatically propagate to generators
if many projects are created/updated frequently.

#### Drift

Even though generators are a good way to kickstart project, modifying
existing projects is also a valuable task. Different technologies
allow this such as Yeoman or Atomist. The problem is when the delta
of creating the new project and the existing project varies too much
as this will make updating new projects difficult.

Modularizing the codebase could allow introducing and updating features
quickly. Microlibs are a good example of modularization that can be
updated easily as generators or distributed refactoring can update
the new version and maybe do a slight modification to configuration.

Because microservices are an instance of an evolutionary architecture,
created projects will quickly get out of date regarding cross-cutting
concerns made available by the platform.

For example, if the platform provides new ways to authenticate
between services or users it will probably won't be added to the
project kickstarter until it is fully developed. The same will happen
with the project generators. This drift between the new architecture
and its reference reflects the problem of drift on microservices.

Further on this book, a whole chapter is dedicated to this topic.

## Conclusion

Project kickstarters are a great way to speed up the adoption of a
microservice architecture. They provide production ready code if
applied correctly within an organization. Kickstarters also serve as
reference architecture for developers to use when coding against a
set of technologies.

The chapter explained some of the possible ways to implement project
kickstarters and the trade-offs of each implementation. Finally, the
chapter explained the tightly coupled nature of project kickstarters
and pipelines.

[1]: https://en.wikipedia.org/wiki/Shotgun_surgery
