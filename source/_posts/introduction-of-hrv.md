---
title: Introduction of HRV
date: 2020-12-22 14:58:04
categories:
- Research
- Read Paper
tags:
- Signal Processing
- PHM
- Statistics
- Smart data
- Sleep apnea
mathjax: true
---
# Introduction

> 심박동과 박동사이의 간격(R-R interval)은 안정을 취하고 있을 때에도 항상 변화하는데, 이것을 심박변동(Heart Rate Variability, HRV)이라고 한다. 일반적으로, 이러한 심장 박동 간의 변화는 안정 상태일수록 더 크고 복잡한 형태를 나타내며, 운동을 하거나 스트레스 상태인 경우 규칙적이고 일정한 형태를 나타낸다.

+ HRV 신호로부터 임상적인 해석을 유도하기 위해 심전도(ECG) 신호 측정
+ 측정하는 시간에 따라
  + 24시간 데이터를 이용하는 장기(long-term) 분석
    + 하루주기리듬(circadian rhythm)을 포함하여 많은 정보를 얻을 수 있음
    + 임상적 상황에서는 측정이 어려움
  + 5분 또는 3분 데이터를 사용하는 단기(short-term) 분석
    + 순간적인 생리적 변화를 반영
    + 환자의 상태와 검사 환경을 제어하지 않을 경우 진단의 오류 가능성 존재
+ HRV 측정 시간 및 방법은 비용대비 효과와 임상적 상황에 따라 적절한 선택 필요

<!-- More -->

***

# HRV Signal

> HRV signal extraction from ECG signal

![HRV signal extraction from ECG signal](https://user-images.githubusercontent.com/42334717/102859435-3ec3a580-446f-11eb-895c-8b85e1b9cfc6.png)

+ HRV
  + 하나의 심장 주기로부터 다음 심장 주기 사이의 변이 측정
  + 끊임없이 변화하는 심혈관계 제어 메커니즘에 있어 R-R 간격의 변동 특징을 관찰 및 심장박동의 변화 추이를 정량화
+ Signal extraction process
  1. 심전도 신호로부터 R 피크 검출
  2. 검출된 R-R 간격을 시계열 신호로 변환하여 시간축에 재배열
  + 시간에 따라 변화하는 심박동 변화를 알 수 있음
+ Condition Indicators of HRV
  + Time domain analysis(시간 영역 해석)
    + 심박동의 평균치 변화나 표준편차와 같은 통계적이고 기초적 정보 제공
    + 주파수 분석 방법이 도입되기 전에 일반적으로 사용된 방법
    + 측정이 용이하며 많은 정보 제공
  + Frequency domain analysis(주파수 영역 해석)
    + HRV 파형을 분석하여 각 주파수 성분의 신호가 상대적으로 어떤 강도로 존재하는지 보는 방법
    + 자율신경계의 교감신경과 부교감신경계의 길항적 활동 추정
    + 대부분의 임상에서는 HF 대역에 대한 LF 대역의 강도를 교감신경과 부교감신경의 균형도로 해석

***

# Condition Indicators of HRV

+ Time domain
  + SDNN : Standard deviation of all NN intervals
    + 심혈관계의 안정도와 더불어 자율신경계의 신체에 대한 제어능력에 관한 정보를 제공하는 강력한 지표
  + RMSSD : The square root of the mean of the sum of the squares of differences between adjacent NN intervals
  + SDSD : Standard deviation of differences between adjacent NN intervals
  + NN50 count : Number of pairs of adjacent NN intervals differing by more than 50ms in the entire recording
  + pNN50 : NN50 count divded by the total number of all NN intervals
+ Frequency domain
  + TP : 5min total power
  + VLF : Power in very low frequency range
  + LF : Power in low frequency range
  + HF : Power in high frequency range
  + LFnorm : LF power in normalized units
  + HFnorm : HF power in normalized units
  + LF/HF : Ratio LF {$ms^2$} / HF {$ms^2$}

|주기성분|주파수 대역|관계되는 신경계|
|:-:|:-:|:-:|
|VLF 성분|0.003 ~ 0.05 Hz|온도조절, 혈관운동, 레닌-엔지오텐신 조절계|
|LF 성분|0.05 ~ 0.15 Hz|압력수용기 반사, 혈압조절계|
|HF 성분|0.15 ~ 0.40 Hz|미주신경(부교감 신경)|