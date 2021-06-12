---
title: "Linux : Apache WEB 02"
layout: post
date: 2021-05-20 16:00
image: false
headerImage: false
tag: [linux]
category: blog
author: nidoos
description: "Linux study"
---

### ftp사용하여 업로드

![ftp](https://user-images.githubusercontent.com/71308719/118918967-9870c300-b96e-11eb-8143-bbfe5db6e117.JPG)

  - ftp로 올릴자료의 위치 / 내려받을 위치로 이동
  - `put 파일명`

<br>

### 파일 설치

- 압축풀기 : `gzip -d 파일명.tar.gz`
- 설치 : `tar xvf 파일명.tar`

<br>

### 소스트리 구성

- apache2.4.x 버전부터 apr과 apr-util을 별도로 설치해야한다.
  - `yum install apr apr-devel apr-util` 또는 http://apr.apache.org/download.cgi 에 접속하여 apr과 apr-util 모두 1.4 이상의 버전 다운받아야함.

<br>

#### apr

- apr-1.7.0.tar.gz 다운

```
tar xvfz apr-1.7.0.tar.gz
cd apr-1.7.0
./configure --prefix=/usr/local/apr
```
