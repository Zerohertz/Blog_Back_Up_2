---
title: Evaluation of Datum Unit for Diagnostics of Journal-Bearing Systems
date: 2020-02-26 12:58:49
categories:
- Research
- Read Paper
tags:
- Machine Learning
- Signal Processing
- PHM
- Read Paper
- Smart data
mathjax: true
---
# Jornal-Bearing

> 저널베어링은 회전하는 축과 베어링 지지부 사이에 유막을 형성하여 회전체를 지지하는 구조물이며, 고속 및 고하중 조건에서도 안정적이기 때문에 발전소와 같은 대형 시스템에 널리 사용되고 있다.

+ 저널베어링 시스템의 신뢰성을 확보하기 위한 감독학습 기반의 상태진단 알고리즘 연구
+ 기존 : 진동신호 특성인자들의 정의에 대한 연구
+ 본 연구 : 정의된 특성인자의 추출단위인 데이텀의 적용 기준에 대한 연구
+ 데이텀의 효용성 평가를 통해 저널베어링 회전체 특성인자의 추출기준
  + 시간영역에서 1 회전
  + 주파수영역에서 60 회전

<!-- More -->

***

> 기호
> $$
> \mu_i\ :\ Class\ i의\ 평균
> $$
> $$
> \sigma_i\ :\ Class\ i의\ 표준편차
> $$

# Introduction

저널베어링은 회전하는 축과 베어링 지지부 사이에 유막을 형성하여 회전체를 지지하기 때문에 고속, 고하중의 조건에서 안정성이 요구되는 시스템에 적합하다.(화력발전소의 터빈, 대형 펌프, 선박 추진부)

> 저널베어링을 포함하는 일반적인 기계시스템에서는 이상조건이나 고장이 발생하면 시스템의 성능이 점차 저하된다.

특히 대형 시스템의 경우, 고장 발생 초기에 적절한 조치가 이루어지지 못하면 심각한 시스템의 손상과 함께 막대한 사회적, 경제적 손실을 야기할 수 있다. 따라서 **시스템의 상태를 실시간으로 평가하고 시스템의 상태에 적합한 조치를 취하여 안전성을 확보해야 한다.** <u>**이를 위해서는 강건한 실시간 진단 시스템이 필요하다.**</u>

진동신호는 회전체 시스템의 거동을 가장 잘 나타내는 대표적인 데이터로써 다양한 형태의 베어링 진단에 널리 활용되고 있다. **일반적으로 저널베어링은 변위 형태로 계측된 진동데이터로부터 진동 크기와 함께 주파수 분석 및 위상경향 분석 결과를 활용하여 진단이 이루어진다. 특히 실시간 상태감시에서는 진동크기가 주로 활용되고 있으며, 기준치 이상의 진동이 발생할 경우 시스템은 비정상으로 판별되어 전문가의 추가적인 분석이 요구된다.** **<u>본 논문에서는 실시간 진단 시스템을 개발하기 위한 과정으로, 감독학습 기반의 진단과정 중 특성인자 추출 기준 연구를 진행하였다. 특성인자 추출은 시스템의 상태 정보를 정량화하는 단계로써 진단관점에서 매우 중요하다.**</u>

***

# 진단 시스템에서의 특성인자 추출

> Machine Learning Process

+ Training
  1. Training Data
  2. Signal Processing
  3. Feature Extraction
  4. Feature Selection
  5. Classifier Training
+ Testing
  1. Testing Data
  2. Signal Processing
  3. Feature Extraction
  4. Feature Selection
  5. Classification

데이터 획득 과정에서는 시스템의 상태를 대표하는 정보를 획득하는데, 본 연구에서는 진동데이터가 사용되었다. 진동 데이터에 적합한 신호처리 과정을 거쳐, 시간 및 주파수영역의 특성인자를 추출하고, 분류능력이 우수한 특성인자를 선별한다. 최종적으로 선별된 특성인자는 artificial neural network(ANN)나 support vector machine(SVM) 등의 알고리즘으로 분류기를 학습하는데 이용된다. 진단과정에서는 학습과정에서 적용된 방법들을 이용하여 특성인자를 추출하고, 기 학습된 분류기를 이용해 시스템의 상태를 진단한다.

<u>**본 연구에서는 감독학습 기반의 진단과정 중 특성인자 추출 과정을 집중적으로 다루고자 한다.**</u>

+ 특성인자 : 대상 시스템의 상태를 두드러지게 표현해주는 정량적 지표
  + 효과적인 특성인자는 물리적 관점에서 상태 분석을 가능하게 하고 궁극적으로 진단 시스템의 성능 향상에 기여

> 현재까지 진행된 연구들은 주로 어떠한 인자를 특성인자로 적용할 것인지에 초점을 두었지만, 특성인자 추출 시 데이터 길이의 기준을 선정하는 연구는 미비하였다.

<u>**따라서 본 논문에서는 최적의 특성인자를 추출하기 위한 방법을 다루고자 한다.**</u> **특성인자의 추출 기본 단위인 데이텀이 어떻게 정의되는지에 따라 효용성에 차이가 있고, 나아가 진단 시스템의 성능도 달라진다.**

***

# 데이터 및 신호처리

## 데이터

> 본 연구에서는 Bently Nevada 사의 RK4 저널베어링 실험장치에서 획득한 5가지 상태 조건의 진동신호와 Matlab을 통해 시뮬레이션된 3종류의 진동신호를 이용하였다.

+ 커플링으로 연결된 두 축을 3개의 베어링이 지지
+ 긴 축에는 800g의 디스크 장착
+ 회전속도 : 3,600RPM
+ 정상조건과 4가지 이상상태 실험 진행
  + 질량불평형
  + 마찰
  + 오정렬
  + 오일훨
+ 베어링 부군에 장착된 갭 센서 이용 : 60초 동안의 변위 진동데이터 측정
+ 진동 신호 : 8,500Hz 샘플링 주기
+ Matlab 이용
  + 시뮬레이션된 신호에서는 정상조건과 실험에 포함되어 있지 않은 2가지 이상상태 고려
  + 정상조건 : 60Hz의 회전성분만 존재하도록 설정
  + 이상상태1 : 정상상태 신호에 60Hz의 절반인 30Hz 주파수 성분 추가
  + 이상상태2 : 정상상태 신호에 60Hz의 조화주파수(2, 3, ..., 10X) 성분 추가
+ 실제 실험데이터에서 주파수 성분의 크기가 바뀌는 특징을 반영하여 조화주파수 성분의 변화 폭을 평균값의 10%로 정하여 불확실성 고려

## 신호처리

> 저널베어링은 회전축과 베어링 지지부 사이에 유막이 형성되어 구동되기 때문에

+ 정상적인 조건 : 정현파에 가까운 진동 발생
+ 이상상태 : 파형이 변형되면서 정상조건의 정현파와 다른 형태를 나타냄
  + 각 상태에서의 파형의 특성을 평가하기 위해 각 회전을 기준으로 데이터를 분석하는 것이 효과적
  + 각 회전 성분의 데이터를 획득하기 위해 회전각 기반 리샘플링(angular resampling) 적용
  + 동일한 회전각 기준으로 데이터를 리샘플링하기 때문에 RPM이 변하더라라도 각 회전당 동일한 개수의 데이터를 가짐

***

# 데이텀 정의에 따른 특성인자 평가

## 특성인자 정의

> Time-domain features

+ Root Mean Square(RMS)
+ Skewness
+ Kurtosis
+ Crest Factor
+ Shape Factor
+ Impulse Factor

동역학적 에너지와 관련된 인자와 진동파형과 관련된 인자 등 총 6개의 인자
진동의 파형이 변형되거나 찌그러지는 경우, 그 효과는 시간영역 특성인자에 반영

> Frequency-domain features

+ Frequency Center
+ RMS Frequency
+ Root Variance Frequency
+ [0~1X]/1X
+ [2,3,4,...,10X]/1X

중심 주파수와 관련된 인자와 특정 주파수영역 성분의 크기와 관련된 인자 총 5개의 인자
회전체 진단에 널리 적용

## 데이텀 정의

> 본 연구에서 논의하고자 하는 데이텀은 특성인자 추출의 기준이 되는 데이터의 길이를 의미한다.

+ 특성인자를 추출하는 데이텀 기준에 따라 특성인자의 분류 성능이 달라질 수 있음
+ 본 연구에서는 1초 길이의 신호에 해당하는 60회전(3,600RPM)을 기준으로 데이텀을 달리하며 효용성 비교

> Datum units for feature extraction

![Datum units for feature extraction](https://user-images.githubusercontent.com/42334717/75640668-2cc30d00-5c79-11ea-8b3b-4b687a55cc22.png)

+ 위와 같이 진동데이터로부터 데이텀 단위를 변경하며 선정한 11개 특성인자를 비교
  + 60회전의 진동신호를 기준으로 1, 10, 20, 30, 60 회전의 데이텀 적용
  + 추출한 특성인자들의 수를 동일하게 하기 위해 1, 10, 20, 30 회전 기준 특성인자들은 각각 60, 6, 3, 2개씩 평균
  + 60회전 기준 특성인자는 평균을 내지 않음
+ **총 5개의 데이텀 중 가장 효용성이 높은 특징인자 추출방법을 선별하기 위해 각각의 데이텀 평가**

## 데이텀 효용성 평가 기준

> 진단의 관점에서 데이텀의 효용성은 특성인자의 분류능력을 기준으로 평가할 수 있다. 분류능력이 높은 인자일수록 더 정확한 진단이 이루어질 수 있기 때문이다.

+ 분류능력 평가 척도 - Fisher Discriminant Ratio(FDR) 사용
  + 2 class 기준 : 각 class의 평균과 분산 만을 사용한 값
    + 직관적인 분류능력을 나타냄
  + M class 기준(M>2)
    + 일반화된 식으로 특징인자의 분류능력을 구함

$$
FDR_{2class}=\frac{(\mu_i-\mu_j)^2}{\sigma_i^2+\sigma_j^2}
$$
$$
FDR_{Mclass}=\sum_i^M\sum_{j\neq i}^M\frac{(\mu_i-\mu_j)^2}{\sigma_i^2+\sigma_j^2}
$$

+ 위 식 모두 class내의 분산이 작고, class간의 거리가 멀수록 FDR은 큰 값을 나타냄
+ FDR이 클수록 특성인자의 분류능력이 크다는 의미
+ 아래 그림 참고

> Example of FDR case

![Example of FDR case](https://user-images.githubusercontent.com/42334717/75641501-cf7c8b00-5c7b-11ea-9539-76de3eae91a6.png)

***

# 결과 및 고찰

> 본 연구에서는 데이텀 크기 변화에 따른 효용성을 평가하기 위해 RK4 실험데이터와 Matlab으로 시뮬레이션된 데이터가 사용되었다.

## RK4 실험 데이터의 FDR 결과

> FDR of RK4 time features

|Time-domain|RMS|Skewness|Kurtosis|Crest Factor|Shape Factor|Impulse Factor|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|1 Cycle|<span style='color:rgb(225,10,10)'>92660</span>|<span style='color:rgb(225,10,10)'>18525</span>|<span style='color:rgb(225,10,10)'>15031</span>|<span style='color:rgb(225,10,10)'>40509</span>|5790|<span style='color:rgb(225,10,10)'>37861</span>|
|10 Cycle|90373|17831|13602|2239|6196|2681|
|20 Cycle|90263|17760|13768|1501|<span style='color:rgb(225,10,10)'>6273</span>|1870|
|30 Cycle|90261|17742|13570|1155|6260|1450|
|60 Cycle|90346|17779|13487|777|6177|996|

+ Shape Factor를 제외한 모든 인자가 1회전 데이텀 기준이 다른 데이텀 기준보다 높은 FDR 값을 나타냄
+ 특히 Crest Factor와 Impulse Factor는 1회전과 다른 데이텀 기준간 비교시, 1회전 데이텀에서 현격이 높은 FDR 값을 나타냄
+ 시간영역에서 1회전 데이텀의 FDR 값이 높게 나타나는 이유는 각 회전의 특성인자를 추출하여 60개 평균을 적용하기 때문에 특성인자의 표준편차를 줄여주기 때문

> FDR of RK4 freq. features

|Freq.-domain|Frequency Center|RMS Frequency|Root Variance Frequency|[0~1X]/X|[2,3,4,...,10X]/1X|
|:-:|:-:|:-:|:-:|:-:|:-:|
|1 Cycle|15831|13116|13723|N/A|16624|
|10 Cycle|16454|17846|19341|3730|32389|
|20 Cycle|<span style='color:rgb(225,10,10)'>26654</span>|<span style='color:rgb(225,10,10)'>21722</span>|23296|3844|<span style='color:rgb(225,10,10)'>35115</span>|
|30 Cycle|19095|19140|21657|<span style='color:rgb(225,10,10)'>4034</span>|34970|
|60 Cycle|21525|20125|<span style='color:rgb(225,10,10)'>24497</span>|3833|35041|

+ 주파수영역의 인자는 모두 주파수 분석(Spectral analysis) 결과를 토대로 생성
+ 1회전 데이텀은 1X 미만 주파수 성분 표현이 불가능하여 [0~1X]/1X 인자를 생성할 수 없음
+ 주파수영역에서는 20회전의 데이텀 기준이 대체로 높은 FDR 값을 나타내지만, 경향이 두드러지지 않음
+ 특히 1X 미만의 주파수 성분은 데이텀 기준에 따라 Spectral leakage의 영향을 받을 수 있음
  + Spectral leakage : 주파수 분해능이 충분히 높지 않거나, 데이텀에 따라 결정되는 분해능이 실험현상을 표현할 수 없을 때 왜곡된 주파수분석 결과가 발생하는 현상
+ 1X 미만 주파수 성분으로 Oil whirl의 0.45X 성분이 있으며, 20회전과 60회전의 데이텀은 0.45X 주파수 성분 표현이 가능하여 상대적으로 높은 FDR 값을 나타냄
+ 해당 주파수 성분의 표현이 가능한 경우는 $FDR_{Mclass}$식의 $\sigma_i$(표준편차) 값을 줄여주어 상대적으로 FDR 값이 증가됨
+ 1회전 데이텀에서 현저히 낮은 FDR 값이 나타나는 이유는 Spectral leakage 현상에 의해 왜곡된 주파수 분석 결과가 반영되었기 때문

## 시뮬레이션 신호의 FDR 결과

> FDR of generated signal time features

|Time-domain|RMS|Skewness|Kurtosis|Crest Factor|Shape Factor|Impulse Factor|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|1 Cycle|42|<span style='color:rgb(225,10,10)'>7</span>|<span style='color:rgb(225,10,10)'>103</span>|<span style='color:rgb(225,10,10)'>116</span>|76|<span style='color:rgb(225,10,10)'>89</span>|
|10 Cycle|42|0|54|59|76|64|
|20 Cycle|42|0|54|40|76|53|
|30 Cycle|42|0|54|33|76|47|
|60 Cycle|42|0|54|21|76|35|

+ RK4 실험 데이터와 유사하게 1회전 기준 데이텀 특성인자가 대부분 가장 높은 FDR 값을 보임
+ RK4와 마찬가지로 시간영역에서는 1회전 데이텀이 상대적으로 낮은 표준편차를 갖기 때문에 분류능력이 높게 나타남

> FDR of generated signal freq. features

|Freq.-domain|Frequency Center|RMS Frequency|Root Variance Frequency|[0~1X]/X|[2,3,4,...,10X]/1X|
|:-:|:-:|:-:|:-:|:-:|:-:|
|1 Cycle|<span style='color:rgb(225,10,10)'>174</span>|<span style='color:rgb(225,10,10)'>193</span>|231|NaN|52|
|10 Cycle|140|184|<span style='color:rgb(225,10,10)'>437</span>|68|52|
|20 Cycle|140|184|436|68|53|
|30 Cycle|140|184|435|68|52|
|60 Cycle|140|184|436|68|52|

+ 1회전 기준을 제외하고, 데이텀 기준에 따른 FDR 값의 차이가 크지 않은 것으로 나타남
+ 시뮬레이션 이상상태1의 신호는 0.5X 성분이 존재하며, 해당 주파수 성분은 1회전을 제외한 모든 데이텀 기준(10,20,30,60회전)에서 정확히 표현이 가능하기 때문에 FDR 값이 유사하게 나타남
+ 반면 1회전 데이텀에서는 0.5X 주파수 성분이 Spectral leakage 현상에 의해 왜곡되어 일부 특성인자에 영향을 미치게 됨
+ 이런영향은 FDR 결과에도 영향을 주어 시뮬레이션에서는 실험과 달리 왜곡된 특성인자의 결과가 일부 특성인자(Frequency Center, RMS Frequency)의 FDR 값을 증가시키는 결과를 초래함

## 데이텀 효용성 평가 결과 고찰

+ 실험과 시뮬레이션 데이터를 이용하여 FDR 효용성을 평가한 결과 시간영역의 특성인자는 1회전 데이텀 기준에서 높은 분류능력을 나타냄
+ 반면 주파수영역의 특성인자는 데이텀 기준에 따른 분류능력이 뚜렷한 경향을 띠지 않으며, Spectral leakage에 따라 FDR 값이 영향을 받음
+ 본 연구에서는 Spectral leakage의 영향으로 인해 실험과 시뮬레이션에서 상반되는 결과가 도출됨
+ 실험에서는 1회전 기준의 FDR 값이 떨어진 반면, 시뮬레이션에서는 일부 1회전 데이텀 특성인자의 FDR 값이 증가됨
+ 두 결과 모두 왜곡된 특성인자 값에 기인한 것으로 유효하지 못한 결과로 평가됨
+ 대신 주파수영역에서는 60회전의 데이텀 기준이 가장 높은 주파수 분해능을 가지기 때문에 다른 데이텀 기준에 비해 임의의 1X 미만 주파수 성분을 상대적으로 정확히 표현할 수 있음
+ 따라서 Spectral leakage 현상이 감소되고, 상대적으로 높은 FDR 값을 일정하게 얻을 수 있음

***

# 결론

> 기존 연구에서는 일정시간의 신호로부터 추출하는 특성인자를 주로 사용하였으나, 본 연구에서는 회전수 기준의 특성인자 사용을 제안하였다.

+ RK4 실험데이터와 Matlab 생성데이터로부터 회전수 기반 데이텀의 효용성을 평가
+ **시간영역의 특성인자는 1회전 기준 데이텀의 분류능력 우수**
+ **주파수영역의 특성인자는 Spectral leakage 현상을 고려하여 60회전 기준 데이텀이 적합**

<u>**본 연구에서 활용한 FDR 분류능력 평가 척도는 간단한 통계량인 평균과 분산값을 이용하기 때문에 널리 사용되고 있다. 하지만 상한과 하한의 제한 값이 없어 특성인자간 또는 다른 데이터 조합간의 절대적 비교가 어렵다.**</u>