---
title: About different Kriging methods
tags:
  - spatial statistics
  - kriging
---
Difference in Simple Kriging, Ordinary Kriging, Co-Kriging, Universial Kriging,
Kriging with external drift, and Regression Kriging.

<!--more-->

There is no rigorous definition of different Kriging methods and those methods are mathematically similar. Therefore, the difference is summarized based on the most general condition and can be different under certain situations:

* **Simple Kriging:**

   known constant mean.
* **Ordinary Kriging (OK):**

   constant unknown mean.
* **Co-Kriging (CK):**

   auxiliary variables are available but not available at all grid-nodes. (cross-variogram is calculated).
* **Universal Kriging (UK):**

   mean trend (drift) is a function of coordinates.
* **Kriging with external drift (KED):**

   drift is defined externally through auxiliary variables which are available at all grid-nodes.
* **Regression Kriging (RK):**

   same condition with KED, but drift and residuals are fitted separately and then summed up.

It is worth noting that to use RK and KED, auxiliary variables must be available at all the locations of interest (predicted locations). If auxiliary
variables are only available at partial locations, CK is adopted instead. 
