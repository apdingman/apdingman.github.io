---
title: "Secure AWS Account Root User with U2F Keys"
date: 2022-11-17T22:06:15-05:00
draft: true
---

The AWS Account Root User is the identity that has complete access to all AWS services and resources in an AWS account. The scenarios that require you to use the root user are pretty sparse, so it's good practice to secure the accounts with Multi-Factor Authentication (MFA), store the credentials in a password manager (also protected by MFA), and create named IAM users for any of your AWS account administrative needs.

Your options to secure the account root user with MFA are:

1. Virtual MFA Device (Microsoft Authenticator, Authy, Google Authenticator, etc.)
1. Universal 2nd Factor (U2F) Security Key (Yubikey)
1. Hardware MFA Device (Gemalto Token)

My go-to is to use option 2 - U2F Keys. They are relatively cheap, easy to acquire, and user-friendly. I'm specifically a fan of the Yubikey brand of U2F keys manufactured by Yubico.

What exactly are they and how do they work? Check out this quick video...

{{< youtube DFzScdDC6xk >}}

## Why not Virtual MFA?

Wait...why don't I just use the Virtual MFA Device option? It's free and it doesn't require me to keep track of a physical object! That's true, but in addition to U2F keys preventing you from having to deal with account management hell (as employees leave, people change devices, etc.) hardware-based security also offers the benefit that it is much more difficult to successfully attack remotely.

## Activate U2F Key MFA for an Account Root User

When logged in as the account root user:

1. On the right side of the navigation bar, choose your account name, and choose **Security Credentials**

![Scenario 1: Across columns](/images/profile-photo.jpg)
