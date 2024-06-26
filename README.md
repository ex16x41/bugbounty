# Cloud AWS Recon & Hacking (s3) ;^)  -if you find bugs using this rep, credit <3

# First let's identify how s3 buckets look like in practice?

**example URL one (here the url format is targetbucket.amazon)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fc44f23e-0afb-4dfa-ad9a-2da9f3ac3ac9)

**example URL two (here the url format is amazon.targetbucket)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/0b4bdcdf-4cdf-4c1b-8c6a-e67005464dae)


# How and where to find buckets directly on target?

**view source code**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6201e729-f33a-49d3-9ca9-2c0faf00f009)

**inspect network traffic - see server GET requests** (can filter keyword as per usual url formats)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/dc6aec45-de04-4d4c-9409-5293fd4458dd)

# other methods to find s3 buckets 

**reverse IP lookup** 
**3rd party sites like git rep/code**
**bruteforce** 

# Type of attacks on s3 by most common first

**exploiting poor permission configuration** 
**information exposure** 
**s3 takeover** 
**


**Got a target?** 

list contents of bucket aws s3 ls s3://bucket --no-sign-request

aws s3 ls s3://bucket --no-sign-request --recursive

aws s3 cp s3://bucket/folder/file . --no-sign-request

to list dirs close with /dir/

good to test --recrusive if there is folder forbidden for ls 

curl -I https://s3.amazonaws.com/bucket - this will show region configured in this bucket

**notes:**
some buckets will allow ls using --no-sign-request but will not allow download of files from it (forbidden) 


**dorks:**
site:http://s3.amazonaws.com intitle:index.of.bucket
site:http://amazonaws.com inurl:".s3.amazonaws.com/"
site:.s3.amazonaws.com "Company"
intitle:index.of.bucket
site:http://s3.amazonaws.com intitle:Bucket loading
site:*.amazonaws.com inurl:index.html
Bucket Date Modified
