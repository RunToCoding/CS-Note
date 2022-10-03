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


# SECTION 1.2 프로그래밍 패러다임

# [1.2.1] 선언형과 함수형 프로그래밍

> **선언형 프로그래밍(declarative Programming) :** ‘무엇’을 풀어내는가에 집중하는 패러다임, ‘프로그램은 함수로 이루어진 것이다’ 라는 명제가 담겨있는 패러다임
> 

> **함수형 프로그래밍(functional Programming)**: 선언형 패러다임의 일종, 작은 ‘**순수 함수**’들을 블록처럼 쌓아 로직을 구현하고 ‘**고차 함수**’를 통해 재사용성을 높인 프로그래밍 패러다임
> 

```jsx
const ret = [1, 2, 3, 4, 5, 11, 12]
.reduce((max, num) => num > max ? num : max, 0)
console.log(ret) // 12
```

reduce () 는 “배열”만 받아서 누적한 결과값을 반환하는 ‘**순수 함수**’ 이다. → Javascript는 함수가 **일급 객체**이기 때문에 함수형 프로그래밍 방식이 선호된다.

### 순수 함수

- 출력이 입력에만 의존하는 함수

```jsx
const pure = (a, b) => {
		return a + b
}
```

- pure 함수는 들어오는 매개변수 a, b에만 영향을 받는다.
- 만약 a, b 말고 다른 전역 변수 c가 출력에 영향을 주면 순수함수가 아니다.

### 고차 함수

- 함수가 함수를 값처럼 매개변수로 받아 로직을 생성할 수 있는 함수

---

**일급 객체 :** 고차 함수를 쓰기 위해서 해당 언어가 일급 객체여야함

- 변수나 메서드에 함수를 할당할 수 있다.
- 함수 안에 함수를 매개변수로 담을 수 있다.
- 함수가 함수를 반환할 수 있다.

```jsx
const division = function (divisionValue) {
  return function (value) {
    return value / divisionValue;
  };
};
```

- division() 함수는 나누는 값(divisionValue)을 전달받아 추후에 나뉘는 값(value)을 전달받을 때 나누기를 할 수 있도록 함수를 반환한다.

# [1.2.2] 객체지향 프로그래밍

- **객체지향 프로그래밍(OOP, Object-Oriented Programming)**
    - 데이터를 객체로 취급하여 객체 내부에 선언된 메서드를 활용하는 방식
    - 설계에 많은 시간이 소요되고, 처리 속도가 다른 프로그래밍 패러다임에 비해 상대적으로 느림

```jsx
const ret = [1, 2, 3, 4, 5, 11, 12]
class List {
		constructor(list) {
				this.list = list
				this.mx = list.reduce((max, num) => num > max ? num : max, 0)
		}
		getMax() {
				return this.mx
		}
}
const a = new List(ret)
console.log(a.getMax()) // 12
```

List라는 클래스를 만들고 a라는 객체를 만들 때 최댓값을 추출해내는 메서드를 만든 예제이다.

### 객체지향 프로그래밍의 특징

- **추상화(abstraction)**
    - 복잡한 시스템으로부터 핵심적인 개념, 또는 기능을 간추려낸 것
- **캡슐화(encapsulation)**
    - 객체의 속성과 메서드를 하나로 묶고 일부를 외부에 감추어 은닉하는 것
- **상속성(inheritance)**
    - 상위 클래스의 특성을 하위 클래스가 이어받아서 재사용하거나 추가, 확장하는 것
    - 코드의 재사용 측면, 계층적인 관계 생성, 유지 보수성에 중요
- **다형성(polymorphism)**
    - 하나의 메서드나 클래스가 다양한 방법으로 동작하는 것
    - 오버로딩, 오버라이딩

---

### 오버로딩

오버로딩은 같은 이름을 가진 메서드를 여러 개 두는 것을 말한다.

- 메서드의 타입, 매개변수의 유형, 개수 등으로 여러 개를 둘 수 있으며 컴파일 중에 발생하는 **정적** 다형성이다.

```java
class Person {
    public void eat(String a) {
        System.out.println("I eat " + a);
    }

    public void eat(String a, String b) {
        System.out.println("I eat " + a + " and " + b);
    }
}

public class CalculateArea {
    public static void main(String[] args) {
        Person a = new Person();
        a.eat("apple");
        a.eat("tomato", "phodo");
    }
}

/*
 * I eat apple
 * I eat tomato and phodo
 */
```

매개변수에 따라 다른 함수가 호출된다.

- 예를 들어 Java에서의 `println` 은 대표적인 오버로딩 메소드.
    - println의 인자값으로 int, double, boolean, String등 다양한 타입의 매개변수를 집어넣어도 콘솔 창에 매개변수 타입에 맞춰 잘 출력되는 것을 볼 수 있다.

### 오버라이딩

- 오버라이딩은 주로 메서드 오버라이딩을 말한다.
- 상위 클래스로부터 상속받은 매서드를 하위 클래스가 재정의하는 것
- 런타임중에 발생하는 동적 다형성

```java
class Animal {
    public void bark() {
        System.out.println("mumu! mumu!");
    }
}

class Dog extends Animal {
    @Override
    public void bark() {
        System.out.println("wal!!! wal!!!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.bark();
    }
}

/*
 * wal!!! wal!!!
 */
```

- 앞선 부모 클래스는 “mumu! mumu!”로 짖게 만들었지만 자식 클래스에서 “wal!!! wal!!!”로 짖게 만들었더니 자식 클래스 기반으로 메서드가 재정의 됨

## 객체 지향 프로그래밍의 설계 원칙

객체지향 프로그래밍을 설계할 때는 **SOLID 원칙**을 지켜주어야 한다.

- **단일 책임 원칙(SRP, Single Responsibility Principle)**
    - 모든 **클래스는 각각 하나의 책임**만 가져야 한다.
- **개방-폐쇄 원칙(OCP, Open Closed Principle)**
    - 유지 보수 사항이 생긴다면 **코드를 쉽게 확장**할 수 있도록 하고, 수정할 때는 닫혀 있어야한다.
    - 즉, 기존의 코드는 잘 변경하지 않으면서도 확장은 쉽게 할 수 있어야 한다.
- **리스코프 치환 원칙(LSP, Liskov Substitution Principle)**
    - 프로그램의 객체는 프로그램의 **정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어**야 한다.
- **인터페이스 분리 원칙(ISP, Interface Segregation Principle)**
    - 하나의 인터페이스보다 **구체적인 여러 개의 인터페이스**를 만들어야 하는 원칙
- **의존 역전 원칙(DIP, Dependency Inversion Principle)**
    - 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 **변하기 쉬운 것의 변화에 영향받지 않게 하는 원칙**
    - 즉, 상위 계층은 하위 계층에 변화에 대한 구현으로부터 독립해야한다.

# [1.2.3] 절차형 프로그래밍

- 로직이 수행되어야 할 연속적인 계산 과정으로 이루어짐
- 순차척인 처리를 중요하게 여기고, 프로그램 전체가 유기적으로 연결되어 있음
- 가독성이 좋으며 실행 속도가 빠름 → 계산이 많은 작업에 쓰임
- 단점: 모듈화하기가 어렵고 유지 보수성이 떨어딤

```jsx
const ret = [1, 2, 3, 4, 5, 11, 12]
let a = 0
for (let i = 0; i < ret.length; i++) {
		a = Math.max(ret[i], a)
}
console.log(a) // 12
```

자연수로 이루어진 배열에서 최댓값을 찾으라고 한다면 이와 같이 로직을 구성한다.

# [1.2.4] 패러다임의 혼합

비즈니스 로직이나 서비스의 특징을 고려해서 적절한 패러다임을 정하는 것이 좋다.

- 명령형 프로그래밍
    - 절차형 프로그래밍
    - 객체 지향 프로그래밍
- 선언형 프로그래밍
    - 함수형 프로그래밍
    

---

# 예상 질문

1. 옵저버 패턴을 어떻게 구현하나요
2. 프록시 서버를 설명하고 사용 사례에 대해 설명해주세요
3. MVC 패턴을 설명하고 MVVM 패턴과의 차이는 무엇인지 설명해보세요
