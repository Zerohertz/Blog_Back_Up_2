---
title: >-
  A PHM Approach to Additive Manufacturing Equipment Health Monitoring, Fault
  Diagnosis, and Quality Control
date: 2020-01-30 09:43:24
redirect_from:
- /2020/01/30/a-phm-approach-to-additive-manufacturing-equipment-health-monitoring-fault-diagnosis-and-quality-control/
- /2020/01/30/A-PHM-Approach-to-Additive-Manufacturing-Equipment-Health-Monitoring-Fault-Diagnosis-and-Quality-Control/
categories:
- Research
- Read Paper
tags:
- Signal Processing
- PHM
- Read Paper
- Smart data
mathjax: true
---
# Introduction

> Fabrication of 3D objects through direct deposition of functional materials using 3D printing equipment is called Additive Manufacturing(AM)

+ Producing goods quickly
+ On-demand
+ Greater customization
+ Complexity
+ Less material waste

> Particulary in the process and equipment category, the highest priority in NDE/NDT techniques have been specified as
>+ Combining NDE techniques to better assess quality via an integrated approach
>+ Adapting existing NDE techniques to AM, expecially parts, and characterizing defects
>+ Lack of affordable quality insepection tools for direct metal parts

## AM(Additive Manufacturing)

> The AM has two unique characteristics
>+ Relatively long cycle time
>+ High quality standard for dimension accuracy

<u>**These unique characteristics of AM can be considered as good opportunities for developing PHM based approach for 3D printer health monitoring, fault detection and quality control**</u> 

> Sensor
>+ The potential capability of acoustic emission(AE)
>+ Piezoelectric(PE) strain

<!-- More -->
## AE(Acoustic Emission) sensor

> Transient elastic waves within a material, caused by the release of localized stress energy

+ AE propagates from the epicenter to sensing apparatus with in materials while vibration sensor requires perpendicular installation along with the vibration direction
+ If vibration direction sources are combinative - Hard to identify vibration direction
+ AE signals are distinguishable from acoustic signals : AE signals lie on a higher frequency range(e.g. 1kHz ~ 1MHz) - The audible range of human(e.g. 20Hz ~ 20kHz)
+ A high sampling rate(2MHz ~ 10MHz) has been a typical choice of sampling rate for AE data collection
+ Other issues which make the AE data processing challenging
  + Including a high data volume
  + Complicated feature of AE signals
+ However, AE sensors are sensitive in early fault detection than various gear and bearing fault diagnostic applications

## PE(Piezoelectric) strain sensor

+ The low maximum sampling rate(up to 1 kHz) of the fiber optic strain sensor limits its wide applicability in machinery fault detection
+ On the other hand, the PE strain sensors measure torsional vibration by quantifying terminal voltage difference released by deformed piezoelectric material
+ Unlike the fiber optic strain sensor, PE strain sensor has a merit in higher sampling rate up to 100kHz
+ Compared to the conventional strain gauge sensors and accelerometers, the PE strain sensors have certain advantages
  + Ability to measure the first derivative from their superior noise immunity
  + High linearity and sensitivity from their superior noise immunity as compared to differentiated sensing performance of conventional strain sensors
  + High frequency range
  + Space-efficiency without a structural change on the measuring target
  + Negligible temperature effect on the measurement output
  + These advantages allow PE strain sensors to potentially have greater sensing resolution and accuracy

***

# Methodology

![Overview of the 3D printer fault diagnosis with PE strain sensor and AE sensor](https://user-images.githubusercontent.com/42334717/75207396-f2122e00-57bb-11ea-91aa-d652c7f3ff0c.png)

+ A data acquistion(DAQ) system is used to collect the AE signals and PE strain signals at the same time
+ While the PE sensor is directly connected to the DAQ, the AE sensor, on the other hands, is connected to the DAQ board through a hardware based heterodyne frequency reduction device
+ Filter bands are chosen for each sensor to remove noise in the collected signals before they can be used to compute condition indicators(CIs) for fault detection

## The Heterodyne Technique

> To apply AE based NDE/NDT techniques to machine fault detection and diagnosis, and technical challenge is to deal with the data storage and processing burden caused by the typical high sampling rate of AE sensor(from several MHz to 10 MHz)

<u>**Frequency shifting technique, namely heterodyne(Fessenden, 1913) based AE fault detection and diagnosis methods**</u>

+ Downshifts the frequency of the AE signals so that a sampling rate comparable to vibration analysis can be utilized
+ The AE based NDE/NDT techniques implemented with heterodyne are significant as size of AE data needs to be stored and the computational cost can be significantly reduced
+ Shifting the carrier frequency to baseband, followed by low pass filtering
+ Based on the trigonometric identify

$$sin(2\pi f_1t)sin(2\pi f_2t)=\frac{1}{2}cos[2\pi(f_1-f_2)]-\frac{1}{2}cos[2\pi(f_1+f_2)]$$

+ Two signals with different frequency $f_1$ and $f_2$, respectively
+ $f_1$ : The AE carrier frequency
+ $f_2$ : The demodulator's reference signal frequency
+ In applications, any desired new output signals called as heterodynes, one at the sum $f_1+f_2$, and the other at the difference $f_1-f_2$, are utilized upon necessity
+ The heterodyning techique is aimed especially at demodulating the amplitude modulated signals

$$U_a=(U_m+mx)cos\omega_ct$$

+ $U_a$ : The amplitude modulated signal
+ $U_m$ : The carrier signal amplitude
+ $m$ : The modulation coefficient
+ $x$ : The signal of interest
+ $\omega_c$ : The carrier signal frequency

$$x=X_mcos\Omega t$$

+ $\Omega$ : Much smaller than $\omega_c$

$$U_0=(U_m+mx)cos(\omega_c t)cos(\omega_c t)=(U_m+mx)[\frac{1}{2}+\frac{1}{2}cos(2\omega_ct)]$$

+ $U_0$ : The modulated signal
+ $cos(\omega_ct)$ : A Unit amplitude reference signal

$$U_0=\frac{1}{2}U_m+\frac{1}{2}mX_mcos\Omega t+\frac{1}{2}U_mcos(2\omega_ct)+\frac{1}{4}mX_m[cos(2\omega_c+\Omega)t+cos(2\omega_c-\Omega)t]$$

+ Since $U_m$ is assumed not to contain any useful information related to the modulated signal, it could be canceled out
+ In the final heterodyning demodulation step, the signal frequency can be reduced to 10s of kHz

<u>**The resulting frequency range for AE signals becomes comparable to that of typical vibration signals**</u>

![Comparison of the heterodyned AE data acquisition procedure with the conventional AE methods](https://user-images.githubusercontent.com/42334717/75210383-40c3c600-57c4-11ea-80a7-f8ca47fffbea.png)

## CIs for 3D Printer Fault Detection

![The definitions of the CIs](https://user-images.githubusercontent.com/42334717/75211354-f98b0480-57c6-11ea-9bfe-c19bc51a5322.png)

+ Each type of CI can be computed using different input signals
+ In addition to raw signals, other types of input signals can be generated
  + Energy operator(EO)
  + Narrow band(NB)
  + AM(Amplitude modulation)
  + FM(Frequency modulation)

$$x_{EO,i}=x_i^2-x_{i-1}\cdot x_{i+1}$$
$$(for i=2,3, ..., N-1)$$

+ The EO introduced by Teager(1992) is defined as the residual of the autocorrelation function
+ Where $x_{EO,i}$ is the $i^{th}$ element of EO data
+ $x_i$ is the $i^{th}$ element of the input data $x_{IN}$


+ NB is the time domain representation after applying narrow band of interest which could be seen in frequency domain
+ AM and FM are obtained by amplitude modulation and phase modulation of the NB filtered data

***

# Experimental Setup

## The 3D Printer Test Rig

+ The 3D printer test rig composes two main parts
  1. Heterodyned AE based DAQ system
  2. 3D printer
+ DAQ board with a maximum analog input sampling rate of 1.25 MHz
+ AE sensor attached on the 3D printer
+ Demodulation board(AD8339)
+ Analog amplifier with gain 20/40/60dB
+ Function generator
+ The 3D printer

## 3D Printer Seeded Fault

> According to the troubleshooting maintenance document of the machine, one potential problem is the looseness of the belt driving the motion of the extruder nozzle

+ The seeded fault was created by inserting five small pieces of metal wire into the slots between teeth of belt to create faulty operation during printing process
+ The 3D printer was run with and without the fault seeded driving belt to produce ten sets of bolt and nut(five sets for each conditions)
+ Individual run took about 28 minutes to print one set of bolt and nut
+ A total of six heterodyned AE data samples were recorded for 10 seconds at pre-specified time location from each run

![Data acquisition procedure](https://user-images.githubusercontent.com/42334717/75214508-29d7a080-57d1-11ea-922c-4055e90deda1.png)

+ Normal : Good fit of the bolt into the nut
+ Defetive : Bad threading prevents the bolt to fit into the nut

***

# Results

> The 3D printer fault diagnostic results from the AE and PE strain sensor based technique

## AE Signal Analysis Results

+ The AE signal analysis results for the seeded fault tests conducted on the 3D printer test rig are provided

### Spectrum(frequency domain)

+ Two different frequency regions were chosen for the low pass and narrow band pass filters
  + Low frequency region up to 20 kHz
  + Narrow band frequency around 3906 Hz
+ A remarkably high peak was observed within low pass range from all of AE samples
+ These peaks are specifically located at 3906 Hz
+ A narrow band pass filter with a band width of $\pm$ Hz around the peak frequency location was chosen

### RMS

+ RMS result from the low pass filter is provided
+ The resulting RMS of the heterodyned AE sample showed clear separation between healthy and faulty 3D printing condition

### CIs

+ CIs from the narrow band filtered AE signals are provided
+ Among all the CIs tested, majority of those that show a clear separation between the healthy and faulty conditions were computed from narrow band filtered signals
+ The bandwidth of this narrow band is in the low frequency filter region
+ A clear separation between the healthy and faulty 3D printing conditions with a 95% statistical significance can be observed for the following AE based CIs
  + RMS
  + NB-RMS
  + NB-RMS
  + NB-P2P
  + AM-RMS
  + AM-P2P

## PE Strain Signal Analysis

> PE strain signals were divided into two parts based on their frequency : low frequency part and high frequency part

+ Actual damage detection was performed on the high frequency part of the strain sensor data using condition indicators
+ High pass filtered PE strain signals were used to compute the CIs
+ In search for the appropriate filter band, the fast kurtogram(Antoni, 2007) was applied to exam the impulsivity locations of PE strain signals collected from the healthy 3D printers

### A sample fast kurtogram of PE strain sensor

![A sample fast kurtogram of PE strain sensor result from the healthy 3D printer](https://user-images.githubusercontent.com/42334717/75218313-33670580-57dd-11ea-8a73-7ddc5db87cbf.png)

+ The area in dark red color indicates the location of impulsivity
+ The 90% and 95% trimmed mean indicate that the impulsivity of PE sensor signals are located around 3.3 kHz to 4.2 kHz, respectively
+ A high pass band above 3 kHz was selected
+ A $X$ % trimmed mean is the average of the data after $(100-X)$ % of the outliers are removed
+ Among all the CIs computed using PE strain signals, only RMS showed a clear separation of the faulty condition from the normal conition

> Statistical results of Fast kurtogram

||90% trimmed mean|95% trimmed mean|
|:-:|:-:|:-:|
|Center frequecy value(Hz)|3320|4199|

## Results Summary

> Summary of the 3D printer fault detection results using AE and PE strain sensors

|Sensor Type|AE Sensor(Low pass band)|AE Sensor(Narrow band)|PE Strain Sensor|
|:-:|:-:|:-:|:-:|
|Sampling frequency|100 kHz|100 kHz|100 kHz|
|Filter bandwidth|Low pass band(<20 kHz)|Narrow band(3906 $\pm$ 3 Hz)|High pass band(>3 kHz)|
|Effective CIs selected|RMS|NB-RMS, NB-P2P, AM-RMS, AM-P2P|RMS|

+ For both the AE sensor and PE strain sensor used in the case study for 3D printer fault detection, a sampling rate of 100kHz was used for data acquistion
+ For AE sensor signals, two band pass filters were used
  + A low pass filter
    + RMS (provided the best performance and was able to detection the fault)
  + A narrow band filter
    + NB-RMS
    + NB-P2P
    + AM_RMS
    + AM-P2P
+ For PE strain sensor signals
  + A high pass filter
    + RMS

<u>**Significant amount of manufacturing time, materials, and cost and be saved and the quality of the product can be assured if a 3D printer fault can be detected and the printer be stopped days before it finishes printing the defective product**</u>

***

# Conclusion

> The methods presented in this paper could be extended to other potential 3D printing faults such as material feed or additional mechanical component faults