+++
title = "스카이와이어와 vi스크립트"
tags = [
    "Development",
    "Skywire",
]
date = "2017-08-15"
image = "img/old-messenger.png"
aliases = [
	"/ko/skywire/skywire-and-viscript/"
]
+++
## 소개

### vi스크립트(Viscript)

[vi스크립트](https://github.com/skycoin/viscript)는 CLI 기반 크로스 플랫폼이며, 응용프로그램 런쳐이고, 이는 결국 클러스터 관리를 위해 사용된다.
이것은 시그널 서버로써 시그널 라이브러리를 기반으로 하기 때문에, 스카이와이어의 컴퍼넌트와 노드 같은 시그널 클라이언트를 관리할 수 있다.
이것은 GUI 및 헤드리스 모드에서 실행할 수 있습니다.

#### Vi스크립트 GUI 스크린 샷:

![스크린 샷](/img/viscript.jpg)

우리는 meshnet-socks-server와 같은 config.yaml 파일에 app 구성을 추가할 수 있습니다.r:

```

메쉬넷-소켓-서버r:
    daemon: true
    desc: DESCRIPTION GOES HERE
    path: bin/meshnet/meshnet-run-socks-server
    default_args: []
    help: |
        [1]  앱의 이름, 반드시 유일해야 함
        [2] 통신하는 앱의 노드 주소. ex 101.202.34.56:9000
        [3] 연결하고자 하는 목표 호스트의 소켓 서버 포트. ex 8000

        전체 명령어(예제):
            start meshnet-socks-server sockssrv0 101.202.34.56:9000 8001
```

viscript 재시작 후, 명령 앱을 사용하여 vi스크립트로 실행되는 응용 프로그램을 체크할 수 있습니다.

스크린 샷에서 볼 수 있듯이 간단한 명령어 `s`( `s apptracker 127.0.0.1:20000`)를 사용하여 앱을 시작할 수 있습니다 .

그 다음 vi스크립트는 고유한 시퀀스 ID로 시작합니다. 이 ID를 통해 우리는 커넥션 확인(`ping`), 리소스 사용량 확인(`ru`) 및 서비스 종료(`sd`)를 수행할 수 있습니다.

### 스카이와이어

[스카이와이어](https://github.com/skycoin/skywire)는 ISP에서 제어권을 얻고 사용자에게 다시 제공하는 P2P(peer-to-peer) 대체 네트워크입니다.
그 안에는 여러 구성 요소가 있습니다. 노드 관리자, 노드 및 응용 프로그램은 vpn 클라이언트, vpn 서버, 소켓 클라이언트, 소켓 서버 등의 메쉬 네트워크에서 실행됩니다.

스카이와이어 내부의 모든 구성 요소는 시그널 클라이언트로서 시그널 라이브러리를 기반으로합니다. 그래서 그들은 vi스크립트에 의해 시작, 관리 및 종료될 수 있습니다.

## 아키텍처

#### 아키텍처 다이어그램:

------

```
                                   +-----------+-------------+
           +---------------^-----+ |     vpn   |    소켓     |
           | ~에 의해 관리됨 |      +-----------+-------------+
           |               <-----+ |          노드           |
           v               |       +-------------------------+
                           <-----+ |       노드 관리자        |
+-------------------+      |       +-------------------------+
|      viscript     |      +-----+ |        메신저           |
+-------------------+--------------+-------------------------+
|                        시그널(signal)                      |
+------------------------------------------------------------+
|                         네트워크(net)                      |
+------------------------------------------------------------+
```

------

각 서비스마다 vpn 클라이언트 및 vpn 서버와 같은 클라이언트, 서버용 응용프로그램이 있습니다. 그것들은 스카이와이어 매쉬넷에서 실행됩니다.
우리가 이미 알고 있듯이, 스카이코인은 스카이와이어에서 사용되는 통화이며, 사용자가 트래픽을 전송하거나 네트워크 자원을 제공한다면 스카이코인을 받게 됩니다.
마찬가지로, 사용자가 네트워크 리소스 또는 미디어를 소비하면 Skycoin을 지불해야 합니다. 일단 요금측정 및 결제가 완료되면, 스카이와이어는 네트워크를 운영하기 위한 코인을 생성할 것입니다.

노드, 노드 관리자 및 메신저는 스카이와이어 메쉬넷의 주요 구성 요소입니다. 노드는 P2P(peer-to-peer) 메쉬 노드입니다.
서비스 응용 프로그램은 노드에 등록되고, 트래픽은 노드를 통해 전달됩니다. 노드 관리자는 매쉬넷에서 노드 사이의 경로를 관리합니다.
메신저를 사용하면 사용자가 공개키를 이용해서 클러스터와 P2P(to-peer)통신을 할 수 있습니다. 그것들은 스카이와이어 메쉬넷의 기본요소입니다.

## 요약

Vi스크립트와 스카이와이어는 여전히 많은 발전이 필요합니다. 그러나 우리는 이미 스카이코인 생태계에서 만족할 만한 성과를 달성했습니다.
그리고 우리는 앞으로의 무료 인터넷의 잠재력을 실현하는 것을 목표로 부단히 노력할 것입니다!