---
layout: post
title:  "GitHub 블로그 만들기"
date:   2019-04-06 23:13:59
author: Ada Lovelace
categories: Etc
tags:	GitHub Pages Blog
cover:  "/assets/instacode.png"
---

GitHub 블로그를 생성하면서 삽질한 내용을 간략하게 정리합니다.



## GitHub 계정 준비

우선 GitHub 의 계정을 생성하고 로그인을 한 후, 새로운 Repository 를 생성합니다.

이때, Repository name 은 username.github.io 로 생성합니다.

![1554560581298](../../../../assets/images/1554560581298.png)

저는 이미 생성해서 이미 존재한다는 경고 메시지가 뜨네요.

생성할때 private 로 repository 를 생성하면 안되는 것 같습니다. 당연한 이야기인가? -_-

생성한 저장소의 Settings 으로 가보시면 이름이 잘(?) 설정된 것을 확인할 수 있습니다.

![1554560767664](../../../../assets/images/1554560767664.png)

스크롤을 조금 내려보면 published 가 되었다고 메시지가 나타납니다.

![1554560845508](../../../../assets/images/1554560845508.png)



## Jekyll Theme

적당히 마음에 드는 테마를 하나 고릅니다.

<http://jekyllthemes.org/>

가장 인기있는 테마는 minimal-mistakes 인 것 같습니다.

<https://github.com/mmistakes/minimal-mistakes>

저는 centrarium 테마를 사용하였기에 이 테마를 기준으로 설명하도록 하겠습니다.

<http://bencentra.com/centrarium>

해당 테마의 [GitHub](https://github.com/bencentra/centrarium) 로 이동을 하여 소스 코드를 다운로드 받고 압축을 푼 후, 아까 생성하였던 자신의 저장소에 push 를 합니다. 혹은 Fork 를 한 후, 저장소 이름을 변경해도 됩니다.



## Theme 수정하기

### 로컬 환경 설정

자신의  GitHub 블로그 주소를 들어가면 화면이 샘플과 차이가 나는 것을 확인할 수 있습니다. 일부 내용의 설정이 잘못되어 발생하는 현상입니다. 이를 편하게 바로 잡고 수정 위해서는 로컬 환경에서도 확인을 할 수 있어야합니다. 이를 위해서  jekyll 관련 도구를 설치합니다.

저는 우분투 18.04 LTS 환경에서 작업하였습니다.

설치하기 전에 패키지를 모두 최신으로 업데이트하는 것을 추천합니다.

$ sudo apt update

$ sudo apt install gem ruby-dev make gcc g++

$ sudo gem update --system

$ sudo gem install jekyll

$ sudo gem install bundle

$ sudo gem install eventmachine

설치를 완료한 후, gemfile.lock 갱신을 위해서

$ bundle install

그 후,  로컬 서버 띄우기

$ jekyll serve

이제 웹브라우저에서 http://127.0.0.1:4000/ 로 접속할 수 있습니다.



### 설정 변경하기

_config.yml 파일을 열어서 수정합니다.

title, subtitle, desc와 이미지, 경로 설정 등을 본인의 환경에 맞게 수정합니다. 전체적인 경로가 안맞는 것은 baseurl 을 수정하시면 됩니다.



### 포스트 작성하기

포스트 파일은 _posts 디렉토리에 위치해야 하며 아래와 같은 형식으로 파일명을 작성해야 합니다.

예시: 2015-05-18-dummy.markdown

markdown 을 편하게 작성하기 위해 자신에게 맞는 에디터를 하나 다운로드 받습니다. 저는 [typora](https://typora.io/) 라는 에디터를 다운로드 받았는데, 좋은지 나쁜지 잘 모르겠네요.

암튼 기존에 있었던 posts 샘플을 참고로 하여 작성합니다. 다 작성을 하였으면, 로컬 서버를 가동한 후 확인을 합니다. 문제가 없다면, git 저장소에 수정한 파일들을 push 하고 조금 있으면 적용이 될 것을 확인할 수 있습니다.

안나올 경우 date: 값에 문제가 있는 경우가 있습니다. date 값이 현재보다 미래인 경우에는 그 글은 표시되지 않습니다. 로컬 환경에서 테스트할 경우 --future 옵션을 주면 날짜와 상관없이 표시됩니다.