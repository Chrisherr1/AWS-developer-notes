# IAM Roles

```text
A roles is one type of identity that is found in AWS, Another type being
IAM users.

IAM users are usually used when you want to give this to ONE entity whether that
be a application,user,etc.

IAM roles are often used when you don't know how many people or services are going to
use this role.

If you can't number the amount of principals that will be using an identity,
then it's often better being a role than a user.
```

> **Role are often TEMPORARY, IAM Roles are assumed... you become that role.**

```text
It's often just a vessel to give you rights, and it's supposed to be temp,
only until you're not that role anymore.
```

---

## Role Policies

```text
IAM Roles can have inline policies and managed policies attached.
    These are called PERMISSIONS POLICIES.

IAM Roles have 2 types of policies.
    1. Permissions - Grant/Deny permissions
    2. Trust Policy - Controls which identities can assume that role.

    You have to explicitly say who IS ALLOWed to be this role.

If a identity is allowed and gains access to a role usually they are given a set of temp
security credentials.
    -> They are Time limited and expire eventually, Renewal is required.
    -> Need to be given at the end
```

> **TIP**
> Roles are used in organizations to allow us to use one account and access different accounts without needing to log in again.
>
> Really useful when managing multiple accounts.

---

## When to use IAM Roles

Common uses:

### 1. AWS services

```text
- AWS Lambda - This is a function as a service.
    - Typically you give it some code and it can start or stop EC2 instances
      or backups or even data processing

- The important bit is
    - like most AWS functions, it often has no rights to begin with.
    - Lambda is a function as a service, and it needs some way to gain
      permissions so it can do stuff.

To do this, we can create an IAM role.
    You'd include lambda in the trust policy allowing it to be that role, and you'd
    attach permissions to that role, often things that lambda would need to function.
```

#### Why would we use a role doe?

```text
The reason is because, you could have multiple lambda functions and you might add
more in the future that'd be a headache to deal with tbh.

AND

The other reason is because if you made lambda a IAM user then you'd have to hard code
credentials and whenever possible YOU wouldn't WANT TO DO THIS.
It's a security risk.
```

> ***It's always the preferred options when you want to make aws services do stuff on your behalf because you don't have to provide any static credentials that could potentially be found and abused.***

### 2. Emergency or Urgent situation

```text
- Used as a Break Glass situations.
- Roles can be used to give emergency permissions to a user.
```

### 3. When you're adding AWS to an existing corporate environment.

```text
- External identities cannot be used in AWS Directly!!!
- Therefore in a corporate environment where there's already a Active Directory service
  implemented, you couldn't use their login to give them access to the AWS.

- We could make a role though, and then give that external login/identity permissions
  to services at which point the login would work and they'd be able to use AWS
  services through a role.
```

> *Remember the 5000 IAM user Limit, if the org has more than 5000 people it's kinda unrealistic to use ONLY IAM users*

```text
ID Federation is the best way to do things.
    You have a couple roles and you just give external people or identities roles
    do what they need to do.
```

### 4. Designing architecture of Mobile application.

```text
- You can give an application a role so it can access AWS resources.
    - No AWS credentials on the app
    - Scales to 1million accounts
    - uses existing customer logins
```

### 5. Cross account access

```text
- Used when you use multiple AWS accounts.
- You can make a role in the partner account, to give access to the resources
  the partner account has.
```
