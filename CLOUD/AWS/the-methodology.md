# AWS Pentester/Red Team Methodology

In order to audit an AWS environment it's very important to know: 
which services are being used?
what is being exposed?
who has access to what?
and how are internal AWS services and external services connected?

From a Red Team pov, first step to compromise an AWS env is to obtain some credentials. 

To obtain creds you could look into:

    OSINT stage: I personally cover all that [HERE](https://github.com/ex16x41/bugbounty/blob/main/CLOUD/AWS/AWS-S3-HACKING-ENUM.md)
    Social Engineering

    Password reuse (password leaks)

    Vulnerabilities in AWS-Hosted Applications

        Server Side Request Forgery with access to metadata endpoint

        Local File Read

            /home/USERNAME/.aws/credentials

            C:\Users\USERNAME\.aws\credentials

    3rd parties breached

    Internal Employee

    Cognito credentials
