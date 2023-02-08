---
author: Adam Dingman
cover:
  image: images/cover.svg
  hidden: true
  relative: true
title: "Deploy an AWS Budget using Pulumi"
date: 2023-02-07T00:00:00-05:00
publishDate: 2023-02-07T00:00:00-05:00
categories: 
- DevOps 
draft: false
---

## What is Pulumi?

[Pulumi](https://www.pulumi.com) is yet another Infrastructure as Code (IaC) tool for deploying infrastructure using declaritive language which offers you the ability to pick your language of choice amongst TypeScript, JavaScript, Python, Go, .NET, Java, and YAML to define your infrastructure.

## How am I using Pulumi?

I really wanted a quick and easy means to get a feel for the basic structure of a Pulumi project and to get a feel for the CLI. In order to accomplish this I'm setting up a super basic budget to track and notify on S3 spend in an AWS account.

## Example

I've included the skeleton Pulumi project that I used for this example here: <https://github.com/apdingman/pulumi-aws-budgets>

### Prerequisites

I'm performing these steps on a macOS (and you should consider adding macOS in your life too if you haven't already).

- An AWS account to deploy resources to
- [Named AWS profiles](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html) configured on your local machine
- Homebrew installed

### Basic Steps

#### Install Pulumi

```shell
brew install pulumi
```

#### Update Pulumi Config to use the Appropriate Named AWS Profile

```shell
pulumi config set aws:profile personal
```

#### Create a Pulumi.yaml file

Create a file named `pulumi.yml` with the following content:

```yaml
name: pulumi-aws-budgets
runtime: yaml
description: A simple example of using Pulumi to deploy a budget in an AWS account
resources:
  s3:
    type: aws:budgets:Budget
    properties:
      name: s3-budget
      budgetType: COST
      costFilters:
        - name: Service
          values:
            - Amazon Simple Storage Service
      limitAmount: '30'
      limitUnit: USD
      notifications:
        - comparisonOperator: GREATER_THAN
          notificationType: ACTUAL
          subscriberEmailAddresses:
            - [youremail@domain.com]
          threshold: 100
          thresholdType: PERCENTAGE
      timeUnit: MONTHLY
```

#### Deploy your budget

Run the command:

```shell
pulumi up
```

You'll be presented with a prompt like so:

![pulumi up](images/pulumi-up.png)

Navigate to **yes**, and press **enter**.

You'll be presented with information that shows that your *pulumi* stack and the budget included specified has been created: 

![pulumi created](images/pulumi-created.png)

#### Verify in the AWS console

Navigate to the AWS billing service in the AWS console and confirm that your budget was created as expected:
![aws console 1](images/aws-console-1.png)

#### Tear down

Destroying resources managed by Pulumi is super straightforward. Simply run the destroy command and confirm that you want to perform the destroy.

```shell
pulumi destroy
```

![pulumi destroy](images/pulumi-destroy.png)

## What is next?

Kicking the tires on Pulumi's Policy as Code (PaC) offering called [Pulumi Crossguard](https://www.pulumi.com/docs/guides/crossguard/).
