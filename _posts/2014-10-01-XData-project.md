---
layout:     post
title:      XData project
date:       2014-10-01 09:01:00
author:     Julien Diener
summary:    Data integration on hadoop and web-service using spark
categories: project
thumbnail:  folder-open 
tags:
 - big-data
 - data-integration
 - java
 - hadoop
 - spark
 - spring
 - database
 - web-service
---

The [XData project](http://www.xdata.fr/) was a french collaboration between industrials, startups as well as big companies, and academics. Its main objective was to develop innovative commercial products constructed from the integration of private data with open data.

I mostly work on the xdata “movement analytics” application. In particular:

  1. I worked on data integration of the movement data type: any type of data that represent people movement such as housing or companies moving, tourist displacement, or cell phone tracking. The integration is done in two main parts: first a generalized data structure defined with a generic data descriptor that allows importing any data set containing movement data ; second an automated data query algorithm made to select suitable movement entries with respect to geographical and temporal area and granularity.
  2. I was in charge of transfering a stand alone prototype of the main web application, which use mysql and spring technologies, on the hadoop cluster of the xdata project, in particular using [spark](http://spark.apache.org/) and hive.
