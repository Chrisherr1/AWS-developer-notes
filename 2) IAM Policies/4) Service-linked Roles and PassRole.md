# Service-linked Roles and PassRole

## Service-linked Roles

A service-linked role is an IAM role linked to a specific AWS service. Its permissions are always predefined by the service.

They provide the permissions a service needs to interact with other AWS services on your behalf.

The service might create/delete the role itself, or might let you do it during setup or within IAM.

*Key differences between service-linked roles and regular IAM roles:*
1. You can't delete a service-linked role until it is no longer required by the AWS service. That means you have to remove the resources that depend on it first. Example: every load balancer has to be deleted before the ELB service-linked role can be. This keeps you from deleting the role and breaking the service.
2. You can't edit its permissions policy, and its trust policy only lets that one service assume it.

They're easy to spot by name. They live under the `/aws-service-role/` path and are named like `AWSServiceRoleForElasticLoadBalancing`.

## Managing Service-linked Roles

* `iam:CreateServiceLinkedRole` is needed by whoever performs the action that makes the service create the role. Example: the first person to create a load balancer in the account. Scope it with the `iam:AWSServiceName` condition key.
* `iam:DeleteServiceLinkedRole` is needed to delete one.

## What is PassRole?

`iam:PassRole` is the permission that lets you hand an existing IAM role to an AWS service so that service can assume the role and act with its permissions.

Many services need a role to do their job. A Lambda function needs an execution role, an EC2 instance needs an instance profile, an ECS task needs a task role, and a CloudFormation stack can use a service role.

When you create or configure one of those resources, you're telling AWS "run this thing as that role." Before the call goes through, AWS checks whether you have `iam:PassRole` on that specific role.

PassRole isn't an API you call directly. AWS checks it as part of another call like `CreateFunction` or `RunInstances`, so it doesn't show up in CloudTrail as its own event.

## Why does PassRole exist?

Without it, anyone with `lambda:CreateFunction` could attach an admin role to a function, invoke it, and run code with full account access.

PassRole stops you from giving a service more power than you're allowed to grant. It blocks privilege escalation.

## Role Separation

Role separation is when you separate the ability to:
1. Create roles
2. Use roles

An admin creates a role with exactly the permissions a service needs. A developer gets `iam:PassRole` on that one role, but no `iam:CreateRole` or `iam:PutRolePolicy`.

The developer can **use** the role by attaching it to a Lambda function or EC2 instance, but can't **create or change** what the role is allowed to do.

PassRole is what makes role separation possible.

## What a pass has to clear

For a pass to work, two things have to be true:
1. Your identity policy allows `iam:PassRole` on that role.
2. The role's trust policy allows the service principal to assume it (example: `lambda.amazonaws.com`).

## PassRole vs AssumeRole

* `sts:AssumeRole`: **you** take on the role and get temporary credentials.
* `iam:PassRole`: you **give** the role to a service, and the service assumes it.

## Scoping PassRole

Limit `Resource` to the specific role ARN, and use the `iam:PassedToService` condition to limit which service the role can be passed to.

```json
{
  "Effect": "Allow",
  "Action": "iam:PassRole",
  "Resource": "arn:aws:iam::123456789012:role/my-lambda-exec-role",
  "Condition": {
    "StringEquals": { "iam:PassedToService": "lambda.amazonaws.com" }
  }
}
```

Using `"Resource": "*"` on PassRole is a common misconfiguration because it lets someone pass any role in the account.

## How does it connect with service-linked roles?

You generally don't pass a service-linked role yourself, because the service creates it and assumes it on its own.

The permission you'd need there is `iam:CreateServiceLinkedRole` (see Managing Service-linked Roles above).

## Exam tip

If a developer gets "not authorized to perform iam:PassRole" while creating a Lambda function or launching an instance with a role, the fix is to grant PassRole on that role. Changing the role's own permissions won't fix it.