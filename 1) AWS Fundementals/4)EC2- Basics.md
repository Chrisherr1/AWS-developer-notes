Elastic Compute Cloud(EC2) Basics

    EC2 is AWS's implement of IAAS Infrastructure as a service.

    It allows you to providion virtual machines known as instances with resources you select and an operating system of your choosing.

    This overviews
        1. What an instance is
        2. Instance states
        3. What an Amazon Machine does
        4. Talks about how to connect to
            instances.


**Notes:
    - EC2 should be the default for any compute needed.

**EC2 Key Facts & Features**
---
    - IAAS - provides Virutal Machines => instances

    - EC2 is a a PRIVATE service by default
        - uses VPC networking

    *Means it runs in the private AWS zone,
    usually configured to launch into a single VPC subnet.

    * You set this when you launce the instance, you also have to configure an public access, if you want that. Because it is by default a private service.

    * If you do want to support public access than the VPC supporting that EC2 must support that public access.

    * With the default VPC this is usually configured for you..
    If you use a custom you'll need to configure that.

    - Now Because an instance is launched into a specific subnet,
    and because a subnet is in a specific availability zone..

    That means that EC2 Is *AZ* resilient!

        That means that if the AZ that an instance is launched into
        fails, then the instance itself will likely fail.

    - Basics - you can choose various sizes and capabilities.

    These choices choices effect the resources the instance gets as well as extra capabilities, such as GPU, more advanced storage or networking or processes. You can change it after as well.

    - Offers On-Demand Billing
        - per second.
        - Only pay what you consume.
        - charge for running the instance,charge for storage the instance uses, charge for commercial software it runs with.
        
    - instances can use two popular types of storage thats on local host...
        1. EC2 Host storage
            - The storage already on the ec2 machine

        2. Elastic Block storage(EBS)
            - which is a network storage made available to that Ec2 if you wanted a separate storage on the network.

**EC2 - Instance Lifecycle**
---
    EC2 instances have attributes called a state.

    the state tells us the condition of the ec2.

    Important states:

        1. Running
        2. Stopped
        3. Terminated

    If you shutdown the instance it can be moved from running to stopped or vise versa when you start up the instance again.

    Like switching off an appliance when you don't need it.

    NOW if you TERMINATE an instance...

    This is a one way change, meaning if you do it you can't undo it.
    it's fully deleted at that point.

    The reasons for the states, is it changes how much you get charged.

**Billing**
---
    When in running:
        - Will get charged for all 4 categories
            1. CPU capacity
            2. Memory
            3. Operating System 
            4. Networking

    When in Stopped:
        - Will get charged for only

            1. EBS Storage that has been allocated for the instance.

            Everything else isn't charged.
            cpu,memory,operating system,networking


    Only way to have no charge for an ec2 instance is through 
    TERMINATION.
    But be careful because it isn't reversable.

**Amazon Machine Image(AMI)**
---
    Is an image of an ec2 instance, it can be used to create 
    a ec2 instance or be created by a ec2 instance.

    an AMI contains
        1. Attached Permissions
            -controls which accounts can or cant use the AMI
            - Can be set public, everyone can use the AMI to launch
            instances
            - default : public LInux or windows

            - The owner of the AMI has implicit allow, allows them to add instances whenever.

            - You can add explicit permissions to that AMI
            where the owner explicitly grants access to that AMI for 
            specific AWS accounts.
        
        2. Boot Volume of the instance
            - Root or C:/ drive
            - It will always have one boot volume.

        3. Block Device mapping
            - configurations that the AMI has and how they're presented.
            - determines which is the boot volume and which is the 
            data volume.

        The way this works is the operating system is exepecting to 
        recieve volumes presented to it as well as an ID, Device ID.

        The block Device mapping links to the device ID that the operating system expects.

        
**Connecting to EC2 Instances**
---
    - They can run Linux or different versions of windows.

    - You connect to windows systems using RDP(Remote desktop protocol) PORT 3389

    - You connect to a Linux system using SSH PORT 22
        - YOu authenticate to that instance using a SSH key Pair.




**Security Groups vs Key Pairs**
- Security groups are firewalls that control which IP addresses can reach your EC2 instances, on which ports and protocols.

- Key pairs are login credentials that prove you're allowed to SSH into an instance once your traffic gets through.




    
