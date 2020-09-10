---
title: hexo-tag-gdemo
date: 2020-07-28 22:01:03
categories:
- Etc.
tags:
- Git
---
# 멋진 Plug in

{% gdemo_terminal 'npm install @heowc/hexo-tag-gdemo' '80px' 'bash' '500' '$' 'demo-teriminal1' %}
install
{% endgdemo_terminal %}

<!-- More -->

***

# 사용법

~~~
{% gdemo_terminal 'command1;command2;...' 'minHeight' 'windowTitle' 'onCompleteDelay' 'promptString' 'id' 'highlightingLang' %}
content
{% endgdemo_terminal %}
~~~

***

# Example

{% gdemo_terminal '2017.03 ~ : Konkuk Univ. Mechanical Engineering;2018.06 ~ 2019.11 : Former undergraduate researcher at MRV Lab.(Medical Robotics and Virtual Reality Laboratory);2019.11 ~ : Undergraduate researcher at SiM Lab.(Smart intelligent Manufacturing system Laboratory)' '150px' 'Career' '300' '$' 'career' 'vim' %}
{% endgdemo_terminal %}

~~~
{% gdemo_terminal '2017.03 ~ : Konkuk Univ. Mechanical Engineering;2018.06 ~ 2019.11 : Former undergraduate researcher at MRV Lab.(Medical Robotics and Virtual Reality Laboratory);2019.11 ~ : Undergraduate researcher at SiM Lab.(Smart intelligent Manufacturing system Laboratory)' '150px' 'Career' '300' '$' 'career' 'vim' %}
{% endgdemo_terminal %}
~~~

[Reference](https://heowc.dev/2018/11/14/introduction-hexo-tag-gdemo/)