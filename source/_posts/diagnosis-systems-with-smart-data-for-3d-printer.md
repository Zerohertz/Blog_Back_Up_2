---
title: Diagnosis Systems with Smart Data for 3D Printer
date: 2020-03-04 20:32:07
categories:
- Research
- Journal
tags:
- Machine Learning
- DNN
- Signal Processing
- Matlab
- PHM
- Statistics
- R
- Smart data
- LabVIEW
mathjax: true
---
# Problem Definition

> Self diagnosis systems for unattended 3D printers

+ 자동화된 다수의 3D printer들을 진단하는 System이 필요
+ 가속도 센서를 이용, ML을 통한 Self diagnosis system 개발

***

# Skills for project

+ LabView
+ MatLab
+ Signal Processing
+ Machine Learning
+ Deep Learning

<!-- More -->

***

# 1차 시도(20200302~20200306)

## Problem Definition

### T-bar

> T-bar의 마모를 가하려했지만 결과물에 지장이 없거나, 모터가 움직이지 못하는 현상 발견

<img width="500" alt="T-bar" src="https://user-images.githubusercontent.com/42334717/75875966-1d4dea80-5e58-11ea-8bab-79a0bac8e103.png">

**따라서 T-bar의 마모가 3D printer의 결함 원인으로는 적합하지 않다.**

### Bolt

> 3D Printer의 좌측, Belt를 지지해주는 Bolt를 통해 풀림을 생성

<img width="500" alt="Bolt" src="https://user-images.githubusercontent.com/42334717/75888687-1aaabf80-5e6f-11ea-9e5a-56868ae7910b.png">

> 좌측 : 정상, 우측 : Bolt 풀림

<img width="500" alt="Healthy and Faulty" src="https://user-images.githubusercontent.com/42334717/75888743-30b88000-5e6f-11ea-86ae-e79dcec0a256.png">

**그림과 같이 눈에 띄게 결과물이 손상됨을 알 수 있다.**
<u>**따라서 Bolt의 풀림을 3D printer의 고장 원인으로 정한다.**</u>

## Data 측정

> X-axis Acceleration Graph

<img width="1000" alt="acc_x" src="https://user-images.githubusercontent.com/42334717/75889024-960c7100-5e6f-11ea-8619-bd2d76f1b58f.png">

**확연한 차이를 보인다.**

~~~R
> summary(health1)
      time             accx               accy               accz         
 Min.   : 10.01   Min.   :-1.83858   Min.   :-1.03260   Min.   :-0.98387  
 1st Qu.:249.24   1st Qu.:-0.12548   1st Qu.:-0.02613   1st Qu.:-0.28147  
 Median :488.47   Median : 0.01764   Median : 0.06829   Median : 0.02165  
 Mean   :488.47   Mean   : 0.01782   Mean   : 0.06824   Mean   : 0.03428  
 3rd Qu.:727.70   3rd Qu.: 0.16088   3rd Qu.: 0.16258   3rd Qu.: 0.33654  
 Max.   :966.93   Max.   : 1.75525   Max.   : 1.26659   Max.   : 1.00005  
> summary(fault1)
      time             accx               accy               accz         
 Min.   : 10.01   Min.   :-1.30125   Min.   :-1.70969   Min.   :-0.96202  
 1st Qu.:249.24   1st Qu.:-0.06878   1st Qu.:-0.00552   1st Qu.:-0.28195  
 Median :488.47   Median : 0.01883   Median : 0.06278   Median : 0.02334  
 Mean   :488.47   Mean   : 0.01876   Mean   : 0.06267   Mean   : 0.03584  
 3rd Qu.:727.70   3rd Qu.: 0.10655   3rd Qu.: 0.13107   3rd Qu.: 0.34062  
 Max.   :966.93   Max.   : 1.34742   Max.   : 1.84255   Max.   : 1.00065
> sd(health1$accx)
[1] 0.2419928
> sd(fault1$accx)
[1] 0.1536977
> sd(health1$accy)
[1] 0.1538164
> sd(fault1$accy)
[1] 0.118694
~~~

> X-axis 확률 밀도 함수

<img width="700" alt="X-axis 확률 밀도 함수" src="https://user-images.githubusercontent.com/42334717/76001793-fde2ba80-5f48-11ea-8595-85e04cc33b94.png">

> Y-axis 확률 밀도 함수

<img width="700" alt="Y-axis 확률 밀도 함수" src="https://user-images.githubusercontent.com/42334717/76002712-5f575900-5f4a-11ea-99fe-0e8cbeb4a405.png">

> Z-axis 확률 밀도 함수

<img width="700" alt="Z-axis 확률 밀도 함수" src="https://user-images.githubusercontent.com/42334717/76002703-5bc3d200-5f4a-11ea-8c92-817442bb34a0.png">

+ <span style='color:rgb(10,10,255)'>Healthy</span>
+ <span style='color:rgb(225,10,10)'>Faulty</span>

## Feature Extraction

<u>**Z축의 데이터는 분포에 차이가 없으므로 무시**</u>

> Skewness of X

<img width="700" alt="skofx" src="https://user-images.githubusercontent.com/42334717/76012300-69348880-5f59-11ea-9ebd-dddbc490aaa5.png">

> Kurtosis of X

<img width="700" alt="kuofx" src="https://user-images.githubusercontent.com/42334717/76012282-65086b00-5f59-11ea-8fb9-4f28acfb4971.png">

> Standard Deviation of X

<img width="700" alt="sdofx" src="https://user-images.githubusercontent.com/42334717/76012298-689bf200-5f59-11ea-8be6-6eb0e42e0e32.png">

> RMS of X

<img width="700" alt="rmsofx" src="https://user-images.githubusercontent.com/42334717/76012295-68035b80-5f59-11ea-9f83-14d8d5b655de.png">

> Peak to peak of X

<img width="700" alt="p2pofx" src="https://user-images.githubusercontent.com/42334717/76012292-676ac500-5f59-11ea-9fed-9a36e97872e8.png">

> Kurtosis of Y

<img width="700" alt="kuofy" src="https://user-images.githubusercontent.com/42334717/76012289-66d22e80-5f59-11ea-98e9-40a883b0ed03.png">

> Standard Deviation of Y

<img width="700" alt="sdofy" src="https://user-images.githubusercontent.com/42334717/76012299-689bf200-5f59-11ea-9cfb-5cff1b27158c.png">

> RMS of Y

<img width="700" alt="rmsofy" src="https://user-images.githubusercontent.com/42334717/76012297-68035b80-5f59-11ea-88a5-bd5a2642fa95.png">

> Peak to peak of Y

<img width="700" alt="p2pofy" src="https://user-images.githubusercontent.com/42334717/76012294-676ac500-5f59-11ea-8d46-c79baff6d566.png">

+ Skewness와 Kurtosis는 위의 그래프와 같이 분류에 적합하지 않으므로 배제
  + Raw data를 통해 Kurtosis가 높을거라 예측
  + 분포에서 큰 차이 없었음
+ 오히려 Standard Deviation의 차이가 컸음
+ **따라서 X, Y 데이터를 이용한 SD, RMS, P2P로 Feature extraction을 진행**

[20200306 SiM Lab. Meeting Presentation - 오효근.pdf](https://github.com/Zerohertz/Zerohertz.github.io/files/4297116/20200306.SiM.Lab.Meeting.Presentation.-.pdf)

***

# 2차 시도(20200309~20200320)

## Problem Definition

### T-bar

> T-bar에 아래로 가해지는 하중이 크므로 마모가 일어날 수 있다

<img width="1920" alt="T-bar 마모" src="https://user-images.githubusercontent.com/42334717/76928008-a4ed2c00-6923-11ea-99c0-c3c4e2285516.png">

## Raw data

![X](https://user-images.githubusercontent.com/42334717/76928858-0e6e3a00-6926-11ea-8754-2169897e5daf.jpg)

![Y](https://user-images.githubusercontent.com/42334717/76928864-10d09400-6926-11ea-8d9a-541514150acf.jpg)

![Z](https://user-images.githubusercontent.com/42334717/76928868-1332ee00-6926-11ea-9f59-909ec11cdcfa.jpg)

![X](https://user-images.githubusercontent.com/42334717/76930088-08c62380-6929-11ea-81f9-9ebc230a4029.jpg)

![Y](https://user-images.githubusercontent.com/42334717/76930095-0d8ad780-6929-11ea-9137-0b74338422d4.jpg)

![Z](https://user-images.githubusercontent.com/42334717/76930097-0f549b00-6929-11ea-9ae6-a34b3ac9daa0.jpg)

~~~R
> fa=rbind(fault6,fault7,fault8,fault9)
> no=rbind(normal5,normal6,normal7,normal8)
> summary(fa)
      time              X                  Y                  Z           
 Min.   : 181.6   Min.   :-14.6193   Min.   :-8.42605   Min.   :-22.2520  
 1st Qu.: 408.7   1st Qu.: -0.2369   1st Qu.: 0.02105   1st Qu.: -0.7343  
 Median : 635.7   Median :  0.3680   Median : 0.59761   Median :  0.3068  
 Mean   : 635.7   Mean   :  0.3716   Mean   : 0.58776   Mean   :  0.3061  
 3rd Qu.: 862.8   3rd Qu.:  0.9775   3rd Qu.: 1.16734   3rd Qu.:  1.3467  
 Max.   :1089.8   Max.   : 13.8975   Max.   :10.59470   Max.   : 22.2974  
> summary(no)
      time              X                  Y                  Z           
 Min.   : 181.6   Min.   :-15.2587   Min.   :-9.47796   Min.   :-24.1539  
 1st Qu.: 408.7   1st Qu.: -0.1979   1st Qu.: 0.02559   1st Qu.: -0.4072  
 Median : 635.7   Median :  0.3737   Median : 0.61580   Median :  0.3183  
 Mean   : 635.7   Mean   :  0.3777   Mean   : 0.60424   Mean   :  0.3178  
 3rd Qu.: 862.8   3rd Qu.:  0.9499   3rd Qu.: 1.19691   3rd Qu.:  1.0425  
 Max.   :1089.8   Max.   : 14.9363   Max.   :10.77779   Max.   : 25.8188  
> IQR(fa$Z)
[1] 2.080954
> IQR(no$Z)
[1] 1.449666
~~~

+ 진동 데이터임에도 불구하고 평균이 0이 아님
  + FFT를 통해 노이즈 필터링 필요
+ Z축의 가속도에 차이
  + Kurtosis(첨도)가 Normal 상태에서 높게 나올 것이라 예상
  + Fault 상태에 더 진폭이 큰 분포를 가짐
  + 따라서 RMS도 높게 나올 수 있음
  + IQR도 수치적으로 다름
+ 하지만 X, Y축의 가속도는 거의 유사

## CIs


### FDR


![FDR](https://user-images.githubusercontent.com/42334717/76924261-212e4200-6919-11ea-8be4-3f90fb5573a7.png)


### 최적의 Condition Indicator(특성인자)와 Window size 선정



|Window size|Z_sk|<span style='color:rgb(225,10,10)'>Z_ku</span>|<span style='color:rgb(225,10,10)'>Z_rm</span>|Z_p2p|<span style='color:rgb(225,10,10)'>Z_iq</span>|<span style='color:rgb(225,10,10)'>Z_cf</span>|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1,000(0.6초)|0.0016|0.8548|9.5726|0.0663|8.8219|1.1792|
|5,000(3초)|0.0075|3.9295|15.095|0.2040|15.543|5.9002|
|10,000(6초)|0.0141|5.9023|16.238|0.3147|17.047|7.9695|
|100,000(60초)|0.1330|16.867|18.878|0.3652|19.921|13.088|

<img width="1024" alt="FDR for window size" src="https://user-images.githubusercontent.com/42334717/76932497-67da6700-692e-11ea-8a7e-44051653d906.png">

~~~R
> fdr(f5[,1],h5[,1])
[1] 12.34253
> fdr(f5[,2],h5[,2])
[1] 18.26443
> fdr(f5[,3],h5[,3])
[1] 19.2982
> fdr(f5[,4],h5[,4])
[1] 12.73563
~~~

## ML(SVM)

<img width="1920" alt="SVM" src="https://user-images.githubusercontent.com/42334717/77077309-5f6e5300-6a38-11ea-9569-033881277e97.png">

## Error

<img width="1920" alt="Error" src="https://user-images.githubusercontent.com/42334717/77077180-3b127680-6a38-11ea-8be0-73659951400e.png">

[20200313 SiM Lab. Meeting Presentation - 오효근.pdf](https://github.com/Zerohertz/Zerohertz.github.io/files/4355057/20200313.SiM.Lab.Meeting.Presentation.-.pdf)
[20200320 SiM Lab. Meeting Presentation - 오효근.pdf](https://github.com/Zerohertz/Zerohertz.github.io/files/4355054/20200320.SiM.Lab.Meeting.Presentation.-.pdf)