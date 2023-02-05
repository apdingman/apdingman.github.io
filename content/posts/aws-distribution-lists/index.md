---
author: Adam Dingman
# cover:
#   image: images/cover.png
#   hidden: true
#   relative: true
title: "3 Reasons why you should use Distribution Lists for the AWS Account Root User"
date: 2022-04-12T00:00:00-05:00
publishDate: 2022-04-12T00:00:00-05:00
categories: 
- AWS 
draft: false
---
The AWS Account Root User is the identity that has complete access to all AWS services and resources in an AWS account. If you spin up a new account, it’s probably first instinct to just slap your johndoe@companyxyz.com email address as the root user account and move on, but maybe that’s not the best idea.

## The List

Here are the 3 reasons why should use distribution lists for AWS account root user:

1. You don’t have to worry about re-assigning the account root user if someone leaves the organization.
2. If there’s an urgent communication from AWS, you don’t have to worry about it getting lost in John’s mailbox while he’s taking a sixth-month sabbatical at Bocas Bali.
3. It’s more likely that you’ll use a complex password if it’s associated to a distribution list vs. if it’s associated to a named user account (just a theory, but I think I’m right).

Oh…and while you’re at it..consider [securing your account root users with U2F keys]({{< ref "/root-user-u2f" >}}).

## Naming Pattern

If you have a multi-account strategy (you probably should), then consider defining your account aliases and account root users following a naming pattern similar to this:

| Account Id                | Account Alias                   | Account Root User                                 |
| ------------------------- | ------------------------------- | ------------------------------------------------- |
| {assigned account number} | {company}-{business unit}-{env} | {company}-{business unit}-{env}@{company domain}  |
| xxxxxxxxxxx1              | acme-iot-dev                    | acme-iot-dev@acmecorp.com                         |
| xxxxxxxxxxx2              | acme-iot-stg                    | acme-iot-stg@acmecorp.com                         |
| xxxxxxxxxxx3              | acme-iot-prod                   | acme-iot-prod@acmecorp.com                        |

## Other things to consider

- Are you storing your root user credentials in a password manager?
- Is your password manager protected by multi-factor authentication (MFA)?
- Are you using the sharing capability within your password manager so that you’re not the only one with access to the creds?
- Do you have an audit plan to periodically review who has access to the creds and a validation to confirm the creds still work?
