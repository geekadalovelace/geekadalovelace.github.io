---
layout: post
title:  "GitHub Pages 에 comment, analytics 달기"
date:   2019-04-07 10:25:59
author: Ada Lovelace
categories: Etc
tags:	GitHub Pages DISQUS Analytics
cover:  "/assets/instacode.png"
---

[이전 포스팅](https://geekadalovelace.github.io/etc/2019/04/06/github-blog.html)에서 우리는 centrarium 테마를 적용해 보았습니다. 여기서는 comment 와 페이지 방문 통계를 확인할 수 있도록 하려고 합니다. GitHub Pages 는 기본적으로 댓글과 방문 통계 등을 확인할 수 있는 기능을 제공하지 않습니다. 따라서 외부 도구를 활용하여 원하는 기능을 추가하려고 합니다.



## Comment (DISQUS)

댓글 기능을 붙이기 위해서 DISQUS 를 이용합니다. 먼저 DISQUS 에 가입을 한 후 "I want to install Disqus on my site" 를 선택합니다.

![1554598528370](../../../../assets/images/1554598528370.png)

원하는 정보를 기입합니다. 기본적으로는 웹사이트 이름을 적으면 Shortname 이 결정되는데 "Customize Your URL" 을 누르면 Shortname 을 원하는 형태로 작성할 수 있습니다.

DISQUS 를 설정하기 위해서 _config.yml 파일에서 주석 처리되어 있는 disqus_shortname 의 주석을 해제하고 Shortname 을 기입하면 연동이 끝납니다.



## 통계 확인

방문자 수 등의 통계를 확인하기 위해서 Google Analytics 에 가입합니다. 가입을 완료하면 Tracking ID(추적 ID) 가 발급됩니다. DISQUS 때와 마찬가지로 _config.yml 을 열고 이 ID 를 ga_tracking_id 에 기입하면 정말 간단하게 연동이 됩니다. 통계는 웹사이트에서도 확인할 수 있고 구글에서 제공하는 모바일 앱으로도 실시간 확인이 가능합니다.



## 마치며

정말 간단하게 댓글과 통계 기능을 추가하였습니다. 더 많은 기능을 설정하고 싶으시면 각각의 사이트에서 설정으로 들어가시면 다양한 기능을 제공하고 있으니 활용해 보는 것도 좋을 것 같습니다.

