---
title: Professional Signal Process for PHM
date: 2020-01-20 10:56:41
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

## PHM?

> Prognostic and Health Management(건전성 예측 및 관리)

### 특징

+ 최근 산업규모가 점차 커지며 기술 발전 - 시스템 운영에서 안전(Risk)와 비용(Cost)을 함께 고려
+ 시스템의 결함(Fault)을 조기 감지(Early detection)
+ 발생한 결함의 종류와 심각도 진단(Diagnosis)
+ 고장 발생 시점 사전 예지(Prognosis)

### 이득

+ 대규모 사고로 이어질 수 있는 가능성을 줄임
+ 전통적 주기정비 또는 예방정비(Periodic or Preventive Maintenance, PM) 방식 탈피
+ 필요한 시점에만 정비를 수행하는 상태 기반 정비(Condition Based Maintenance, CBM) 실현

<!-- More -->

### 단계

1. Signal processing
2. Feature extraction
3. Diagnosis
4. Prognosis

## Gear, Bearing

+ 회전기계에 사용되는 부품으로, 많은 고장이 이들에 의해 발생
+ 예방을 위해 건전성 예측관리(PHM) 기술 - 결함 감지, 진단 고장시점 사전 예측
+ 플랜트, 화력발전소, 철도와 같은 사회기반 시스템에서 CNC 머신, 로봇과 같은 단위 설비까지 회전을 통해 전력을 전달하는 공통 부품
+ 사용 중 발생하는 고장과 그로 인해 발생하는 비용 및 다운타임(Down-time)의 상당부분은 기어와 베어링으로부터 기인
+ Ex) 풍력발전기 산업 - 전체 유지정비비용의 38%가 기어와 베어링으로 구성된 기어박스(Gearbox)에 의해 발생

***
# General Signal Processing Technique

+ 신호처리의 기본 목적은 다양한 다른 신호와 노이즈가 혼재된 신호에 대해 고장 진단에 필요한 정보를 남기고 그 외의 정보를 제거
+ 주기적인 신호를 제거하는 특성신호 분리(Discrete signal separation)
+ 미세한 신호를 강화 시키는 신호 강화(Signal enhancement)
+ 신호처리를 한 데이터로 특징을 추출해야 쉽게 결함관련 정보 습득
+ 원신호를 다양한 성분으로 분해하는 신호 분해(Signal decomposition)

## Discrete signal separation

> 고장과 관련된 신호를 취득하기 위해서는 고장신호와 무관한 신호들을 제거하는 것이 효과적

+ 무관한 신호들은 주변 장치에서 발생하는 주기적인 신호와 노이즈 포함
+ 이를 위한 대표적인 기법 - Linear prediction, Self Adaptive Noise Cancellation(SANC), Time Synchronous Averaging(TSA)

### Linear prediction

> 과거의 데이터를 이용하여 신호의 Deterministic한 부분을 선형적으로 모델링하여 미래의 출력 값을 추정하는 방법
> Autoregressive model $$x_p(n)=-\sum_{k=1}^{p}a(k)x(n-k)$$

+ $x$ - 원신호
+ $x_p(n)$ - AR Model로 얻은 주기신호
+ $p$ - AR Model의 차수
+ $a(k)$ - AR Model의 계수
+ 일반적으로 원데이터 $x(n)$의 자기상관함수를 이용하는 Yule-Walker equation을 통해 계산

#### Yule-Walker equation on Matlab

~~~Matlab
aryule(x,p) %a(k)
filter([0 -a(2:end)],1,x) %xsubp(n)
~~~

> $$e(n)=x(n)-x_p(n)$$

+ $e(n)$ - 잔여 신호
+ 불필요한 성분 제거
+ 고장과 관련된 고주파 성분
+ AR Model은 Model의 차수를 의미하는 값 $p$값, 즉, 과거 데이터를 어느 정도 사용할 것인지 결정하는 파라미터가 성능에 영향
+ Model 차수가 높아지면 Model이 복잡해지기 때문에 예측결과 부정확
+ Model 차수가 낮아지면 신호의 주기적인 특징을 확보하는데 무리
+ 목적에 맞게 적절한 $p$값을 선정
+ 이를 위해 보통 AIC값을 계산하여 그 값이 최소가 되는 $p$값을 사용

### (Self) Adaptive Noise Cancellation(SANC)

> Primary signal과 Reference signal을 사용하는 필터, Reference signal을 Primary signal에 내재되어 있는 특정 신호와 유사하도록 최적화 시키는 신호처리 기법

+ Primary input - 기어와 베어링에서 발생하는 신호가 혼재된 원신호
+ Reference input - 기어 신호(ANC)
+ 최적화 과정을 통해 Primary 내의 기어신호를 제거한 오차 $e$를 얻기 위한 Filter parameter $w$를 구하여 원하는 베어링 신호 선별
+ 하지만 현실에서는 적절한 Reference input을 확보하기 어려움 따라서 ANC -> SANC
+ Reference를 Primary signal의 Delay version 사용(SANC)
+ 베어링 고장신호에 비해서 높은 주기성을 보이는 기어신호 제거
+ 베어링 고장과 관련된 신호만 출력

> $$w_i^{n+1}=w_i^n\mu e(n)x(n-\delta-i)$$
> $$y(n)=W^T(n)X(n-\delta)$$
> $$e(n)=x(n)-y(n)$$

+ $w$ - Adaptive filter parameter
+ $y$ - Reference input
+ $e$ - SANC의 최종적인 출력 값
+ Matlab 함수는 없음

### Time Synchronous Averaging(TSA)

> 내재된 노이즈를 제거, 주기적인 특성을 보이는 신호만 남기기 위해 사용

+ 진동 신호를 현재 회전하고 있는 축(Shaft)의 회전 주기에 맞추어 리샘플링(Resampling)한 후 이들의 평균값을 구하는 것

> $$y(t)=\frac{1}{N}\sum_{n=0}^{N-1}x(t+nT)$$

+ 고장신호와 무관한 랜덤 노이즈 성분 제거
+ 회전에 따라 주기적 성질을 가지는 신호 성분만 남음
+ 일반적으로 축의 회전주기를 측정하기 위해 매 회전 마다 펄스신호를 발생시키는 타코미터(Tachometer)나 축의 각도를 측정하는 광학 엔코더(Optical encoder) 사용
+ TSA 기법은 주로 기어박스 고장 진단에 사용되어 좋은 효과를 보임
+ 반면, 베어링의 경우 TSA를 적용하기 전 단계인 리샘플링까지만 하고 평균은 취하지 않는 것이 효과적

~~~Matlab
tsa(x,fs,tach,'PulsesPerRotation',ppr)
~~~

+ $x$ - 원신호
+ $fs$ - 샘플링 주파수
+ $tach$ - 타코미터 신호
+ $ppr$ - 회전 당 펄스 수

> 노이즈가 심하거나 고장과 무관한 축회전과 같은 Signal이 섞여 있을 때 제거하기 위해 사용

## Signal Enhancement

> Discrete signal separation을 통해 무관한 신호를 제거한 후에도 고장신호가 여전히 미세한 경우 사용 - 고장 신호 자체를 강조

+ 진단 신뢰도 증가
+ 고장 신호를 대표하는 특성 첨도(Kurtosis)

### Minimum Entropy Deconvolution(MED)

> 원래의 Impulse 신호가 주변의 노이즈 및 다른 성분들에 의해 왜곡된 상황에서 본래의 신호에 가까운 신호로 되돌림

+ 원신호가 High kurtosis를 보이는 Impulse signal 가정
+ Transmission path의 효과를 제거하는 Inverse filter를 찾는 것
+ $e(n)$ - 고장신호
+ $h$ - 구조적 필터
+ $v(n)$ - 랜덤 노이즈
+ $x(n)$ - 측정신호
+ $x(n)$에는 고장 정보 파악을 어렵게 하는 노이즈 및 기타 신호들이 포함
+ MED필터를 의미하는 $f$를 통해 본래의 고장신호 $e(n)$과 유사한 $y(n)$으로 변환

> $$O_k(f)=\frac{\sum_{n=0}^{N-1}y^4(n)}{[\sum_{n=0}^{N-1}y^2(n)]^2}$$

+ Matlab 함수는 없음

### Spectral Kurtosis

> 기어와 베어링의 고장으로 인한 진동 신호는 일반적으로 임펄스 형태의 충격 신호를 보이며 이를 잘 나타내기 위해 Kurtosis를 사용

+ 주변 노이즈가 심하고 다른 회전 신호가 많은 경우 Raw signal 상에서 값이 잘 식별되지 않음
+ 이 값을 잘 나타내는 특정 주파수 대역을 알아내야 함 - Spectral kurtosis(SK)
+ 베어링 고장진단에서 가장 많이 이용하는 포락선 분석(Envelope analysis)도 Kurtosis가 최대가 되는 주파수 대역을 알아내여 Band pass filtering을 하면 결함신호가 훨씬 잘 보임
+ 전체가 아닌 국부적인 주파수 영역에 대해 Kurtosis를 계산
+ 시간-주파수 영역(Time-frequency domain) 신호처리 기법의 하나인 Short-Time Fourier Transform(STFT)를 사용
  
> $$SK(f)=\frac{<|H(t,f)|^4>}{<|H(t,f)|^2>^2}-2$$

+ STFT를 통해 계산된 Power spectral density를 $H(t,f)$

~~~Matlab
pkurtosis(x,fs)
kurtogram(x,fs)
~~~

+ fs - Sampling rate
+ Spectral kurtosis는 STFT의 Window size에 따라 성능 차이를 보일 수 있으므로 보다 결함 신호의 특징을 잘 반영하는 Window size를 선정하기 위해 다양한 Window size에 대해 Spectral kurtosis를 계산하고 2D 그림으로 나타냄

## Signal Decomposition

> Empirical Mode Decomposition(EMD), STFT, Wavelet 변환 등이 있고 원신호를 다양한 성분으로 분해

+ FFT를 포함한 전통적인 신호 처리 기법은 Stationary signal을 전제
+ 이러한 기법들은 기계적 고장으로 인해 Non-stationary signal의 특징을 보이는 진동신호에 적용하면 부정확한 결과가 간혹 도출
+ 시간-주파수 영역의 신호처리 기법 사용

### Empirical Mode Decomposition

> 신호의 국보적인 극대, 극소값을 연결한 Upper & Lower envelope의 평균을 이전 신호에서 제거하는 과정인 Sifting을 반복하며 신호가 다음 두 조건을 만족할 때까지 진행
>+ 극점의 수와 Zero-crossing의 수가 동일
>+ Upper, Lower envelope의 평균값이 0에 수렴

+ 가장 뛰어난 성능
+ 어떤 신호라도 IMF(Intrinsic Mode Function)라 불리는 서로 직교(Orthogonal)한 성분들의 합으로 이루어져 있다는 가정

> $$x(t)=sum_{i=1}^{l}c_i+\eta$$

+ $l$ - 분해된 IMF 신호 수
+ $\eta$ - Residual 성분
+ 결과적으로 IMF는 원신호를 고주파부터 저주파 영역으로 분해한 성분 신호
+ HS 데이터에 TSA 적용 후 EMD 적용

~~~Matlab
emd(x)
~~~

## Envelope Analysis

> 결함이 발생하면 반복 주파수가 진폭 변조가 되는데 이렇게 진폭 변조된 신호로부터 고장 주파수에 해당된느 변조파를 복조(Demodulation), 즉 변조된 신호로부터 고장 신호를 추출하기 위한 과정으로 일반적으로 포락선 분석(Envelope analysis)을 사용

+ Hilbert transform을 통해 이루어짐(위상을 -90도 지연)

> $$x_{analytic}(t)=x(t)+j \hat x(t)$$
> $$Envelope=|x_{analytic}(t)|$$

+ $x(t)$ - 원신호
+ $\hat x(t)$ - Hilbert 변환된 신호
+ Analytic signal - 원신호를 실수부, Hilbert 변환된 신호를 허수부로 하는 복소수 차원
+ 이 신호의 Magnitude가 원신호의 Envelope signal
+ 원신호의 스펙트럼 상에서는 베어링의 고장 주파수를 확인할 수 없음
+ 스펙트럼 상에서 고유 진동수로 간주되는 부분(최대 SNR)을 확보하는 부분을 대역 통과 필터(Band pass filter)에 통과시킨 신호의 Envelope 스펙트럼에서는 고장 주파수를 확인 가능
+ 하지만 베어링 고장 신호는 Shaft, Gear로부터 측정되는 진동에 비해 매우 작음
+ Matlab 함수는 없음