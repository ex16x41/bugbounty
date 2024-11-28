# in black box lab env or red team setting after obtained and config'd creds (e.g., regular user, non root, and want to escalate or pivot) 
# that is my personal methodology (by default taken from https://cloud.hacktricks.xyz but with my modifications and examples/ explanation / order that fit me)

## The very first commands to fire up after obtain creds of user (check who you are and your permissions on the aws env > from permissions > policies > see exploit points, priv esc points)

| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile <PROFILENAME> sts get-caller-identity| ![image](https://github.com/user-attachments/assets/63860e9e-35a7-4409-b3f7-8446ae91f0e9) | generic true to any command - you can specify the --profile at the start or finish of command|   


| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile <PROFILENAME> iam list users| ![image](https://github.com/user-attachments/assets/f8038ce5-c25b-4851-a260-7e4a93fe3c3c) | if permissions allow this action you should see list of users (path/username/userid/arn/createdate) |   


| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile <PROFILENAME> iam get-user --user-name >USERNAME>| ![image](https://github.com/user-attachments/assets/06b2aeac-8189-490e-b381-03ef234e0a9d) | here below we get the info of our own user (the one we have auth'd with using the creds) | 


| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile <PROFILENAME> iam list-user-policies --user-name <USERNAME> |  ![image](https://github.com/user-attachments/assets/a6f5397f-9ab4-4227-aef5-ce85886a8d7e)| here we can sometimes see empty brackets, no policies to user, instead check attached (or other commands) | 


| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile <PROFILENAME> iam list-attached-user-policies --user-name <USERNAME>| ![image](https://github.com/user-attachments/assets/4ebe35b0-52f0-4727-9ffc-9ed3ad1b9826) | N/A | 


list version of policy 

![image](https://github.com/user-attachments/assets/49a00e02-5768-47dc-8faa-7125108f42a7)

![image](https://github.com/user-attachments/assets/cc6d572b-32f2-4f6b-8e64-6835dcf4e73e)


attach user policy IRL username 1 policy of another user with priv access
![image](https://github.com/user-attachments/assets/4c03ed46-4631-4d19-86e5-b242c82628f0)

