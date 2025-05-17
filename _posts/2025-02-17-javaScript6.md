---
layout: single
title: "자바스크립트 프로퍼티·메소드 활용법"
categories: javaScript
author_profile: false
toc: true
---

웹 애플리케이션의 데이터와 로직을 구조화하려면 **자바스크립트 객체**(JavaScript Object)를 제대로 이해해야 합니다. 객체는 *프로퍼티*와 *메소드*를 묶어 실생활 사물처럼 표현하기 때문에, 유지보수성과 재사용성을 높이는 핵심 도구입니다.

------

## 객체(Object)란 무엇인가요?

### 이름·값 쌍으로 이뤄진 프로퍼티의 집합

자바스크립트 객체는 **이름(name)** 과 **값(value)** 으로 이뤄진 **프로퍼티**를 모아 놓은 자료형입니다. 여기에 **메소드**(메소드 = 프로퍼티에 저장된 함수)를 추가해 동작까지 묶을 수 있습니다.

```jsx
const cat = {
  name: "나비",
  family: "코리안 숏 헤어",
  age: 0.1,
  weight: 300,
  mew()  { console.log("야옹!"); },
  eat()  { console.log("맛있다!"); }
};

console.log(cat.name); // 나비
cat.mew();             // 야옹!
```

### 자바스크립트에서 객체가 차지하는 비중

숫자·문자열·불리언·`undefined`를 제외한 **모든 값이 객체**이며, 원시 타입도 필요 시 *래퍼 객체*로 변환돼 메소드(`length`, `toString()` 등)를 사용할 수 있습니다.

------

## 프로퍼티 다루기: 점 표기법 vs 대괄호 표기법

| 표기법            | 사용 예         | 특징                   |
| ----------------- | --------------- | ---------------------- |
| **점 표기법**     | `person.name`   | 코딩 가독성이 높다     |
| **대괄호 표기법** | `person["age"]` | 변수를 키로 쓸 때 유용 |

```jsx
const person = { name: "홍길동", age: 30 };
console.log(person.name);      // 홍길동
console.log(person["age"]);    // 30
```

> Tip: 공백·특수문자가 포함된 키는 대괄호 표기법을 사용하세요.

------

## 메소드와 this 키워드 이해하기

### 객체 내부 함수 = 메소드

메소드는 객체에 저장된 함수이며, 내부에서 `this`는 **메소드를 호출한 객체**를 가리킵니다.

```jsx
const student = {
  name: "이영희",
  grade: 3,
  study(subject) {
    console.log(`${this.name} 학생이 ${subject}를 공부합니다.`);
  }
};

student.study("수학"); // 이영희 학생이 수학을 공부합니다.
```

- 괄호`()`를 붙여야 실행됩니다.
- 괄호 없이 `student.study`를 콘솔에 찍으면 **함수 객체** 자체를 반환합니다.

------

## 객체 생성·활용 베스트 프랙티스

### 1. 객체 리터럴을 우선 사용

간결하고 가독성이 높습니다.

```jsx
const user = { id: 1, name: "Alice" };
```

### 2. 생성자 함수·클래스(ES6) 활용

동일 구조의 객체를 여러 개 만들 땐 **클래스**가 유지보수에 유리합니다.

```jsx
class Car {
  constructor(brand, model){
    this.brand = brand;
    this.model = model;
  }
  drive(){ console.log(`${this.brand} 주행 중`); }
}

const myCar = new Car("Tesla", "Model 3");
myCar.drive(); // Tesla 주행 중
```

### 3. 프로퍼티·메소드 분리로 가독성 확보

객체 선언부가 길어질 땐 **메소드 분리** 혹은 모듈화로 코드를 정리하세요.

------

## 원시 값도 객체처럼? — 래퍼(Wrapper) 객체

```jsx
const num = 123;
console.log(num.toString()); // "123"
```

- 숫자 리터럴 `num`이 *Number 객체*로 일시 래핑되어 메소드를 호출합니다.
- 호출 후 즉시 사라지므로 **성능 이슈**는 걱정하지 않아도 됩니다.

------

## FAQ:  질문

1. **객체와 배열의 차이는 무엇인가요?**

   배열은 *순서가 있는 값 집합*이며, 객체는 *키–값 쌍 집합*입니다. 배열 역시 객체의 한 종류이지만, 길이(`length`)와 인덱스 기반 메소드가 추가된 특수 형태입니다.

2. **`this`가 `window`를 가리키는 이유는?**

   **메소드가 아닌** 일반 함수로 호출하면 전역 객체(`window`/`global`)가 `this`가 됩니다. `use strict` 모드에서는 `undefined`가 됩니다.

3. **프로퍼티를 동적으로 추가·삭제할 수 있나요?**

   가능합니다. `obj.newKey = value` 로 추가, `delete obj.key` 로 삭제할 수 있습니다.

4. **객체 비교(`===`)가 항상 false인 이유는?**

   두 객체는 **메모리 주소(참조)**를 비교하므로, 내용이 같아도 다른 주소면 `false`입니다. 내용을 비교하려면 *깊은 비교* 로직이 필요합니다.
