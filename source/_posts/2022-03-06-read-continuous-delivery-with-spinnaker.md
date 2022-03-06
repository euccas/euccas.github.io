---
layout: post
title: "Read Continuous Delivery with Spinnaker"
date: 2022-03-06 22:30:58 -0800
comments: true
categories: Reading Continuous-Delivery
keywords: continuous delivery spinnaker CICD
description: continuous delivery with Spinnaker CICD Teletraan
---
[Spinnaker](https://spinnaker.io/) is an open-source, multi-cloud continuous delivery platform originally developed by Netflix. Today, Spinnaker has built a community and many companies adopted it to power their Continous Delivery. Pinterest also uses Spinnaker to deploy some of its core services, including web and API. Recently I read this eBook: [Continuous Delivery with Spinnaker](https://spinnaker.io/docs/concepts/ebook/). What I like about this short eBook is that it explains the key design considerations of Spinnaker, and those are, as I think of them, what really matter when designing a good cloud CD platform. In this post, I will share a few topics mentioned in this eBook together with my thoughts after reading.

# Cloud Deployment Considerations

Important things to consider:

- Credentials management
- Regional isolation
- Autoscaling
- Immutable infrastructure and data persistence
- Service discovery
- Using multiple clouds
- Abstracting cloud operations from users

When you work on designing a CD platform, pay attention to where do you focus on. When I joined Pinterest back in 2019, I was working on the Continuous Delivery Platform team initially and I started designing Pinterest's new CD platform. For that project, the team and I put a lot of focus on the developer experience and making the new system easy to use. While I think that was good, I also think we should more thoughts into the other areas such as credentials management, autoscaling, deploy policy support, different ways of triggering a deployment, etc.

# Structuring Deployments as Pipelines

Benefits of flexible user-defined pipelines: allowing each team to build and maintain their own deployment pipeline from the building blocks the platform provides lets engineers experiment freely according to their needs.

Encapsulate the built-in features as platform defined pipeline stages:

- Infrastructure stages: operate on the underlying cloud infrastructure by creating, updating, or deleting resources.
- External systems integration stages: examples are integrations with CI (Jenkins/Travis CI), run job, webhook.
- Testing stages: Chaos automation platform, Canary + ACA
- Controlling flow stages: allows to control the flow of pipelines, whether that is authorization, timing, or branching logic.
- Triggers stages: controls how a pipeline is started, eg. time-based triggers, event-based triggers.

Continuous delivery is a complex process. I think using *pipeline* and *stage* as the two core concepts in Spinnaker's design is an awesome idea. It abstracts the complexity of various type of deployments, and allows enough flexibility and extensibility by having both the *managed stages* and *customized stages*. On a side note, [Apache Airflow](https://airflow.apache.org/), the data pipeline orchestration system uses a similar principle in its design by providing *operators*. I may delve into the design of Airflow in another post later.

# Working with Cloud VMs and Kubernetes

For continuous deployment into Amazon’s EC2 virtual machine–based cloud, Spinnaker models a well-known set of operations as pipeline stages. Other VMbased cloud providers have similar functionality. Those operations mainly include:

- Baking AMIs
- Tagging AMIs
- Deploying in EC2
- Availability zones
- Health checks
- Autoscaling

Kubernetes makes deployment to the cloud much easier because of some of its advantages comparing to the VM-based cloud platform:

- Faster: provisioning resources in Kubernetes takes seconds, while provisioning a VM can take minutes.
- Declarative: Kubernetes uses manifest files (YAML) to provide a declarative description of your infrastructure, and this is central to how Kubernetes works.
- Multi-cloud: whether Kubernetes is running in Google’s cloud or Amazon’s, in your on-premise datacenter or on your laptop, it exposes the same interface and behavior for running your workloads. This makes it trivial to deploy the same application to multiple clouds and regions, when you can treat each as being identical.
- Native deployment orchestration: when a change is submitted to a running Kubernetes workload, it orchestrates a rollout of your change according to policies you specify. In some cases, this becomes the only deployment orchestration that you need.

Pinterest has an internal deployment system [Teletraan](https://github.com/pinterest/teletraan), and it was designed and used for deploying services to VMs (Amazon EC2). After joining Pinterest, I learned that a major user pain point of Teletraan was the complicated configurations needed for setting up a deployment environment for user's services. For example, in Teletraan users need to configure AMI, place AZs, etc. I agree that Teletraan's UI can be improved to make the experience better, but I think this problem is a result of the complexity of VM deployment. To solve it, we could either choose to move to Kubernetes, or redesign some parts of Teletraan to have a better abstraction model, similar to what Spinnaker did. In short, reducing the complexity in developer experience cannot be done just by fixing the UI.

Right now I'm no longer working on the Continuous delivery platform, but I still like to think about the problems and solutions in this area because I used to work on it, built a new system from scratch when I didn't really have much knowledge in the cloud deployment space, had many questions and learned lessons (and got some wins too). If you happen to read this and want to continue the discussion with me on a specific topic, please feel free to drop me a line.