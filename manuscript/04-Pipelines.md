# Continuous Delivery Pipelines

Nowadays, Continuous Delivery Pipelines are accepted as the one true
way of delivering software by many developers. They provide faster
feedback cycles while building, testing and deploying applications
thus they were adopted widely on the industry during the emergence of
Continuous Delivery and Continuous Integration.

While a single pipeline to deliver a monolith was the norm, in a
microservices architecture a single pipeline would mean that there is
only a single type of services to deploy. This is, of course, false
in most cases.

The first problem with deploying many microservices is that you will
need to provision many pipelines, with different instances and
different definitions according to the type of services.

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
creating these templates, the process to production is streamlined and
becomes the paved road to production.

The first version of the pipeline template allows to greatly increase
the delivery speed of microservices across the platforms but it has
a big trade-off. Templates must be updated to introduce new features
and policies and safeguards are required due to the new found velocity.

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

The tradeoff of pulling the latest pipeline code, as stated before,
is that it won't allow you to have reproducible builds and will
possibly break projects that are not ready for using the latest policy
or features coming from the template.

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
nowadays. The only possible action that most developers think of when
a stage fails is to fail the entire build.

Failing the build may look like the only way to provide feedback to
developers but it's not. For example, notifications for fixing minor
linting details should be a better option. Also, Marking some stages
as totally optional is also a valid option i.e. have stages that run
certain tools and only are there for checking the results instead of
failing the pipeline.

Pipeline stages can also provide information through other means such
as messaging notifications for warnings about tools that not
necessarily mean failure of a build. A common pattern is to notify
the developer that created a commit of such warnings directly through
notifications or emails.

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
resources with such metadata. These kind of parameters allow pipelines

#### Feature Toggles

Yet another strategy you can use in your pipeline templates if you are
always using the latest code on them is the use of feature toggles.
This technique to code allows you to introduce features based on
parameters and test new builds using those features before properly
releasing them to all the teams. While this could be introduced using
template parameters, feature toggles allow you to test the feature
on live pipelines and observe the behavior or apply them selectively.



### DSLs Instead Of Templates

After working for a while with pipeline templates, we started to
stretch the boundaries of what a template can generate. Removing and
adding sections to a template and parameterize it enough could become
very complex over time thus the creation of DSLs on Jenkins for this
kind of operations has been a good way to introduce the required
flexibility.

It's important to note that centralizing policy across organizations is
an important step to avoid pipeline drift and the drawbacks it has. The
trade off of this approach is possibly the ossification of the pipeline
code as making changes to it may be risky but with DSLs developers
can regain some control over the pipeline code.
