+++
title = "스카이코인/CXO vs 파일코인/IPFS"
tags = [
    "Ask the Developers",
    "CXO",
    "Skywire",
]
bounty = 4
date = "2017-08-09"
aliases = [
	"/ko/ask-the-developers/skycoin-vs-ipfs/"
]
+++

우리는 [CXO](https://github.com/skycoin/cxo) 와 IPFS의 차이점에 대해 물어볼 수 있습니다.

파일 코인은 스카이코인 인프라의 일부와 동일한 목표를 가지고 있지만, 다른 접근 방식을 취하고 있습니다.
그들에는 3 개의 다른 프로토콜이 있습니다:

- IPLD
- IPFS
- 다중-포맷

어느 곳에,

- IPLD는 불변의 데이터 객체와 해시를 표현하는 언어입니다.
- IPFS는 파일 시스템입니다.
- 다중 포맷은 자체 기술 데이터 표준입니다.

스카이코인에서 CXO는 이 세 가지를 모두 수행합니다.

- 멀티 포맷은 CXO의 "스키마"일 뿐입니다.
- IPLD는 CXO(불변의 데이터 구조, 해시 체인, 복제, 머클 트리 등)일 뿐입니다.
- IPFS는 CXO 상위에 있는 애플리케이션 일 뿐입니다. (CXO는 변경 불가능한 객체 시스템이며 파일은 단지 객체이므로 특별한 처리가 필요하지 않습니다.)

파일코인은 "저장 증명" 방식입니다. 스카이코인은 다른 기술 접근 방식을 취하는데, 저장증명 방식이 너무 복잡하며 실제로 사용자가 원하는 것이 아니며, 실제 병목 현상이 아니라고 생각하기 때문입니다.

IPFS/IPLD/파일코인은 기존 웹 인프라와 자바 스크립트에 통합되도록 설계되었습니다. 스카이코인은 새로운 생태 시스템 de-novo([스카이와이어](https://github.com/skycoin/skywire), CXO, CX)를 구현하고 있지만, 기존 생태계에는 수학 속성이 필요하지 않기 때문에 (자바스크립트는 완벽하지 않고 브라우저마다 구현이 다르며 블록체인에 포함되거나 전체적으로 사용되지 않습니다. 기존 문제가 다시 발생할 가능성 있음).

또한 개인정보보호와 보안은 스택의 최상위 레벨에 고정될 수 없지만, 하드웨어의 모든 구성 요소를 적절하게 디자인 해야 하기 때문에 필요합니다. 스카이코인은 수학적으로 엄격하고 진보적인 접근 방식을 채택하여 자체 포함 표준 및 생태 시스템을 구현함으로써 보다 단순한 구현을 가능하게 합니다.

따라서 파일 코인은 기존 인터넷과 통합되어 가져올 수 있는 자바 스크립트 라이브러리 입니다. 스카이코인은 병렬 프로토콜과 하드웨어를 갖춘 새로운 인터넷을 갖출 것입니다.

우리가 인센티브를 위해 "저장 증명" 방식을 채택하지 않은 이유 중 하나는 그것이 블록체인 상에서 파일 저장의 종속성을 요구하고, 우리가 생각하기에 블록체인의 오버헤드 없이 파일 저장소는 이미 효율적으로 작동하고 있기 때문에, 이것은 사용자 인센티브를 위해 적절한 것이 아니라고 판단했습니다.

우리는 사용자가 코인을 충분히 넣지 않았기 때문에, 아케이드 기계처럼 간단히 종료되는 "새로운 인터넷"을 만들고 싶지 않았습니다. 우리는 사용자의 정보를 원하지 않으며, 모든 기능, 버튼 클릭, 파일 다운로드 또는 작업에 대해 비용을 지불하지 않아도 되고, 각 작업에 비용이 거의 들지 않습니다.

따라서 메이드세이프, 이더리움, 파일코인/IPFS는 모두 다른 접근 방식과 철학을 취하고 있지만 같은 방향으로 나아가고 있습니다. 범위와 기술 구현에는 상당한 차이가 있습니다.

- 이더리움은 세계의 모든 것을 하나의 블록 체인에 넣으려고합니다.(스카이코인은 코인 지불을 제외하고는 블록 체인에 거의 아무것도 넣지 않습니다. 스카이코인은 모든 토큰을 한 덩어리의 블록 체인에 넣는 대신 ERC20 토큰 버전에 대한 개별 블록 체인을 가지고 있습니다.)
- 메이드세이프는 개인 식별에 대한 최소 블록 체인입니다. (스카이코인은 글로벌 개인식별 블록체인입니다. 개인식별자는 공개 키이며 가상 값입니다.)
- 파일코인은 저장 증명 및 파일 저장에 대해서만 쓰입니다.(스카이코인은 통신 및 연산을 기본 요소로 포함하고 있으며 스카이코인의 저장 메커니즘은 블록 체인과 독립적이며 간접적으로만 수익을 창출합니다.)
- 골렘은 서버/GPU를 코인으로 시간 당 임대하는 것에 쓰입니다. (이는 비트코인을 사용하는 EC2와 동일하며 고급 네트워크의 부수 기능일 뿐입니다.)

스카이 코인 프로젝트의 문제점 중 하나는 문서와 [백서](https://www.skycoin.net/whitepapers.html)가 합의(이미 2 년 전)에 대한 작업만을 다루고 현재의 개발 작업과 생태계는 보여주지 않는다는 것입니다. 따라서 웹 사이트를 업데이트 해야 하며, 각 하위 프로젝트에 대한 새로운 백서가 필요합니다.

개발은 문서보다 훨씬 앞서 있습니다. 예를 들어 CXO용 백서는 아직 작성되지 않았지만, CXO 응용 프로그램 ([BBS](https://github.com/skycoin/bbs))은 이미 테스트되고 기본적인 기능을 사용하고 있습니다.

따라서 우리는 여전히 마케팅 및 커뮤니케이션 기존 로그를 따라잡고 있습니다.