# Continuous Delivery Pipelines

Continuous Delivery Pipelines are accepted as the one true
way of delivering software by many developers. They provide faster
feedback cycles while building, testing and deploying applications
thus they were adopted widely on the industry during the emergence of
Continuous Delivery and Continuous Integration.

While a single pipeline to deliver a monolith was the norm, in a
microservices architecture a single pipeline would mean that there is
only a single type of services to deploy. This is, of course, false
in most cases.

The creation of many different microservices implies that there will
be as many pipelines as there are microservices but in reality some
microservices will have very similar technology stacks. The first
problem with deploying many microservices is that you will need to
provision many pipelines, with different instances and different
definitions according to the type of services.

The worst possible scenario is that you have a pipeline definition on
each code repository you have. This would mean that whenever you
require to introduce new stages, you will have to modify many code
repositories to achieve it.

Most CI/CD servers would allow some kind of mechanism to share common
step of a pipeline. For example, Jenkins provides shared libraries to
do this. This is a first good step to avoid duplication.

But sharing pipeline code will introduce a new type of friction
because code repositores will have a new dependency on them based on
the pipeline definition.

## Pipeline Templates

The next logical step after being able to share code between pipelines
is to create a template pipeline that encapsulates all the policies
and best practices and makes them available to all the microservices
in the platform.

This allows delivery of many services faster because in the process of
creating these templates, the path to production is streamlined and
becomes a paved road useful for taking application code directly.

The first version of the pipeline template allows to greatly increase
the delivery speed of microservices across the platforms but it has
a big trade-off: templates must be updated to introduce new features
and policies and safeguards are required due to the new found velocity.

### Versioning Templates

If you always use the latest template automatically, it means that any
enhancements or fixes are applied automatically across all of the
organization and they are immediately reflected. The possible problem
with this approach is that builds are not going to be reproducible
because while you are checking out the repository code at a certain
revision, the pipeline is still pulled on its newest version.

If you want to have reproducible builds your only option is to version
within your repository the pipeline version that can build your
microservices at the required revision and then gradually upgrade
versions of the pipeline as required by the platform i.e. when new
platform policy or features are introduced in newer versions of the
pipeline template.

This can be achieved in many different ways. You could use git
submodules to get your build server files. Some CI/CD servers already
let you share libraries between pipelines and you can point to a
specific revision of the pipeline.

### Using Always The Latest Template

Arguably, pipeline code benefits from continuous integration with the
code it deploys. This prevents pipeline drift because projects take
the latest pipeline template version the moment it is released.

The tradeoff of pulling the latest pipeline code, is that it won't
allow you to have reproducible builds and will possibly break projects
that are not ready for using the latest policy or features coming from
the template. This can be both good and bad depending on how you want
to react to this kind of feedback. If a new policy needs to be
enforced, introducing changes to pipeline templates will force
developers to take action if the new policy fails the pipeline.

If using the latest pipeline template, rolling forward instead of
rolling back can be a better strategy to fix errors during the
integration and deployment process.

A possible option to avoid the breakage of introducing new features or
policies is to gradually introduce warnings instead of failing the
whole pipeline and gradually allow developers to accomodate new
policies. Of course, this depends on the organization maturity. Further
on the chapter there is a section to introduce these policies or
features using feature toggles.

### Gradually Introducing Non-breaking Stages

Pipelines are policy. They are usually the means to enforce
required build steps for all the services within a platform. The
sooner some cross-cutting concerns such as security scans appear, the
sooner pipelines will be the means to implement them.

Here is where the first difficulties of a microservice CI/CD pipeline
appear. It is very probable that when you introduce new step
definitions pipelines will fail automatically. For example, when a new
security scan is introduced, many builds that do not had such scan will
fail because many of them may have security problems right away.

A common pattern to avoid such harsh pipeline step introductions is
to not to fail of course. Yes, this may be against the conventional
wisdom of having a pipeline fail to provide faster feedback but the
principle could be intact if the new step only alerts the developers
instead of failing.

Gradually introducing steps and stages with warnings gives developers
time to catch up with impending change or prepare before the step
becomes a requirement.

Another example of this are linting steps. Many times pushing code
to a pipeline with a required style check is prone to failure. If this
step could only generate a warning that developers could see in a
build monitor then it won't surprise them but will still have an
effect. Of course, there are many ways to notify developers of these
types of errors such as Slack notifications.

### _Not_ Failing Pipelines On Every Problem

The saying goes that when you only have a hammer at hand, every problem
starts to look like a nail. This is a fantastic analogy for pipelines
because the only possible action that most developers think of when
a stage fails is to fail the entire build.

Failing the build may look like the only way to provide feedback to
developers but it's not. For example, notifications for fixing minor
linting details should be a better option because they are less
disruptive to their workflow. Also, Marking some stages totally
optional is also a valid option i.e. have stages that run certain tools
and only are there for checking the results instead of failing the
pipeline.

Pipeline stages can also provide information through other means such
as messaging notifications for warnings about tools that not
necessarily mean failure of a build. A common pattern is to notify
the developer that created a commit of such warnings directly through
notifications or emails.

### Linters And Autofixers

Linting code to keep codebases consistent and free of small errors is
among the most common steps on Continuous Integration pipelines and
these usually fail the pipeline if errors are detected. While the
argument of having consistent stylistic codebases and detect small
errors is arguably good, opinionated and automated code formatting
could be better.

If possible, adding autofixers instead of failing the pipeline saves
developers roundtrips to the CI/CD server.

## Pipeline Template Flexibility

Sometimes, microservices won't require all the stages defined in the
pipeline to be executed. Other times, microservices will require more
than the stages defined in the template. As stated before, pipelines
are policy thus they must be applied where necessary but there is merit
on having optional stages being applied or allow developers to execute
their own stages.

This is very typical use case of build systems and implementations seen
are described next.

### Convention Over Configuration To Execute Stages

The Convention Over Configuration paradigm can be very useful to add
flexibility to pipelines. The code that executes the build stages can
be programmed to look for certain files or even tasks of the build
automation system and react based on the presence or absence of those.

A typical example I have implemented is to deliver atomic microservices
along optional caches by inspecting for the existence of a Kubernetes
object described in a YAML file. If the file exists, the necessary
cache server is created by applying the file and provisioning the
credentials to both the cache and the microservice in an automated
fashion.

### Template Parameters

The idea behind this pattern is to allow parametrizable steps or stages
feeding from a microservice project specific values. Passing
parameters could be supported by the function returning the pipeline
definition, a specific file in the repository with key-value pairs
that can be read during build time, environment variables, etc.

Typical parameters are application names for creating kubernetes
resources with such metadata.


#### Template Parameters As Extensions

If the pipeline definition is a fully fledge programming language,
template parameters can be callbacks or funtions that could be executed
at certain points of the execution of the pipeline. Examples of these
are tasks to be run before or after the execution of a particular
step to customize the result or react to its output.

#### Feature Toggles

Yet another strategy you can use in your pipeline templates if you are
always using the latest code on them is the use of feature toggles.
This technique to code allows you to introduce features based on
parameters and test new builds using those features before properly
releasing them to all the teams. While this could be introduced using
template parameters, feature toggles allow you to test the feature
on live pipelines and observe the behavior or apply them selectively.

Feature toggles can be activated even without parameters using also
convention over configuration. For example, I once had to implement
multi-cluster deployments. Instead of changing the way that the
current deployment process worked, I simply inspected the
repository for a configuration file and then use a different pipeline
code to read the file contents and deploy to the clusters specified
there instead of the default one.

### DSLs Instead Of Templates

After working for a while with pipeline templates, we started to
stretch the boundaries of what a template can generate. Removing and
adding sections to a template and parameterize it enough could become
very complex over time thus the creation of DSLs (Domain Specific
Languages) on Jenkins for this kind of operations has been a good way
to introduce the required flexibility.

It's important to note that centralizing policy across organizations is
an important step to avoid pipeline drift and the drawbacks it has. The
trade off of this approach is possibly the ossification of the pipeline
code as making changes to it may be risky but with DSLs developers
can regain some control over the pipeline code.

DSL for deployment can enforce policy across pipelines but can be
created to be flexible enough to skip non-required stages. Their
domain is deployment within the Digital Platform.

## Pipeline Template Antipatterns

### Not Having Integration Tests With Pipeline Templates

A common mistake is to think that pipeline code is different from
production code. It should be tested and integrated as much as possible
and preferably with reference architecture applications.

Integration tests are very important for pipeline templates and project
templates/code generators because they provide feedback about the
paved road for production i.e. if the integration fails then it means
that the overall process is broken.

Pipeline code should be tested as any other software. The [practical
test pyramid][1] is a good gideline to test pipeline templates and
the integrations with project generators. Ideally, while the pipeline
will have more unit tests than integration tests, the integration
tests may need to generate more than one type of project archetype
or template. Parallelizing is key to get the feedback faster if any
type of project fails.

Project generators should have pipeline template projects as upstream
dependencies so that when a new pipeline version comes out, it will
automatically trigger project generator tests to integrate with it. If
these tests fail, it may signal that the new version of the pipeline
might have problems integrating with the current generator version.


### Having Different Build Agents For Each Build Tool

Working with pipeline templates implies a set of technologies used by
different microservices i.e. the Digital Platform. These technologies,
usually called stack, will be used by the CI/CD server to build
different microservices thus usually they are installed on virtual
machines or any agent in charge of building the required artifacts.

A common problem arises when trying to provision these tools into
very small agents or try to specialize such agents too narrowly. For
example, if you require to build front-end and backend applications
with different technology stacks, most likely the first implementation
will create two different agents with separate tooling.

This choice poses two problems. First is that there is always overlap
over the tools regardless of the platform. Examples of these tools
are version control, security scanners, code analysis, etc. Because of
this overlap, you will have duplication whenever you decide to build
different applications.

The second problem occurs is when a new technology stack needs to be
supported. This also requires duplication because most of the tools
and steps will be reused or are required for compliance.

This duplication means that when a tool needs to be updated or
modified it will invariably be done on two or more different places and
this generates overhead over time as the platform adopts a myriad of
required tools. Every stack agent will have duplicated provisioning
efforts.

One of the solutions to this problem is to consolidate as many tools
as possible under a single agent. Even all the platform tools to
build microservices could be set up into a single spot.

For example, having worked with many different Jenkins setups and
dockerized CI/CD solutions, building a single agent with all the
required tools for any type of application is usually easier to
maintain over time instead of multiple docker images/virtual machines
for each specialized stack.

Benefits of this approach is less points of contact when updating tools
required to build microservices, a one-time setup of such tools and
possibly the benefit of only transfering once a docker/virtual machine
image so you only pay the price once for modyfing it, less operational
and cognitive overhead when resolving issues regarding configuration
or provisioning.


## Conclusions

Pipelines are policy imposed across a microservice architectures and
keeping them consistent means there will be drift. Some patterns to
avoid drift and consolidate paved roads to production were presented
using paradigms such as Convention over Configuration and template
parameters. More advanced patterns such as DSLs can add flexibility to
pipelines because microservices will have different needs as they are
built and deployed.

[1]: https://martinfowler.com/articles/practical-test-pyramid.html
