# in black box lab env or red team setting after obtained and config'd creds (e.g., regular user, non root, and want to escalate or pivot) 
## that is my personal methodology (by default taken from https://cloud.hacktricks.xyz but with my modifications and examples/ explanation / order that fit me)

## think of exploiting cloud as a tree > one commamnd gives X type of output > take output X into a new command > extract output Y > put X and Y together and pivot to the next one to extract further info or pivot to cases like priv esc, exposure, misconfigured policies, permisions, etc. 
## The very first commands to fire up after obtain creds of user (check who you are and your permissions on the aws env > from permissions > policies > see exploit points, priv esc points)

| command (user data) | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> sts get-caller-identity| ![image](https://github.com/user-attachments/assets/217a2bd1-34aa-486c-87d3-3af248d05036) | generic true to any command - you can specify the --profile at the start or finish of command , also from this command we get the username (it's after :user/USERNAME") we need the USERNAME to use it to leverage other commands below| 

| command (user data) | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> iam get-user --user-name >USERNAME>| ![image](https://github.com/user-attachments/assets/f0eefcc8-d0bf-4bfe-a683-0c7f3f1e0b75)| here below we get the info of our own user (the one we have auth'd with using the creds) | 


| command (list users) | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> iam list users| ![image](https://github.com/user-attachments/assets/f8038ce5-c25b-4851-a260-7e4a93fe3c3c) | if permissions allow this action you should see list of users (path/username/userid/arn/createdate) |   


| command (policies)| IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> iam list-user-policies --user-name >USERNAME> |  ![image](https://github.com/user-attachments/assets/a6f5397f-9ab4-4227-aef5-ce85886a8d7e)| here we can sometimes see empty brackets, no policies to user, instead check attached (or other commands) | 


| command (policies) | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> iam list-attached-user-policies --user-name >USERNAME>| ![image](https://github.com/user-attachments/assets/4ebe35b0-52f0-4727-9ffc-9ed3ad1b9826) | from here we obtain policyARN, that we can pivot with this to next command (as below) | 

| command (policies versions) | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile >PROFILENAME> iam list-policy-versions --policy-arn >POLICYARN>|![image](https://github.com/user-attachments/assets/49a00e02-5768-47dc-8faa-7125108f42a7) | ARN can be pasted into its placeholder in the command with our without quatation marks, same output | 


## other enum options and commands here 
https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-services/aws-iam-enum 
