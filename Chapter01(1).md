# 1장. 디자인 패턴과 프로그래밍 패러다임

# 1.1 디자인 패턴

> **디자인 패턴** : **프로그램을 설계할 때 발생했던 문제점**들을 **객체 간의 상호 관계 등을 이용하여 해결**할 수 있도록 하나의 **‘규약’ 형태**로 만들어 놓은 것
> 

### 1.1.1. 싱글톤 패턴

### 싱글톤 패턴 (singleton pattern)

- **하나의 클래스**에 오직 **하나의 인스턴스**만 가지는 패턴
- 하나의 인스턴스를 만들어 놓고 해당 **인스턴스를 다른 모듈들이 공유**하며 사용
- **데이터베이스 연결 모듈**에 많이 쓰임 - Node.js에서 MongoDB (mongoose 모듈), MySQL

- **싱글톤 패턴의 단점**
    - **TDD**(Test Driven Development)를 할 때 주로 하는 **단위 테스트**는 **테스트가 서로 독립적**이어야 하는데, 싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이므로 각 테스트마다 **독립적인 인스턴스를 만들기가 어려움**
    - **모듈 간의 결합을 강하게** 만들 수 있음

- **의존성 주입 (DI, Dependency Injection)**
    - 모듈 간의 결합을 조금 더 느슨하게 만들어줌
    
 ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/087d51d6-5db2-444e-89b4-0f848b1904bb/Untitled.png)
    
    - 메인 모듈이 직접 다른 하위 모듈에 대한 의존성을 주는 것이 아닌, 중간에 **의존성 주입자** (dependency injector)가 이 부분을 가로채 메인 모듈이 **간접적으로 의존성을 주입**하는 방식
    
    - **의존성 주입의 장점**
        - 모듈들을 쉽게 교체할 수 있는 구조가 되어 테스팅하기 쉽고, 마이그레이션하기도 수월함
        - 애플리케이션의 의존성 방향이 일관됨
        - 애플리케이션을 쉽게 추론할 수 있음
        - 모듈 간의 관계들이 조금 더 명확해짐
    - **의존성 주입의 단점**
        - 모듈들이 더욱더 분리되므로 클래스 수가 늘어나 복잡성이 증가될 수 있음
        - 약간의 런타임 페널티가 생기기도 함
    - **의존성 주입 원칙**
        - 상위 모듈은 **하위 모듈에서 어떤 것도 가져오지 않아야** 함. 또한, **둘 다 추상화에 의존**해야 하며, 이때 **추상화는 세부사항에 의존하지 말아야** 함

### 1.1.2 팩토리 패턴

### **팩토리 패턴** (factory pattern)

- 객체를 사용하는 코드에서 **객체 생성 부분을 떼어내 추상화**한 패턴
- 상속 관계에 있는 두 클래스에서 **상위 클래스가 중요한 뼈대를 결정**하고, **하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정**하는 패턴

- **느슨한 결합**, 더 많은 **유연성**을 가짐
- 객체 생성 로직이 따로 떼어져 있기 때문에 **유지 보수성 증가**

- 자바스크립트의 팩토리 패턴
    
    ```jsx
    const num = new Object(42)
    const str = new Object('abc')
    num.constructor.name; // Number
    str.constructor.name; // String
    ```
    
    - **전달받은 값에 따라 다른 객체를 생성**하며 인스턴스의 타입 등을 결정

### 1.1.3 전략 패턴

### **전략 패턴** (strategy pattern)

- **정책 패턴** (policy pattern) 이라고도 함
- **객체의 행위를 바꾸고 싶은 경우** 직접 수정하지 않고, **전략**이라고 부르는 ‘**캡슐화한 알고리즘**’을 컨텍스트 안에서 바꿔주면서 **상호 교체가 가능**하게 만드는 패턴

- passport의 전략 패턴
    - **passport**: Node.js에서 **인증 모듈을 구현**할 때 쓰는 미들웨어 라이브러리로, **여러 가지 전략을 기반으로 인증**할 수 있게 함
    

### 1.1.4 옵저버 패턴

### 옵저버 패턴 (observer pattern)

- 주체가 어떤 **객체의 상태 변화를 관찰**하다가 **상태 변화가 있을 때**마다 메서드 등을 통해 옵저버 목록에 있는 **옵저버들에게 변화를 알려주는** **디자인 패턴**
    - **주체**: 객체의 상태 변화를 보고 있는 **관찰자**
    - **옵저버**: 객체의 상태 변화에 따라 **추가 변화 사항이 생기는 객체**
- 주로 **이벤트 기반 시스템**에 사용
- **MVC** (Model-View-Controller) **패턴**에도 사용 - **주체**인 **모델**에서 변경 사항이 생겨 **옵저버**인 **뷰**에 알려주고, 이를 기반으로 **컨트롤러**가 작동

- 자바스크립트에서의 옵저버 패턴
    - 프록시 객체를 통해 구현 가능
        - **프록시(proxy) 객체**: 어떠한 **대상의 기본적인 동작** (속성 접근, 할당, 순회, 열거, 함수 호출 등)의 **작업을 가로챌 수 있는 객체**
        - 두 개의 매개변수 - **target**: **프록시할 대상**, **handler**: 프록시 객체의 target 동작을 가로채서 **정의할 동작들이 정해져 있는 함수**
        
        ```jsx
        const handler = {
        	get: function(target, name) {
        		return name === 'name' ? `${target.a} ${target.b}` : target[name]
        	}
        }
        const p = new Proxy({a: 'KUNDOL', b: 'IS AUMUMU ZANGIN'}, handler)
        console.log(p.name) // KUNDOL IS AUMUMU ZANGIN
        ```
        
        - `new Proxy`로 선언한 객체의 `a`와 `b`라는 속성에 특정 문자열을 담아서 `handler`에 “name이라는 속성에 접근할 때는 a와 b라는 것을 것을 합쳐서 문자열을 만들어라.” 를 구현
        - `p.name`으로 `name` 속성에 접근하려고 할 때, 그 부분을 가로채 문자열을 만들어 반환
        
- Vue.js 3.0의 옵저버 패턴
    - `ref`나 `reactive`로 정의하면 해당 값이 변경되었을 때 자동으로 DOM에 있는 값이 변경됨