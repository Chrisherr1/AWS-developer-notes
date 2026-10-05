Public vs Private Services:

    Both are not what you think, they are referring to
    networking ONLY.

    Public service is something that is accessed via public endpoints.
    eg: simple storage.(S3)
        It can be accessed ANYWHERE, with a internet connection

    Private service is something that runs in a VPC, So only things
    within that VPC can access the service or things that are connected to that VPC.

    For both there are permissions as well as networking.

    So even though S3 is a public service, by default an identity
    other than the account root user, has no authorization to access
    that resource.

    So permissions and networking are two different considerations.

When reviewing public versus private services,

    It's the networking that matters.

When thinking about any public cloud environment:

**Think about 3 Zones!**


*Internet ZONE*
- Internet services Direct Access to Internet Services.

*AWS Private Network Zone*
- Think home networks, how only things connected can often communicate via LAN or things you've let in.

    VPCs are isolated unless configured otherwise.
    Nothing from the internet can access these, services can be put
    inside them(EC2 instances,etc).

    Internet access inbound/outbound is only allowed if you allow it.

*AWS Public Zone*

- This runs between the public internet and private zone networks. It is not on the public internet, it's a network that is connected to
the public internet.

    This Public Zone is where AWS public services operate from.

    Services with public endpoints such as S3.


If you're accessing a service from the internet, you are basically going through the public Internet zone and access the AWS Public zone to access those services.


**later you'll find out that private networks in the AWS Private Zones can be connected to other private zones and even to business private servers**
**You can also create and attach an internet gateway to a VPC to allow you to allow resources within that VPC to access the internet
at the requirement of a public IP address**
    having the gateway can allow it to gain access to public aws services like S3, but crucially you'll see that this never hits the public internet at any point, it communicated only to the AWS Public Zone.

    
