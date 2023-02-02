---
cover:
  image: images/cover.png
title: "Continuous Delivery vs. Continuous Deployment"
date: 2023-02-01T21:00:15-05:00
draft: false
---
The term CI/CD gets used a lot to describe how to modernize the Software Delivery Lifecycle (SDLC). While there's usually clear understanding on what **CI - Continuous Integration** means, that clarity isn't always present surrounding the CD part.

The reason? CD can have two similar, but distinct meanings - **Continuous Delivery** or **Continuous Deployment**.

## Comparison

### Continuous Delivery

Through the Continuous Integration process one or more artifacts are generated that can be used to deploy infrastructure and application code. Continuous Delivery is the act of deploying those artifacts into environments in an automated fashion.

Deployments made to production require a manual intervention often times consisting of testing, approvals, and release schedules.

![Continuous Delivery](images/continuous-delivery.png)

### Continuous Deployment

Continuous Deployment follows the exact same pattern as Continuous Delivery pattern seen above with one key differentiator.

*Humans intervention is removed from the process.*

![Continuous Deployment](images/continuous-deployment.png)

## Why would you want to use Continuous Deployment?

Getting to the point of deploying to the production environment eliminates unnecessary human effort and toil and facilitates a much greater rate at which technical features can be delivered to achieve desired business outcomes.

## How might you get there?

**WARNING**: This usually doesn't happen without a fair amount of investment.

What does it take to achieve this nirvana state of practicing Continuous Deployment?

A few thoughts come to mind:

- Small changsets
- Unit testing performed via CI
- Integration testing built into the pipeline
- Pipeline integrated with ChatOps tool of choice (Teams, Slack, etc.)
- Well instrumented systems for logs, metrics, and traces.

I'm sure a few other ideas might come to your mind.

The *most critical* characteristic to allow for Continuous deployment is an organizational culture that breaks down silos between technical teams and unites technical teams with their business counterparts. A culture based on trust, collaboration, and Continuous improvement are required to facilitate this level of automation in an organization's SDLC.  

## Useful Resources

- <https://about.gitlab.com/topics/ci-cd/>
- <https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment>