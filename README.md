check-reserved-instances
------------------------

This script shows summary about using "Reserved" and "On-demand" ec2 instances. Namely:

* Which "On-demand" instances haven't got a "Reserved" instance;
* Which "Reserved" instances are unused;
* And which "Reserved" instances are expiring soon.

The script is heavily based on Scott Bigelow's work: https://github.com/epheph/ec2-check-reserved-instances

### Requirements

The script is written in Python and uses only `boto`, `optparse` and standard datetime modules. 

### How to work with it

For the script needs your [AWS Security Credentials](http://docs.aws.amazon.com/AWSSecurityCredentials/1.0/AboutAWSCredentials.html). You can specify them in [the Boto config](http://boto.readthedocs.org/en/latest/boto_config_tut.html) (`~/.boto` or `/etc/boto.cfg`) or using script command line arguments or by exporting in an environment variables (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).

Example:

    host# export AWS_ACCESS_KEY_ID=ABCDE
    host# export AWS_SECRET_ACCESS_KEY=5ji7haengeeFoh8eziebeu
    host# check-reserved-instances --region us-west-1 -w 60
    Unused reserved instances:
    	(2)	m1.small	us-west-1c
    	(3)	m1.large	us-west-1c

    Soon expiring (less than 60d) reserved instances:
    	93bbbca2-d072-4dcc-bb7e-7c137ad565f7	m1.small	us-west-1c	2014-04-15
    	bbcd9749-4bf0-440a-bf53-3641e3732b73	m1.small	us-west-1c	2014-04-03

    On-demand instances, which haven't got a reserved instance:
    	(1)	m3.medium	us-west-1c
    	(3)	m1.large	us-west-1b
    	(1)	m1.medium	us-west-1b

    Running on-demand instances:   27
    Reserved instances:            22


For more help use:

    host# check-reserved-instances -h

