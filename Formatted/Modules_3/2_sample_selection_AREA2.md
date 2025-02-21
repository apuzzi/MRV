---
title: Sample selection using AREA2
summary: In sampling design methods for estimation of area and map accuracy, we design a sample by choosing a selection protocol and determining the sample size and allocation. In this tutorial we will physically draw from a study area a sample that was designed based on tutorials here on OpenMRV under process "Sampling design". Here, we illustrate how to draw a sample in AREA2. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- GEE
- AREA2
- Sampling design
- Sample design
- Sample selection
- Sample
- Sampling frame

group:
- category: Stratified
  stage: Sampling
- category: Simple Random
  stage: Sampling
- category: Cluster
  stage: Sampling
- category: Systematic
  stage: Sampling
---

# Sample selection using AREA2

## 1 Background

In sampling design methods for estimation of area and map accuracy, we design a sample by choosing a selection protocol and determining the sample size and allocation. In this tutorial we will physically draw from a study area a sample that was designed based on tutorials here on OpenMRV under process "Sampling design". Drawing a sample involve creating a *sampling frame* which is a list of population units that can be selected for inclusion in a sample. The population units in the list are referred to as sampling units. In other words, a frame is a device that provides observational access to the population by associating the population units with the sampling units (Särndal et al., 1992, p. 9). In our case, the sampling frame is for example a list of all the pixels that make up the study area. We could, therefore, simply export a list of all map pixels with unique identifiers from which we randomly select *n* units. Under stratified random sampling (STR), each pixel would in addition to the identifier also have a stratum code such that a random sample are selected from each stratum. Such an approach can easily become impractical as the number of population units tend to be large. Instead, sample selection is supported by various tools and software -- here, we illustrate how to draw a sample in Google Earth Engine/AREA2. 

## 2 Learning Objectives

Upon completion of the tutorial, the user should be able to sample an arbitrary study area under stratified random sampling (STR) using AREA2.
* Draw a sample in GEE/AREA2 under STR

### 2.1 Pre-requisites

* Relevant terminology for sampling techniques can be found at the end of this document

## 3 Tutorial: Sample selection using AREA2

We will draw a sample using a stratified random design in Google Earth Engine/AREA2.

### 3.1 Stratified random sampling in Google Earth Engine/AREA2
Based on tutorials here on OpenMRV under process "Sampling design", where we had Forest, Non-Forest, Forest Disturbance and Forest Disturbance buffer as strata, let's assume a sample size required to reach a 25% margin of error of the forest disturbance area estimate. We also allocated the sample in strata for the purpose of area estimation. Then we will use the following sample size:

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

To select this sample, let's use AREA2 to select a sample under stratified random sampling:
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling and specify the path to a map of Colombia, used in a tutorial here on OpenMRV under tool "CODED", (https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer) with a buffer under "Specify stratification/image to define study area"; use the other default arguments click "Load image" which will display the strata areas in the Console (NOTE: it will take a some time). Select Arbitrary sample size under "Determine sample size", and specify under "Allocate sample size to strata": 275, 200, 30, 30. Click "Create sample" -- note: only click once; it looks like GEE doesn't react but it's drawing the sample after you clicked. Clicking Add to map will display the sample units as red dots in the Map display. The final step is to export the sample: click the Tasks tab, and then Export sample in the Dialog – two entries named “sample_asset” and "sample_CSV" will appear in Tasks. These are identical but one is for exporting the sample as a CSV file, one to save as a GEE Asset file for use in Google Earth Engine. Click the Run button right next to the entries and save as GEE Asset and CSV (the latter should be saved to your Google Drive). Use the name “STR_sample_Col” for GEE Asset and the CSV file.  

![](figures/STR_AREA2.png)

## 4 Frequently Asked Questions (FAQs)

**Must I use AREA2 to select a sample?**

No, not at all! This is just one example and there many other ways to sample a study area. Common applications include QGIS, R, ENVI and ArcGIS. Here on OpenMRV under process "Sampling design" and tool "QGIS" you can learn how to select a sample using QGIS.

**Do I have to select pixels? What if I want to select segments or blocks of pixels?**

The spatial unit of the sample does not have to be a pixel but should be of equal size to satisfy the criteria of probability sampling. Pixels are used as units in this tutorial for the sake of simplicity. For an in-depth discussion of spatial units, see Stehman and Wickham (2011).

## 5 Terminology

A list of terms relevant to the sampling and inference techniques are provided in the AREA2 documentation: https://area2.readthedocs.io/en/latest/definitions.html Below are a few additional terms not included in the AREA2 documentation.

### 5.1 Response design
Defined by (Stehman and Czaplewski, 1998): “The reference or ‘true’ classification is obtained for each sampling unit based on interpreting aerial photography or videography, a ground visit, or a combination of these sources. The methods used to determine this reference classification are called the ‘response design.’ The response design includes procedures to collect information pertaining to the reference land-cover determination, and rules for assigning one or more reference [labels] to each sampling unit.” Referred to as “measurement plan” by Särndal et al. (1992).

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

Cochran, W.G., 1977. Sampling Techniques, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. Sampling: Design And Analysis, CRC Press.

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. Remote Sensing of Environment, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

Stehman, S.V. and Wickham, J.D., 2011. Pixels, blocks of pixels, and polygons: Choosing a spatial unit for thematic accuracy assessment. Remote Sensing of Environment, 115(12), pp.3044-3055. https://doi.org/10.1016/j.rse.2011.06.007

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
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)  
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)  
Tatiana Nana, Cameroon, REDD+ Technical Secretariat  

Attribution  
Olofsson, P. 2021. Sample selection using AREA2. © World Bank. License:  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/) 
![](figures/wb_fcfc_gfoi.png)
