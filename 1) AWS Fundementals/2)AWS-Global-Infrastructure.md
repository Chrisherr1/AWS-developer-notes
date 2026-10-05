AWS GLOBAL INFRA

AWS Regions:
-------------
    - It's an area of the world that they have selected and inside this region is a full deployment of AWS services(EC2,s3,etc,etc).
    - Usually far from people due to noise.

Benefits:
    *Geographic Separation - Isolated Fault Domain
        - meant to be 100% Isolated
    *Geopolitical Separation- Different Governance
        - Depending on the country/region you will have to follow
        their rules, for better or for worse.
        - Data will stay in that location, unless you configure it. You Have to tell it to be okay with transferring data over countries.
    *Location Control - Performance
        - You can have your stuff super close to customers for fast
        services.

AWS Edge Locations:
---------------------
    - Smaller, only have content distribution services,some computing services.
    - Found in many more places.
    - Useful when your service needs to be close to customers.
    - Useful for fast efficient data transfer.


How can we refer to a region?
-----------------------------
    - Via Region code
    - Via Region

    eg: Region Code: ap-southeast-2
        Region Name: Asia Pacific(Sydney)

    Terminal will use code, console management will often use the name.
    it just depends.


What's inside a region?
-----------------------

    AWS gives MULTIPLE availability zones.

    The zones are isolated infrastructure inside a region.

    They are isolated so if one goes down for any reason, if it isn't region wide the other zones more likely than not be affected.


How do we describe the resilience level of a service?
----------------------------------------------------
    Globally Resilient
        - few in AWS
        - Means a service operates with a single database, it's one product.
        - Data is replicated across multiple regions inside AWS.
        - It would take the world to fail for a full outage.
    eg: IAM, Route53

    Region Resilient
        - One Set of data per region
        - Often will be replicated through many availability zones.
        - It would take the WHOLE region to fail for the service to fail.

    A-Z Resilient
        - Very prone to failure.
