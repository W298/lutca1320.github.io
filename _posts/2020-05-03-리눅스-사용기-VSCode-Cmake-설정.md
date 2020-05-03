---
title: 리눅스 사용기 - VSCode / CMake 설정
author: RUKA SPROUT
date: 2020-05-03 14:05:00 +0900
categories: [Linux]
tags: [linux]
---

## Background
현재 우분투, MasOS, 윈도우즈를 사용하고 있는데, 이 3개의 운영체재에서 더 원활하게 빌드하기 위해 CMake를 이용해보고자 했다. CMake는 터미널이나 CMD로 사용할 수는 있으나 설정이 복잡한데, VSCode 의 확장 플러그인들을 이용하면 쉽게 CMake 설정파일을 만들 수 있다. 그래서 이번에는 우분투에 먼저 VSCode를 설치하고, CMake 플러그인을 설정하는 것을 다룰 것이다.

## Installation
### VSCode
이번에는 설치를 위해 `curl` 이 필요하다. 참고로 `curl` 은 http, ftp 프로토콜들을 이용해 웹 페이지의 소스를 가져온다거나 파일을 다운받을 수 있다.

아래 코드를 터미널에 입력해 설치하자.

```shell
sudo apt install curl
```

MS GPG 키를 다운로드한다.

```shell
sudo sh -c 'curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.gpg'
```

저장소를 추가하고, 패키지 목록을 가져온다.

```shell
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

```shell
sudo apt-get update
```

마지막으로 VSCode 를 설치한다.

```shell
sudo apt-get install code
```

귀찮으면 [웹페이지](https://code.visualstudio.com/)에서 직접 다운받을 수도 있다. 우분투는 `.deb` 파일을 다운받아 설치하면 된다.

![스크린샷 2020-05-03 오후 2.30.09](https://i.imgur.com/ToPd8zI.png)

#### Error Debug

필자와 같은 경우에는 다음과 같이 하얀 화면만 나오고 UI가 보이지 않는 현상이 발생하였다. 찾아보니 `virtualbox` 나 `parallels` 와 같은 가상머신을 이용하면 생기는 오류라고 한다.

![스크린샷 2020-05-03 오후 2.52.16](https://i.imgur.com/SD7Ub1j.png)

이는 다음 코드를 이용해 정상적인 실행이 가능하다.

```shell
code --disable-gpu
```

![스크린샷 2020-05-03 오후 2.58.16](https://i.imgur.com/k3fDOsV.png)

### CMake

플러그인을 설치하기 이전에 먼저 CMake 가 설치되어있는지 확인하자.

![스크린샷 2020-05-03 오후 2.35.41](https://i.imgur.com/quhdifU.png)

기본적으로 우분투에는 CMake가 설치되어 있지는 않다. 아래를 터미널에 입력해 설치할 수 있다.

```shell
sudo apt install cmake
```

설치한 뒤 `cmake --version` 을 통해 잘 설치되었는지 확인해 볼 수 있다.

![스크린샷 2020-05-03 오후 2.38.32](https://i.imgur.com/OwVAEc8.png)

3.10.2 버젼은 현재 최신 버젼은 아니다. 최신 버젼을 받기 위해서는 웹페이지에서 tar 파일을 받아 설치해야 한다. 하지만 지금은 굳이 필요하지 않기에 넘어가도록 하자.

### VSCode Plugin

- CMake
- CMake tools

이 두가지 확장 플러그인을 설치한다.

![스크린샷 2020-05-03 오후 3.01.30](https://i.imgur.com/f6NsHhY.png)

## Configure / Test
### Configure

설정을 위해 먼저 프로젝트 폴더를 만들고 열어두자.

![스크린샷 2020-05-03 오후 3.04.53](https://i.imgur.com/lUyk4vV.png)

이 상태로 `Ctrl` + `Shift` + `P` 를 이용해 콘솔 창을 연 뒤, `CMake: quick start` 를 선택해 준다.

![스크린샷 2020-05-03 오후 3.06.27](https://i.imgur.com/xlulnGM.png)

그러면 다음과 같은 창이 나오는데, `Scan for kits` 를 눌러준다.

![스크린샷 2020-05-03 오후 3.07.20](https://i.imgur.com/ApUvlLw.png)

현재 설치되어 있는 컴파일러들을 보여주는데, 이는 환경마다 다를 수 있다. 자신이 사용하고 싶은 컴파일러를 선택해 주면 된다. 필자는 `GCC 7.5.0` 을 선택하였다.

![스크린샷 2020-05-03 오후 3.08.17](https://i.imgur.com/ISAvpTD.png)

그다음 `Enter a name for the new project` 에 프로젝트 이름을 입력하고, `Executable` 을 선택해주면, 다음과 같은 화면이 나오게 된다.

`[CMake] Generating done` 이 출력되면 정상적으로 CMake 환경이 설정된 것이다.

![스크린샷 2020-05-03 오후 3.08.47](https://i.imgur.com/BgguD3P.png)


### Test

`main.cpp` 에 이미 "Hello World" 소스가 있으니 이를 실행해보도록 하겠다.

![스크린샷 2020-05-03 오후 3.15.58](https://i.imgur.com/rfmASCz.png)

아까와 똑같이 `Ctrl` + `Shift` + `P` 를 눌러 콘솔 창을 띄운 뒤, `CMake:Run without Debugging` 을 눌러주면 실행된다.

![스크린샷 2020-05-03 오후 3.18.03](https://i.imgur.com/LRhkLD5.png)

"Hello World" 가 잘 출력되는 것을 확인할 수 있다.

![스크린샷 2020-05-03 오후 3.19.51](https://i.imgur.com/cGy5RGD.png)

## 소감
VSCode 에러를 고치는 데 시간을 좀 들여 고생을 했지만, CMake 는 그만한 가치가 있다고 생각한다. 이 설정을 그대로 윈도우즈와 MasOS 에도 적용하였으며, 굉장히 만족스럽게 사용하고 있다. 지금은 플러그인을 이용해 CMake 파일을 자동으로 만들어주는 기능을 사용하고 있지만, 나중에 수동으로 조작하는 방법도 익혀둘 것이다.
