# Introduction

The microservices architecture pattern has changed the way we create
software at many levels. I remember working on my first microservice
project during the times before Kubernetes, on the apogee of the
Netflix platform implementation.

While working as a front-end developer, I landed on a project that
exposed me to my first microservices implementation. This project used
the Netflix stack to deliver microservices.

From that point of time to the moment of writing these lines I have
been in various other projects implementing a similar architecture
style but using different technologies and also working on other
positions such as infrastructure, backend and platform developer.

While I can say that I matured as a developer during the monolith era
of the early 2000's, I think my most challenging projects were the
ones in which I was not coding application code but platform code. This
means that I coded small libraries and utilities for developers in
order to accelerate adoption of platforms such as Kubernetes.

While working on Kubernetes related technologies for more than two
years I started to realize that developers required opinionated tools
but with enough flexibility to allow them to skip stages and do their
jobs.

This is when I started my research on tools and patterns that I have
used over the years to allow adoption of the microservices paradigm
and at the same time, give developers enough tools to work confidently
on their own services without cluttering their job with platform code.

Over these years, I have seen the same problems appear again and again.
From the explosion of projects being delivered by dozens of pipeline
that in reality are only a couple to the necessity of creating
templates for each microservice type because cloning already existing
projects and modyfing them by hand is very error prone. These problems
occur on every project in which I have started from scratch and
sometimes they appear over time when the Digital Platform reaches some
maturity.
