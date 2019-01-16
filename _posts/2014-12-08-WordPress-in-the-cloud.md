---
layout:     post
title:      WordPress in the cloud
date:       2014-12-08 09:00:00
author:     Julien Diener
summary:    Free and simple
categories: blog-post
thumbnail:  blog
tags:
 - cloud
 - cms
 - dns
 - website
---

Here is a simple method to deploy a wordpress server on the redhat cloud and attach it to a domain name, for free.

This is what I have done to host this site [Not anymore, see this post]({{ site.baseurl }}{% post_url 2017-12-01-Wordpress-on-AWS %}).

Create a wordpress server:

  1. Create an account on [OpenShift](https://www.openshift.com/), or login
  2. Add an application, and select “wordpress”
  3. If the account was just created, choose [its (unique) namespace](https://access.redhat.com/documentation/en-US/OpenShift/2.0/html/User_Guide/chap-OpenShift-User_Guide-Namespaces.html)
  4. Choose the application name and fill up the form
  5. Go to `application-namespace.rhcloud.com` site to create the wordpress user account
  6. Add content and customize the site directly from wordpress

Access the server:

  1. [install the rhc command](https://developers.openshift.com/en/getting-started-client-tools.html), then run  rhc setup
  2. log in with ssh and/or git clone the wordpress repo from openshift
    - The url for ssh and git can be found on the page of the application once [logged in openshit](https://openshift.redhat.com/app/login?then=%2Fapp%2Fconsole).
  3. Note for git: content should be added in the `.openshift/[themes|plugins|...]` folder of the repo. It will be copied in the suitable folder of the wordpress server (i.e. `$OPENSHIFT_DATA/[themes|...]`) by git push.

Finally, to attach this application to a domain name:

  1. Follow this [2 steps procedure](https://help.openshift.com/hc/en-us/articles/202301854-How-can-I-set-up-my-own-domain-name-to-point-to-my-app-)
  2. Then in wordpress dashboard > setting > general, change the “site address (url)” with the url of your domain
  3. Note: to get a free (sub)domain name, check [freedns.afraid.org](http://freedns.afraid.org/)
