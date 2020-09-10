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