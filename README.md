# Cloud AWS Recon & Hacking (s3) ;^)  -if you find bugs using this rep, credit <3

# First let's identify how s3 buckets look like in real life? we have multiple scenarios

**example URL one (here the url format is targetbucket.amazon)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fc44f23e-0afb-4dfa-ad9a-2da9f3ac3ac9)




**example URL two (here the url format is amazon.targetbucket)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/0b4bdcdf-4cdf-4c1b-8c6a-e67005464dae)




**example URL three (here the domain is not revealing the bucket directly, but instead under name tags that differ)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/572c8421-cd1b-415b-a580-ea3cfc926aad)



**example URL four (here the name of the subdomain and bucket name match)** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d15189e3-646b-4b7a-914a-c2c5f189892a)



# How and where to find buckets directly on target? manually

**view source code (S3 Bucket URL hardcoded in HTML of webpage)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6201e729-f33a-49d3-9ca9-2c0faf00f009)

**inspect network traffic - see server GET requests** (can filter keyword as per usual url formats)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/dc6aec45-de04-4d4c-9409-5293fd4458dd)

# other methods to find s3 buckets 

**reverse IP lookup** 

**3rd party sites like git rep/code**

**bruteforce** 


# Find s3 buckets using tools 

https://github.com/nahamsec/lazys3/ 


# Type of bugs to look for on s3 by most common first

**exploiting poor permission configuration** 

**information exposure** 

**s3 takeover** 





# commands to run tests with

**list contents of bucket aws** s3 ls s3://bucket --no-sign-request

**recsuisively list files** aws s3 ls s3://bucket --no-sign-request --recursive

**download files test** aws s3 cp s3://bucket/folder/file . --no-sign-request

**upload file test permissions** aws s3 cp localfile s3://[name_of_bucket]/test_file.txt –-no-sign-request

to list dirs close with /dir/

good to test --recrusive if there is folder forbidden for ls 

curl -I https://s3.amazonaws.com/bucket - this will show region configured in this bucket

Identify overly permissive policies (e.g., Action set to "*")





# Read access control list

At bucket, level allows to read the bucket’s Access Control List and at the object level allows to read the object’s Access Control List. Read ACL can be tested with the AWS command line using the following command

aws s3api get-bucket-acl --bucket [bucketname] --no-sign

aws s3api get-object-acl --bucket [bucketname] --key index.html --no-sign-request




**notes:**
some buckets will allow ls using --no-sign-request but will not allow download of files from it (forbidden) 



# Let's talk about non direct recon 

**here we have two options, one is google dorks, another is 3rd party site tools** 

**tools** 
https://buckets.grayhatwarfare.com/ - some paid features 



**dorks:**

site:http://s3.amazonaws.com intitle:index.of.bucket

site:http://amazonaws.com inurl:".s3.amazonaws.com/"

site:.s3.amazonaws.com "Company"

intitle:index.of.bucket

site:http://s3.amazonaws.com intitle:Bucket loading

site:*.amazonaws.com inurl:index.html

Bucket Date Modified
