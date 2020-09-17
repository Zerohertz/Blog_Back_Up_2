---
title: CAM and CNC
date: 2020-09-02 13:19:07
categories:
- Mechanical Engineering
tags:
- Mechanical Engineering
mathjax: true
---
# Introduction

## 유연생산시스템(FMS)

> 생산성과 유연성의 양립을 목적으로 한 시스템으로서, 가공, 반송, 자재의 착탈, 제어의 기능을 유기적으로 결합한 자동화된 생산시스템

+ FMS(Flexible Manufacturing System) : 기계와 외부적인 연결
  + 다양한 순서의 자동 재료흐름
  + AGV(Automatic Guidied Vehicle), 산업용 Robot, Tooling, Pallet, Fixture
  + 공장무인화
+ FMC(Flexible Manufacturing Cell) : 독자적으로 작동
  + Machining center : 공작기계 내에서의 Pallet를 이용한 자동생산, 자동공구교환
  + 기계간 Pallet는 도움 필요
  + 40 ~ 800 부품
+ FTL(Flexible Transfer Line) : 기계와 내부적인 연결
  + 자동재료 이송시스템, NC 공작기계, 자동헤드 교환장치
  + 직접적인 재료흐름, 공작물의 순환운동
  + 1,500 ~ 15,000

|특성\종류|Transfer Line(FTL)|FMS|Standard-alone NC machines(FMC)|
|:-:|:-:|:-:|:-:|
|생산량|상|중|하|
|제품종류/유연성|하|중|상|

<!-- More -->

+ FMS 구성요소
  + A group of workstations(CNC machine tools)
    + Machining centers
    + Milling modules
    + Turning modules
    + Assembly workstations
    + Inspection stations
    + Sheet metal processing machines
    + Forging stations
  + Automated material handling and storage systems
    + AGV(Automated Guided Vehicle)
    + Tool transporter
    + Industrial robots
    + Pallet and fixture
    + Conveyor
    + Stacker crane
  + Computer control systems
    + Control of each workstation(CAM)
    + Distribution of control instructions to workstation
    + Production control
    + Traffic control
    + Work handling system monitoring
    + Tool control
    + System performance monitoring and reporting
    + Production planning and management

## CAD / CAM

+ CIM : Computer Integrated Manufacturing, 통합생산시스템
  + 공장 자동화 기술
  + Database(EDB, MDB)
  + 통신기술
  + Web based
+ FMS : Flexible Manufacturing System, 유연생산시스템
  + 공장 자동화 기술 : CAD / CAM, CNC machining
+ CAD / CAM : Computer Aided Design and Computer Aided Manufacturing
  + CAD : Computer를 이용한 부품의 모델링
    + Wire frame : 제도용
    + Surface model : 금형가공용
    + Solid model : 해석용
  + CAM : 기계가공을 위한 모델링과 CNC machine을 작동시키기 위한 NC code 생성
    + Input : CAD
    + Output : NC code
  + NC code
    + NC 가공을 위한 표준화된 수치데이터 형식
    + Machining center의 Controller 명령문
  + Part program : 가공을 위한 일련의 NC code
+ CAD / CAM의 데이터 교환 : IGES, DXF, STEP
+ CAPP : Computer Aided Process Plan

***

# 절삭 가공

+ 절삭 가공이란?
  + 상대적으로 경도가 높은 날끝공구(Cutting Tool)를 사용하여 피가공물(Workpiece)의 불필요한 부분을 칩(Chip)의 형태로 제거하여 원하는 형태로 만드는 작업
+ 절삭 가공의 특징
  + 정밀 가공 가능
  + 가공에 따른 소재 내부의 물성 변화 적음
  + 다양한 형상가공(Flexible Process)
  + 칩의 발생에 따른 재료 손실
+ 절삭 가공을 수행하기 위한 3요소
  + 공작기계
  + 공구
  + 공작물

## 공작기계

+ 공작기계란?
  + 기계를 만드는 기계
  + 일반적으로는 절삭, 연삭 등과 같이 재료를 가공하여 원하는 형상으로 만들어 내는 기계
+ 공작기계의 분류
  + 비절삭 공작기계 : 주조, 소성가공, 용접 등과 같이 Chip을 발생하지 않고 가공
  + 절삭 공작기계 : 선삭, 밀링, 연삭 등 Chip을 발생시키면서 가공
  + 좁은 의미의 공작기계 : 절삭 공작기계를 의미

### 공작기계의 분류

+ 금속공작기계(Metal Cutting Machining Tool)
  + 범용 공작기계
    + 절삭공구 사용 기계
      + 고정공구 사용 기계
        + 선삭(Lathe)
        + 형삭(Shaper)
        + 평삭(Planer)
      + 회전공구 사용 기계
        + 밀링(Milling M/C)
        + 드릴링(Drilling M/C)
        + 보링(Boring M/C)
        + 쏘잉(Sawing M/C)
    + 연삭공구 사용 기계
      + 연삭(Grinding M/C)
      + 호닝(Honing M/C)
  + 전용 공작기계
    + 전용기(Special Purpose M/C)
  + NC 공작기계
    + NC Lathe
    + NC Drilling M/C
    + NC Milling M/C
    + NC Boring M/C
    + NC Grinding M/C
    + Machining Center
+ 금속가공기계(Metal Forming Machine Tool)
  + Press
  + Rolling M/C
  + Shearing M/C
  + Bending M/C

### NC 공작기계에 의한 가공의 특성

+ 높은 공작 정밀도(Accuracy)
  + 주축 회전정밀도
  + 안내면 직선 정밀도
  + 온도변화에 대한 변형
  + 진동
  + Etc.
+ 우수한 가공능률(Efficiency)
  + 절삭효율
    + 유효 절삭시간
    + 준비시간
    + 유휴시간
+ 융통성(Flexibility)
  + 프로그램에 의한 가공의 자동화
    + NC code
    + Controller
+ 안전성(Safety)
  + 작업자에 대한 안정성
  + 기계 자체의 안정성

### 공작기계의 운동

+ 공작기계의 가공 원칙
  + 절삭공구와 공작물간에 적절한 상대운동을 통하여 요구되는 형상 생성
+ 절삭운동과 이송운동 : 공작기계로부터 공급되는 상대운동
  + 절삭운동(Cutting motion, 주운동)
    + 기계가공 수행을 위한 총동력의 대부분을 사용
    + Chip의 길이 방향으로 공구가 움직이는 운동
  + 이송운동(Feed motion)
    + 가공물을 절삭 방향으로 피이드 하는 운동
    + 기계가공 수행을 위해 필요한 총동력의 소량을 사용

### 좌표계의 정의

+ Z축 운동
  + 주운동을 제공하는 기계의 주축에 평행하게 정렬
  + 주축이 없는 기계 : 공작물 지탱면에 수직으로 정렬
  + +Z 운동 : 공작물과 공구대 사이의 거리를 증가시키는 방향
+ X축 운동
  + 공작물 지탱면에 수평하고 평행
  + 주축이 없는 기계 : 주절삭 방향에 평행하고 주운동 방향이 플러스 방향
  + 공작물이 회전하는 기계 : 횡이송대에 방사형이고 평행
  + +X 운동 : 공구가 공작물의 회전축으로부터 멀어졌을 때의 공구 운동으로 정의
+ Y축 운동
  + 좌표계를 완성하는 방향

## 선삭

### 선반의 구성

+ 주축에 고정한 공작물을 회전, 공구대에 설치된 공구에 절삭깊이와 이송을 주어 공작물을 절삭
+ 베드 : 다른 구성요소들의 지지 역할
+ 왕복대(Carriage) : 베드의 안내면(Slide way)을 따라 이동
+ 주축대(Headstock) : 베드에 고정
+ 정밀도에 중요한 요소
  + 주축 흔들림(주축 베어링)
  + 이송운동의 정밀도(베드, Linear guide 정밀도)

![Lathe](https://user-images.githubusercontent.com/42334717/93463236-724bdc80-f922-11ea-81c7-c1d8f6af10af.jpg)