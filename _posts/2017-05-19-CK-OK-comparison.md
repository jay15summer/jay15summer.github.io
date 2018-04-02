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
ordinary Kriging (OK) in terms of prediction error and variance. For example, a
[technical note](http://www.css.cornell.edu/faculty/dgr2/teach/R/R_ck.pdf)
about CK with ``gstat`` package in R compares CK and OK using different co-variates with different strength of correlation with the response.
Also, the documentation of CK in [ArcGIS](http://desktop.arcgis.com/en/arcmap/latest/extensions/geostatistical-analyst/understanding-cokriging.htm)
mentions that "theoretically, you can do no worse than kriging because if there is no cross-correlation,
you can fall back on autocorrelation for the response."

To summarize, a common conclusion is that
* if there is a strong correlation between
a covariate and the response, CK would make better prediction than OK, otherwise,
CK would make no better prediction than OK.

So, the answer to the question is "no", as CK is better than OK only if there exist strong correlations between covariates and response.
The "better" means smaller prediction error and variance.

## 2. A new discussion
The conclusion above is not strictly accurate or reliable for all situations, as in many conditions, even with strong correlated covariates, the outperformance of CK compared to OK is still hard to notice. So, a new problem would be
* when and why doesn't CK outperform OK?

Previous discussions focus on testing the influence of the correlation strength between covariates and response.
However, considering that Kriging is to make predictions at unknown locations based on known sampling locations and
[a previous post](https://jay15summer.github.io/2017/04/14/kriging-difference.htmlCK) mentions that CK is used when
auxiliary variables are available but not available at all grid-nodes, therefore,
* the sampling size and locations should affect the performance of CK a lot in real practice.

A paper titled ["When Doesn't Cokriging Outperform Kriging"](https://arxiv.org/pdf/1507.08403.pdf) discussed the problem theoretically.
The conclusion is that:
* CK is identical to OK when the sampling locations of auxiliary variables is the same with or is a subset of locations where the
response variable is observed.
* CK might outperform OK when the auxiliary variable is observed at more locations than the response variable.

The above conclusion is quite intuitive and not hard to understand.  
