# Discover vuln(ver)/exposed/misconfig'd s3 bucketsMy hunting methodlogy

## Sources for external search (osint only)

1. https://osint.sh/buckets/ - a little better than grayhat because not limited to filtering by filetype (no reg req) 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/ef73ae2b-67e6-4e02-b418-0873517125a1)

2. https://buckets.grayhatwarfare.com/

![image](https://github.com/ex16x41/bugbounty/assets/44981946/f9c53007-c327-4d08-b0cc-3aa520ed650b)


# Internal search - host targeted 

## Identify s3 buckets - passive method 

[x] site:http://s3.amazonaws.com intitle:index.of.bucket

[x] site:http://amazonaws.com inurl:".s3.amazonaws.com/"

[x] site:.s3.amazonaws.com "Company"

[x] intitle:index.of.bucket

[x] site:http://s3.amazonaws.com intitle:Bucket loading

[x] site:*.amazonaws.com inurl:index.html

[x] Bucket Date Modified


## Identify s3 buckets - active method 

| Method | Detail if available|
|-----:|---------------:|
|    HTML inspection (S3 Bucket URL hardcoded in HTML of webpage) | e.g., "    <img src="https://s3.amazonaws.com/my-bucket/my-image.jpg" alt="My Image">"     |
|Brute-Force | Try to request folders that exist and see the server behavior (403s, blank page, or directory listing).  |  
|    DNS caching | send a very large path, break the headers format, or change the HTTP version.     |
| Reverse IP lookup (Bing Reverse IP) | Identify possible input points where the application is expecting data.  | 
|    Tools on GitHub |Lazy S3, bucket_finder, AWS Cred Scanner, sandcastle, Mass3, Dumpster Diver, S3 Bucket Finder, S3Scanner|




    


AWS S3 comes equipped with a range of permissions and access control mechanisms which if in the case overlooked by administrators and improperly implemented can act as a treasure of data

Misconfigured AWS S3 buckets that leave unauthorized access are thus abused by attackers to compromise the privacy of the data stored in those buckets breaching the privacy of millions of users around the world. If the case misconfigured S3 Bucket contains EC2 snapshot instances, then attackers might be able to retrieve the snapshot instance and then get security keys for the EC2 instance itself. 
