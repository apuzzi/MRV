---
title: Simple random/systematic sampling
summary: Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. A sampling-based approach to estimation can be separated into three different components - sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial for the case of simple random/systematic sampling design. Other tutorials here on OpenMRV under process "Sampling design" explore other sampling design approaches (e.g. Stratified Random Sampling).
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- GEE
- QGIS
- AREA2
- Sampling design
- Sample design
- Sample
- Sampling frame
- Simple Random
- Systematic

group:
- category: Simple Random
  stage: Sampling
- category: Cluster
  stage: Sampling
- category: Systematic
  stage: Sampling

---

# Simple random/systematic sampling 

## 1 Background

A sampling-based approach to estimation can be separated into three different components: sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial.  The sampling design defines the protocol for selecting the subset of units -- i.e. the sample -- from a larger population. In our case, the population is the equivalent of the study area, and characteristics of the study area, such as the area of a certain land cover, are estimated by analyzing the sample.  Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. As explained in the GFOI Methods & Guidance Document, estimating areas of land cover and land cover change by simply counting pixels in maps will produce erroneous results because of classification errors (GFOI, 2016, p. 125):

> Methods that produce estimates of activity data as sums of areas of map units assigned to map classes are characterized as pixel counting and generally make no provision for accommodating the effects of map classification errors. Further, although confusion or error matrices and map accuracy indices can inform issues of systematic errors and precision, they do not directly produce the information necessary to construct confidence intervals. Therefore, pixel-counting methods provide no assurance that estimates are “neither over- nor under-estimates” or that “uncertainties are reduced as far as practicable”. The role of reference data, also characterized as accuracy assessment data, is to provide such assurance by adjusting for estimated systematic classification errors and estimating uncertainty, thereby providing the information necessary for construction of confidence intervals for compliance with IPCC good practice guidance.

When choosing a sampling design, we need to consider a few but important design criteria. Of primary importance is the adherence to probability sampling.  Probability sampling is defined in terms of inclusion probabilities, where an inclusion probability relates the likelihood of a given unit being included in the sample; the inclusion probability must be known for each unit selected in the sample and the inclusion probability must be greater than zero for all units in the study area (Stehman, 2009). Several probability sampling designs are applicable to accuracy and area estimation, with the most commonly used designs being simple random, stratified random, and systematic. Two-phase (also called double), two-stage and cluster sampling are applicable but more complicated. 

## 2 Learning Objectives
The objective of this tutorial is to provide the user an understanding of the various key decisions involved in designing a sampling-based effort to estimation. Of importance is an understanding of the relationship between the sample size and the allocation of sample units to strata, and critical estimation objectives such as target precision. Upon completion of the tutorial, the user should be able to choose a sample selection method -- systematic (SYS), simple random (SRS) or stratified random (STR) --, determine sample size, and allocate the sample to strata, based on estimation objectives. For this specific tutorial, we will focus on Simple random/systematic sampling design.
* Understand the various key decisions involved in designing a sampling-based effort to estimation
* Choose a sample selection method -- SYS, SRS or STR based on estimation objectives
* Determine sample size, and allocate the sample to strata, based on estimation objectives for the simple random/systematic sampling design

### 2.1 Pre-requisites
* Relevant terminology for sampling techniques can be found at the end of this document 
* Google Earth Engine (GEE) account. Please refer to process "Pre-processing" and tool "GEE" here on OpenMRV for more information about working in this environment.

## 3 Tutorial: Sampling design for estimation of area and map accuracy - Simple random/systematic sampling

### 3.1 How to choose a sampling design?
Choosing a sampling design often involves tradeoffs among different criteria and priorities.  The desire to  provide estimates for subregions or the need to meet precision targets will need to be balanced against desirable sampling design criteria such as the ease and practicality of implementation, cost effectiveness, the ease of accommodating changes in sample size.  Stehman (2009) provides a detailed review of sampling design options, objectives, and criteria, but the decision typically boils down to three key decisions: whether to use strata, whether to use clusters, and whether to implement a systematic or simple random selection protocol. 

#### 3.1.1 Use strata?

Strata are “subpopulations that are non-overlapping, and together comprise the whole population” (Cochran, 1977, p. 89). Stratifying the study area prior to the sample selection can ensure that estimates of accuracy and area are obtained for certain subregions in the study area, and it results in higher precision of estimates. Accordingly, there are several good reasons for using strata. Even with simple random sampling, the use of strata after selecting the sample is a good idea (see Section 3.2.1 Post stratification below). Stratified sampling provides an obvious advantage if we are interested in a very small proportion of the study area, as is often the case in tropical MRVs. For example, the area of forest loss, even in countries with rampant deforestation, is often a very small proportion of the country, especially over short time intervals. The use of a map of forest loss (and other categories) to stratify the study area in such situations allows for targeted sampling in areas of particular interest. Not stratifying in such situations will require a very large sample size. 

#### 3.1.2 Use simple random or systematic selection?
Systematic selection involves selecting a starting point at random with equal probability and then sampling with a fixed distance between sample locations. In short, simple random selection is preferable if collecting reference observations in satellite data whereas systematic selection is preferable if visiting sample locations in situ (Olofsson et al. 2014). The rationale for this recommendation is that systematically selected units are easier to locate in the field while random selection is easier to augment. Note that the same estimators are used with both simple random or systematic selection. 

#### 3.1.3 Use cluster?
A cluster is a sampling unit that consists of one or more of the basic assessment units specified by the response design. For example, a cluster could be a 3 × 3 block of 9 pixels or a 1 km × 1 km cluster containing 100 1 ha assessment units. In cluster sampling, a sample of clusters is selected and the spatial units within each cluster are therefore selected as a group rather than selected as individual entities. Two-stage sampling is a form of cluster sampling where large primary sampling units are (PSUs) are selected at the first stage;  smaller secondary sampling units (SSUs) are selected within each PSU in the second stage.  Such designs have the benefit of requiring reference data (i.e. the data used for collecting reference observations) only over PSUs instead of the entire study area which is the case with the aforementioned designs. However, unless the cost savings are considerable, cluster-based designs are not recommended as the correlation between SSUs  often reduces precision relative to a simple random sample of equal size, and because they are complicated designs that are difficult to augment with sample results that are difficult to analyze. 


### 3.2 Simple random/systematic sampling
If the units (e.g. pixels) of a population/study area are numbered from 1 to *N*, simple random sampling (SRS) is “A method for selecting *n* units out of the *N* such that every one of (the sets of *n* specified units) has an equal chance of being drawn” (Cochran 1977, p. 18). In a geography context, we are often interested in estimating a proportion of the population/study area, such as the area proportion of a certain land cover or change in land cover, from the sample data. Using Cochran's notions, the units of a population are ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_N) from which a sample  ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_n) is selected under SRS; we record ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=1) if the land cover of interest is observed at unit *i* and ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=0) otherwise. An advantage of SRS is that the mean of the observations is an unbiased estimator of the population proportion (*p*) of interest (Cochran, 1977, Eq 3.3):

![](https://latex.codecogs.com/svg.latex?\Large&space;\bar{y}=\frac{1}{n}\sum_{i=1}^{n}y_i=\hat{p})

and the variance of the estimated proportion *p^* is  easily estimated as (Cochran, 1977, Eq 3.11)

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=\frac{\hat{p}(1-\hat{p})}{n-1})

These estimators are applicable also to sample data collected under simple systematic sampling (SYS). The straightforward analysis of sample data collected under SRS/SYS, and the ability to augment the sample size with ease (especially under SRS), make these designs attractive.  

#### 3.2.1 Post stratification 
Another important advantage of SRS/SYS is the ability to stratify the study area after sample results have been collected -- applying a stratification subsequent to sampling is referred to as post-stratification (PSTR). PSTR is likely to increase the precision of estimates, and there are seldom reasons not to post-stratify using maps. 

#### 3.2.2 Sample size
Determining the sample size regardless of design involves calculating the number of units in a sample required to meet a certain target precision of an estimate of a population parameter of interest. The calculation is based on solving the variance estimator corresponding to the design for *n*. If the variance in variance estimator above is the desired variance of an estimate, solving for *n* gives  (Cochran, 1977, Eq. 4.2)

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})})

where *p^* is an estimate of the proportion of units in the class of interest in the study area. For example, let's assume we want to  estimate the overall accuracy (as in Olofsson et al., 2014, p. 53) with a 5% margin of error. We would then define *p* as overall map accuracy. We obviously don't know the overall accuracy of the map at this stage so an educated guess is required. If we assume 80% overall accuracy, a 5% margin of error (*MoE*) would translate into a variance of (the z-score of 1.96 at the 95% confidence level is rounded to 2)

![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{2\sqrt{\hat{V}}(\hat{p})}{\hat{p}}\Leftrightarrow\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.05\times0.8}{2})^2=0.0004)

which gives a sample size of

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})}=\frac{0.8(1-0.8)}{0.0004}=400)

Even though estimation of overall accuracy was illustrated in Olofsson et al. (2014), specifying a margin of error of the overall map accuracy is not intuitive and rarely an estimation objective. A more realistic example would be the  estimation of the area of deforestation or forest degradation with a certain precision. In another tutorial here on OpenMRV under process "Change detection" and tool "CODED", a map of deforestation, forest degradation, forest and non-forest was created for Colombia, and we will use it as an example (https://code.earthengine.google.com/?asset=users/openmrv/MRV/CODED_Colombia_Stratification_No_Buffer); for the sake of simplicity, let's lump the deforestation and forest degradation into a single forest disturbance class, which was mapped as 1.4% of the country from 2010 to 2020. Note, for estimation of activity data within REDD+ (and other initiatives), it is recommended to estimate deforestation and degradation separately -- and hence use a deforestation stratum and a degradation stratum -- rather than combining the two classes into a single forest disturbance class. Here, we are using a combined disturbance class to facilitate the illustration of the workflow and calculations.  Let's assume we want to estimate the area of forest disturbance (again, combined deforestation and degradation) with a 25% margin of error. Note that 25% is used here simply to illustrate the workflow -- the target error will depend on the circumstances of the study. First, a 25% margin of error is equivalent to a variance of  

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.25\times0.014}{2})^2=0.000003)

which gives a sample size of

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(p)}=\frac{0.014(1-0.014)}{0.000003}=4,600)

Collecting observations at almost five thousand sample locations is rarely attainable for an individual study. The example illustrates one of the drawbacks with SRS/SYS -- because we are not using any information on the location of deforestation, a very large sample size is required to achieve high precision. Another, quicker, way to estimate the sample in this case is to assume that we need at least 30 units in areas of deforestation which would require a sample size of 30/0.014 = 2,142 units which is more manageable but still large, and we are not sampling to meet a precision target.

The reason for why 30 is regarded is the minimum sample size is best described by Lohr (1999): 

> The imprecise term “sufficiently large” occurs in the central limit theorem because the adequacy of the normal approximation depends on n and on how closely the population {yi, i = 1, ... , N} resembles a population generated from the normal distribution. The “magic number” of n = 30 is often cited in introductory statistics books as a sample size that is “sufficiently large” for the central limit theorem to apply

The central limit theorem is important because it states that the sum of independent random variables are normally distributed  even if the variables themselves are not. For example, the theorem allows us to construct confidence intervals by using common z-scores and a standard error.
   

### 3.3 Software that allows for sample size estimation
SEPAL/CEO has built-in support for estimating sample size as explained in [this documentation](https://sepal-ceo.readthedocs.io/en/latest/).

Similar to SEPAL is this spreadsheet developed by the World Bank which also calculates the sample size required to meet a precision of overall accuracy: https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE

### 3.4 Selecting the sample
The final step of the sampling design is to physically draw the sample from the study area, which is covered here on OpenMRV under process "Sampling design" and tools "QGIS", "GEE", "AREA2".

## 4 Frequently Asked Questions (FAQs)

**How do I know if I can use SRS or if I will need a more complex design such as STR?**

The easiest way to determine if simple designs such as SRS and SYS viable is to following the equations in this tutorial to determine the sample size required to reach a certain precision. If the sample size required is too large to be managable, then you might need have to use strata when sampling.


**How do I determine a target standard error?**

Certain programs specify a desired or required precision; the Forest Carbon Partnership Facility (FCPF) for example stipulate a margin of error of 30% at the 95% confidence level for area estimates of activity data. The margin of error is 1.96 times the standard error divided by the area estimate. When no such precision requirements are specified, a target standard error needs to be determined based on other criteria. Note that the smaller the area proportion of the target class, the larger the sample is needed to reach a small margin of error. Accordingly, for small area proportions, the target precision will need to be relaxed to avoid having to select a very large sample. 



## 5 Terminology

A list of terms relevant to the sampling and inference techniques are provided in the AREA2 documentation: https://area2.readthedocs.io/en/latest/definitions.html  Below are a few additional terms not included in the AREA2 documentation.  

### 5.1 Response design

Defined is defined by Stehman and Czaplewski (1998) as  “The reference or ‘true’ classification is obtained for each sampling unit based on interpreting aerial photography or videography, a ground visit, or a combination of these sources. The methods used to determine this reference classification are called the ‘response design.’ The response design includes procedures to collect information pertaining to the reference land-cover determination, and rules for assigning one or more reference [labels] to each sampling unit.” Referred to as “measurement plan” by Särndal et al. (1992).

### 5.2 Sample

A subset of population units selected from the population.

### 5.3 Sample design

Synonymous with sampling design, which is the preferred term in the seminal literature (Cochran, 1977, Särndal et al., 1992). The term occurs in Rice (1995) who uses both “sampling design” and “sample design”. 

### 5.4 Sampling design

“The sampling design is the protocol by which the reference sample units are selected.” (Stehman and Czaplewski, 1998). “Sampling design” is also used by Cochran (1977) and Särndal et al. (1992) - the former also uses “sampling plan”. 

### 5.5 Survey

Särndal et al. (1992) defines a survey as a “partial investigation of a finite population”, and further that “that the terms ‘survey’ and ‘sample survey’ are used to denote statistical investigations with the following methodological features: [...] probability sampling [...] measurement plan [and] estimation”

### 5.6 Survey design

A “total survey design” defines the procedures for “obtaining the possible precision in the survey estimates while striking a balance between sampling and non-sampling errors [...] The survey design gives rise to survey operations” such as sample selection (Särndal et al., 1992). Lohr (1999) describes a total survey design as “A philosophy of survey design for minimizing nonsampling as well as sampling errors.” Also, in Lohr (1999) “survey design” is synonymous with sampling design. 

## 6 References

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

GFOI. 2016. *Integration of remote-sensing and ground-based observations for estimation of emissions and removals of greenhouse gases in forests: Methods and guidance from the Global Forest Observations Initiative* (2nd ed.), UN Food and Agriculture Organization, Rome.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Arévalo, P., Espejo, A.B., Green, C., Lindquist, E., McRoberts, R.E. and Sanz, M.J., 2020. Mitigating the effects of omission errors on area and area change estimates. Remote Sensing of Environment, 236, p.111492. https://doi.org/10.1016/j.rse.2019.111492

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Potapov, P.V., Dempewolf, J., Talero, Y., Hansen, M.C., Stehman, S.V., Vargas, C., Rojas, E.J., Castillo, D., Mendoza, E., Calderón, A. and Giudice, R., 2014. National satellite-based humid tropical forest change assessment in Peru in support of REDD+ implementation. Environmental Research Letters, 9(12), p.124012. https://doi.org/10.1088/1748-9326/9/12/124012

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Sannier, C., McRoberts, R.E., Fichet, L.V. and Makaga, E.M.K., 2014. Using the regression estimator with Landsat data to estimate proportion forest cover and net proportion deforestation in Gabon. Remote Sensing of Environment, 151, pp.138-148. https://doi.org/10.1016/j.rse.2013.09.015

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., 2009. Sampling designs for accuracy assessment of land cover. International Journal of Remote Sensing, 30(20), pp.5243-5272. https://doi.org/10.1080/01431160903131000

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](figures/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2021, World Bank 

This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries’ MRV implementation. 

Material reviewed by:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)    
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)    
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)    
Tatiana Nana, Cameroon, REDD+ Technical Secretariat  

Attribution  
Olofsson, P. 2021. Simple random/systematic sampling. © World Bank. License:  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)  
![](figures/wb_fcfc_gfoi.png)
