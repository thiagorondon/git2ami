git2ami
=======

Create a new Amazon Machine Image from a git repository.

You need just bash script and Amazon EC2 API Tools.

- http://www.gnu.org/software/bash/
- http://aws.amazon.com/developertools/351

How ? Why ?
===========

You just need a ".git2ami" file in your repository with all instructions for build your new AMI.

It's a good way to manage changes, continuous integration and auto-scaling in Amazon EC2.

Synopsis
========

```
$ ./git2ami user@repo.domain.org:app.git tmpdir
ami-ca20XXXX

$ GIT2AMI_DEBUG=1 git2ami user@repo.domain.org:app.git tmpdir
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

PACKAGER=aptitude
PACKAGES="build-essentials nginx"

RUN=scripts/deploy.sh
```

NO WARRANTY
===========

This software is provided "as-is," without any express or implied warranty. In no event shall the author be held liable for any damages arising from the use of the software.

LICENSE
=======

GPLv3


