# AWS Pentester/Red Team Methodology

In order to audit an AWS environment it's very important to know: 
which services are being used?
what is being exposed?
who has access to what?
and how are internal AWS services and external services connected?

From a Red Team pov, first step to compromise an AWS env is to obtain some credentials. 

**To obtain aws creds you could look into:**

**OSINT search for direct aws creds:** leaks via git-like sites (using collective dorks or one by one, also look into company profile on git-like sites, use scripts or scanners to mass scan for targeted creds + keyword of company name

**Password reuse** (3rd party breaches or password leaks that can lead to creds of aws, e.g., hacked github with private rep with creds to aws OR anything like that) 

**Web frameworks misconfigs** that expose directly hardcoded aws credentials like via this file I created https://github.com/ex16x41/bugbounty/blob/main/WEB/WEB-FRAMEWORKS/WebFrameworks-Exposures.md

**Vulnerabilities in AWS-Hosted Applications**

**Server Side Request Forgery with access to metadata endpoint**

**Local File Read**

 /home/USERNAME/.aws/credentials

 C:\Users\USERNAME\.aws\credentials

**Internal Employee**(social eng. enagegement sample of target firm)

**Cognito credentials**
