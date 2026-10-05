# IAM Users and ARNs

```text
IAM Users are an identity used for anything requiring long-term AWS access
e.g. Humans, Applications, or service accounts.

If you need to give someone access to your AWS account 99% of the time it would
be through a IAM user.
```

---

## Principal

```text
- Represents a entity trying to access an AWS account.
- At this point it's unidentified.
- Can be people,computers, services, or a group of any of these.
- For it to do anything it needs to authenticate and be authorized.

It is a entity that makes requests to IAM to interact with resources.

For it to do anything it must authenticate to a user within a IAM.

Authentication for IAM users is done via.
    1. Username and Password
    2. Access Keys

These are example of long term credentials.

1 is for usual users going through the console, 2 is usually for applications
trying to gain access or users connecting to the AWS Console via ssh console.
```

---

## Once a principal goes through the authentication process

```text
The principal is now known as a authenticated Identity.

An Authenticated Identity has been able to prove to AWS that it is the identity
it's claiming to be.

Once it is authenticated AWS knows which policies apply to that identity.
```

> **Authentication** is how a principal prove to IAM that it is the identity it claims to be(username&password OR Access Keys)
>
> **Authorization** is IAM checking statements either allowing or denying that access.

---

## Amazon Resource Name (ARN)

```text
They do one thing, uniquely identify resources within any AWS accounts.

When you're working with resources via Console or APIs, you'd use
the resources' ARN to do so.
```

### These are different

Format:

```text
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
```

Examples:

```text
arn:aws:s3:::catgifs
-> References a bucket ONLY, You'd use this if you wanted to
   grant access to a bucket or any actions regarding the bucket itself.

arn:aws:s3:::catgifs/*
-> References the object within the bucket ONLY, not the bucket itself doe.
```

> **These DO NOT OVERLAP, If you need access to the bucket AND the objects you'd potentially need both.**
>
> This is really tricky for most admins/architects.

---

## Exam PowerUps

```text
1. You can ONLY have 5,000 IAM users per AWS account.
    - IAM is global, so it's not per region it's per user.
    - An IAM User can be a member of 10 groups MAXIMUM.
    - Both have design impacts:
        - If you have system that requires more than 5000
          IAM users means you cannot have 1 IAM Identity per USER.

        - Might be a limit for internet-scale applications, might limit
          Large orgs & org merges.

        - If you have a project that needs more than 5,000
          identifiable users then IAM might not be the best for it.

Alternatives might be using IAM Roles & Identity federation fix.
```
