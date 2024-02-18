---
layout:     post
title:      WordPress on AWS
date:       2017-12-01 09:00:00
author:     Julien Diener
summary:    from Scratch
categories: blog-post
thumbnail:  blog 
tags:
 - cloud
 - aws
 - wordpress
 - web-site
 - database
---

On September 2017, the redhat cloud I used to host my wordpress site changed its structure (and pricing). It didn't fit my need anymore so I moved my website to AWS, which I used to work with.

Here is a summary of what I had to do:

There are lots of tutorial that explained everything (but for solving some critical problem explained below):

  - [account creation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html): signup, create an IAM account and follow all steps (vpc, security group)
  - [Launch an instance](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html#ec2-launch-instance): deploy your first AWS instance. I used the free tier t2.micro with standard EBS volume.
  - [Connect to instance](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
  - [Install the LAMP stack](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html): follow all steps (install pck, start apache+config, secure mysql, …)
    - Here I probably made a mistake when changing the ownership of some directories :-\
  - [Install WP](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hosting-wordpress.html)

It all worked fine, but I later had some trouble. My site wasn’t answering anymore and I couldn’t connect with ssh, timeout. I now think that I must have made an error with the credential. But at the time I didn’t know and, following some advice found on internet, I restarted my instance: I still couldn’t connect, but this time with connection refused…

After looking at the console log of my instance, I found out that ssh didn’t start, due to some incorrect owner rights on some system directories. But how to correct some file-system ownership when I cannot connect to the instance!?!

The solution, in short :

  - Shutdown the instance
  - Disconnect the EBS volume
  - Create a new instance (same config) and connect the EBS of the 1st instance on it
  - Start and connect to it.
  - Correct the files owner ship on the mounted drive
  - Revert the three first steps

