---
title: "Linux : Apache WEB 01"
layout: post
date: 2021-05-12 16:00
image: false
headerImage: false
tag: [linux]
category: blog
author: nidoos
description: "Linux study"
---

>윈도우에서 아파치.zip 다운받아 ftp를 이용하여 리눅스에 전송하기

<br>
1. 리눅스에 vsftpd 패키지 설치 <br>
2. 방화벽 설정 <br>
3. virtual box 네트워크 설정

---

### vsftpd 패키지 설치
- vsftpd의 설치유무 확인<br>
    `# ps -ax | grep vsftpd` <br>
- vsftpd 설치<br>
   `# yum -y install vsftpd`

<br>

### 방화벽 설정

```
# firewall-cmd --permanent --add-service=ftp

# firewall-cmd --permanent --add-port=21/tcp

# firewall-cmd --reload

```

- `vi /etc/selinux/config`
  - `SELINUX = enforcing` -> `SELINUX = disabled` 로 변경

<br>

### 재시작

```
# systemctl restart vsftpd
# systemctl enable vsftpd  (재부팅시에도 자동실행 활성화)
ps -ax | grep vsftpd (vsftpd 실행 확인)
```

<br>

### NAT네트워크 설정하여 포트포워딩

- 윈도우에서 리눅스의 FTP, SSH를 사용하고 싶다면 포트포워딩을 해야한다. <br>
  1) virtual box 파일-> 환경설정 -> 네트워크 -> NAT 네트워크 편집 -> 포트포워딩 <br>
  2) 해당 os 설정 -> 네트워크 -> NAT 네트워크

![port](https://user-images.githubusercontent.com/71308719/118240210-b012fc00-b4d5-11eb-823f-27cadf55c9d0.JPG)

*이게 맞는 설정인지는 모르겠음*

<br>

### 고정ip 설정

- 가상머신이 2개 이상 작동된다면 같은 ip를 사용하게 되므로 문제가 발생한다.
  
  1) `cd /etc/sysconfig/network-scripts`
   
  2) `vi ifcfg-enp0s3`
  
  3) 다음과 같이 수정
   
   ![ip](https://user-images.githubusercontent.com/71308719/118241860-9a063b00-b4d7-11eb-9a1c-bc18244733fd.JPG)

  4) putty로 ssh 확인 (error발생)
   
   ![puttyError](https://user-images.githubusercontent.com/71308719/118242411-4516f480-b4d8-11eb-8b4b-c36a75e6ecda.jpg)

   - `vi /etc/ssh/sshd_config`
   - UseDNS no 로 변경 (주석풀기 필수)
   - 포트넘버 22 주석풀기
   - systemctl restart sshd
  
  5) 윈도우 cmd에서 ftp 확인
   
    ![ftp](https://user-images.githubusercontent.com/71308719/118243893-ec485b80-b4d9-11eb-8705-3fd7e46cc17d.JPG)

