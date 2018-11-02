---
layout: defaults/page
permalink: about.html
narrow: true
---

{% include components/intro.md %}

<hr />

### Research
My research focuses on **developing data models and algorithms to improve the quality of manufacturing processes**, e.g., the spatial modeling for engine deck surface machining and assembly, and transfer learning for the modeling of manufacturing processes with limited data/measurements. To this end, other than **engineering knowledge** about manufacturing, I am also studying **statistical modeling** and **machine learning**.

### Programming language
* Python
* R
* Matlab
* SAS

### Selected projects
1. **Cloud data processing and modeling for IoT based additive manufacturing (3D printing).** (Jan.2018-Present)
* Used IBM cloud to build infrastructure for collecting data from multiple sensors in different 3d printers/printing arms.
* Adopted boosting (AdaBoost) based joint learning algorithms for modeling the data from multiple sources to improve the 3d printing accuracy.
* Studied online joint learning dealing with cloud data that arrive sequentially.

2. **Multivariate modeling and variable selection for spatial non-stationary processes.** (Oct.2017-Apr.2018)
* Used spatial adaptive network-based inference rule model, spatial varying coefficient model and spatial partition-wise regression model to characterize different types of non-stationary (spatially abrupt or gradual change relations).
* Proposed an efficient algorithm (greedy merging) for identifying the spatial boundary of non-stationarity.
* Embedded lasso-type penalty for spatial variable selection either locally or globally.

3. **Transfer learning for data-lacking process modeling.** (Jan.2017-Oct.2017)
* Built regularization-based transfer learning algorithm for multiple models, e.g., geographically weighted regression model (varying coefficient model), region-wise regression model and adaptive network-based fuzzy inference model, to address the problem of lacking sufficient training data.
* Proposed engineering knowledge (engineering effect equivalence) guided transfer learning algorithm to improve the modeling accuracy of the multivariate linear regression model with insufficient data.
* Applied the proposed transfer learning technique to model the machined surface variation and additive manufacturing printing errors for quality improvement.

4. **Spatial leak modeling for surface assembly.** (Aug.2016-Apr.2017)
* Used a graph-shortest-path algorithm to calculate the leak flow with the least pressure loss in the assembly (interface) void areas.
* Extracted features from the minimum-pressure-loss paths and used logistic regression to classify leak and no leak.
* The proposed model was demonstrated to have strong robustness against noise.

5. **Multidimensional gait data analysis for lower limb orthoses.** (Oct.2015-Aug.2016)
* Collected and analyzed spatial-temporal gait data via phase-amplitude separation and FPCA (functional principal component analysis).
* Built statistical spatial model to characterize the relationship between insole and gait.
* Proposed cost-effective personalized design and manufacturing of lower limb orthoses.
* Related supplementary material [1](https://drive.google.com/open?id=1KKBqMid-H9iXaJVY6QSymZYPJKNFbO8r) & [2](https://drive.google.com/open?id=1qkS8fCOB-4HFeD9JudffIENrWpgoB7Qg)

6. **Multi-task learning for spatial gaussian process additive model and its application to machined surface shape prediction.** (Dec.2014-Dec.2015)
* Proposed an engineering knowledge incorporated Gaussian process additive model.
* Proposed a novel multi-task learning algorithm to iteratively estimate the model parameters for multiple tasks simultaneously.
* The proposed model was demonstrated to achieve better spatial prediction accuracy than traditional data-driven model without multi-task learning.

### Activities and volunteer experience
* Mentor for [RETREAT](http://eng.fsu.edu/retreat/) program at FSU.
  - (Jun.2015-Aug.2015) Topic: Physics guided stochastic modeling of nanostructure variations in nanomaterial manufacturing processes.
  - (Jun.2016-Aug.2016) Topic: A data acquisition system for personalized gait modeling.
* Mentor for [RISE](https://ww2.eng.famu.fsu.edu/nsfscholars/rise.html) program.
  - (Jun.2018-Aug.2018) Topic: Study the inconsistent material deposition problem in extrusion-based additive manufacturing.
  - (Jun.2018-Aug.2018) Topic: Interconnected sensing and logic control in additive manufacturing based on a cloud platform.
* Mentor for [Young Scholars Program](https://www.bio.fsu.edu/ysp/)
  - (Jun.2018-Jul.2018) Topic: Construct a time of flight algorithm for feature reconstruction through ultrasonic scanning.

### Journal publications
* **Ren, J.** and Wang, H., (in preparation). Online transfer learning for process variation modeling of cloud-connected additive manufacturing.
* **Ren, J.** and Wang, H., 2019. Surface variation modeling by fusing multiresolution spatially nonstationary data under a transfer learning framework. Journal of Manufacturing Science and Engineering, 141(1), p.011002. [Paper link](http://manufacturingscience.asmedigitalcollection.asme.org/article.aspx?articleid=2702492)
* **Ren, J.**, Park, C. and Wang, H., 2018. Stochastic modeling and diagnosis of leak areas for surface assembly. Journal of Manufacturing Science and Engineering, 140(4), p.041011. [Paper link](http://manufacturingscience.asmedigitalcollection.asme.org/article.aspx?articleid=2668591)
* Shao, C., **Ren, J.**, Wang, H., Jin, J.J. and Hu, S.J., 2017. Improving machined surface shape prediction by integrating multi-task learning with cutting force variation modeling. Journal of Manufacturing Science and Engineering, 139(1), p.011014. [Paper link](http://manufacturingscience.asmedigitalcollection.asme.org/article.aspx?articleid=2551758)
* Nguyen, H.T., Wang, H., Tai, B.L., **Ren, J.**, Hu, S.J. and Shih, A., 2016. High-definition metrology enabled surface variation control by cutting load balancing. Journal of Manufacturing Science and Engineering, 138(2), p.021010. [Paper link](http://manufacturingscience.asmedigitalcollection.asme.org/article.aspx?articleid=2442384)
* Wu, X., Miao, R., Li, Z., **Ren, J.**, Zhang, J., Jiang, Z. and Chu, X., 2015. Process monitoring research with various estimator-based MEWMA control charts. International Journal of Production Research, 53(14), pp.4337-4350. [Paper link](https://www.tandfonline.com/doi/abs/10.1080/00207543.2014.997406)

### Conference publications & presentations
* **Ren, J.** and Wang, H. Process Variation Modeling and Monitoring for Interconnected Additive Manufacturing using Cloud Data. To be presented at INFORMS Annual Meeting, Phoenix, USA, 2018.
* **Ren, J.** and Wang, H. Joint Process Modeling for Improving the Accuracy of Additive Manufacturing with Cloud Based Multiple Sources of Data. Presented at FACAM, University of Southern California, Los Angeles, USA, 2018. [FACAM link](http://facam-online.blogspot.com/2018/01/tentative-agenda-of-facam-2018-workshop.html) & [PPT link](https://drive.google.com/open?id=1bcdfYLQsMCpPqOruvXdqmeO8kpQ9yjxC)
* **Ren, J.**, Park, C. and Wang, H. Stochastic Modeling and Diagnosis of Leak Areas for Surface Assembly. Presented at INFORMS Annual Meeting, Houston, USA, 2017. [PPT link](https://drive.google.com/open?id=17kcXvAAALErhui1FARqhkfUgRFX9lvH4)
* **Ren, J.**, Wang, H. and Jin, X. Engineering Effect Equivalence Enabled Transfer Learning. Presented at IEEE Conference on Automation Science and Engineering, Xi'an, China, 2017. [Paper link](https://ieeexplore.ieee.org/abstract/document/8256262) & [PPT link](https://drive.google.com/open?id=1bzjH6_yCX5LedM1Zpf6uhNWkuGWS05RT)
* **Ren, J.** and Wang, H. Surface Variation Modeling by Fusing Surface Measurement Data with Multiple Manufacturing Process Variables. Presented at ASME Manufacturing Science and Engineering Conference, Blacksburg, VA, USA, 2016. [Paper link](http://proceedings.asmedigitalcollection.asme.org/proceeding.aspx?articleid=2558745) & [PPT link](https://drive.google.com/open?id=1A382RLgher6EvzJmTfDvBmMLvBcEgcYc)
