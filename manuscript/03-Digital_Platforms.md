# Digital Platforms, Microservices And Their Challenges

The foundation of a microservices architecture is a Digital Platform.
A Digital Platform is the set of technologies that function as the
context in which the microservices run.

You may have created microservices divided by business capability or
business domain but regardless you will need supporting software to
run the application code, deploy the required artifacts and
orchestrate the required components.

Nowadays, the de facto standard for microservice deployment is
Kubernetes. Before the advent of Kubernetes we had virtual machines
and we used other orchestrators to manage the required infrastructure
for deployment and monitoring applications.

The technology choice of orchestration for containers or virtual
machines, while important, is not the entire picture. You still need
concensus on other aspects of the Digital Platform such as the way
services authenticate with each other, log aggregation, monitoring,
tracing, deployment workflows, etc.

With the advent of DevOps, great advances in the way Digital Platforms
are created and the practices around deploying microservices have made
a lot of progress but there are still gaps I have identified during
each one of the projects I have worked on.

These gaps are usually around properly managing drift. The nature of
software is organic and quoting one of the most iconic books on
software development:

> It is better to have 100 functions operate on
> one data structure than to have 10 functions operate on 10 data
> structures. As a result the pyramid must stand unchanged for a
> millenium; the organism must evolve or perish".
>
> Structure and Interpretation of Computer Programs

If you do not make change easy, the stagnation will become ossification
and the microservices will start to rot and crumble. But the price of
this change is drift. Parts of the architecture evolve faster because
microservices are an example of evolutionary architecture. Other parts
of the architecture remain static but still need maintenance.

A good example of necessary evolution is security. What would happen
if a new vulnerability is discovered days after you have deployed your
microservice? What if one of your platform libraries is affected thus
affecting all the services using it? In the monolith days you would
have spent some hours updating the required library and forget about
it (if you were not concerned with delivery!). On a microservices
architecture, while change should be easy, probably changing a single
library would be a daunting task if you have a dozens of affected
services running not because it's difficult but because there are too
many.

While the previous example is an instance of a critical problem, many
libraries need updates that are not related to security. Many times
during normal development of an service you will find bugs that keep
features from being delivered. If this happens on a single service
probably it is still OK to look for a workaround but in platform
libraries the introduction of new features could pose a huge delay on
all the services.

These concerns are always present while delivering microservices to
production and this book will try to describe patterns seen and
implemented to tackle them.
