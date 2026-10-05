**S3 Basics**
---
    Simple Storage Service(S3)

    It provides a near infinitely scalable object storage platform-
    Accessible from anywhere with a public internet connection.

    It tends to be default storage location for 
    `data ingestion` and output for many AWS services.

    This will go over s3, Objects, and Buckets.

**S3 101**
---
    It's a global storage platform
        - regional based / resilient

        - Resilient because the data is replicated to the availability zones within that region.

        - Regional because Its because the data is stored in a specific AWS region at
        rest.

        - Never Leaves that region unless YOU configure it to.

    It's a PUBLIC service, so it can be reached anywhere you have an 
    internet connection.

    The service itself runs from the AWS public zone.

    It can cope with unlimited data amounts and is designed for multi-user usage of that data.

**s3 is PERFECT for hosting large amounts of data.**
    - Movies,audio,photos,text,large datasets
    - Scales to Unlimited storage.
    - Great VALUE

You can access it via HTTP,SSH,or even gui.

**Think of it as your default starting point, when you need data storage**

S3 has 2 main things it delivers
    1. Objects
    2. Buckets

Objects are the data that s3 stores, Photos,video, etc.
Buckets are containers for objects.


**S3 Objects**
---
    You can think about objects as files/ Interchangeable.

    An object in s3 is made up of two main components
    and some associated meta data.

    1. Object key
        - Similar to a file name
        - Identifies the object in a bucket.
        - So if you know the object key you know which bucket it's in and its easy to identify the object.
        - * Remember unless you configured it only the root user can access the files in s3.

    2. Value
        - This is the actual file
    
    3. Metadata
        - Version Id
        - MetaData
        - Access Control for the object
        - Subresources

**S3 Buckets**
---
    Region locked, meaning that the data is stuck in the region you set it to and MUST adhere to laws of that area.

    It also means that if the entire region affected, your data will be affected.

**A BUCKET name MUST BE unique, as they can be placed in any region and BE UNIQUELY named compared to OTHER AWS accounts Buckets.**

    Buckets can hold unlimited objects, as they are more of a way of organizing/managing objects.

    Infinitely scalable.

    An S3 bucket has no complex structure.

    It has a FLAT structure.
        - ALL OBJECTS stored within the bucket are stored at the same level!
        - Not like a file system with directories within directories.
        - There's only one Directory/Bucket and everything GOES IN.

        - Everything is stored in the root.

        - It will be presented as a file system but it isn't that way.

            -No Concept of file types/ They are just stored as keys.
            - if we write a filename like..
                /old/Koala1.jpg.

            S3 will interpret it as /old being a folder. even though they aren't actually folders.

**Folders are often referred to as prefixes in S3, because they are part of the object names**

**Buckets are just a container that's stored in a region. And for S3 they're generally where a lot of permissions and options are set.**

**SO you go to the bucket to configure the way the S3 works.**


**EXAM POWERUPS!!!!!!**
---

    - Bucket names are globally unique!
        - if you try making a bucket and it gives you an error it's usually because someone else already has that bucket name

    - 3-63 characters all lowercase, start with lowercase letter or number, CANNOT BE IP FORMATTED 1.1.1.1

    - Buckets have a soft limit of 100 and HARD limit of 1000 per account.
        Use Prefixes to your advantage!, prefixes to sort data within 1 bucket!

    - You may have unlimited objects in a bucket, 0 bytes to 5TB

    - An Object consists of a key, value, Meta data

**S3 Patterns and AntiPatterns**
---
    S3 is an object store, not a file or block storage.
        - Meaning you can't mount an S3 bucket.
        - If you need block storage, you go to EBS storage.
            - Block storage is limited to one thing accesses it at a time.
        - S3 doesn't have that limitation but also means you can't 
        mount it as a drive.

    S3 is great for large scale data storage or distribution.

    It is good for offloading things as well.
        If you need users to grab photos or videos from a website you can instead point them to a S3 bucket directly to reduce compute costs.
    
    S3 should be your default when you're ingesting data OR Outputting data from a AWS product.


**BONUS TIP**

    Rule of thumb: if the site is pure frontend (a React build, a portfolio, docs, a landing page), S3 is cheaper, simpler, and scales for free. The moment you need server-side code or a database, you need EC2 (or a service like Lambda/Elastic Beanstalk).

    For the Developer exam, know that S3 static hosting is the go-to answer for "cheapest way to host a static site," and it's almost always paired with CloudFront in front of it for HTTPS and CDN caching, since S3 website endpoints don't do HTTPS on their own.

*When Implementing s3 Static website*

One exam-relevant nuance: data transfer from S3 to CloudFront is free, so putting CloudFront in front of your bucket can actually lower your total bill versus serving straight from S3, since edge caching means fewer requests hit S3 at all.

You'd need to implement a WAF+CloudFront to prevent abuse from flooding if necessary.

Usually CloudFront is enough though if no real traffic.

If someone tries hammering it it usually hammers the CDN instead.


**Deleting an S3 Bucket**
---
    You'll need to empty the bucket and then you can delete the bucket.

    Delete it if you're not using it as it takes up space meaning that you're paying for that space.
    
