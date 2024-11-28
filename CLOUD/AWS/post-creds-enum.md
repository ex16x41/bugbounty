# in black box lab env or red team setting after obtained and config'd creds 
# that is my personal methodology (by default taken from https://cloud.hacktricks.xyz but with my modifications that fit me)

## The very first commands to fire up after obtain creds of user (check who you are and your permissions on the aws env > from permissions > policies > see exploit points, priv esc points)

| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile XYZ sts get-caller-identity| ![image](https://github.com/user-attachments/assets/63860e9e-35a7-4409-b3f7-8446ae91f0e9) | generic true to any command - you can specify the --profile at the start or finish of command|   


| command | IRL sample | comments | 
|-----:|---------------:|---------------|
|aws --profile XYZ iam list users| ![image](https://github.com/user-attachments/assets/f8038ce5-c25b-4851-a260-7e4a93fe3c3c) 
![image](https://github.com/user-attachments/assets/874e2033-9609-497b-b19d-3239aa4c87a1) | generic true to any command - you can specify the --profile at the start or finish of command|   


![image](https://github.com/user-attachments/assets/e4f79ee9-8b1b-46b9-be0e-e642ce92556c)
![image](https://github.com/user-attachments/assets/d1e66c86-f2fb-46c0-90a9-2f8ab309951f)

here below we get the info of our own user (the one we have auth'd with using the creds) 

![image](https://github.com/user-attachments/assets/06b2aeac-8189-490e-b381-03ef234e0a9d)

here below output means no policies of user 

![image](https://github.com/user-attachments/assets/a6f5397f-9ab4-4227-aef5-ce85886a8d7e)

here below we check attached policies 

![image](https://github.com/user-attachments/assets/4ebe35b0-52f0-4727-9ffc-9ed3ad1b9826)

list version of policy 

![image](https://github.com/user-attachments/assets/49a00e02-5768-47dc-8faa-7125108f42a7)

![image](https://github.com/user-attachments/assets/cc6d572b-32f2-4f6b-8e64-6835dcf4e73e)


attach user policy IRL username 1 policy of another user with priv access
![image](https://github.com/user-attachments/assets/4c03ed46-4631-4d19-86e5-b242c82628f0)

