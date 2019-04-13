---
layout: post
title:  "Raspberry Pi 에 Ubuntu Mate와 RetroPie 설치하기"
date:   2019-04-13 01:02:59
author: Ada Lovelace
categories: RaspberryPi
tags:	Raspberry Pi, Ubuntu Mate RetroPie
cover:  "/assets/instacode.png"
---

라즈베리 파이를 이용해서 2가지 작업을 하려고 합니다. 첫번째는 간단한 리눅스 개발 작업을 하기 위해서 우분투를 설치하려고 합니다. 두번째는 레트로 파이를 설치해서 고전 게임기로 활용하고자 합니다.

## 준비물

세팅에 사용한 하드웨어는 아래와 같습니다.

- Raspberry Pi 3 Mobel B+
  - Arrow 에서 구입, 세일할때 사면 저렴함($25~$30)
- Micro SD 32GB
  - 집에서 굴러다니던 메모리 재활용
- USB Memory 32GB
- NESPi CASE+
  - 갬성을 위해서 알리에서 마련함.($20)
  - 본체, 파우치, 방열판, 쿨러로 구성
  - 전면부에 전원 버튼, 리셋, USB, 랜포트 제공
  - 후면부에 파워 아탑타 연결
- 5V 3.1A 아답타
  - 3+ 는 2.5A 를 요구하므로 안정적인 전력 공급을 위해 구입
- HDMI to DVI 컨버터
  - 갬성용 4:3 20인치 LCD 모니터 이용을 위해 집에서 굴러다니던 것 사용(구형이라 HDMI 포트 X)

대략적인 박스샷은 아래와 같네요.

![1554604589563](../../../../assets/images/1554604589563.png)



## 하드웨어 조립

제일 귀찮은 과정인 것 같습니다. NESPi 케이스로 검색하면 조립 방법이 자세히 나와있으니 참고하시면 쉽게 조립할 수 있습니다. 전 아래 사이트를 참고하였습니다.

http://bitly.kr/W4cKQ



## 설치 준비

앞서 이야기한 것처럼 하나의 메모리 카드에 멀티 부트을 통해 우분투와 레트로 파이를 설치하려고 합니다.

- BerryBoot
  - 멀티 부팅용 부트로더
  - <https://www.berryterminal.com/doku.php/berryboot>
- Ubuntu MATE 18.04
  - <https://berryboot.alexgoldcheidt.com/images/>
  - berryboot 용 Ubuntu MATE 최신 버전을 검색해서 다운로드
    - ubuntu_bionic_beaver_v18.04.2_preinstalled_server_rpi3_2019.02.09_berryboot
- RetroPie
  - <https://github.com/RetroPie/RetroPie-Setup/releases>
  - berryboot 용 RetroPie 4.4 다운로드
    - [retropie-4.4-rpi2_rpi3-berryboot.img256](https://github.com/RetroPie/RetroPie-Setup/releases/download/4.4/retropie-4.4-rpi2_rpi3-berryboot.img256)



## 설치

### BerryBoot

우선 SD 카드 리더에 메모리를 꼽고 컴퓨터에 연결하여 포맷을 합니다. 포맷이 완료되면 다운받은 BerryBoot 의 압축을 풀고 파일을 메모리 카드의 root 에 모두 복사합니다.

BerryBoot 가 복사된 메모리 카드를 라즈베리 파이에 연결하고 부팅을 합니다. 처음 부팅하면 화면, 지역, 네트워크 등의 설정 창이 뜨는데 큰 어려움 없이 설정을 할 수 있습니다.

##### Ubuntu MATE, RetroPie 설치

준비한 USB 메모리에 다운받은 Ubuntu MATE 를 압축해제하여 나온 img 파일과 RetroPie 의 img 를 복사합니다. USB 메모리의 파일 시스템은 FAT32 여야 합니다.

USB 메모리를 라즈베리 파이에 연결합니다. 그리고 Add OS 버튼을 마우스로 길게 누르고(Long Press) 있으면 USB 메모리 스틱으로부터 OS 설치하는 메뉴가 나타납니다. USB 메모리에 복사해준 Ubuntu MATE 와 RetroPie 를 차례로 설치합니다.



### 시작 및 설정

BerryBoot 를 통해서 원하는 OS 를 모두 설치한 후, Default OS 를 선택합니다. 저는 화면을 켜지 않고도 리눅스 부팅을 한 후 원격 작업을 할 수 있도록 우분투 마테를 기본 OS 로 설정하였습니다. 어차피 레트로 파이는 게임을 하려면 모니터를 켜야하니 화면을 보고 고를 수 있습니다.

#### Ubuntu MATE

먼저, 우분투 마테로 부팅을 합니다. 제가 받은 버전은 GUI 가 포함되지 않은 Server 버전이었습니다. 초기 비밀번호는 ubuntu/ubuntu 입니다. 로그인을 한 후 모든 리눅스 Package 를 업데이트 합니다.

`$ sudo apt update`

`$ sudo apt dist-upgrade`

에러 메시지가 몇개 뜨면서 완료되면, 아래 명령으로 rpi-update 를 통해서 펌웨어 업데이트를 수행하고 재시작을 합니다.

`$ sudo curl -L --output /usr/bin/rpi-update  https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update`

`$ sudo rpi-update`

`$ sudo reboot`

부팅이 완료되면, fstab 파일을 열고 아래 내용을 추가합니다.

`$ sudo vi /etc/fstab`

`tmpfs	/boot/firmware tmpfs rw 0 0`

`$ sudo mount /boot/firmware`

그 후 다시 리눅스 Package 업데이트를 수행합니다.

`$ sudo apt update && sudo apt dist-upgrade`

그러면 이전처럼 오류가 발생하지 않고 정상적으로 완료가 됩니다. 다시 재부팅을 합니다. 재부팅이 완료되면 이제 무선랜을 잡아야 합니다.

`$ sudo apt install ifupdown`

`$ sudo vi /etc/network/interfaces`

`auto wlan0`

`iface wlan0 inet hdcp`

`wpa-conf /etc/wpa-supplicant/wpa_supplicant.conf`

wpa_supplicant.conf 는 berryboot 에서 무선랜 설정을 했으면 이미 생성되어 있습니다. 만약 없으면 아래와 같이 입력합니다.

`$ sudo vi /etc/wpa_supplicant/wpa_supplicant.conf`

`country=KR`

`ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev`

`ap_scan=1`

`update_config=1`

`network=[`

​	`ssid="무선랜이름"`	

​	`psk="비밀번호"`

`]`

재부팅을 한 후에 ifconfig 로 wlan0 의 ip 가 잡혔는지 확인합니다. 잘 잡혔으면 이제 유선랜 케이블을 제거하고 네트워크가 정상 동작하는지 확인을 합니다.

$ ping google.com

PING google.com (216.58.197.142) 56(84) bytes of data.
64 bytes from nrt12s01-in-f142.1e100.net (216.58.197.142): icmp_seq=1 ttl=128 time=34.4 ms
64 bytes from nrt12s01-in-f142.1e100.net (216.58.197.142): icmp_seq=2 ttl=128 time=34.7 ms
64 bytes from nrt12s01-in-f142.1e100.net (216.58.197.142): icmp_seq=3 ttl=128 time=34.2 ms

이대로 재부팅을 하면 부팅시에 유선랜을 잡기위해서 엄청 오래 기다리게 됩니다.(wait for network to be configured) 이를 제거하기 위해서 아래 명령어로 wait for network 를 제거 합니다.

`$ systemctl stop systemd-networkd-wait-online.service`

`$ systemctl disable systemd-networkd-wait-online.service`

`$ systemctl mask systemd-networkd-wait-online.service`

재부팅을 한 후 문제가 없는지 확인을 합니다.

##### samba

`$ sudo apt install samba`

`$ sudo smbpasswd -a ubuntu`

설정에 아래와 같이 추가를 합니다.

`$ sudo vi /etc/samba/smb.conf`

`[ubuntu]`

`comment = ubuntu`

`path = /home/ubuntu`

`valid user = ubuntu`

`writable = yes`

`create mask = 0644`

`directory mask = 0755`

samba 데몬을 재시작합니다.

`$ sudo service smbd restart`

설정 완료 후 윈도우의 탐색기에서 \\\\ip주소로 접근이 잘 되는 것을 확인하였습니다.

##### ssh

ssh 서버는 기본적으로 설치가 되어 있습니다. 윈도우에서 putty 를 사용해서 원격 접속을 시도하였는데 잘 동작했습니다.



#### RetroPie

이제는 레트로 파이를 설정할 차례입니다. 라즈베리파이를 재부팅 시킨후 레트로  파이로 부팅을 합니다. 엑박 패드를 사용하기 위해서 USB 에 연결하고 부팅을 하였습니다. 조이스틱 모양의 아이콘이 나오면서 부팅이되면 패드의 키 설정을 하게 됩니다. 설정을 완료하고 재부팅을 하면 에뮬레이터를 선택하는 화면이 나타납니다.

루카스 어드벤처 게임을 돌릴 수 있는 ScummVM 도 있네요. 인터넷, 설정을 위해서 조이스틱 모양의 RetroPie 를 실행시킵니다.

저는 무선 인터넷을 설정하기 위해서 CONFIGURE WIFI 를 선택하였습니다.

헛! 그런데 이미 설정이 잘 잡혀있네요. ROM 파일을 PC에서 편하게 집어넣기 위해서 samba 를 설정합니다. F4 를 누르고 쉘로 진입합니다.

`$ sudo smbpasswd -a pi`

$ sudo service smbd restart

우분투와 RetroPie 의 IP 가 동일하기 때문에 윈도우의 samba 자격증명이 꼬여서 접속이 안되는 경우가 있습니다. 윈도우의 cmd 창을 열어서 아래 명령을 수행하면 자격증명이 모두 삭제가 됩니다.

`$ net use * /delete`

이제 즐기시면 됩니다.

