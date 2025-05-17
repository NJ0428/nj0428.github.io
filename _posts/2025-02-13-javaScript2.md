---
layout: single
title: "자바스크립트 기본 타입"
categories: javaScript
author_profile: false
toc: true
---

웹 개발을 시작한다면 **자바스크립트 기본 타입**(JavaScript Data Types)을 확실히 이해해야 합니다. 값의 *종류* 를 정확히 알아야 변수 선언·비교·함수 인자 검증 등 모든 로직이 매끄럽게 작동하니까요. 이번 글에서는 **원시 타입**(Primitive Type) 6종과 **객체 타입**Object Type)을 한눈에 정리해 드립니다.

------

## 자바스크립트 타입 개념 살펴보기

자바스크립트에서 *타입* 은 **값이 가질 수 있는 형태**를 정의합니다.

크게 두 부류로 나뉩니다.

1. **원시 타입** – 변경 불가능(immutable)한 단일 값
2. **객체 타입** – 여러 속성·메서드를 담는 집합형 구조

타입을 올바르게 다루면 버그를 줄이고 코드 의도를 명확히 전달할 수 있습니다.

------

## 원시 타입 6가지 자세히 보기

### 1. Number — 정수·실수를 모두 포괄

```jsx
let intNum   = 10;     // 정수
let floatNum = 10.5;   // 실수
let largeNum = 10e6;   // 10,000,000
let smallNum = 10e-6;  // 0.00001
```

- **정수·실수 구분 없이** IEEE-754 64bit 부동소수점으로 저장
- 지수 표기법 지원으로 큰 수, 작은 수 모두 표현 가능

### 2. String — 문자열

```jsx
let greeting = "Hello";
let name     = 'John';
let msg      = "It's a sunny day!";
console.log(10 + " apples"); // "10 apples"
```

- 큰따옴표(`" "`), 작은따옴표(`' '`) 모두 사용
- 숫자 + 문자열 ⇒ 숫자가 **문자열로 암묵 변환**되어 연결

### 3. Boolean — 참·거짓

```jsx
let isAvailable = true;
let isEqual     = (10 === 20); // false
```

조건문, 필터링 로직 등에서 필수

### 4. Symbol (ES6 이상) — 고유 식별자

```jsx
const s1 = Symbol("id");
const s2 = Symbol("id");
console.log(s1 === s2); // false
```

- **절대 충돌하지 않는** 키로 객체 프로퍼티를 안전하게 지정
- 디버깅용 설명 문자열만 같을 뿐 실제 값은 서로 다름

### 5. undefined — 초기화되지 않은 변수

```jsx
let x;              // undefined
console.log(typeof x); // "undefined"
```

암묵 초기값이므로 의도적 미할당 상황 체크에 활용

### 6. null — “값 없음”을 명시

```jsx
let y = null;
console.log(typeof y); // "object" (역사적 이유의 버그)
```

- 개발자가 **의도적으로 비어 있음을 표현**
- `typeof` 결과가 `"object"`인 점을 주의

------

## 객체(Object) 타입 이해하기

```jsx
const car = {
  brand: "Tesla",
  model: "Model 3",
  year : 2023
};
console.log(car.brand); // "Tesla"
```

- **프로퍼티(키–값 쌍)** 와 **메서드**를 포함하는 복합 구조
- 원시 타입과 달리 **참조(Reference)** 로 전달되어, 같은 객체를 가리키는 복수 변수가 생성될 수 있습니다.

> 원시 vs 객체
>
> - *원시*: 값 자체를 복사 → 변경 불가(immutable)
> - *객체*: 참조를 복사 → 내부 속성 변경 가능

------

## typeof 연산자 활용법

```jsx
console.log(typeof 10);           // "number"
console.log(typeof "hello");      // "string"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof null);         // "object" 
console.log(typeof {name: "Lee"}); // "object"
```

- **실행 중 타입 확인** 가능 → 디버깅·유효성 검사에 유용
- `null` 은 역사적 이유로 `"object"` 를 반환하니, `value === null` 로 별도 체크!

------

## null 과 undefined 비교하기

| 연산자               | 결과    | 비고                   |
| -------------------- | ------- | ---------------------- |
| `null == undefined`  | `true`  | 느슨한 동등(값만 비교) |
| `null === undefined` | `false` | 엄격 일치(타입도 비교) |

- **동등 연산자(`==`)**: 두 값이 *비어 있음* 을 동일하게 인정
- **일치 연산자(`===`)**: 타입까지 비교하므로 서로 달라짐

------

## 요약 한눈에 보기

| 타입          | 설명                  | 예시                  |
| ------------- | --------------------- | --------------------- |
| **Number**    | 정수·실수를 모두 포함 | `10`, `10.5`, `10e6`  |
| **String**    | 문자들 집합           | `"Hello"`, `'World'`  |
| **Boolean**   | 참/거짓 값            | `true`, `false`       |
| **Symbol**    | 고유·불변 식별자      | `Symbol("id")`        |
| **undefined** | 초기화되지 않음       | `let x; // undefined` |
| **null**      | 의도적 “빈 값”        | `let y = null;`       |
| **Object**    | 키–값 집합체          | `{name:"Alice"}`      |

------

## 질문(FAQ)

### Q1. 자바스크립트 기본 타입을 왜 알아야 할까요?

**A.** 타입을 올바로 이해해야 값 비교, 함수 매개변수 처리, 오류 디버깅을 **효율적** 으로 수행할 수 있습니다.

### Q2. `typeof null` 이 `"object"` 로 나오는 이유는?

**A.** 초창기 언어 설계 버그가 남아 있습니다. 스펙을 바꾸면 기존 코드가 깨지므로 그대로 유지됩니다.

### Q3. Symbol을 언제 활용하나요?

**A.** 객체 프로퍼티 키가 **절대 충돌하면 안 되는** 라이브러리·프레임워크 내부 식별자에 주로 사용합니다.

### Q4. 원시 타입은 정말 변경 불가능한가요?

**A.** 네, 새로운 값을 할당하면 **기존 값을 복사하지 않고 교체**하기 때문에 원본 자체는 변하지 않습니다.

### Q5. undefined와 null 중 무엇을 써야 할까요?

**A.** *할당하지 않은 변수* 는 자동으로 `undefined` 가 되므로, **“값이 아직 없음”을 명시** 하고 싶을 때 `null` 을 사용하세요.
