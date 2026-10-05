# CloudFormation Basics

```text
CloudFormation is an infrastructure as Code (IaC) product in AWS which allows
automation infrastructure creation,update, and deletion.

Templates created in YAML or JSON can be used to automate infrastructure operations.

Templates are used to create stacks, which are used to interact with resources
in an AWS account.

These templates can be used to update infrastructure.
```

---

## What makes up a template?

```text
The components are..

1. List of resources, at least one
    - It's the resources section of a CloudFormation template that tells
      CloudFormation what to do. IF resources are added to it then
      CloudFormation creates resources.
    - It updates and if a resource is removed and the template is reapplied
      then the resources are removed.
    - Only Mandatory part of a template.
```

> **IN EXAM**

```text
2. Description
    - It allows the author of the template to give some details about what the
      template is for what it does. Basically anything a dev should know about
      the resources being used here.

3. AWSTemplateFormatVersion
    - If you have both a description and a AWStemplateformatversion then the
      description MUST IMMEDIATELY follow it.
    - This template is NOT MANDATORY, but if you use them both you need to be
      aware of the conditions. So templateversion then description.
    - Its the way AWS can extend the standards over time.
```

> **IN THE EXAM**

```text
4. Metadata
    - Controls how different things in the CloudFormation Template are shown
      in the AWS Console.
    - You can specify groupings,control order, add descriptions and labels.
    - Generally the bigger the section the bigger the audience.

5. Parameter
    - Where you can add fields to prompt the user for more information in the AWS console.
    - Useful when you want to limit input or have default inputs for a user.

6. Mappings
    - It allows you to create lookup tables..
    - Note to self: Didn't really say much.

7. Conditions
    - this allows decision making in the template. So you can set stuff that
      will only occur if a condition is met.
    - Kinda like an If else for events that may occur.
    - Two step process
        1. Create the condition
        2. That condition is used within resources in the cloud formation template.
           (AKA needs to be stated that you're going to use it in the RESOURCES
           SECTION TOO if you're going to use it)

8. Outputs
    - Once the template has been created it can present outputs based on
      what's being affected.
    - create,update,deleted.
```

---

## Architecture of a Cloud formation

```text
Cloud Formations are made from a template.

Template contains all of the above remember.

Resources within a cloud formation template are called Logical Resources.

    A logical resource has a type, that helps in creating your resource.

    It also has properties that helps configure the resources in a certain way.

When you take a template, and give it to CloudFormation,
Then CloudFormation creates what's known as a stack.

It contains all of the logical resources that the template tells it to contain.

So a stack is a living and active representation of a template.

One template can create one stack or many stacks.

BUT a stack is basically when you take a template and tell
CloudFormation to do something with that template.
```

> **IMPORTANT**
> For any logical resources in the stack.. CloudFormation makes a corresponding physical resource in your AWS account.
>
> It's CloudFormation's job to keep the logical and physical resources in sync.

```text
So when you use a template to create a stack, CloudFormation will scan the template,
create a stack with logical resources inside, and then create physical resources which match.

You can ALSO take a template edit it and then use it to update the same stack.
    When you do that either new logical resources are added,
    or existing ones are updated or deleted

    - CloudFormation will do it on the physical resources.
```

### If you delete a stack..

```text
The Logical resources are deleted, which causes CloudFormation to delete the
matching physical resources.
```

---

## Many uses include

```text
1. You can use a template to deploy 1-infinite amount of sites at the same time.
2. Change Management- You can store templates in repos to have version control and
   have someone be able to look at it and edit it before actually applying the template.
3. You can use a template to spin up one-off deployments.
```
