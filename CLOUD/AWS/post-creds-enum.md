e.g, 
in black box lab env or red team setting after obtained and config'd creds 

first best commands to fire up

Whoami & Permissions

One of the first things you need to know is who you are (in the account you are in other info about the AWS env):

Easiest way, but might be monitored?
1. aws sts get-caller-identity
   
![image](https://github.com/user-attachments/assets/63860e9e-35a7-4409-b3f7-8446ae91f0e9)

aws iam get-user # This will get your own user


