**S3 Basics**
---
    Simple Storage Service(S3)

    It provides a near infinitely scalable object storage platform-
    Accessable from anywhere with a public internet connection.

    It tends to be default storage location for 
    `data ingestion` and output for many AWS services.

    This will go over s3, Objects, and Buckets.

**S3 101**
---
    It's a global storage platform
        - regional based / resilient

        - Resilient because the data is replicated to the availabilities zones within that region.

        - Regional because Its because the data is stored in a specific AWS region at
        rest.

        - Never Leaves that region unless YOU configure it to.

    Its a PUBLIC service, so it can be reached anywhere you have an 
    internet connection.

    The service itself runs from the AWS public zone.

    It can cope with unlimited data amounts and is designed for multi-user usage of that data.

**s3 is PERFECT for hosting large amounts of data.**
    - Movies,audio,photos,text,large datasets
    - Scales to Unlimited storage.
    - Great VALUE

YOu can access it via HTTP,SSH,or even gui.

**Think of it as your default starting point, when you need data storage**

S3 has 2 main things it delivers
    1. Objects
    2. Buckets

Objects are the data that s3 stores, Photos,video, ect.
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
        - * Rememeber unless you configured it only the root user can access the files in s3.

    2. Value
        - This is the actual file
    
    3. Metadata
        - Version Id
        - MetaData
        - Access Control for the object
        - Subresources

**S3 Buckets**
---
    Region locked, meaning that the data is stuck in the region you set it to and MUST adhear to laws of that area.

    It also means that if the entire region effected, your data will be effected.

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

**Buckets are just a container that's stored in a region.And for S3 they're generally where alot of permissions and options are set.**

**SO you go to the bucket to configure the way the S3 works.**


**EXAM POWERUPS!!!!!!**
---

    - Bucket names are globally unique!
        - if you try making a bucket and it gives you an error it's usually becuase somone else already has that bucket name

    - 3-63 characters all lowercase, start with lowercase letter or number, CANNOT BE IP FORMATTED 1.1.1.1

    - Buckets have a soft limit of 100 and HARD limit of 1000 per account.
        Use Prefixes to your advantage!, prefixes to sort data within 1 bucket!

    - You may have unlimited objects in a bucket, 0bytes to 5TB

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


