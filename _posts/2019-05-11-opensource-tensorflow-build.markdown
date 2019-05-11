---
layout: post
title:  "Tensorflow 를 소스코드로부터 빌드하기"
date:   2019-05-11 16:10:00
author: Ada Lovelace
categories: ai
tags:	AI 인공지능 머신러닝
cover:  "/assets/instacode.png"
---

텐서플로우의 내부 구조와 소스 코드를 분석하기 위해서는 소스를 수정해보는 것도 중요하기 때문에 우선 텐서플로우를 소스 코드로부터 직업 빌드하는 방법을 알아보도록 하겠습니다.

빌드 절차는 공식 사이트에 잘 나와있어서 번역 수준으로 작성하였습니다. 제가 첨언한 부분은 *이탤릭*으로 표시하였습니다.

[공식 가이드: Build from source](https://www.tensorflow.org/install/source){:target="_blank"}

# 소스로부터 빌드

우분투 리눅스와 macOS 에서 소스코드로부터 pip 패키지를 빌드하고 설치해보도록 하겠습니다. 설치 명령어는 우분투와 macOS에서 테스트하였지만, 다른 시스템에서도 동작할 수 있습니다.

------

Note: 이미 우리는 리눅스와 macOS 시스템에서 테스트 완료하여 프리-빌트된 텐서플로우 패키지를 제공합니다.

------

*저는 아래 환경을 기준으로 설치하였으므로 우분투 위주로 설치 방법을 기재하도록 하겠습니다.*

- *우분투 리눅스 18.04 LTS*
- *python3*



## 목차

[리눅스와 macOS 설정](리눅스와-macos-설정)

​	[파이썬과 텐서플로우에서 사용하는 라이브러리 설치](파이썬과-텐서플로우에서-사용하는-라이브러리-설치)

​	[Bazel 설치](bazel-설치)

​	[GPU 지원 관련 설치](gpu-지원-관련-설치)

​	[텐서플로우 소스 코드 다운로드](텐서플로우-소스-코드-다운로드)

[빌드 설정](빌드-설정)

​	[설정 옵션](설정-옵션)

[pip 패키지 빌드](pip-패키지-빌드)

​	[Bazel 빌드](Bazel-빌드)

​	[패키지 빌드](패키지-빌드)

​	[패키지 설치](패키지-설치)

[Tested build configurations](tested-build-configurations)

​	[Linux](linux)

​	[macOS](macos)

## 리눅스와 macOS 설정

개발환경 설정을 위해 아래의 빌드 도구들을 설치합니다.

### 파이썬과 텐서플로우에서 사용하는 라이브러리 설치

```bash
$ sudo apt install python3-dev python3-pip
```

텐서플로우에서 사용하는 파이선 pip 패키지 라이브러리 설치(만약 가상환경을 사용중이면 `--user` 옵션을 제거하세요.)

```bash
$ pip3 install -U --user pip six numpy wheel setuptools mock
$ pip3 install -U --user keras_applications==1.0.6 --no-deps
$ pip3 install -U --user keras_preprocessing==1.0.5 --no-deps
```

의존 패키지들의 목록은 [setup.py](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/pip_package/setup.py) 파일의 `REQUIRED_PACKAGES` 에서 확인할 수 있습니다.

*간혹 설치중에 ImportError: cannot import name 'main' 와 같은 오류 메시지가 발생한다면 기본 쉘을 bash 로 변경하고 다시 쉘을 띄워서 실행해 보시기 바랍니다.*

*우분투의 기본 쉘 dash 를 bash 로 변경하는 방법*

```bash
$ sudo dpkg-reconfigure dash
No 선택
```



### Bazel 설치

[Bazel 설치하기](https://docs.bazel.build/versions/master/install.html){:target="_blank"}, Bazel 은 텐서플로우를 컴파일하는데 사용하는 빌드 도구입니다.

위의 공식 설치 문서를 참조하여 Bazel 을 설치하고 Bazel 실행파일의 경로를 PATH 환경 변수에 추가합니다.

*참고로 우분투에서는 아래와 같이 설치할 수 있습니다.*

```bash
$ sudo apt-get install pkg-config zip g++ zlib1g-dev unzip python
$  wget https://github.com/bazelbuild/bazel/releases/download/0.25.2/bazel-0.25.2-installer-linux-x86_64.sh
$ chmod +x bazel-0.25.2-installer-linux-x86_64.sh
$ sudo ./bazel-0.25.2-installer-linux-x86_64.sh --user
```

*~/.bashrc 에 아래 내용 추가*

```bash
export PATH="$PATH:$HOME/bin"
```

*이제 `source ~/.bashrc` 를 하면 bazel 을 바로 실행할 수 있습니다.*

### GPU 지원 관련 설치

맥OS 는 GPU 를 지원하지 않습니다.

GPU 에서 텐서플로우를 실행하는데 필요한 드라이버와 추가적인 소프트웨어를 설치하기 위해서는 [GPU 지원](https://www.tensorflow.org/install/gpu){:target="_blank"} 가이드를 참조해주세요.

### 텐서플로우 소스 코드 다운로드

텐서플로우의 저장소를 clone 하기 위해서 git 을 사용합니다.

```bash
$ git clone https://github.com/tensorflow/tensorflow.git
$ cd tensorflow
```

repo 의 기본설정은 master 개발 브랜치입니다. 빌드를 하기 위해서 release branch 로 체크아웃을 할 수 있습니다.

```bash
$ git checkout branch_name # r1.9 r1.10, etc
```

*저는 가장 최신 버전으로 보이는 r1.14 로 체크아웃을 하여 빌드롤 하도록 하겠습니다.*

```bash
$ git checkout r1.14
```



## 빌드 설정

다운로드 받은 텐서플로우 소스 코드의 최상위 디렉토리에서 아래 명령어를 실행하여 빌드관련 설정을 합니다.

```bash
$ ./config
```



### 설정 옵션

[GPU 지원](https://www.tensorflow.org/install/gpu){:target="_blank"}을 위해서 CUDA 와 cuDNN 버전을 명시할 수 있습니다. 만약 시스템에 여러 버전의 CUDA 혹은 cuDNN 이 설치되어 있다면, 기본값을 사용하지 말고 명시적으로 버전을 설정해야 합니다. `./configure` 는 시스템의 CUDA 라이브러리에 심볼릭 링크를 생성합니다. 따라서 CUDA 라이브러리 패스를 업데이트할 경우에는 이 configuration 단계를 다시 진행해야 합니다.

컴파일 최적화를 위한 기본 옵션(`-march=native`) 은 현재 시스템의 CPU 에 맞게 생성된 코드를 최적화하는 것입니다. 그러나 만약 다른 CPU 에 맞게 텐서플로우를 빌드한다면, 추가적인 최적화 옵션 설정을 고려해야 합니다. [GCC 설명서](https://gcc.gnu.org/onlinedocs/gcc-4.5.3/gcc/i386-and-x86_002d64-Options.html){:target="_blank"}를 참조해 주세요.

몇가지 사전 설정(프리-셋)된 빌드 설정을 `bazel build` 명령에 추가하여 사용할 수 있습니다. 예를들어:

- `--config=mkl`
  - [Intel® MKL-DNN](https://github.com/intel/mkl-dnn){:target="_blank"}. 을 위한 설정
- `--config=monolithic` 
  - 주로 static, monolithic 한 빌드를 위한 설정

------

Note: 텐서플로우 1.6 바이너리부터는 오래된 CPU 에서 실행안될수도 있는 AVX 명령어를 사용합니다.

------

## pip 패키지 빌드

### Bazel 빌드

#### CPU-only

CPU 버전 텐서플로우 패키지 빌더를 만들기 위해서 `bazel` 을 사용합니다.

```bash
$ bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
```

#### GPU 지원

GPU 용 텐서플로우 패키지 빌더를 만들기 위해서는 아래와 같은 명령어를 수행합니다.

```bash
$ bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
```

#### bazel 빌드 옵션

소스로부터 텐서플로우를 빌드하는 것은 많은 메모리가 필요합니다. 만약 시스템 메모리가 제한적이라면, bazel 의 메모리 사용량을 제안해야 합니다: `--local_resources 2048,.5,1.0`

[공식적인 텐서플로우 패키지들](https://www.tensorflow.org/install/pip){:target="_blank"}은 GCC 4 로 빌드했고 더 오래된 ABI 를 사용한다. GCC 5 부터는 오래된 ABI 와의 호환 가능하도록 옵션을 지정해야 합니다: `--cxxopt="-D_GLIBCXX_USE_CXX11_ABI=0"` ABI 호환성은 공식적인 텐서플로우 패키지로 빌드된 커스텀 연산이 GCC 5 빌드 패키지로도 계속 동작할 수 있도록 합니다.

### 패키지 빌드

bazel build 명령어는 `build_pip_package` 라는 실행가능한 파일을 생성합니다. -- 이것은 pip 패키지를 빌드하는 프로그램입니다. .whl 패키지를 빌드하기 위해서는 `/tmp/tensorflow_pkg` 디렉토리에서 아래와 같은 명령어를 실행합니다.

release branch 로부터 빌드:

```bash
$ ./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

master 로부터 빌드를 하려면, 올바른 dependencies 을 획득하기 위해서 `--nightly_flag` 를 사용하세요.

```bash
$ ./bazel-bin/tensorflow/tools/pip_package/build_pip_package --nightly_flag /tmp/tensorflow_pkg
```

같은 소스 트리로 CUDA 와 non-CUDA 설정 둘다 빌드가 가능하지만, 같은 소스 트리에서 이 2개의 설정 사이를 스위칭할 때에는 `bazel clean` 명령을 수행할 것을 추천합니다.

### 패키지 설치

생성된 `.whl` 파일의 파일명은 텐서플로우 버전과 당신의 플랫폼에 의존합니다.

패키지를 설치하기 위해서 `pip install` 을 사용하세요. 예를들어:

```bash
$ pip install /tmp/tensorflow_pkg/tensorflow-<u>version-tags</u>.whl
```

**Success:** TensorFlow is now installed.



## Tested build configurations

### Linux

| Version           | Python version | Compiler | Build tools  |
| :---------------- | :------------- | :------- | :----------- |
| tensorflow-1.13.1 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.19.2 |
| tensorflow-1.12.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 |
| tensorflow-1.11.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 |
| tensorflow-1.10.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 |
| tensorflow-1.9.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.11.0 |
| tensorflow-1.8.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 |
| tensorflow-1.7.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 |
| tensorflow-1.6.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  |
| tensorflow-1.5.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.8.0  |
| tensorflow-1.4.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.5.4  |
| tensorflow-1.3.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  |
| tensorflow-1.2.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  |
| tensorflow-1.1.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  |
| tensorflow-1.0.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  |

| Version               | Python version | Compiler | Build tools  | cuDNN | CUDA |
| :-------------------- | :------------- | :------- | :----------- | :---- | :--- |
| tensorflow_gpu-1.13.1 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.19.2 | 7.4   | 10.0 |
| tensorflow_gpu-1.12.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.11.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.10.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.9.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.11.0 | 7     | 9    |
| tensorflow_gpu-1.8.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 | 7     | 9    |
| tensorflow_gpu-1.7.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  | 7     | 9    |
| tensorflow_gpu-1.6.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  | 7     | 9    |
| tensorflow_gpu-1.5.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.8.0  | 7     | 9    |
| tensorflow_gpu-1.4.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.5.4  | 6     | 8    |
| tensorflow_gpu-1.3.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  | 6     | 8    |
| tensorflow_gpu-1.2.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  | 5.1   | 8    |
| tensorflow_gpu-1.1.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  | 5.1   | 8    |
| tensorflow_gpu-1.0.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  | 5.1   | 8    |

### macOS

CPU

| Version           | Python version | Compiler         | Build tools  |
| :---------------- | :------------- | :--------------- | :----------- |
| tensorflow-1.13.1 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.19.2 |
| tensorflow-1.12.0 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.15.0 |
| tensorflow-1.11.0 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.15.0 |
| tensorflow-1.10.0 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.15.0 |
| tensorflow-1.9.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.11.0 |
| tensorflow-1.8.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.10.1 |
| tensorflow-1.7.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.10.1 |
| tensorflow-1.6.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.8.1  |
| tensorflow-1.5.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.8.1  |
| tensorflow-1.4.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.5.4  |
| tensorflow-1.3.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.5  |
| tensorflow-1.2.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.5  |
| tensorflow-1.1.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.2  |
| tensorflow-1.0.0  | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.2  |

GPU

| Version              | Python version | Compiler         | Build tools | cuDNN | CUDA |
| :------------------- | :------------- | :--------------- | :---------- | :---- | :--- |
| tensorflow_gpu-1.1.0 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.2 | 5.1   | 8    |
| tensorflow_gpu-1.0.0 | 2.7, 3.3-3.6   | Clang from xcode | Bazel 0.4.2 | 5.1   | 8    |