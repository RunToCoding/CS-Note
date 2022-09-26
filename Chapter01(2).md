# Chapter 1 디자인 패턴과 프로그래밍 패러다임

---

# [1.1.5] 프록시 패턴과 프록시 서버

- 프록시 객체는 사실 디자인 패턴 중 하나인 프록시 패턴이 녹아있는 객체이다.

## 프록시 패턴

**프록시 패턴 ( Proxy pattern )**은 **대상 객체(subject)**에 접근하기 전, 그 접근에 대한 흐름을 가로채 대상 객체 앞단의 인터페이스 역할을 하는 디자인 패턴이다. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7553075f-2a08-4ef1-9c49-48bb36c56527/Untitled.png)

## 프록시 서버

**프록시 서버 ( proxy server )**는 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용 프로그램이다.

- 프록시 서버로 쓰이는 nginx
    - 비동기 에벤트 기반의 구조와 다수의 연결을 효과적으로 처리 가능한 웹 서버
    - 주로 Node.js 서버 앞단의 프록시 서버로 활용
        - 버퍼 오버플로우 취약점을 예방하기 위해 nginx를 프록시 서버 앞단에 두고, Node.js를 그 뒤에 놓는 방식
        - 익명 사용자의 직접적인 서버로의 접근을 차단하고 간접적으로 한 단계를 더 거침으로써 보안성을 더욱 강화할 수 있다.
        - 실제 포트를 숨길 수 있고 정적 자원을 gzip 압축하거나, 메인 서버 앞단에서의 로깅을 할 수 있다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49db5777-1542-41ea-9bb7-c272cffa0956/Untitled.png)
        

> **버퍼 오버플로우**: 버퍼(데이터가 저장되는 메모리 공간)가 메모리 공간을 벗어나는 경우. 이때 사용되지 않아야 할 영역에 데이터가 덮어씌워져 주소, 값을 바꾸는 공격이 발생
> 

> **gzIp 압축**: DEFLATE 알고리즘을 기반으로 한 압축 기술. 데이터 전송량을 줄일 수 있음
> 

### CloudFlare

전 세계적으로 분산된 서버가 있고 이를 통해 시스템의 콘텐츠 전달을 빠르게 할 수 있는 CDN 서비스이다.

- DDOS 공격 방어, HTTP 구축의 이점이 있다. → 웹 서버 앞단에 CLOUDFLARE를 두어 **프록시 서버**로 사용하기 때문에 가능한 것

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d262674-5281-45e2-9f26-8131e42aa5e4/Untitled.png)

- DDOS 공격 방어
    - 짧은 시간 동안 네트워크에 많은 요청을 보내 네트워크를 마비시켜 웹사이트를 공격
    - CloudFlare는 의심스러운 트래픽(사용자가 아닌 시스템으로부터 오는 트래픽)을 자동으로 차단
    - 거대한 네트워크용량과 캐싱 전략으로 DDOS 공격 방어가 가능함
- HTTPS 구축
    - 서버에서 HTTPS를 구축할 때 인증서를 기반으로 구축
    - 별도의 인증서 설치 없이 좀 더 쉽게 HTTPS를 구축할 수 있다.

### CORS와 프런트엔드의 프록시 서버

CORS(Cross-Origin Resource Sharing)은 서버가 웹 브라우저에서 리소스를 로드할 때 다른 오리진을 통해 로드하지 못하게 하는 HTTP 헤더 기반 메커니즘

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59956161-e2a4-430d-9215-77fdd11df41c/Untitled.png)

- 프런트엔드 개발 시 프런트엔드 서버를 만들어서 백엔드 서버와 통신할 때 주로 CORS 에러를 마주치는데, 이를 해결하기 위해 프런트엔드에서 프록시 서버를 만들기도 한다.
- 예시
    - 프런트엔드: 127.0.0.1:3000으로 테스팅
    - 백엔드 서버: 127.0.0.1:12010
    - → 포트번호가 달라서 CORS 에러 발생
        - 이 때 프록시 서버를 통해 프런트엔드 서버에서 요청되는 오리진을 127.0.0.1:12010 로 바꾼다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccbca1ee-1828-4cda-a636-392140926df9/Untitled.png)
        
        - 프런트엔드 서버 앞단에 프록시 서버를 놓아
        - API 요청은 users API,
        - API1 요청은 users API2
        - 에 요청할 수 있다.
        - 에러 해결 + 다양한 API 서버와의 통신도 매끄럽게 할 수 있다.

> **오리진:** 프로토콜과 호스트 이름, 포트의 조합
> 

> **127.0.0.1:** 루프백 IP, 본인 PC의 IP
> 

# [1.1.6] 이터레이터 패턴

이터레이터 패턴( Iterator patter )은 이터레이터( iterator )를 사용하여 컬렉션( collection ) 요소들에 접근하는 디자인 패턴이다.

이를 통해 순회할 수 있는 여러 가지 자료형의 구조와는 상관없이 이터레이터라는 하나의 인터페이스로 순회가 가능

```jsx
const mp = new Map()
mp.set('a', 1)
mp.set('b', 2)
mp.set('c', 3)
const st = new Set()
st.add(1)
st.add(2)
st.add(3)
for (let a of mp) console.log(a)
for (let a of st) console.log(a)
/*
[ 'a', 1 ]
[ 'b', 2 ]
[ 'c', 3 ]
1
2
3
*/
```

둘 다 다른 자료구조인 set과 map임에도 for a of b 라는 이터레이트 프로토콜을 통해 순회함.

# [1.1.7] 노출모듈 패턴

노출모듈 패턴( revealing module patter )은 즉시 실행 함수를 통해 private, public 같은 접근 제어자를 만드는 패턴

자바스크립트는 private나 public 같은 접근 제어자가 존재하지 않고 전역 범위에서 스크립트가 실행

따라서 노출모듈 패턴을 통해 private와 public 접근 제어자를 구현하기도 함

```jsx
const pukuba = (() => {
	const a = 1
	const b = () => 2
		c : 2,
		d : () => 3
	}
	return public
})()
console.log(pukuba)
console.log(pukuba.a)
// { c: 2, d: [Function: d]}
// undefined
```

a와 b는 다른 모듈에서 사용할 수 있는 변수나 함수인 private 범위를 가진다. c와 d는 다른 모듈에서 사용할 수 있는 변수나 함수이며 public 범위를 가진다.

# [1.1.8] MVC 패턴

MVC 패턴은 모델 ( Model ), 뷰 (View ), 컨트롤러 ( Controller )로 이루어진 디자인 패턴 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1ef64353-a3dc-4729-ad56-27fa40df847f/Untitled.png)

### 모델 (Model)

모델: 애플리케이션의 데이터인 데이터베이스, 상수, 변수

### 뷰 (View)

inputbox, checkbox, textarea등 인터페이스 요소를 나타냄

모델 기반으로 사용자가 볼 수 있는 화면

모델이 가지고 잇는 정보를 따로 저장하지 않고, 단순히 사각형 모양 등 화면에 표시하는 정보만 가지고 있어야함

### 컨트롤러

하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며 이벤트 등 메인 로직을 담당

모델과 뷰의 생명주기도 관리하고, 모델이나 뷰의 변경 통지를 받으면 이를 해석하여 각각의 구성요소에 해당 내용에 대해 알려준다.

### 예

- react → 가상 DOM을 통해 실제 DOM을 조작하는 것을 추상화해서 성능 향상
    - 불변성: state는 setState를 통해서만 수정이 가능하고 props를 기반으로 해서 만들어지는 컴포넌트인 pureComponent가 있다.
    - 단방향 바인딩이 적용되어 있고, 자유도가 높고, 메타(페이스북)가 운영하고 있음

# [1.1.9] MVP 패턴

MCP 패턴은 MVC 패턴으로부터 파생되었으며, MVC에서 C에 해당하는 컨트롤러가 프레젠터(presenter)로 교체된 패턴이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2ae1ead1-4ffd-4bc3-9c9b-ef4bf3659535/Untitled.png)

뷰와 프레젠터는 일대일 관계이기 때문에 MVC 패턴보다 더 강한 결합을 가진 디자인 패턴이라고 볼 수 있다.

# [1.1.10] MVVM 패턴

MVVM 패턴은 MVC의 C에 해당하는 컨트롤러가 뷰모델(view model)로 바뀐 패턴이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ebe9e98-45f9-421b-9298-f60500c7ab91/Untitled.png)

- 뷰모델은 뷰를 더 추상화한 계층이다
- MVVM 패턴은 MVC 패턴과는 다르게 커맨드와 데이터 바인딩을 가진다.
- 뷰와 뷰모델 사이의 양방향 데이터 바인딩을 지원한다.
- UI를 별도의 코드 수정 없이 재사용할 수 있고 단위 테스팅하기 쉽다는 장점이 있다.

### MVVM 패턴의 예: 뷰

- MVVM 패턴을 가진 대표적인 프레임워크는 뷰(Vue.js)가 있다.
    - 뷰는 반응형이 특징인 프런트엔드 프레임워크이며, watch와 computed 등으로 쉽게 반응형적인 값들을 구축할 수 있다.
    - 함수를 사용하지 않고 값 대입만으로도 변수가 변경되며 양방향 바인딩, html을 토대로 컴포넌트를 구축할 수 있다.
    - 재사용 가능한 컴포넌트 기반으로 UI를 구축할 수 있으며, BMW, 구글, 루이비통 등에서 사용한다.
