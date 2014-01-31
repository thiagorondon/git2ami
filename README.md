git2ami
=======

Create a new AMI from a git repository.

Synopsis
========

```
$ ./git2ami path/to/git.cookbook
ami-ca20XXXX

$ GIT2AMI_DEBUG=1 git2ami path/to/git.cookbook
- Create instance i-4d5dXXXX
- Check if instance i-4d5dXXXX is running.
- Get IP address ... ec2-54-214-000-00.us-west-2.compute.amazonaws.com
- Stop instance i-4d5dXXXX
- Check if instance i-4d5dXXXX is running.
- Check if instance i-4d5dXXXX is running.
- Create AMI
- New AMI is ami-9020XXXX

```

Cookbook for git2ami
====================

````
#
# .git2ami config
#

# Debug - Print a lot of messages.
# If you comment this line, just print errors or new AMI.
# GIT2AMI_DEBUG=1

# Define base AMI for deploy git repository
FROM=ami-6aad335a

# AWS instance type
INSTANCE_TYPE=t1.micro

# Specify REGION as the web service region to use.
REGION=us-west-2

# Private key to use
KEY_PAIR=justtest

# Private key file
PEM=$KEY_PAIR.pem

# Specifies the security group (or groups if specified multiple times)
# within which the instance(s) should be run. Determines the ingress
# firewall rules that will be applied to the launched instances.
SECURITY_GROUP=default

# Extra parameters for ec2-run-instances
EXTRA_EC2_RUN_INSTANCES=

# SSH port
SSH_PORT=22

# SSH username
SSH_USER=ubuntu

# The PREFIX name of new AMI.
PREFIX_AMI=GIT2AMI

#
# Deploy
#

RUN=scripts/deploy.sh
```

