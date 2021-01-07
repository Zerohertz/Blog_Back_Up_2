---
title: Development of a Obstructive Sleep Apnea Diagnosis Algorithm Using HRV
date: 2021-01-07 10:30:26
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
- Smart data
- Sleep apnea
mathjax: true
---
# Introduction

+ Obstructive Sleep Apnea(폐쇄성 수면무호흡증)
  + 정의 : 수면 중 상기도가 좁아지거나 막혀 무호흡과 저호흡이 되풀이되는 질환
  + 위험성 : 혈중 산소포화도 감소 - 산소를 많이 필요로 하는 장기(뇌, 심장)에 영향
    + 증상 : 두통, 기억력 및 집중력 저하, ...
    + 질환 : 수면질환(불면증), 고혈압, 심부정맥, 신부전 및 관상 동맥, ...
  + 유병률 : 국내 농촌인구의 3%, 미국 중년 남성의 4%, 여성의 2%
+ 현재의 기술 - 야간 수면다원검사
  + 여러 가지 감지기 부착
  + 평소의 수면환경이 아닌 수면검사실에서 수면
  + 장시간 검사에 따른 높은 비용
  + 현실적 대안 : 간이형 수면다원기록기 or 활동 기록기
+ 손목부착형 활동기록기(액티그라피)
  + 손목 운동에 따른 가속을 감지해 몸의 활동량을 측정
  + 사용이 간편하며 피험자에게 익숙한 환경에서 장기간 검사 가능
  + 수면다원검사에 비해 경제적 이점
  + 미국수면학회 : 불면증과 일주기 수면-각성 장애에서 유용
  + 수면분절지수에 의해 민감도가 특이도가 낮음
    + 무호흡 및 저호흡과 관련된 움직임의 빈도만 반영
  + 수면무호흡수치 반영
    + 폐쇄성 수면무호흡증 환자의 수면 시간을 짧게 평가하는 현상 개선
+ 기술개발계획
  + 심박변이도 신호 분석을 통한 폐쇄성 수면무호흡증 진단 알고리즘 개발
  + 음성신호 분석을 위한 마이크 이용
  + 획득된 폐쇄성 수면무호흡수치를 바탕으로 수면/각성 주기 계산 알고리즘 개발

<!-- More -->

***

# Condition Indicator(HRV)

+ 비침습적인 심박변이도(Heart Rate Variability, HRV)
  + 심전도상의 R-R 간격 변화 측정
    + R-R 간격 : 하나의 심장 주기와 다음 심장 주기 사이의 미세한 변이
  + 일반적으로 교감신경과 부교감신경의 영향을 받아 조절되는 것으로 알려짐
  + 수면은 자율신경계에 영향을 주며, 이는 곧 HRV에 영향을 줌
    + 수면무호흡증과의 상관관계
  + 영향을 주는 인자 : 호흡, 혈합, 호르몬, 감정, ...


## Time domain analysis

> R-R 간격의 변화(NN interval)를 통계적 분석

+ SDNN
+ SDNN index
+ RMSSD
+ pNN50
+ SDANN

## Frequency domain analysis

> R-R 간격의 주기적 진동을 주파수와 진폭으로 분해

+ VLF(Very Low frequency) : 0.003~0.04Hz
+ LF(Low Frequency) : 0.04~0.15Hz
+ HF(High Frequency) : 0.15~0.4Hz

***

# Data Result

## 2020/07/22

> 특수문자 사용으로 인한 .csv 파일 저장 오류

## 2020/07/27

> Acceleration

![Acc](https://user-images.githubusercontent.com/42334717/88665268-58a7c900-d119-11ea-9861-3e05d5f4c587.jpg)

> Acoustic Emission

![AE](https://user-images.githubusercontent.com/42334717/88665261-56de0580-d119-11ea-86b5-31a9b10bb816.jpg)

> Accerleration & Acoustic Emission

![Acc & AE](https://user-images.githubusercontent.com/42334717/88665402-868d0d80-d119-11ea-8e9f-98daa1f4f6a1.png)

> Accerleration & Acoustic Emission & Scoring Data

![20200813_무호흡_진단_알고리즘_발표_H_Oh-3](https://user-images.githubusercontent.com/42334717/90608792-110aed80-e23e-11ea-9887-a03d635c1e58.jpg)

![20200813_무호흡_진단_알고리즘_발표_H_Oh-4](https://user-images.githubusercontent.com/42334717/90608764-051f2b80-e23e-11ea-9156-8175f6ebb90e.jpg)

## 2021/01/06

> R-R interval & HRV

![R-R interval & HRV](https://user-images.githubusercontent.com/42334717/103840890-cb0fd280-50d5-11eb-94fa-a6bd83468619.png)

> Frequency Domain Analysis

![Frequency Domain Analysis](https://user-images.githubusercontent.com/42334717/103643405-fa202a00-4f97-11eb-980f-1bb66f5a9e10.png)

***

# Index

+ Sleep Fragmentation Index(SFI, 수면분절지수)
  + 수면 분절의 정도를 유추하는 계산식을 통해 산출
  + 기존에는 폐쇄성 수면무호흡증을 78%의 민감도, 95%의 특이도로 진단
  + 수면무호흡 및 저호흡과 관련된 신체 움직임의 빈도만 반영
  + 관련이 없는 움직임도 포함시킴으로써 민감도와 특이도가 낮아짐
+ Apnea-Hypopnea Index(AHI, 수면무호흡지수)
  + 수면 시, 호흡의 장애 심각도를 측정하는 지표
  + 무호흡 및 저호흡의 지속 시간, 혈중 산소 포화도 감소, 뇌파의 변화, 신체적 각성 등을 고려
+ Heart Rate Variability(HRV, 비침습적인 심박변이도)
  + 심전도상의 R-R 간격의 변화를 측정하여 얻음
  + 일반적으로 교감신경과 부교감신경의 영향을 받아 조절되는 것으로 알려짐