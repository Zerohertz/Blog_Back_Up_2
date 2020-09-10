---
title: EMS(Electrical Muscle Stimulation) 논문 분석(2)
date: 2018-08-27 12:34:51
categories:
- Research
- Read Paper
tags:
- VR Project
- Read Paper
thumbnail: https://user-images.githubusercontent.com/42334717/44307447-cd2a4700-a3dd-11e8-8bef-587e498aeeac.png
---
# [Providing Haptics to Walls&Heavy Objects in Virtual Reality by Means of Electrical Muscle Stimulation](https://dl.acm.org/citation.cfm?id=3025600)
***
# The repulsion(반발) object design

+ Reducing the duration of EMS signal
+ 위 결과로 나온걸 `Repulsion object`라고 한다
+ A brief(짧은) EMS pulse(of 200-300ms, 사용자의 최대 강도가 눈금됨)
+ 이를 통해 사람들의 손을 뒤로가게 만듦
+ EMS pulse of still reasonably low intensity(다른 EMS pulse들과 다르게)
+ 효과를 극대화하기 위해 시각적, 청각적 장치를 이용
<!-- more -->
***
# Validating(타당화) designs

## Interface conditions
+ 오각형의 벽을 만들어 `User`들에게 실험함
    1. `The soft wall` : Magnetic visual
    2. `The repulsion wall` : Electro visual
    3. `The soft wood wall` : Soft wall
    4. `The soft vibro wood wall` : 부드러운 나무 벽과 같지만 진동촉각 자극을 주는 `Actuator`을 손목 뒤에 착용시킴
    5. `The vibro only wall` : `Actuator`를 사용하고 `EMS feedback`을 적용하지 않았다
## Apparatus
+ `EMS`
+ `Actuator`
+ `Two pairs of electrodes(전극)` : 이두박근, 손목 신근에 부착한다
## Hypotheses(가설)
+ `Repulsion condition` : (`H1`)`Vibro only condition`보다 더 사실적으로 받아들여진다. (`H4`)Impermeable(불침투성)`을 `Vibro only condition`보다 더 고려해야 한다.
+ `Soft condition` : (`H2`)`Vibro only condition`, (`H3`)`Soft wood condition`보다 더 사실적으로 받아들여진다
## Results
+ Preference(선호도)
    1. `Repulsion condition` : 8
    2. `Soft wood condition` : 3
    3. `Vibro only condition` : 2
+ Realism/consistency
    1. `Repulsion` : 6.3
    2. `Soft` : 4.8
    3. `Soft vibro wood` : 4.1
    4. `Soft wood` : 4.0
    5. `Vibro only` : 3.5
        + `H1` Confirmed
        + `H2` Not supported
        + `H3` Not supported
+ Impermeability
    1. `Repulsion` : 6.2
    2. `Soft vibro wood` : 5.7
    3. `Soft` : 5.2
    4. `Soft wood` : 5.1
    5. `Vibro only` : 3.5
        + `H4` Confirmed
    + 또한 `Repulsion`이 평균적으로 3.6cm에 참가자들의 손을 멈췄다(최고의 기록)
        
결론 : **Repulsion이 최고였다**
