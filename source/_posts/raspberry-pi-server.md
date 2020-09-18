---
title: 라즈베리파이로 간단한 서버 만들기
date: 2020-09-18 20:29:40
categories:
- RaspberryPi
tags:
- RaspberryPi
---
# RASPBERRY PI OS 설치

[RASPBERRY PI OS](https://www.raspberrypi.org/downloads/)

> 위 사이트에서 프로그램을 받은 뒤, SD카드 연결 후 아래와 같이 WRITE하면 설치가 된다.

![Raspbian](https://user-images.githubusercontent.com/42334717/93593200-a096ee00-f9ee-11ea-9ea0-e0eb7fb979b4.png)

<!-- More -->

***

# ssh 연결 허용

> RASPBERRY PI OS는 기본적으로 ssh가 disable이므로 설정을 바꿔줘야 한다. SD카드의 최상위 디렉토리에 확장자가 없는 ssh라는 파일을 생성하면 ssh가 enable이 된다.

![ssh](https://user-images.githubusercontent.com/42334717/93593734-975a5100-f9ef-11ea-98c6-06172342eaad.png)

> 만약 WiFi를 통하여 라즈베리 파이를 이용할 예정이라면, 아래의 이름과 소스를 작성하여 최상위 디렉토리에 저장해야한다.

~~~cpp wpa_supplicant.conf
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="WiFi 이름"
    psk="WiFi 비밀번호"
}
~~~

***

# 라즈베리 파이의 IP

> 라즈베리 파이에 연결된 공유기의 Gateway 주소로 접속 후, 라즈베리 파이의 IP를 알아낸다. Gateway는 아래의 코드를 입력하여 알 수 있다.

{% gdemo_terminal 'route get default' '30px' 'zerohertz@zerohertz: ~' '300' 'zerohertz@zerohertz\ ~\ ' 'zerohertz1' 'applescript' %}
{% endgdemo_terminal %}

<br/>
<br/>

![IP](https://user-images.githubusercontent.com/42334717/93594589-2025bc80-f9f1-11ea-869b-eecafaf3e4d8.png)

***

# ssh 접속

> 위의 IP를 이용해 ssh로 접속할 수 있다.

![ssh](https://user-images.githubusercontent.com/42334717/93594705-4f3c2e00-f9f1-11ea-915d-cf68fa265a84.png)

![ssh](https://user-images.githubusercontent.com/42334717/93594775-75fa6480-f9f1-11ea-9b75-73e182a4ef75.png)

***

# 고정 IP 할당

> WiFi 내에서 라즈베리 파이가 항상 같은 IP(192.168.123.123)를 갖도록 설정하였다.

![IP_Config](https://user-images.githubusercontent.com/42334717/93595293-71827b80-f9f2-11ea-9afd-218e8805b629.png)

![IP_Config](https://user-images.githubusercontent.com/42334717/93595386-a098ed00-f9f2-11ea-9600-c2e1231ae1a0.png)

> 이후 공유기 자체의 IP를 고정 IP로 설정을 바꿔준다. 또한 포트포워딩을 통해 내부 포트는 22로 외부 포트는 자유로 설정하고 IP는 위에서 라즈베리 파이에 할당한 IP를 기입한다.

{% gdemo_terminal 'ssh pi@xxx.xxx.xxx.xxx(고정IP) -p(외부 포트)' '30px' 'zerohertz@zerohertz: ~' '300' 'zerohertz@zerohertz\ ~\ ' 'zerohertz2' 'applescript' %}
{% endgdemo_terminal %}