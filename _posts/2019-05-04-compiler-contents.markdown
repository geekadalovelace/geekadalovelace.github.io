---
layout: post
title:  "컴파일러 소개"
date:   2019-05-04 16:28:00
author: Ada Lovelace
categories: Compiler
tags:	Compiler 컴파일러
cover:  "/assets/instacode.png"

---


컴파일러 이론 관련 글들을 적어볼까 합니다. 프로그래머들은 누구나 매일매일 컴파일러를 사용하지만, 정작 컴파일러가 어떻게 구성되어 있고 어떠한 원리로 프로그램을 컴파일하는지에 대한 이론적인 내용에 대해서 관심을 갖는 사람은 잘 없습니다.

전문가들은 컴파일러의 동작 원리를 알게됨으로서 보다 더 *효율적인 코드*를 작성할 수 있기 때문에 컴파일러를 학습해야 한다고 합니다. 그러나 그것보다 더 중요한 것은 바로 컴파일러가 온갖 컴퓨터 과학적 기술이 집약된 가장 오래된 소프트웨어중 하나라는 것입니다. 컴파일러를 만들기 위해서 오래동안 연구된 다양한 이론들은 매우 많은 프로그램에 적용되어 있습니다. 예를들어 프로그램의 취약점을 분석해주는 정적분석은 컴파일러의 연구 분야입니다. 또한, JVM 과 같은 가상기계도 컴파일러의 이론 속에서 나왔습니다. 그리고 정규 표현식도 있습니다. 따라서 컴파일러의 원리에 대해서 공부를 하면, 컴퓨터 과학 분야의 많은 고급 이론들을 배움으로써 프로그램을 작성할 때 활용할 수 있는 여러가지 고급 기법들을 쉽게 이해하고 배울 수 있습니다. 물론 프로그래밍 언어도 더 깊게 이해할 수 있습니다.



## 그래서 컴파일러가 뭐야?

한국인과 미국인이 있습니다. 한국인은 영어를 이해하지 못하고 ~~교육과정으로만 10년을 배워도 영어를 못하다니...~~ 미국인은 한국어를 이해할 수 없습니다. 둘 사이에 의사 소통을 하기 위해서는 통역이 있어야 합니다. 글로 의사 소통을 한다면 번역기가 필요합니다. 번역기는 어떤 언어로 된 글을 다른 언어의 글로 옮기는 일을 합니다. 아래에서 사용한 것은 한영 번역기입니다.

![1556950572834](../../../../assets/images/1556950572834.png)

프로그래머는 내가 원하는 ~~사실은 갑님~~ 일을 컴퓨터에게 시키기 위해서 컴퓨터와 의사 소통이 필요합니다. 이를 위해 프로그래머가 이해할 수 있는 언어를 컴퓨터가 이해할 수 있는 언어로 번역해주는 번역기가 필요합니다. 컴파일러는 바로 이러한 번역을 해주는 프로그램입니다. 컴파일러란 사람이 이해할 수 있는 고급 언어를 컴퓨터가 이해하기 쉬운 언어(기계어)로 번역하여 목적 프로그램을 출력하는 프로그램입니다. 컴파일러의 바이블인 공룡책에서는 컴파일러를 다음과 같이 정의하고 있습니다.

> 'A compiler is program that can read a program in one language and translate it into an equivalent program in another language'
>

아주 깔끔하고 명확하게 정의가 되어있습니다.



## 컴파일러의 구조

정의에서 보신것처럼 컴파일러가 하는 일은 아주 명확합니다. 프로그래머가 작성한 프로그램을 읽어서 기계가 이해하기 쉬운 형태로 번역된 프로그램을 생성하면 됩니다.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=286&x=41&y=149&w=1278&h=222&store=1&accept=image%2F*&auth=LCA%2044f6e67d9bd2213588ec31275a7197d015de6a32-ts%3D1556951379)

우리는 컴파일을 하면 보통은 수많은 문법 에러들을 만나게 됩니다. 이 이야기는 컴파일러가 우리가 작성한 코드의 문법이 올바른지 검사를 한다는 의미입니다. 예를들어 C 언어로 작성된 프로그램을 읽어 컴파일러는 C 문법에 맞게 잘 작성하였는지 문법을 검사합니다. 문법이 올바르면 Intel CPU 가 알아먹을 수 있도록 기계가 이해하기 쉬운(어셈블리 언어와 같은) 언어로 프로그램을 번역하여 출력 파일을 생성합니다.

그럼 위와 같은 단순한 구조는 문제가 한가지 있습니다. 무엇이 문제일까요 ?

예를들어 제가 Intel CPU/리눅스 에서 돌아갈 프로그램을 컴파일하기 위해서 C 컴파일러를 하나 만들었습니다.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=308&x=41&y=369&w=1278&h=222&store=1&accept=image%2F*&auth=LCA%206c2dc61b330a865156157bcca3978e6de94b921d-ts%3D1556951379)

그런데 제가 컴파일러를 너무 잘만들어서 ARM 에서도 제가 만든 컴파일러를 쓰고 싶다고 합니다. 위에서 만든 컴파일러는 Target Program 을 Intel 에 맞게 생성했으므로 ARM 에서는 돌아가지 않을 것입니다. 그래서 저는 다시 컴파일러를 개발합니다.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=345&x=41&y=609&w=1278&h=222&store=1&accept=image%2F*&auth=LCA%20733c1e2cbd95b93aedc07051fa414fd51c40757e-ts%3D1556951379)

힘겹게 만들었더니 이번엔 C++ 용 컴파일러를 만들어 달라고 합니다. 2개를 더 만들어야하네요.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=365&x=41&y=837&w=1278&h=486&store=1&accept=image%2F*&auth=LCA%20c8945f425c14e4cca6d9600a54c8c59f79be0b8d-ts%3D1556951379)

보시는 것처럼 2개의 언어가 있고 2개의 기계가 있으면 4개의 컴파일러를 제작해야 합니다. 결과적으로 N 개의 언어가 있고 M 개의 기계가 있으면, 우리는 N * M 개의 컴파일러를 제작해야 합니다. 컴파일러를 만드는 것은 매우 어렵고 비용이 많이 드는 일입니다. 그래서 훌륭하신 분들이 언어 의존적인 부분과 기계 의존적인 부분을 분리하였습니다. 언어 의존적인 부분은 기계와는 독립적인 부분이고 마찬가지로 기계 의존적인 부분은 언어와 독립적입니다.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=680&x=41&y=1149&w=1278&h=222&store=1&accept=image%2F*&auth=LCA%2040e06b41a8de1eb3a9408b2b6d59d97bf60080c3-ts%3D1556951379)

보통 언어 의존적인 부분을 Front-end, 기계 의존적인 부분을 Back-end 로 나타냅니다. Front-end 에서 소스 프로그램을 읽어 언어와 관련있는 문법 체크등의 작업을 수행하고 그 결과를 Back-end 에서 받아 기계 의존적인 작업을 처리하여 프로그램을 생성하게 됩니다. 이러한 구조를 사용하면 N 개의 언어에 대해서 N 개의 Front-end 가 필요하고 M 개의 기계에 대응하기 위해서 M 개의 Back-end 가 필요하므로, N + M 개의 컴파일러 제작 비용이 발생하게 됩니다. 예를들어 C 언어용 Front-end 와 Intel 용 Back-end 조합으로 Intel 용 C 컴파일러를 만들 수 있습니다.

 ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=895&x=398&y=1789&w=904&h=662&store=1&accept=image%2F*&auth=LCA%201dd864bf8c919253427250f434b1a5eaba401813-ts%3D1556951379)

우리는 앞으로 Front-end 와 Back-end 에서 하는 작업에 대해서 더 자세히 살펴볼 것입니다. 대략적으로 언급하면 각각 아래와 같은 일들을 수행합니다.

### Front-end

전단부에서는 프로그램을 읽어 의미있는 최소단위(토큰)로 분리하고 분리된 토큰을 이용하여 구문 구조를 분석합니다. 분석된 구문 구조를 이용하여 중간 코드를 생성합니다. ![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=1080&x=6&y=2449&w=1168&h=222&store=1&accept=image%2F*&auth=LCA%20f4586e186849bb813b6e44976fd48139d550958c-ts%3D1556951379)

### Back-end

 후단부에서는 전단부에서 생성된 중간 코드를 읽어 최적화를 수행하고 기계가 이해할 수 있는 언어로 코드를 생성합니다. 중간 코드는 분리된 2개의 모듈인 전단부와 후단부를 연결해주는 역할을 합니다.![img](https://documents.lucidchart.com/documents/fba024f5-1aff-43c4-9980-2d9ace6a0b38/pages/YGcM5DNywbTK?a=1079&x=34&y=2689&w=552&h=222&store=1&accept=image%2F*&auth=LCA%20d6174ad3d459a01f6d22301da96906713bcae179-ts%3D1556951379)

대략적인 설명은 여기까지입니다. 컴파일러의 이론적인 내용이 너무 난해하여 전공수업이 있어도 골파일러라 부르며 학생들이 잘 듣지 않는 것 같습니다. 각종 공식과 Notation 들을 보고 있으면 머리가 아픈 것도 사실이죠. 앞으로 조금씩이라도 이해하기 쉽게 컴파일러 관련 내용 적어볼까합니다.



## 책 소개

#### Compilers: Principles, Techniques, & Tools

더이상 설명이 필요없는 컴파일러의 바이블입니다. 표지에 용이 있어서 드래곤 북이라고도 부릅니다. 컴퓨터 공학을 전공했다면 한권쯤 장식용으로 있는 것도 좋습니다. 번역서도 있습니다.

<http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788945076069&orderClick=LAH&Kc=>

#### 컴파일러 입문

국내에서 쓰여진 책입니다. 예제와 함께 코드까지 있어서 Mini C 컴파일러라는 것을 만들어 볼 수 있습니다. 전단부의 내용을 자세히 잘 설명하고 있습니다. 다만, 후단부의 내용이 빈약한 점이 아쉽습니다. 그래도 전단부만 잘 알아도 굉장히 유용하기는 합니다.

<http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788935304677&orderClick=LAG&Kc=>

