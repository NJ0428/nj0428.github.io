---
layout: single
title: "자바스크립트 객체 생성 방법"
categories: javaScript
author_profile: false
toc: true
---

**자바스크립트 객체 생성** 패턴을 정확히 알면 데이터 구조 설계·상속 체계를 한층 깔끔하게 만들 수 있습니다. 이번 글에서는 **리터럴 표기**, **생성자(new)**, **`Object.create()`** 세 가지 핵심 방식을 예제와 함께 비교 정리합니다.

------

## 객체 생성이 중요한 이유

자바스크립트 애플리케이션은 대부분 **객체(Object)** 중심으로 동작합니다. 객체를 *어떻게 만드느냐*에 따라

- **코드 재사용성**과 **유지보수성**
- 상속(프로토타입 체인) 설계 난이도
- 메모리 사용량 및 실행 성능

이 달라집니다. 따라서 **자바스크립트 객체 생성 방법**을 상황에 맞게 선택해야 합니다.

------

## 리터럴 표기(Literal Notation)로 빠르게 생성

### 문법 & 특징

```jsx
const kitty = {
  name: "나비",
  family: "코리안 숏 헤어",
  age: 1,
  weight: 0.1
};
```

- **가장 간결·직관적**인 방법
- 코드 한 줄로 **데이터 구조**를 즉시 정의
- 초기화 후 프로퍼티·메소드 추가‧삭제 가능

### 언제 쓰면 좋을까?

- JSON과 유사한 **단순 데이터 묶음**
- 앱 초기 설정, 임시 객체 등 **1회성** 구조

------

## new 연산자를 이용한 생성자(Constructor)

### 1. 내장(built-in) 생성자

```jsx
const today = new Date();
console.log(today.getFullYear()); // 2025
```

- `Date`, `String`, `Number` 등 **런타임 제공**
- **유틸리티 메소드**가 이미 포함되어 편리

### 2. 사용자 정의 생성자 함수

```jsx
function Cat(name, family, age, weight){
  this.name   = name;
  this.family = family;
  this.age    = age;
  this.weight = weight;
}

const kitty = new Cat("나비", "코리안 숏 헤어", 1, 0.1);
```

### 장점

- **템플릿**처럼 동형 객체를 무한 생성
- 프로토타입에 메소드를 추가해 **메모리 절약**

### 단점

- `new` 없이 호출 시 `this` 바인딩 오류 발생
- 클래스 문법(ES6 `class`)을 함께 이해해야 가독성↑

------

## Object.create()로 명확한 상속 설계

### 기본 문법

```jsx
const animal = {
  type: "포유류",
  sound(){
    console.log("동물이 소리를 냅니다.");
  }
};

const dog = Object.create(animal, {
  name : { value: "멍멍이",     enumerable: true },
  breed: { value: "리트리버",   enumerable: true }
});

dog.sound();           // 동물이 소리를 냅니다.
console.log(dog.type); // 포유류 (상속)
```

### 특징 한눈에

- 첫 인자로 **프로토타입 객체**를 명시
- 두 번째 인자로 **프로퍼티 서술자**(열거 가능 여부 등) 지정
- 클래스 없이도 **깔끔한 상속 구조** 구현

> Tip
>
> 라이브러리·프레임워크 내부에서 믹스인, 객체 풀(Factory) 패턴을 구현할 때 유용합니다.

------

## 생성 방법 비교 & 선택 가이드

| 방법                   | 핵심 장점                 | 주 사용 사례                 |
| ---------------------- | ------------------------- | ---------------------------- |
| **리터럴 표기**        | 빠르고 간단               | 설정 객체, JSON-like 데이터  |
| **내장 생성자**        | 풍부한 내장 메소드        | 날짜, 숫자 포맷팅 등         |
| **사용자 정의 생성자** | 대량의 동일 구조 생성     | 도메인 엔티티(회원, 상품)    |
| **Object.create()**    | 프로토타입 명시·상속 편리 | 프레임워크 핵심 로직, 믹스인 |

**결론**

- **단일·단순 객체** → *리터럴*
- **재사용 가능한 템플릿** → *생성자(new)* 또는 `class`
- **상속 체계가 중요한 설계** → `*Object.create()*`

------

## 요약

1. **리터럴 표기**: 가장 직관적, 1회성 데이터에 최적.
2. **생성자 함수(new)**: 반복 생성·템플릿 패턴에 강력.
3. **Object.create()**: 프로토타입 체인을 정밀 제어.

각 기법을 프로젝트 규모·유형에 맞춰 조합하면 **유연하고 효율적인 객체 구조**를 구축할 수 있습니다.

------

## 질문 정리

1. **리터럴로 만든 객체를 나중에 프로토타입 체인에 넣을 수 있나요?**

   가능합니다. `Object.setPrototypeOf(obj, proto)`로 동적으로 변경할 수 있지만, 성능 저하를 유발할 수 있어 초기 설계 단계에서 프로토타입을 잡는 편이 좋습니다.

2. **`class` 문법은 생성자 함수와 완전히 다른가요?**

   `class`는 **문법적 설탕(Syntactic Sugar)** 입니다. 내부적으로는 프로토타입 기반이며, 생성자 함수와 동등한 기능을 제공합니다.

3. **`Object.create(null)`을 쓰면 어떤 이점이 있나요?**

   최상위 프로토타입(`Object.prototype`)을 제거해 **완전한 딕셔너리**를 만들 수 있습니다. `hasOwnProperty` 충돌을 피할 수 있어 해시 테이블처럼 활용됩니다.

4. **객체를 복사할 때 각 방법이 영향을 미치나요?**

   모든 방식으로 만든 객체는 **얕은 복사** 시 프로퍼티 참조를 공유합니다. 깊은 복사가 필요하면 `structuredClone()` 또는 라이브러리를 사용하세요.
