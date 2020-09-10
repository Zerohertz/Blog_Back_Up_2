---
title: >-
  Development of Data-Driven In-Situ Monitoring and Diagnosis System of Fused
  Deposition Modeling(FDM) Process Based on Support Vector Machine Algorithm
date: 2020-01-22 14:37:37
categories:
- Research
- Read Paper
tags:
- Machine Learning
- Signal Processing
- PHM
- Read Paper
- Smart data
---
# Introduction

> Fused Deposition Modeling(FDM), one of representative Additive Manufacturing(AM, 3D printing) technologies

## AM(Additive Manufacturing) technologies

+ Stereolithography(SLA)
+ Multijet Modeling(MJM)
+ Fused Deposition Modeling(FDM)
+ Selective Laser Sintering(SLS)
+ Selective Laser Melting(SLM)
+ Laminated Object Manufacturing(LOM)
+ Laser Engineering Net Shaping(LENS)

<!-- More -->

## Among them, FDM, one of Fused Filament Fabrication(FFF) 3D printing processes

+ Most widely used for fabricating thermoplastic parts
+ Components with low cost
+ Easy material change
+ Without geometrical complexity limitation

## Used materials in FDM

+ Acrylonitrile Butadiene Styrene(ABS)
+ Polylatic Acid(PLA)
+ High-Impact Polystyrene(HIPS)
+ Thermoplastic Polyurethane(TPU)
+ Aliphatic Polyamides(Nylon)

## Drawbacks of FDM

+ Limitations on part quality
+ Process reliability and controllability
+ Significant amount of material been wasted during the FDM process
+ A disposal of defective products due to faulty FDM process and equipment has become an enviromental problem in the industrial field

<u>**Therefore, it is necessary to identify and monitor major factors of the FDM process that can have a profound influence on the part quality and process reliability**</u>

## Using sensor

+ Accelerometer(353B03, PCB Piezotronics Inc.)
+ Acoustic Emission(AE) sensor(R.45, Physical Acoustics Inc.0)

## Method

+ `The root mean square(RMS)` is found to be most appropriate to diagnose the FDM process states
+ When constructing the FDM process monitoring and diagnosis model, `a Support Vector Machine(SVM) algorithm` is chosen
+ `A k-fold cross validation approach` is applied to obtain the best models having the highest diagnosis accuracy

***

# FDM Experiments and Data Collection

## Faulty quality modes

+ Warping
+ Elephant foot
+ Shifting layer
+ Leaning part

**Major reason : A looseness of the bolt driving a motion of the nozzle head - Shifting layer**
<u>**A Faulty state of the FDM process - The loosened bolt**</u>

## Layer difference

+ Odd-numbered(1, 3, 5 ,7) layer
  + The 3D printing path was divided into 4 sections
  + The outline, The left part, The central reduced part, The right part
+ Even-numbered(2, 4, 6, 8) layer
  + The 3D printing path was divided into 5 sections
  + The outline, The left-upper part, The central reduced part, The right part, The left-lower part

<u>**They had different paths to finish each layer**</u>

***

# Development of Monitoring and Diagnosis Models of FDM Process States

## Signal Processing and Feature Extraction

+ A feature extraction - An essential procedure to construct an index indicating FDM process states
+ Various features showing different tendencies about signal transition
  + `A root mean square(RMS)`
  + A maximum
  + A crest factor
  + A variance
  + A kurtosis
  + A skewness
+ Among them, `the RMS values` seemed to be best one(those in the cases of healthy and faulty states were more obviously different)
+ The RMS values in the case of faulty state are larger than those in the healthy state
+ In particular, for the acceleration along x- and y-direction and the AE
+ Meanwhile, the RMS values extracted from the z-acceleration data did not show that kind of difference between the healthy and faulty states
+ The loosened bolt could result in faulty motions of the pulley, belt and shaft, thus an abnormal lateral motion of the nozzle head along x- and y-direction could be generated

<u>**Therefore, the RMS values of x- and y-acceleration data could be different between the healthy and faulty states**</u>

## Development of FDM Process Monitoring and Diagnosis Models

> `An SVM(Supprot Vector Machine)` which is a learning model for data analysis is mainly used for classification(It creates a non-probabilistic binary linear classification model when given a set of data belonging to one of two categories that determines to which category new data belong based on a given set of data)

+ Linear and non-linear SVM algorithms were applied
+ The RMS values of x- and y-acceleration and AE signals were used as input variables and output responses were numerical confidence values, which were 0 for the healthy state and 1 for the faulty state, respectively
+ These SVM-based models were developed for the odd- and even-numbered layers in the cases of healthy and faulty states
  
> Thus, while building one FDM specimen, four SVM-based models could be developed by using one collected signal out of x- and y-acceleration and AE
>+ One for the odd-numbered layer in the healthy state
>+ One for the even-numbered layer in the healthy state
>+ One for the odd-numbered layer in the faulty state
>+ One for the even-numbered layer in the faulty state

+ In a single FDM specimen
  + Odd-numbered layers - 16 RMS data
  + Even-numbered layers - 20 RMS data
+ For each states(Three repeated FDM experiments were conducted for the healthy and faulty states)
  + Odd-numbered layers - 48 RMS data
  + Even-numbered layers - 60 RMS data
+ While testing the models
  + Odd-numbered layers - Total 32 heathy and faulty RMS data
  + Even-numbered layers - Total 40 healthy and faulty RMS data

> When developing `the SVM-based models`, both linear and non-linear SVM approaches were considered

+ A non-linear classification is carried out by mapping given data to a high dimensional feature space - A kernel trick shoud be used
+ The non-linear SVM models based on the kernel function were optimized through an objective function using allowable parameters for two categories of the healthy and faulty process states
+ It is necessary to empirically determine an adjustment factor value for maximizing classification accuaracy
  + In the models
  + The adjustment factor value : 10 - An overfitting was occurred
  + The adjustment factor value : 0.1 - Non-linear SVM models were similar to the linear SVM models
  + Therefore, 1 was selected as the adjustment factor value
+ The training results indicates that the SVM-based models using `the acoustic emission signals` could have a better accuaracy to diagnose the FDM process states

> `A k-fold cross validation approach` has been applied to increase a statistical reliability of the developed SVM-based models

+ Original data are randomly divided into k sub-data sets having a same size
+ One sub-set of k sub-data sets is maintained as validation data for testing the model
+ Remaining (k-1) sub-data sets are used to train the model

![k-fold cross validation approach](https://user-images.githubusercontent.com/42334717/73340015-43162b80-42bd-11ea-8bdd-8af32807ad8d.png)

> A total of four consecutive FDM experiments were repeated, three for training the models and the last one for testing the models

+ The sub-data sets for training and testing of the models were cyclically changed(In k-fold cross validation approach)
+ Four sub-data sets were prepared for both healthy and faulty states in the case of one sensor among three sensors by repeating the FDM experiments four times
+ Training of the models using three sub-data sets and testing using the remaining one sub-data set were cyclically carried out
+ Example(In the case of fold 1)
  + The sub-data sets from cases 2, 3 and 4 were used for training
  + The sub-data sets from case 1 was used for testing

## Validation of FDM Process Monitoring and Diagnosis Models

![Diagnosis accuracies of FDM process states](https://user-images.githubusercontent.com/42334717/73340050-57f2bf00-42bd-11ea-8945-acceaeb244d5.png)

+ The diagnosis accuracies of the linear and non-linear SVM-based models for the odd-numbered layers are given in the cases using the x-acceleration, y-acceleration and AE signals, respectively
  + By validating the models with total 32 data
    + 16 healthy and 16 faulty data
    + From 4 odd-numbered layers
    + 4 RMS data per each odd-numbered layer
+ The diagnosis accuracies of the linear and non-linear SVM-based models for the even-numbered layers are given in the cases using the x-acceleration, y-acceleration and AE signals, respectively
  + By validating the models with total 40 data
    + 20 healthy and 20 faulty data
    + From 4 even-numbered layers
    + 5 RMS data per each even-numbered layer

<u>**Overall, the non-linear SVM-based models showed a better performance than the linear SVM-based models(While observing their diagnosis accuracies)**</u>
<u>**The AE signals shows the best performance for diagnosing healthy and faulty FDM process states for both linear and non-linear SVM-based models(Their RMS values were quite different to each other for the healthy and faulty states)**</u>

## Software Module Development and Real-Time Validation

> The best FDM process monitoring and diagnosis models based on the x- and y-acceleration signals having the highest accuracies were selected from `the k-fold cross validation` results, and they were used for developing the software module by using a commercial package of `Matlab`

+ In the learning mode, the models for healthy and faulty FDM process states were trained by clicking either healthy state or faulty state after inputting the acceleration data which were collected in each state
+ After completion of training of the models, the FDM process states could be determinded in the diagnosis mode
+ The real-time validation experiments were conducted by using the developed software
  + 8 healthy process states
  + 8 faulty process states

<u>**The final accuracy was 87.5%, which meant two misdiagnosis cases out of 16 total cases**</u>

> In the software development, the models based on the AE signals were not considered, since they can be disturbed in a factory floor due to an enviromental noise

+ To utilize such models in the factory floor, additional filtering and signal processing should be needed to minimize effects of the enviromental noise
+ Since the models based on the AE signals had the highest accuracy(100%), it could be also possible to use them to develop the software with an appropriate signal processing technology(A wavelet transform method, which can characterize the signals in both time and frequency domains)

***

# Conclusion

> The monitoring and diagnosis system for FDM process, which is the most popular additive manufacturing technology, was developed based on a data-driven approach

1. Collect mass data that are highly related to the FDM process - `Three accelerometers`, `an AE sensor`
2. Through a series of FDM experiments, the acceleration and AE data were collected with the sensors in the cases of the healthy and faulty process states
   + The faulty FDM process state was realized by considering the loosened bolt
3. The collected data were processed to obtain various features, and `the RMS values` were selected due to their distinctive differences for the healthy and faulty states
4. Constructing the FDM process monitoring and diagnosis models
   + Odd-numbered layers
   + Even-numbered layers
5. The linear and non-linear `SVM algorithms` were adopted due to their superiority for a classification of the data into two categories - healthy and faulty states
6. `A k-fold cross validation method` was applied, and the best models having the highest accuracy were chosen for validation(In order to further enhance the diagnosis accuaracy)
7. The `non-linear SVM based models` had diagnosis accuaracy better than 77.5% from an average point of view
8. The best modelsbased on `x- and y-acceleration signals` were selected(Since AE signals could be disturbed by and enviromental noise)
9. The real-time validation experiments were carried out by considering 8 healthy and 8 faulty process states, and the final accuracy was 87.5%

<u>**By using the developed FDM process diagnosis system, the faulty processes can be prevented in advance, and therefore, waste of material and energy can also be prevented**</u>
**During the validation experiments for the faulty processes states, 6 cases were correctly diagnosed among total 8 cases -** <u>**Those 6 faulty cases can be prevented, and therefore, the rate of saving material and energy is 75%**</u>