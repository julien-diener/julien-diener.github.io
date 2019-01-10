---
layout:     post
title:      Web app using Spark
date:       2015-03-16 09:00:00
author:     Julien Diener
summary:    Processing hdfs data from a spring web app
categories: blog-post
thumbnail:  blog
tags:
 - big-data
 - cloud
 - hadoop
 - spark
 - spring
 - web-service
 - java
---

In the [XData project]({{ site.baseurl }}{% post_url 2014-10-01-XData-project %}) I had to convert a stand alone Spring web app into a “big-data” web app running on a hadoop cluster. To do that, I chose to use apache spark and spark-hive because it provided the most practical interface. I however could not find any documentation or tutorial on such use of spark in java spring web application.

To test how to setup such application, I made two getting-started prototypes:

  1. [A spring+spark web app](https://github.com/julien-diener/sparkwebapp): a minimal web service that reads and converts files either on local file system or on hdfs, using spark.
  2. [A spring+spark-hive web app](https://github.com/julien-diener/sparkhivewebapp): a minimal web service that generate a hive table and requests content from it.

The main difficulty is about run-time dependencies: dependencies used for compilation (such as provided through maven) are not working together at run-time (at the time of writing this post).

To run stand alone app, one should add the `$SPARK_HOME/lib/spark-assembly-X.X.X-hadoopY.Y.Y.jar` (provided by the spark installation) to the classpath. For the spark-hive case, the datanucleus dependencies found in spark lib should also be added. Because, web app are run by a servlet container, such as tomcat or jetty, this jar should be added:

  1. Either to the war file, such as recommended for web app. It is however a 140Mb dep. This is what is used in the spring+spark web app (1).
  2. Or to the class path of the servlet container. This is what is used in the spring+spark-hive web app (2) which is added to the maven jetty plugin.

For my (professional) work, I choosed the second solution: add the spark jar to maven jetty plugin which is used during development, and I included the jetty-runner to the project which I run with spark jar added to to classpath (using the `–jar` option).
This entry was posted in big-data, hadoop, java, other, spark, spring, web-service on 16 March 2015 by diener. 