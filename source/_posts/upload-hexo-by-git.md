---
title: Upload Hexo by git
date: 2018-08-19 20:03:41
categories:
- Etc.
tags:
- Git
thumbnail: https://user-images.githubusercontent.com/42334717/44308335-990b5200-a3ee-11e8-9b51-604da7f71bb9.png
---
## 첫 업로드
~~~
$ git init
$ git remote add origin https://github.com/Zerohertz/Hexo_Blog.git    (github의 주소)
$ git add .
$ git remote -v   (확인)
$ git commit -m "내용"  (주석)
$ git push origin master
~~~
***
## 수정, 추가 업로드
```
$ git add .
$ git commit -m "내용"
$ git push origin master
```