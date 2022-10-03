# Chapter 2 네트워크

# 2.1 네트워크의 기초

네트워크란 **노드(서버, 라우터, 스위치 등의 네트워크 장치)**와 **링크(유선 또는 무선)**가 서로 연결되어 있거나 연결되어 있지 않은 집합체를 의미한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02a38bfc-05e3-4073-a05b-411c62c4faa2/Untitled.png)

## [2.1.1] 처리량과 지연 시간

네트워크를 구축할 때는 ‘**좋은’ 네트워크**로 만드는 것이 중요하다.

- 좋은 네트워크란 **많은 처리량**을 처리할 수 있으며 **지연시간이 짧고** 장**애 빈도가 적으며** **좋은 보안**을 갖춘 네트워크

### 처리량

- 링크를 통해 전달되는 단위 시간당 데이터양
- 단위: bps(bits per second)
- 사용자들이 많이 **접속할 때마다 커지는 트래픽**, **네트워크 장치 간의 대역폭**, **네트워크 중간에 발생하는 에러**, **장치의 하드웨어 스펙**에 영향을 받는다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8da56c62-a0bc-425d-adec-e0f18223ff1c/Untitled.png)

### 지연 시간

- 요청이 처리되는 시간, 어떤 메시지가 두 장치 사이를 왕복하는 데 걸린 시간
- 매체 타입(유선, 무선), 패킷 크기, 라우터의 패킷 처리 시간에 영향을 받는다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e3bfca6-4ed5-4cd4-82f4-3bc1942b5c8e/Untitled.png)

## [2.1.2] 네트워크 토폴로지와 병목 현상

### 네트워크 토폴로지

- 노드와 링크가 어떻게 배치되어 있는 지에 대한 방식이자 연결 형태

**트리 토폴로지**

- 계층형 토폴로지라고도 하며 트리 형태로 배치한 네트워크 구성
- 노드의 추가, 삭제가 쉬우며 특정 노드에 트래픽이 집중될 때 하위 노드에 영향을 끼칠 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc6a8d2b-02eb-4c8a-8cff-9bb3ff2b5dd1/Untitled.png)

**버스 토폴로지**

- 버스 토폴로지는 중앙 통신 회선 하나에 여러 개의 노드가 연결되어 공유하는 네트워크 구성
- 근거리 통신망(LAN)에 사용된다.
- 설치비용이 적고 신뢰성이 우수하며 중앙 통신 회선에 노드를 추가하거나 삭제하기 쉽다
- 단점: 스푸핑이 가능한 문제점이 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8cb9f909-49e8-463d-9f40-bde9c95df3aa/Untitled.png)

**스타 토폴로지**

- 중앙에 있는 노드에 모두 연결된 네트워크 구성
- 노드를 추가하거나 에러를 탐지하기 쉽고 패킷의 충돌 발생 가능성이 적다.
- 어떤 노드에 장애가 발생해도 쉽게 에러 발견 가능하며,장애 노드가 중앙 노드가 아닐 경우 다른 노드에 영향을 끼치는 것이 적다.
- 단점: 중앙 노드에 장애가 발생하면 전체 네트워크를 사용할 수 없고 설치 비용이 고가이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eaeb4d0e-cee0-462f-a96f-1456eb897767/Untitled.png)

**링형 토폴리지**

- 각각의 노드가 양 옆의 두 노드와 연결하여 전체적으로 고리처럼 하나의 연속된 길을 통해 통신을 하는 망 구성 방식
- 노드에서 노드로 데이터가 이동하게 되며, 각각의 노드는 고리 모양의 길을 통해 패킷을 처림
- 노드 수가 증가되어도 너트워크상의 손실이 거의 없고 충돌이 발생되는 가능성이 적고 노드의 고장 발견을 쉽게 찾을 수 있다.
- 단점: 네트워크 구성 변경이 어렵고 회선에 장애가 발생하면 전체 네트워크에 영향을 크게 끼침

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91c2baa3-565a-4e46-b87e-2c884e14b446/Untitled.png)

**메시 토폴로지**

- 그물망처럼 연결되어있는 구조
- 한 단말 장치에 장애가 발생해도 여러 개의 경로가 존재하여 네트워크를 계속 사용할 수 있고 트래픽도 분산 처리가 가능하다.
- 노드의 추가가 어렵고 구축 비용과 운용 비용이 고가이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f55d7a2d-4ece-435c-aeac-e294ade807a8/Untitled.png)

### 병목 현상

- 토폴로지(네트워크의 구조)가 중요한 이유는 병목 현상을 찾을 때 중요한 기준이 되기 때문이다.

> **병목 현상:** 전체 시스템의 성능이나 용량이 하나의 구성 요소로 인해 제한을 받는 현상
> 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/97e99011-412f-4d54-af7b-e0c45e069d1b/Untitled.png)

→ **병목현상 발생** ⇒ 사용자가 서비스를 이용할 때 지연 시간이 길게 발생

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb88d373-2bc9-4586-a003-7936d3e28be1/Untitled.png)

→ 네트워크의 토폴로지를 확인하고 이에 맞는 서버와 서버 간 게이트웨이로 이어지는 **회선을 추가하여 병목현상 해결**

## [2.1.3] 네트워크 분류

규모를 기반으로 네트워크 분류: LAN(사무실과 개인 규모), MAN(서울시 규모), WAN(세계 규모)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/777cef6a-08cf-44ac-af0b-d836b37fdef2/Untitled.png)

- LAN: 전송 속도가 빠르지 않고 혼잡하지 않음
- MAN: 전송 속도는 평균, LAN 보다는 더 많이 혼잡
- WAN: 전송 속도는 낮으며, MAN 보다 더 혼잡

## [2.1.4] 네트워크 성능 분석 명령어

- 네트워크 병목 현상의 원인
    - 네트워크 대역폭
    - 네트우크 토폴로지
    - 서버 CPU, 메모리 사용량
    - 비효율적인 네트워크 구성
- 네트워크와 무관한 테스트를 통해 ‘네트워크로부터 발생한 문제점’인 것을 확인한 후 네트워크 성능 분석을 해봐야 한다.

**<네트워크 테스트 명령어>**

### Ping

- 네트워크 상태를 확인하려는 대상 노드를 향해 일정 크기의 패킷을 전송하는 명령어
- 해당 노드의 패킷 수신 상태와 도달하기까지의 시간, 해당 노드까지 네트워크가 잘 연결되어 있는지 확인할 수 있다.
- ping [IP 주소 or 도메인 주소]

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32026358-d1f3-4c05-8cca-dd91fd3f6b44/Untitled.png)

### Netstat

- 접속되어있는 서비스들의 네트워크 상태를 표시하는데 사용
- 네트워크 접속, 라우팅 테이블, 네트워크 프로토콜을 보여준다.
- 서비스의 포트가 열려 있는지 확인할 때 사용

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8fb7c5a-ca12-469f-ac87-8223087b08e3/Untitled.png)

### nslookup

- DNS에 관련된 내용을 확인하기 위해 사용
- 특정 도메인에 매핑된 IP를 확인하기 위해 사용

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/746bee0e-dcef-4ad9-9e17-22d96e01ca87/Untitled.png)

### tracert

- 위노우에서 tracert이고 윈도우에서 traceroute로 구동
- 목적지 노드까지 네트워크 경로를 확인할 때 사용하는 명령어
- 목적지 노드까지 구간들 중 어는 구간에서 응답 시간이 느려지는 등을 확인

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50b30337-ead4-485e-89e8-9ed2c1c051ca/Untitled.png)

## [2.1.5] 네트워크 프로토콜 표준화

네트워크 프로토콜이란 다른 장치들끼리 데이터를 주고받기 위해 설정된 공통된 인터페이스

- IEEE 또는 IETF 단체가 이를 정한다.

# [2.2] TCP/IP 4계층 모델

ㅇ인터넷에서 컴퓨터들이 서로 정보를 주고받는 데 쓰이는 프로토콜의 집합 → TCP/IP 4계층 또는 OSI 7계층 모델

### [2.2.1] 계층 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd9c3e01-eee9-409a-a5e4-6f362998542e/Untitled.png)

### 애플리케이션 계층

- 애플리케이션 계층은 FTP, HTTP, SSH, SMTP, DNS등 응용 프로그램이 사용되는 프로토콜 계층
- 웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 층

### 전송 계층

- 전송 계층은 송신자와 수신자를 연결하는 통신 서비스를 제공
- 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어를 제공
- 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때 중계 역할 진행

**TCP**

- 패킷 사이의 순서를 보장하고 연결지향 프로토콜을 사용하여 연결을 하여 신뢰성을 구축해서 수신 여부를 확인
- *가상회선 패킷 교환 방식*

**UDP**

- 순서를 보장하지 않고 수신 여부를 확인하지 않음
- *데이터그램 패킷 교환 방식*

### 가상회선 패킷 교환 방식

- 각 패킷에는 가상회선 식별자가 포함되며 모든 패킷을 전송하면 가상회선이 해제되고 패킷들은 전송된 “**순서대로**” 도착하는 방식

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cea0f80f-4284-441d-b624-cd3b078c2a71/Untitled.png)

### 데이터그램 패킷 교환 방식

- 패킷이 독립적으로 이동하며, 최적의 경로를 선택하여 가는데, 하나의 메시지에서 분할된 여러 패킷은 서로 다른 경로로 전송될 수 잇으며 도착한 “**순서가 다를 수**” 있는 방식

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/999951cd-d0f1-4d3c-b85e-84c7a7cf40b7/Untitled.png)

### TCP 연결 성립 과정

- TCP는 신뢰성을 확보할 때 ‘3-웨이 핸드쉐이크(3-way handshake)’라는 작업을 진행

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2aaa879a-5576-40e4-9b7c-06c31098ab56/Untitled.png)

1. **SYN 단계**
    1. 클라이언트는 서버에 클라이언트의 ISN을 담아 SYN을 보낸다.
        1. ISN: 새로운 TCP 연결의 첫 번째 패킷에 할당된 임의의 시퀀스 번호
        2. SYN: 연결 요청 플래그
2. **SYN + ACK 단계**
    1. 서버는 클라이언트의 SYN을 수신하고, 서버의 ISN을 보내며 승인번호로 클라이언트의 ISN + 1을 보낸다.
3. **ACK 단계**
    1. 클라이언트는 서버의 ISN + 1 한 값인 승인번호를 담아 ACK를 서버에 보낸다.
- 이 과정 이후 신뢰성이 구축되고 데이터 전송 시작
- TCP는 이 과정이 있기 때문에 신뢰성이 있는 계층이라고 하며, UDP는 이 과정이 없기 때문에 신뢰성이 없는 계층이라고 한다.

### TCP 연결 해제 과정

- 연결 해제 시에는 4-way handshake 과정이 발생.

 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c7c3c07-beb8-40ab-9821-2ef7f05e09f5/Untitled.png)

1. 먼저 클라이언트가 연결을 닫으려고 할 때, FIN으로 설정된 세그먼트를 보낸다. 
    1. FIN_WAIT_1 상태로 들어가고 서버의 응답을 기다린다.
2. 서버는 클라이언트로 ACK라는 승인 세그먼트를 보낸다.
    1. CLOSE_WAIT 상태로 들어간다.
    2. 클라이언트가 FIN_WAIT_2 상태에 들어간다.
3. 서버는 ACK를 보내고 일정 시간 이후에 클라이언트에 FIN이라는 세그먼트를 보낸다.
4. 클라이언트는 TIME_WAIT 상태가 되고 다시 서버로 ACK를 보내서 서버가 CLOSE 상태가 된다.
    1. 이후 클라이언트는 어느 정도의 시간을 대기한 후 연결이 닫히고 클라이언트와 서버의 모든 자원의 연결이 해제된다.

### 인터넷 계층

- 장치로부터 받은 네트워크 패킷을 IP 주소로 지정된 목적지로 전송하기 위해 사용되는 계층
- 패킷을 수신해야 할 상대의 주소를 지정하여 데이터 전달
- 상대방이 제대로 받았는지에 대해 보장하지 않는 비연결형적

### 링크 계층

- 전선, 광섬유, 무선 등으로 실질적으로 데이터를 전달하며 장치 간에 신호를 주고받는 ‘규칙’을 정하는 계층
- 물리 계층
    - 무선 LAN과 유선 LAN을 통해 0과 1로 이루어진 데이터를 보내는 계층
- 데이터 링크 계층
    - 이더넷 프레임을 통해 에러 확인, 흐름 제어, 접근 제어를 담당

**전이중화 통신**

- 양쪽 장치가 동시에 송수신할 수 있는 방식
- 송신로와 수신로로 나눠서 데이터를 주고받으며 현대의 고속 이더넷은 이 방식을 기반으로 통신

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/747b49af-357e-479f-b982-b769238a00ab/Untitled.png)

**CSMA/CD**

- 데이터를 보낸 이후 충돌이 발생한다면 일정 시간 이후 재전송하는 방식
- 수신로와 송신로를 각각 둔 것이 아니고 한 경로를 기반으로 데이터를 보내기 때문에 데이터를 보낼 때 충돌에 대해 대비해야함

**트위스트 페어 케이블**

- 여덟 개의 구리선을 두개씩 꼬아서 묶어 하나처럼 보이게 하는 케이블

**광섬유 케이블**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7286b9b-c097-48e2-b40e-7a76a1c3b511/Untitled.png)

### **반이중화 통신**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c092df3e-9390-43bb-a475-151c64205a67/Untitled.png)

**CSMA/CA**

- 장치에서 데이터를 보내기 전에 캐리어 감지 등으로 사전에 가능한 한 충돌을 방지하는 방식
1. 데이터를 송신하기 전에 무선 매체를 살핀다.
2. **캐리어 감지**: 회선이 비어 있는지를 판단한다.
3. **IFS(Inter FrameSpace)**: 랜덤 값을 기반으로 정해진 시간만큼 기다리며, 만약 무선 매체가 사용 중이면 점차 그 간격을 늘려가며 기다린다.
4. 이후에 데이터를 송신

**와이파이**

- 전자기기들이 무선 LAN 신호에 연결할 수 있게 하는 기술
- 무선 접속 장치가 있어야 함

**BSS**

- 기본 서비스 집합
- 단순하게 공유기를 통해 접속하는것이 아닌 동일 BSS 내에 있는 AP들과 장치들이 서로 통신이 가능한 구조

**ESS**

- 하나 이상 연결된 BSS 그룹

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66f4b4d5-d51a-4325-b082-f4fbc05bf44c/Untitled.png)

**이더넷 프레임**

- 이더넷 프레임의 구조

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72e690c9-ca35-4a03-a3c5-551c0c184cbf/Untitled.png)

- Preamble: 이더넷 프레임이 시작을 알림
- SFD: 다음 바이트부터 MAC 주소 필드가 시작됨을 알림
- DMAC, SMAC: 수신, 송신 MAC 주소
- EtherType: 데이터 계층 위의 계층인 IP 프로토콜 (ex) IPv4, IPv6
- Payload: 전달받은 데이터
- CRC: 에러 확인 비트

### 계층 간 데이터 송수신 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0feac33c-02e1-4fe1-9a94-80613d921aa8/Untitled.png)

- 애플리케이션 계층에서 전송 계층으로 필자가 보내는 요청(request)값들이 캡슐화 과정을 거쳐서 전달
- 다시 링크 계층을 통해 해당 서버와 통신
- 해당 서버의 링크 계층으로부터 애플리케이션까지 비캡슐화 과정을 거쳐 데이터가 전송

**캡슐화 과정**

- 캡슐화 과정은 상위 계층의 헤더와 데이터를 하위 계층의 데이터 부분에 포함시키고 해당 계층의 헤더를 삽입하는 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cec787e7-3c3a-4b79-b80f-8b69fcc1d15e/Untitled.png)

**비캡슐화 과정**

- 하위 계층에서 상위 계층으로 가면서 각 계층의 헤더 부분을 제거하는 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6a5587c-7f46-4b5b-aca3-f6c28cbee35f/Untitled.png)

## [2.2.2] PDU

- 네트워크의 어떤한 계층에서 계층으로 데이터가 전달될 때 한 덩어리의 단위를 PDU(Protocol Data Unit)이라고 한다.
- 구성
    - 헤더: 관련 정보들이 포함
    - 페이로드: 데이터
- 계층마다 부르는 명칭이 다름
    - 애플리케이션 계층: 메시지
    - 전송 계층: 세그먼트(TCP), 데이터그램(UDP)
    - 인터넷 계층: 패킷
    - 링크 계층: 프레임(데이터 링크 계층), 비트(물리 계층)
