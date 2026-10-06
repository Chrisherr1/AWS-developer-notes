# Security Token Service

The Security Token Service is a web service that enables you to request temporary, limited-privilege credentials for AWS IAM users or for users you authenticate (federated users).

It generates temporary credentials whenever `sts:AssumeRole*` is used, along with a few other calls (see Other STS Calls below).

## At a high level

When you assume an IAM role, you use `sts:AssumeRole`, and in doing so you gain access to temporary credentials, which can be used by the identity that assumes the role.

Temporary credentials are requested by an identity (either AWS or external).

They can be used to access AWS resources.

## What the credentials are

Similar to access keys, but with three parts:
1. Access key ID
2. Secret access key
3. Session token

The session token is what makes them temporary credentials. Every request has to include it (in the CLI or SDK, that's `AWS_SESSION_TOKEN`).

They expire and don't belong to the identity which assumes the role.

## Permissions

The credentials get the permissions in the role's permissions policy.

You can narrow them further by passing a session policy in the AssumeRole call, but they can never go beyond what the role allows.

## Expiration

* Default: 1 hour
* Range: 15 minutes up to the role's maximum session duration (1 to 12 hours)
* Role chaining (using role credentials to assume another role) is capped at 1 hour

## Steps usually when using STS

0. The trust policy controls who can assume a role.
1. `sts:AssumeRole*` calls are made by an existing identity, either AWS or external (federation). For cross-account access, the caller's own identity policy also has to allow `sts:AssumeRole` on that role. The trust policy alone isn't enough.
2. STS generates temporary credentials which can access AWS resources until expiration. They authorize access based on the role's permissions policy.
3. Credentials are returned to the identity requesting them. Another `sts:AssumeRole` is required when the credentials expire.

## Other STS Calls

* `GetSessionToken`: gives an IAM user temporary credentials. Most often used to make API calls with MFA.
* `GetCallerIdentity`: returns the account, ARN, and user ID of whoever is making the call. Handy for checking which credentials your code is actually using.
* `DecodeAuthorizationMessage`: decodes the encoded error some services return on an access denied. Classic exam question.
* `GetFederationToken`: temporary credentials for a federated user without assuming a role.
* `AssumeRoleWithSAML`: for SAML identity providers like a corporate Active Directory.
* `AssumeRoleWithWebIdentity`: for web identity providers like Google or Facebook. For mobile and web apps, AWS recommends Cognito instead.

## Exam

For the Developer Associate, a few STS calls are tested directly: `AssumeRole`, `AssumeRoleWithWebIdentity`, `GetSessionToken`, `GetCallerIdentity`, and `DecodeAuthorizationMessage`.

How other services use STS also matters. An EC2 instance profile or a Lambda execution role gets STS credentials behind the scenes, and the SDK picks them up and refreshes them automatically.