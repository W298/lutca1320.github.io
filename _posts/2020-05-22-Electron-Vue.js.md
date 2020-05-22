---
title: 리눅스 사용기 - Electron 과 Vue.js 로 데스크탑 앱 만들기
author: RUKA SPROUT
date: 2020-05-22 17:59:00 +0900
categories: [Linux]
tags: [linux, electron, node.js, vue.js]
---

## Background
간단히 `Electron` 을 소개하자면, 웹 기반으로 사용하던 `Javascript` 를 네이티브 데스크탑애서 사용할 수 있게 만들어주는 프레임워크이다. 기존에 데스크탑 앱을 개발하기 위해서는 윈도우의 경우 `Visual Studio`, 맥의 경우 `Xcode` 를 이용해 개발했어야 했는데, `Electron` 을 이용하면 크로스 플랫폼을 지원하는 데스크탑 앱을 개발할 수 있다.

`Electron` 으로 개발된 프로그램은 대표적으로 `Atom`, `Github Desktop`, `Slack`, `VS Code`, `Discord` 등 우리가 자주 사용하는 프로그램들이 다수 있는데, 이를 통해 이미 `Electron` 이 적극적으로 사용되고 있다는 것을 느낄 수 있었다.

## Installation
### Vue-Cli 설치
먼저 `Vue-Cli` 설치를 진행하자. `Vue-Cli` 를 이용하면 프로그램의 기본 골조를 잡아주어 훨씬 쉽게 `Electron` 앱을 개발할 수 있다.

[Document](https://nklayman.github.io/vue-cli-plugin-electron-builder/guide/#installation)

터미널을 열고 아래 코드를 입력한다. `npm` 이 설치되어있어야 한다.

```shell
sudo npm install -g vue-cli
```
잘 설치되었는지 확인하기 위해 아래 코드를 입력한다. 버젼이 나오면 설치에 성공한 것이다.

```shell
vue -V
```

![스크린샷 2020-05-22 오후 5.38.25](https://i.imgur.com/7oMphVa.png)

또한 다음 과정에서 `yarn`을 사용할 것이므로 다음 코드를 입력해 설치해 주자.

```shell
sudo npm install -g yarn
```

## Configure

일단 필요한 패키지들은 모두 설치했다. (`vue`, `nodejs`) 이제 `vue-cli` 를 이용해 `Electron` 프로젝트를 만들 것이다.

아래 코드를 입력해 프로젝트를 생성하자. (vue-electron 은 프로젝트 명)

```shell
vue create vue-electron
```

정상적으로 실행되어야 하나, 필자는 다음과 같은 에러가 발생하였다. CLI 버전이 낮아서 생기는 오류로 CLI 3를 설치해주야 한다고 한다.

![스크린샷 2020-05-22 오후 5.43.43](https://i.imgur.com/fl2xfV0.png)

위에서 하라는 대로 다시 설치해 보겠다.

```shell
sudo npm uninstall -g vue-cli
sudo npm install -g @vue/cil
```

그 다음 다시 프로젝트를 만들면 다음과 같은 화면이 나오는데, 일단 테스트 용으로 프로젝트를 만들 것이기 때문에 `default` 를 선택했다.

```shell
vue create vue-electron
```

![스크린샷 2020-05-22 오후 5.48.29](https://i.imgur.com/Jrxyowc.png)

다음으로 `yarn` 과 `npm` 중에 선택하라고 하는데, 아까 설치한 `yarn` 을 선택해 주자.

![스크린샷 2020-05-22 오후 5.49.38](https://i.imgur.com/yBBPLJB.png)

그러면 알아서 프로젝트 파일을 만들기 시작하는데, 꽤 시간이 걸린다. 프로젝트가 완성되면 다음과 같은 화면일 것이고, `cd vue-electron` 으로 프로젝트 경로로 이동해 두자.

![스크린샷 2020-05-22 오후 5.51.18](https://i.imgur.com/trA1bAc.png)

그다음으로 할 일은 `electron-builder` 를 프로젝트에 추가하는 것이다. 다음 코드를 입력하자. 이 또한 시간이 좀 걸릴 것이다.

```shell
vue add electron-builder
```

이렇게 만들어진 `electron` 프로젝트를 아래 코드를 통해 직접 실행해 볼 수 있다.

```shell
yarn eletron:serve
```

현재 필자는 페러렐즈 데스크탑으로 우분투를 돌리고 있는데, 이 환경에서는 다음 코드로 실행하여야 제대로 화면이 보인다.

```shell
yarn electron:serve --disable-gpu
```

![스크린샷 2020-05-22 오후 7.12.52](https://i.imgur.com/PetH9Bg.png)

위 화면을 구성하고 있는 파일을 찾아보기 위해 프로젝트 경로에 들어가 찾아보았다. `HelloWorld.vue` 파일이 위 화면을 구성하고 있다.

![스크린샷 2020-05-22 오후 7.20.01](https://i.imgur.com/2ek54Al.png)

수정이 적용되는지를 확인해보기 위해 `Welcome to Vuetify` 부분을 `Hello World !!` 로 수정하고 저장하면 알아서 컴파일을 한 뒤 수정된 사항을 앱에 적용시킨다.

![스크린샷 2020-05-22 오후 7.22.37](https://i.imgur.com/2DCjO2S.png)

![스크린샷 2020-05-22 오후 7.24.43](https://i.imgur.com/sWsYBUF.png)

수정한 대로 앱이 변경된 것을 확인할 수 있다.
