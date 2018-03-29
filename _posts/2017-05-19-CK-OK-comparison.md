---
title: Is co-Kriging always better than ordinary Kriging?
tags:
  - spatial statistics
  - question
---
A quick summary of the comparison between co-Kriging and ordinary Kriging.

<!--more-->

## 1. Discussions on CK and OK

There have been many discussions about the comparison between co-Kriging (CK) and
ordinary Kriging (OK) in terms of prediction error and variation. For example, a
[technical note](http://www.css.cornell.edu/faculty/dgr2/teach/R/R_ck.pdf)
about CK with ``gstat`` package in R compares CK and OK using different co-variates with different degree of correlation with the response.
Also, the documentation of CK in [ArcGIS](http://desktop.arcgis.com/en/arcmap/latest/extensions/geostatistical-analyst/understanding-cokriging.htm)
mentions that "theoretically, you can do no worse than kriging because if there is no cross-correlation,
you can fall back on autocorrelation for the response."

To summarize, a common conclusion is that if there is strong correlation between
a covariate and the response, CK would make better prediction than OK, otherwise,
CK would make no better prediction than OK. So, the answer to the question is "no"
as CK is better that OK only if there exist strong correlations between covariates and response.

## 2. A new discussion
We should know that the conclusion above is not strictly accurate or reliable for every situation. Under some situations, even a strong correlation is found between a covariate and the response from the observations, CK is still likely to be worse than OK. An example is as follows:
