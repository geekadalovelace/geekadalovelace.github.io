---
layout: post
title:  "인공지능 관련 유용한 콘텐츠 정리(rev.2019.05.05)"
date:   2019-05-05 15:21:00
author: Ada Lovelace
categories: ai
tags:	AI 인공지능 머신러닝
cover:  "/assets/instacode.png"
---

그동안 모아놓았던 인공지능과 머신러닝 관련된 강좌, 이야기, 재미있는 글들을 정리합니다. SNS 나 웹에서 재미있는게 보이면 일단 저장만 눌러놓고 나중에 정리하려고 했던 콘텐츠가 많이 쌓였네요. 계속 정리해야지 하면서도 게을러서 마음 먹기가 쉽지 않았습니다. 정리한 내용에는 제가 본것도 있고 아직 보지는 않고 저장만 해 놓은 것들도 많습니다. 필요하신 분들은 참고 바랍니다. 한번에 다 정리하려고 했는데 Keep 에 메모해 놓은 것만 정리하는데도 시간이 너무 많이 걸려서 우선 1차적으로 정리하고 차후 리비전을 하도록 하겠습니다.(rev.2019.05.05)

# 목차

[동영상 강좌](#동영상-강좌)

[머신러닝, 딥러닝, 인공지능](#머신러닝-딥러닝-인공지능)

[Tensorflow](#tensorflow)

[Keras](#keras)

[NLP](#nlp)

[Embedding](#embedding)

[현업 응용](#현업-응용)

[주요 논문과 구현](#주요-논문과-구현)

[Books](#book)

[볼만한 것들](#볼만한-것들)

[기타 정리 사이트](#기타-정리-사이트)

[컴파일러, 최적화, 백엔드 포팅](#컴파일러-최적화-백엔드-포팅)



# 동영상 강좌

### 머신러닝, 딥러닝, 인공지능

[모두를 위한 딥러닝 시즌 1](https://hunkim.github.io/ml/){:target="_blank"}

- 김성훈 교수님의 한국어 강의, 아주아주 이해하기 쉽게 설명해주셔서 아무것도 모르는 초보 입문 용으로 매우 좋음, 딥러닝의 기본을 들으면 기초적인 감을 잡을 수 있다.

[모두를 위한 딥러닝 시즌 2](https://deeplearningzerotoall.github.io/season2/){:target="_blank"}

- 위 강의에 최신 내용을 추가하여 새로 만든 강의

[Andrew Ng 의 Machine Learning 기초 강좌(무료)](https://www.coursera.org/learn/machine-learning){:target="_blank"}

- 인공지능 분야의 석학인 앤드류 응 교수님의 코세라 강의
- 이론적인 내용을 쉽게 설명
- 모두를 위한 딥러닝에서도 많이 참고하고 있는 강좌이고 이론적으로 더 자세한 설명을 하기 때문에 부족했던 부분을 잘 이해할 수 있었다.
- 최근 많이 사용하는 파이썬, Tensorflow 가 아니라 구현에 Octave 를 사용하는게 좀 아쉽다.

[인공지능, 충북대학교 이건명 교수님](http://www.kocw.net/home/search/kemView.do?kemId=1170523&fbclid=IwAR3NnlWQ-kaA08nT9KwQmyOJ7ayxDABQYHIQeYsarJ7ReVrFaiVmwN-M36U){:target="_blank"}



#### KOOC 문일철 교수님 강좌들

- 좀 어렵기 때문에 위 강좌들로 이론적인 배경이 생긴후 들으면 좋다고 함

[인공지능 및 기계학습 개론 1](https://kaist.edwith.org/machinelearning1_17){:target="_blank"}

[인공지능 및 기계학습 개론 2](https://kaist.edwith.org/machinelearning2__17){:target="_blank"}

[인공지능 및 기계학습 심화](https://kaist.edwith.org/aiml-adv){:target="_blank"}



### 학률, 통계, 선형대수

[Essence of linear algebra](https://www.youtube.com/watch?v=kjBOesZCoqc&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab){:target="_blank"}

[2013 2학기 선형대수[이상화 교수님]](https://www.youtube.com/playlist?list=PLSN_PltQeOyjDGSghAf92VhdMBeaLZWR3&fbclid=IwAR0JvowP5nwZ7l-iqp6w5Azs-lLQKccJHJ2jLZs_GnTH8qhunOjvS205b68){:target="_blank"}

[확률 및 통계 한양대학교 이상화 교수님](http://www.kocw.net/home/search/kemView.do?kemId=1056974&fbclid=IwAR0dsW05ZL7ary7RJ-A9YUppVjk-x_8rgn6pt3-o23CkFe0gatcH3PkAFRE){:target="_blank"}

[PYTHON 확률과 통계 기초 이해(동영상 아님)](https://www.slideshare.net/dahlmoon/lambda-20160315?from_m_app=ios&fbclid=IwAR0WOLr9arLHe-lT9VCdg7kqCP1sf9i3IumYZo4bhoHU0Bpv1Kt__fQyQHs){:target="_blank"}



# 머신러닝, 딥러닝, 인공지능

[자습해도 모르겠던 딥러닝, 머리속에 인스톨 시켜드립니다.](https://www.slideshare.net/yongho/ss-79607172){:target="_blank"}

[수학 포기자를 위한 딥러닝과 텐서플로우 이해](https://docs.google.com/document/d/1eX7RM6_AOAeVIxI_Yz0iutcZG_0L5b-3pWlSe6Af0t8/mobilebasic#heading=h.2ulyjv47ei1w){:target="_blank"}

[계산 그래프로 역전파 이해하기](https://brunch.co.kr/@chris-song/22){:target="_blank"}

[ResNet, AlexNet, VGGNet, Inception: Understanding various architectures of Convolutional Networks](https://cv-tricks.com/cnn/understand-resnet-alexnet-vgg-inception/?fbclid=IwAR1uJcFCjhKrx0NT_xEx7UWENuXZJOe2XVYhMk3uCndMsv3waTLgYPRSBhA){:target="_blank"}

[PRML(Pattern Recognition & Machien Learning, Bishop)을 정리한 문서](http://norman3.github.io/prml/){:target="_blank"}

- 머신러닝의 바이블로 취급되는 책을 무려 한글로 요약 정리하고 있는 문서

[SNU_AL 스터디 발표자료](https://goo.gl/ihvrGV){:target="_blank"}



# Tensorflow

[구글 텐서플로우 첫걸음](https://www.slideshare.net/mobile/HwanheeKim2/ss-137921987){:target="_blank"}

[Gentlest Introduction to Tensorflow #1](https://medium.com/all-of-us-are-belong-to-machines/the-gentlest-introduction-to-tensorflow-248dc871a224){:target="_blank"}

[2019 Tensorflow Dev Summit 요약](https://developers-kr.googleblog.com/2019/03/recap-of-the-2019-tensorflow-dev-summit.html?m=1){:target="_blank"}



# Keras

[김태영님의 케라스 강좌](https://tykimos.github.io/lecture/){:target="_blank"}



# NLP

[D. Jurafsky, Speech and Language Processing](http://web.stanford.edu/~jurafsky/slp3/){:target="_blank"}

[C. Manning, Foundation of Statistical Natural Language Processing](ttp://nlp.stanford.edu/fsnlp/){:target="_blank"}

[Natural Language Processing with Python](http://www.nltk.org/book){:target="_blank"}

[딥러닝 기반 자연어처리 기법의 최근 연구 동향](https://ratsgo.github.io/natural%20language%20processing/2017/08/16/deepNLP/){:target="_blank"}

[챗봇의 구조: 챗봇은 AI가 필요한가?](https://brunch.co.kr/@gentlepie/7){:target="_blank"}



##### <자연언어처리(NLP)를 위한 언어학 기초>

[언어의 기원](http://blog.naver.com/bcj1210/221144574548){:target="_blank"}

[단어의 형성](http://blog.naver.com/bcj1210/221144651784){:target="_blank"}

[형태론](http://blog.naver.com/bcj1210/221145151867){:target="_blank"}

[구와 문장](http://blog.naver.com/bcj1210/221145989566){:target="_blank"}

[통사론](http://blog.naver.com/bcj1210/221147134955){:target="_blank"}

[의미론](http://blog.naver.com/bcj1210/221147150551){:target="_blank"}

[화용론](http://blog.naver.com/bcj1210/221147166747){:target="_blank"}

[담화분석](http://blog.naver.com/bcj1210/221147187757){:target="_blank"}

[언어와 뇌](http://blog.naver.com/bcj1210/221276099605){:target="_blank"}

[언어와 뇌 2](https://blog.naver.com/bcj1210/221277463741){:target="_blank"}



# Embedding

[단어 임베딩을 사용하여 텍스트 유사성 계산하기](https://eda-ai-lab.tistory.com/118){:target="_blank"}



## 현업 응용

[TensorFlow 를 활용한 네이버쇼핑의 상품 카테고리 자동 분류](https://d2.naver.com/helloworld/1264836){:target="_blank"}



# 주요 논문과 구현

[Trending Research](https://paperswithcode.com/?fbclid=IwAR30-Yg-ZUweLOUYswOJYVPuVm0Jr7LmuOfwX0mkUbaaqlQ7ZIzry_yoQIM){:target="_blank"}



# Books

### 책 내용 포함

[Dive into Deep Learning](http://d2l.ai/){:target="_blank"}

[Reinforcement Learning: An Introduction](http://incompleteideas.net/book/the-book.html){:target="_blank"}

[앤드류 응(Andrew Ng.) 교수저 'Machine Learning Yearning'라는 책의 한국어 번역](https://github.com/deep-diver/Machine-Learning-Yearning-Korean-Translation){:target="_blank"}



### 책 소개 링크

[Christopher Bishop](https://www.microsoft.com/en-us/research/people/cmbishop/#!prml-book){:target="_blank"}

[밑바닥부터 시작하는 딥러닝 1](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788968484636&orderClick=LEA&Kc=){:target="_blank"}

- Tensorflow 등의 플랫폼을 사용하지 않고 딥러닝 이론을 직접 구현함.

[밑바닥부터 시작하는 딥러닝 2](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791162241745&orderClick=LEA&Kc=){:target="_blank"}

- 시즌 1에서 다루지 않았던 RNN과 NLP 관련 내용을 다룸

[핸즈온 머신러닝](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791162240731&orderClick=LEB&Kc=){:target="_blank"}

- 데이터 분석부터 시작해서 실제 모델 구현까지 설명하고 있는 좋은 책



# 볼만한 것들

[왜 최근에 빌 게이츠, 엘론 머스크, 스티븐 호킹 등 많은 유명인들이 인공지능을 경계하라고 호소하는가?](https://coolspeed.wordpress.com/2016/01/03/the_ai_revolution_1_korean/){:target="_blank"}

- 좀 길긴한데 강추합니다.

[Jeremy Howard: The wonderful and terrifying implications of computers that can learn](https://www.ted.com/talks/jeremy_howard_the_wonderful_and_terrifying_implications_of_computers_that_can_learn){:target="_blank"}

[Google Duplex: A.I. Assistant Calls Local Businesses To Make Appointments](https://www.youtube.com/watch?v=D5VN56jQMWM&feature=youtu.be){:target="_blank"}

[레이 커즈와일, 특이점이 온다](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788934924067&orderClick=LAH&Kc=){:target="_blank"}

-  테슬라, 스페이스X 등으로 유명한 특이점을 굉장히 좋하하시는 분의 책

[유발 하라리, 사피엔스](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788934972464&orderClick=LAG&Kc=){:target="_blank"}

- 논란이 되는 부분도 있지만 책 내용은 재미있고 한번쯤 읽어볼만 합니다.

[유발 히라리, 호모데우스](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788934977841&orderClick=LAG&Kc=){:target="_blank"}

[박정일, 튜링 & 괴델: 추상적 사유의 위대한 힘](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788934921783&orderClick=LAH&Kc=){:target="_blank"}

[이미테이션 게임(영화)](https://movie.naver.com/movie/bi/mi/basic.nhn?code=113348){:target="_blank"}

- 컴퓨터 과학과 인공지능의 아버지 정도되는 튜링의 이야기

[튜링: 이미테이션 게임(책)](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788956059372&orderClick=LAH&Kc=#review){:target="_blank"}

- 이책이 아래 책보다 영화 내용에 가깝고 가벼운 내용이라고 해야할 것 같음.

[앨런 튜링의 이미테이션 게임(책)](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788962620979&orderClick=LAH&Kc=){:target="_blank"}

- 원서명 Alan Turing



# 기타 정리 사이트

[공부하면 좋은 List](https://github.com/Team-Neighborhood/I-want-to-study-Data-Science/wiki/%EA%B3%B5%EB%B6%80%ED%95%98%EB%A9%B4-%EC%A2%8B%EC%9D%80-List#%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B8%B0%EC%B4%88){:target="_blank"}



# 컴파일러, 최적화, 백엔드 포팅

### Compiler for Machine Learning.

[TVM: An Automated End-to-End Optimizing Compiler for Deep Learning](https://www.usenix.org/system/files/osdi18-chen.pdf){:target="_blank"}

[TVM: An Automated End-to-End Optimizing Compiler for Deep Learning](https://www.usenix.org/conference/osdi18/presentation/chen){:target="_blank"}

[Compiling machine learning programs via high-level tracing](http://www.sysml.cc/doc/146.pdf){:target="_blank"}

[Compiling machine learning programs via high-level tracing](https://ai.google/research/pubs/pub47008){:target="_blank"}

[Deep Learning을 위한 컴퓨터 구조](http://www.mysnu.org/m/community/newtechnology.php?search_order=&search_part=&c_cate1=&mode=v&idx=10586&thisPageNum=){:target="_blank"}

[DLVM: Modern Compiler Infrastructure for Deep Learning Systems](http://dlvm.org/){:target="_blank"}

[ACM: Halide: a language and compiler for optimizing parallelism, locality, and recomputation in image processing pipelines](https://dl.acm.org/citation.cfm?id=2462176){:target="_blank"}

[TensorFlow XLA compiler and the NNVM compiler](https://developers-kr.googleblog.com/2017/03/xla-tensorflow-compiled.html){:target="_blank"}

[XLA is a compiler that optimizes TensorFlow computations.](https://www.tensorflow.org/xla/){:target="_blank"}

[TVM](https://tvm.ai/about){:target="_blank"}

[딥 뉴럴 네트워크 지원을 위한 뉴로모픽 소프트웨어 플랫폼 기술 동향](https://ettrends.etri.re.kr/ettrends/172/0905172002/33-4_14-22.pdf){:target="_blank"}

[Glow: Graph Lowering Compiler Techniques for
Neural Networks](https://arxiv.org/pdf/1805.00907.pdf){:target="_blank"}

### 병렬 Job, 캐시, 최적화

[텐서플로우를 이용하여 신경망 양자화(Quantize) 하는 방법](https://github.com/tensorflowkorea/tensorflow-kr/blob/master/g3doc/how_tos/quantization/index.md){:target="_blank"}

[Post-training quantization](https://www.tensorflow.org/lite/performance/post_training_quantization){:target="_blank"}

#### 대량의 입력 데이터 캐시 정책

- Gradient Optimization, Backpropagation, derivate
  2017 년에들어서 컴파일러 테크닉이 머신러닝에 적용됨(TVM, NNVM, tensorflow XLA compiler)

[Model optimization](https://www.tensorflow.org/lite/performance/model_optimization){:target="_blank"}

[SIMD 병렬 프로그래밍](https://stonzeteam.github.io/SIMD-%EB%B3%91%EB%A0%AC-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/){:target="_blank"}

[Speed up TensorFlow Inference on GPUs with TensorRT](https://medium.com/tensorflow/speed-up-tensorflow-inference-on-gpus-with-tensorrt-13b49f3db3fa){:target="_blank"}

[OpenCL Optimization](https://www.nvidia.com/content/gtc/documents/1068_gtc09.pdf){:target="_blank"}

[문돌이가 이해한 머신러닝(8) - Normal Equation(정규방정식)](https://blog.naver.com/dreamclouud/221327081159){:target="_blank"}