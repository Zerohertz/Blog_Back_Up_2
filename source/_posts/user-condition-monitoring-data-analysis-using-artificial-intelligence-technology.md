---
title: >-
  User Condition Monitoring Data Analysis Using Artificial Intelligence
  Technology
date: 2020-12-21 16:36:15
categories:
- Research
- Read Paper
tags:
- Machine Learning
- DNN
- Signal Processing
- PHM
- Statistics
- Smart data
- Sleep apnea
mathjax: true
---
# Introduction

+ 사용자 상태 측정 시스템
  + 전기적 측정
    + 뇌파
    + 심전도
    + 근전도
    + 안전도
  + 움직임 및 행동 측정
    + 가속도 센서
    + 자이로 센서
+ 심전도
  + 심장의 상태를 전기적으로 측정할 수 있음
  + 심전도 정보를 통해 사용자의 심장 상태 정보 및 자율신경계 반응을 얻을 수 있음
+ 가속도
  + 사용자의 행동 상태 정보를 모니터링
  + 일상생활 중의 움직임 정보를 얻을 수 있음
  + 모니터링을 통해 수면의 질을 평가하는데 많이 사용
+ 기존의 기술 
  + 대부분 특정 모델 기반 특징점 추출을 통해 이루어짐
  + 신호들의 정형성 및 선형성을 가정한 모델
  + 생체신호들이 가지고 있는 비정형성 및 비선형성의 특징을 반영하여 분석하기 어려움
+ 생체신호 데이터로부터 모델을 설계하고 최적화하는 알고리즘 필요 - DNN 이용
  + Deep ECGNet
  + Deep ACTINet

<!-- More -->

***

# Deep Neural Network Algorithm

+ 기존의 심전도 및 액티그라피 신호 분석
  + 대부분 모델 기반의 특징점 추출 알고리즘
  + 기계 학습 분석을 통해 사용자의 상태를 최종 추정
  + 고정된 모델 및 가정을 통해 분석이 이뤄짐
  + 시간에 따라 지속적으로 특징이 변하는 생체신호 분석에 최적은 아님
+ Deep Neural Network
  + 고정된 모델 및 가정에 기반하지 않고 데이터로부터 특징을 추출하여 분석함
  + 입력 신호와 그 신호에 따른 상태를 딥러닝 네트워크 구조에 대입하고 최적화 기술을 활용하여 네트워크의 파라미터 값들을 찾아내어 최적의 모델을 데이터 자체로부터 유도하는 End-To-End 기술

## Deep ECGNet

+ 심전도 신호의 특징점을 입력으로 받지 않고 심전도 데이터 자체 입력
+ 입력 신호의 패턴을 딥러닝 구조 내에서 찾아내기 위하여 Convolution Neural Network(CNN) 레이어 사용
  + 필터 및 Pooling 레이어의 크기를 결정하기 위하여 심전도의 생리학적 특징을 바탕으로 설계해야 최적의 심전도 패턴 추출 성능을 기대할 수 있음
+ CNN 구조를 통해 얻어낸 심전도 패턴 정보는 Recurrent Neural Network(RNN) 구조를 거쳐 시간에 따라 유사한 패턴이 나타나는 시계열 심전도 신호의 순차적 특징을 추출

## Deep ACTINet

+ 가속도 센서 데이터의 패턴을 추출하기 위해 네 개의 CNN 구조 설계
+ 시계열의 순차적 패턴을 찾아내기 위해 RNN 구조 Long Short-Term Memory(LSTM) 적용