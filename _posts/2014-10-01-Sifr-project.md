---
layout:     post
title:      SIFR project
date:       2014-10-01 09:00:00
author:     Julien Diener
summary:    Ontology and web semantic
categories: project
thumbnail:  folder-open 
tags:
 - biological-data
 - ontology
 - sementic-web
 - web-service
 - java
 - spring
---

The [SIFR project](http://www.lirmm.fr/sifr/) investigate the scientific and technical challenges in building ontology-based services to leverage biomedical ontologies.

My work is on the the [annotators web service](https://github.com/sifrproject/annotators/) which purpose it to:

  1. Provide a unique access point to several server running the ontology annotators developed by the [NCBO](http://www.bioontology.org/), such as their [bioportal.bioontology.org/annotator](http://bioportal.bioontology.org/annotator).
  2. Wrap new functionalities around these annotators. In particular I work on adding RDF output format and the annotation scoring methods which have been published in [Scoring semantic annotations returned by the NCBO Annotator](https://hal.inria.fr/INRA/lirmm-01099860v1)
