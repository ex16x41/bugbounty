e.g, 
in black box lab env or red team setting after obtained and config'd creds 

first best commands to fire up

Whoami & Permissions

One of the first things you need to know is who you are (in the account you are in other info about the AWS env):

Easiest way, but might be monitored?
1. aws --profile [profilename from config cred file] sts get-caller-identity (if error output, check creds config file)
   
![image](https://github.com/user-attachments/assets/63860e9e-35a7-4409-b3f7-8446ae91f0e9)
![image](https://github.com/user-attachments/assets/f8038ce5-c25b-4851-a260-7e4a93fe3c3c)
![image](https://github.com/user-attachments/assets/874e2033-9609-497b-b19d-3239aa4c87a1)
![image](https://github.com/user-attachments/assets/e4f79ee9-8b1b-46b9-be0e-e642ce92556c)
![image](https://github.com/user-attachments/assets/d1e66c86-f2fb-46c0-90a9-2f8ab309951f)

here below we get the info of our own user (the one we have auth'd with using the creds) 

![image](https://github.com/user-attachments/assets/06b2aeac-8189-490e-b381-03ef234e0a9d)




