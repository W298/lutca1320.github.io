---
title: 리눅스 사용기 - Node.js 설치 및 디스코드 챗봇 만들기
author: RUKA SPROUT
date: 2020-05-15 15:24:00 +0900
categories: [Linux]
tags: [linux, discord, node.js]
---

## Background
`Node.js` 를 이용해 웹 어플리케이션 개발을 체험해보고 싶었는데, 마침 필자가 자주 사용하는 소프트웨어인 `Discord` 의 챗봇을 `Node.js` 로 만들 수 있다는 것을 알게 되었다. *(`Discord` 챗봇은 `Python` 으로도 만들 수 있다)* 이번 기회에 우분투에 `Node.js` 를 설치하는 것부터 챗봇을 직접 만들어 테스트해보는 것까지 해볼 것이다.

## Installation
### Node.js 설치
이번 설치에도 `curl` 이 필요하다. 설치되어 있지 않으면 아래 명령어로 설치해주어야 한다.

```shell
sudo apt install curl   # 필요시 설치
```
12버전 기준으로 최신 버전을 PPA를 통해 가져올 것이다.

```shell
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

그다음 Node.js 를 설치해 준다.

```shell
sudo apt-get install -y nodejs
```

잘 설치되었는지 확인하기 위해 아래 명령어를 입력하자.

```shell
node -v
npm -v
```

![스크린샷 2020-05-15 오후 3.44.08](https://i.imgur.com/3ntqhgi.png)

또는 그냥 https://nodejs.org/ 에서 파일을 받아 설치해도 된다. 현재 우리가 다룰 버전은 12.16.3 LTS 이다.

![스크린샷 2020-05-15 오후 3.45.46](https://i.imgur.com/1IrVxtQ.png)

### discord.js 모듈 설치
다음으로 [discord.js](https://discord.js.org/#/) 모듈을 설치해 주어야 한다.

```shell
npm install discord.js
```

## Configure
### Discord 봇 애플리케이션 설정

*(설정은 어디에서 하든지 상관없다. 필자는 맥에서 진행하였다.)*

https://discord.com/developers/applications

먼저 위 페이지에 접속하여 `New Application` 를 눌러 애플리케이션을 만들어 준다. Bot 탭으로 이동하여 `Add Bot` 을 눌러준다.

![스크린샷 2020-05-15 오후 3.57.53](https://i.imgur.com/dt3qOI5.png)

다음으로 `OAuth2` 탭으로 이동하여 Scopes 의 bot 을 체크해주면 봇의 권한을 설정할 수 있는데, 일단 관리자(Administrator) 권한을 주도록 하겠다.

![스크린샷 2020-05-15 오후 4.03.19](https://i.imgur.com/RuGNL64.png)

설정한 뒤, `Copy` 버튼을 눌러 링크를 복사한 뒤 주소창에 붙여넣으면 다음과 같은 화면을 볼 수 있는데, 추가할 서버를 선택해 준다.

![스크린샷 2020-05-15 오후 4.05.24](https://i.imgur.com/bdgZPzW.png)

정상적으로 등록되었지만, 아직 서버를 열지 않았기 때문에 오프라인으로 뜬다.

![스크린샷 2020-05-15 오후 4.11.28](https://i.imgur.com/guj6fGX.png)

### Discord 봇 프로그래밍

일단 [discord.js](https://discord.js.org/#/) 에 있는 튜토리얼을 따라가도록 하겠다.

에디터를 연 뒤, 다음 코드를 입력하고 `app.js` 로 저장한다.

```js
const Discord = require('discord.js');
const client = new Discord.Client();

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}!`);
});

client.on('message', msg => {
  if (msg.content === 'ping') {
    msg.reply('Pong!');
  }
});

client.login('token'); // 토큰값 넣는곳
```

일단 이를 실행하기 위해서는 토큰값을 입력해야 하는데, 아까 봇 설정 페이지에서 가져올 수 있다. Token 의 Copy 를 눌러주면 복사된다.

![스크린샷 2020-05-15 오후 4.22.12](https://i.imgur.com/lMC4jry.png)

이 값을 'token' 에 넣어주면 된다.

```js
client.login('NjgyOD.......')
```

일단 저장하고 실행해보도록 하자. 터미널을 열고 저장한 경로로 이동한 뒤, 다음을 입력하면 실행된다.

```shell
node app.js
```

![스크린샷 2020-05-15 오후 4.26.32](https://i.imgur.com/R6zQtPS.png)

서버에 추가한 봇이 온라인이 되는 것을 확인할 수 있다. 테스트로 채널에 'ping' 을 보내보았더니 답장으로 'Pong!' 이 되돌아 왔다.

![스크린샷 2020-05-15 오후 4.28.52](https://i.imgur.com/ly4ahyk.png)

출력이 어떻게 나오는지 알았으니 이제 아까 적었던 `app.js` 를 어느정도 이해할 수 있게 되었다.

아래 부분은 client, 즉 봇이 준비되었을 때 콘솔로 로그를 출력하는 부분이다. `client.user.tag` 를 이용해 봇의 이름과 태그를 출력하는 것을 알 수 있다.

```js
client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}!`);
});
```

아래 코드는 메시지 이벤트가 생길 때, msg 를 파라미터로 받은 뒤 만약 그 내용이 'ping' 이면, 그 메시지에 'Pong!' 으로 답장을 하는 코드이다.

```js
client.on('message', msg => {
  if (msg.content === 'ping') {
    msg.reply('Pong!');
  }
});
```

추가적인 정보가 [discord.js](https://discord.js.org/#/) 의 Document 에 잘 정리되어 있어 이를 참고하면서 개발하면 좋을 것이다.

![스크린샷 2020-05-15 오후 4.38.02](https://i.imgur.com/h2TmUqz.png)
