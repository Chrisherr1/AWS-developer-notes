**Shared Responsibility Model**
---

At a high level:
    AWS is responsible for the security of the cloud itself.

    You as a customer are responsible for security in the cloud.


So AWS are responsible for managing the security of the aws regions, availability zones, and the edge locations.

This is true for any compute,storage, database, and networking provided to you by AWS.

AND

Any software which assists in those services.

Don't need to worry about that stuff as a customer.

**So what is the customer responsible for?**
---
    1. Client-side data encryption,integrity & Authentication
    2. Server-Side Encryption (File System AND/OR data)
    3. Networking Traffic Protection(encryption,integrity, identity)

If your server uses SSL certificates, you manage that.
If you encrypt sever to server communication, you manage that.

You also responsible for the operating system,network,and firewall configuration for the instances.

You are also responsible for the platform, applications,idenity & access management.

You are also responsible for any customer data.(Backups and security)


**Very Important to know what you're responsible for**

