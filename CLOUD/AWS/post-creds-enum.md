e.g, 
in black box lab env or red team setting after obtained and config'd creds 

first best commands to fire up

Whoami

One of the first things you need to know is who you are (in where account you are in other info about the AWS env):

# Easiest way, but might be monitored?
aws sts get-caller-identity
aws iam get-user # This will get your own user

