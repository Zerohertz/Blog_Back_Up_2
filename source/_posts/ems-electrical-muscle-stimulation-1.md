---
title: EMS(Electrical Muscle Stimulation) 논문 분석(1)
date: 2018-08-19 18:10:32
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
# How to add `haptics` to walls and other heavy objects in virtual reality

+ `EMS` create `a counter force` that pulls the user's arm backwards.(`전기자극`을 통해 `반력`을 느끼게 한다.)
+ 하지만 무거운 물체의 `haptic`은 adding `haptic`에 많은 도전이 필요하다.
<!-- more -->
***
# 만족해야하는 4가지 Criteria(기준)

+ `Belivable` : 사용자가 믿을 수 있는가?
+ `Impermeable` : VR object에 침투 되지 않는가?
+ `Consistent` : Visual과 haptic이 잘 맞는가?
+ `Familiar` : 현실과 같은 친숙한 feedback인가?
***
# The hard object design does not work

+ 체험자의 손이 벽에 prevent 성공(근본적으로 비례하는 전류)
+ 성공적인 실험처럼 보였음
+ 하지만 체험자가 느끼기에 자석에 의해 밀리는 것과 같다고 언급
+ `Belivable`에서 실패한 모델
+ 대책으로 `weaker signal`과 `short signal`이 기반인 두 모델을 만듦
***
# The soft object design

+ Cut-off to `EMS` intensity(강도)
+ About 10cm의 penetrate(관통)을 허용
+ Permeable surface(투과성)
+ Magnetic field(참가자의 손등에 metal을 붙이기도 함)