Virtual Private Cloud
----------------------

    VPC - Virtual Private Cloud is a virtual network inside AWS.

    A VPC is within 1 account & 1 region.

    Regionally resilient, they operate from multiple availability zones.

    - By default, are private and isolated unless you decide otherwise.

    - Services deployed into the same VPC can communicate,
    but the VPC is isolated from other VPCs and from the Public AWS zone and the public internet.


**-Two Types - Default VPC and Custom VPCs.**

    Default VPC is MAX 1 per REGION.

    Custom VPC is as many as you want.
        - you can configure them as you want as long as you stay under the rules and limits of VPCs.
        - Require you to configure everything end-to-end in detail, 100% private by default.
        
*In real deployments you will be using a VPC*

    You can configure these to communicate to other cloud platforms or even your own infra.

    Default VPCs are created by AWS.
        They come preconfigured in a specific way, so they are less flexible than custom VPCs.

**VPC Basics**
--------------
    A region can have multiple custom VPCs within it and unless you configure it otherwise there is no way a VPC can communicate outside their specific private network.

*This example is for default VPC*

    Every VPC is allocated a range of IP addresses called the 
    VPC CIDR
    --------

    The VPC CIDR defines the IP address the VPC can use,

    Everything inside a VPC uses the CIDR range of that VPC.

    If anything needs to communicate with a VPC and assuming you allow it, it needs to communicate to that VPC CIDR.

    Any outgoing connections will originate from somewhere in that VPC CIDR.

    It's just the IP address range of the VPC.


*Custom VPCs can have multiple CIDR ranges*

    But the custom always gets 1 CIDR range, and it's ALWAYS the same.

    172.31.0.0/16

    This is strength because it's always configured in the same predictable way.

    You'll know that each region will have multiple availability zones, and each is an independent pool of infrastructure.

    The way that a VPC provides resilience is that it can be subdivided into subnets/subnetworks.

    Each subnet is located in one availability zone.

    This is set on creation and can never be changed.

    With the default VPC it's always configured in the same way,
    it's preconfigured to have one subnet per availability zone in that region.

    Each will use the IPs available to them by the CIDR 172.31.0.0/16

    These IP ranges cannot be the same as other subnets in the VPC,
    and they cannot overlap with any subnets inside the VPC.

    /20 Subnet in each AZ in the region
    - Each Default VPC comes with
        1. Internet Gateway(IGW)
        2. Security Group(SG)
        3. NACL
    - The subnets assign public IPv4 addresses.

    
