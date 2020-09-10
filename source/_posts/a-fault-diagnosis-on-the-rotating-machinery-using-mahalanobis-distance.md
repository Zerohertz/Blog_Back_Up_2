---
title: A Fault Diagnosis on the Rotating Machinery Using Mahalanobis Distance
date: 2020-02-26 11:59:39
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
# Introduction

> 회전기기의 이상을 모니터링하는 경우 구조물의 운전에 기인하여 발생하는 진동신호를 이용한 기법들이 종래부터 많이 사용되고 있으며, 일반적으로 이러한 기법들은 통계적인 방법과 신호처리법으로 구분할 수 있다.

+ 통계적 방법
  + RMS
  + Peak-Peak
  + Crest Factor
  + Kurtosis
  + PDF
+ 신호처리기법
  + Spectrum
  + Cepstrum
  + ANC
  + Filtering

결과는 여러가지 진단의 항목이 종합적으로 하나의 결과를 나타낸다. **즉, 진단기법의 여러 항목들은 독립적 관계가 아닌, 서로 상관관계를 가지고 있게 된다. 따라서 보다 정확한 진단시스템의 구축을 위해서는 다변량 분석이 필요하다.**

<!-- More -->

***

# Theory

## 통계적 기법

> RMS(Root Mean Square)

$$
x_{rms}=\sqrt{\frac{1}{T}\int_0^Tx(n)^2dt}
$$

+ $x(n)$ : 회전기기로부터 얻은 시간데이터
+ $x_{rms}$ : RMS 값
+ RMS 변화를 관찰하면 결함이 진전하는 경우 RMS 값도 증가

> Crest Factor

$$
Crest\ Factor=\frac{Crest\ value}{rms\ value}=\frac{sup|x(n)|}{(1/N)\sum_{n=1}^N[x(n)]^2}
$$

+ Peak 치와 RMS 값의 비
+ 충격파형의 신호를 검출
+ 초기결함을 감지할 수 있는 factor

> Kurtosis value

$$
Kurtosis=\frac{M_4}{M_2^2}=\frac{\frac{1}{N}\sum_{n=1}^N(x(n)-\bar x)^4}{[\frac{1}{N}(x(n)-\bar x)^2]^2}
$$

+ 4차 모멘트와 2차 모멘트의 비율
+ 무차원화된 값이므로 입력 데이터의 절대량에 관계없이 상대적인 값으로 표시
+ 따라서 이상진단에 유효하게 사용

## Mahalanobis Distance

> 마할라노비스 거리(Mahalanobis Distance)는 다차원의 단위공간으로서 마할라노비스 공간을 정의하고 임의의 대상이 그 공간으로부터 얼마나 떨어져 있는가를 거리로 나타낸 것이다.

***

# Experiment and Discussion

+ Rotor Kit(1300rpm)의 상태
  + Normal
  + Unbalance
  + Impulse
+ 실험장치
  + FFT Analyzer
  + 가속도계 : Rotor Kit의 베어링 부위에 설치
  + Impact Hammer

## 정상그룹 및 특성인자 선정

+ RMS
+ Peak to Peak
+ Kurtosis
+ Skewness
+ $1^{st}$ peak
+ Overall level

정상상태의 마할라노비스 거리를 구하기 위하여, 정상상태의 분석결과를 표준화 시킨다. 구해진 상관행렬을 이용하여 **회전기기의 정상상태 마할라노비스 거리를 구해보면 0.7 이하의 값들을 가지게 된다.**

## 비정상 그룹의 선정 및 식별능력 확인(1)

+ 로터에 불평형 질량 추가
+ 불평형 질량 : 4g의 추
+ RMS, Overall level, $1^{st}$ peak가 정상상태에 비해 증가

정상상태의 마할라노비스 거리와 비교하면 식별결과가 뚜렷함을 알 수 있다. 추후 불평형 질량에 따른 마할라노비스 거리값을 데이터베이스화 한다면 정량적 평가가 가능할 것으로 사료된다.

## 비정상 그룹의 선정 및 식별능력 확인(2)

+ 정상상태에 Impact Hammer로 가진을 하여 과도상태로 만들어 측정
+ 베어링 결함을 모사하기 위한 충격파형으로 인해 통계적 분석 시 정상상태와 불평형 상태 대비 Crest Factor가 큰 것을 확인 가능

각 상태에 따른 신호의 분석 결과 정상상태와 비교하였을 때 불평형 상태는 약 110배, 충격파형 상태는 약 3500배로써 **마할라노비스 거리를 통하여 확실한 분별력 확인이 가능하다.**

***

# Conclusion

1. 정상상태의 시스템을 분석
2. 통계적 분석과 신호처리의 결과를 이용
3. 정상상태의 마할라노비스 거리 : 0.67~0.68
4. 불평형 질량의 시스템의 마할라노비스 거리 : 68~84
5. 충격파형의 시스템의 마할라노비스 거리 : 2000~2800
6. 식별력 최고

<u>**마할라노비스 거리가 짱이다.**</u>