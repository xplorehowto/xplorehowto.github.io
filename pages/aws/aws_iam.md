---
title: AWS IAM
keywords: aws, iam
tags: [aws]
summary: "Identity Access Management"
sidebar: aws_sidebar
permalink: /aws_iam
folder: aws
---

## Overview

**IAM** or Identity and Access Management is used to manage access to 
AWS *services* and *resources* securely. IAM is also used to creates and 
manage AWS *users* and *groups*, and use *permissions* to allow and deny 
access to AWS resources.  

Features worth highlighting:
- FREE
- **Granular permissions**; to users & resources
- **Multi-factor authentication (MFA)**; code from another registered device
- **Identity federation**; web identity or SAML
- **Audit trail** when use AWS CloudTrail, IAM identities based log records that
include information about those who made requests for resources in your account.
- **PCI DSS Compliance**; supports the processing, storage, and transmission of 
credit card data by a merchant or service provider; compliant with 
Payment Card Industry (PCI) Data Security Standard (DSS);
see [PCI DSS Level 1](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/){:target="_blank"}
- **Eventually consistent**; changes will be replicated across IAM, 
which can take some time.


## How IAM works
<img src="https://docs.aws.amazon.com/IAM/latest/UserGuide/images/intro-diagram%20_policies_800.png" alt="IAM Concepts"/>

  
- **Principal** is a *person* or *application*; 
- Principal need to sign in using **entity**, IAM resource objects that 
  AWS uses for *authentication*. These include users and roles.
  **Identities** is IAM resource objects that are used to identify and to group
- Authorization checks for policies that apply to the request; 
  to determine whether to allow or deny the request
- Principal makes **request** for an *action* or *operation* on an AWS *resource*.
- Request includes:
  - Actions or operations - initiated from AWS Management Console, AWS CLI or AWS API.
  - Resources – The AWS resource object upon which the actions or operations are performed.
  - Principal – including the policies that are associated with the entity that the principal used to sign in.
  - Environment data – Information about the IP address, user agent, SSL enabled status, or the time of day.
  - Resource data – can include information such as a DynamoDB table name or a tag on an Amazon EC2 instance.

- **Policy** is an object that when associated with an identity or resource, 
  defines their **permissions**. AWS evaluates these policies when a principal 
  makes a request. Permissions in the policies determine whether the request is 
  allowed or denied. Most policies are stored in AWS as JSON documents.


## Policies

Two methods for assigning policies:
- attached policies to user, or 
- attached policies to group; and assign user to the group

IAM console displays policies in three tables: 
- policy summary; includes a list of services
- service summary; includes a list of the actions and associated permissions for the chosen service
- action summary; includes a list of resources and conditions for the chosen action

<img src="https://docs.aws.amazon.com/IAM/latest/UserGuide/images/policy_summaries-diagram.png" alt="IAM Policies"/>

Two types of policies:
- **Identity-based** policies includes: Managed policies (AWS managed policies & Customer managed policies);
  and Inline policies (not recommended)
  - [Example IAM Identity-Based Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html){:target="_blank"}
- **Resource-based** policies


## Common IAM Tasks

- [Creating IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html){:target="_blank"}
- [Quick Links to Common Tasks](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_quick-links-common-tasks.html){:target="_blank"}
- [Example IAM Identity-Based Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html){:target="_blank"}

## References

- [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html){:target="_blank"}
- [IAM API Reference](https://docs.aws.amazon.com/IAM/latest/APIReference/Welcome.html){:target="_blank"}
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html){:target="_blank"}