---
layout: single
title: "자바스크립트 타입 변환"
categories: javaScript
author_profile: false
toc: true
---

**자바스크립트 타입 변환**(JavaScript Type Conversion)은 값의 형태를 상황에 맞게 바꿔 주는 핵심 개념입니다. 묵시적 *형변환*(Type Coercion)과 명시적 변환을 이해하면 숫자·문자열·불리언뿐 아니라 날짜·객체까지 오류 없이 다룰 수 있습니다. 이번 글에서는 초보자도 따라 할 수 있도록 예시 코드와 함께 상세히 설명드리겠습니다.

------

## 타입 변환이란? — 데이터 형태의 유연한 변신

자바스크립트 엔진은 연산 또는 비교 시 **타입을 자동 변환**하기도 하고, 개발자가 직접 명령해 **명시적 변환**을 실행하기도 합니다. 잘못 변환하면 `NaN`, `undefined` 같은 예기치 못한 값이 튀어나오므로 동작 원리를 정확히 알아야 안정적인 코드를 작성할 수 있습니다.

------

## 묵시적 타입 변환 (Type Coercion)

묵시적 변환은 **연산자·문맥**에 따라 자동으로 일어납니다. 알아두면 디버깅 시간을 크게 줄일 수 있습니다.

### 숫자 ↔ 문자열 변환

```jsx
console.log(10 + "문자열"); // "10문자열"  → 숫자 → 문자열
console.log("3" * "5");     // 15          → 문자열 → 숫자
console.log(1 - "문자열");  // NaN         → 변환 실패
```

- `+` 연산자는 피연산자 중 하나가 문자열이면 **문자열 결합**으로 동작합니다.
- 산술 연산(, , `/`)은 숫자 변환을 시도하며, 실패 시 `NaN`(Not a Number)을 반환합니다.

### NaN 이해하기

```jsx
Number("abc");   // NaN
0 / 0;           // NaN
Math.sqrt(-1);   // NaN
```

`NaN`은 **자체와도 일치하지 않는** 독특한 값이라 `Number.isNaN()`으로만 정확히 검사할 수 있습니다.

------

## 명시적 타입 변환 — 의도를 명확히 하기

개발자가 스스로 호출하는 변환 함수·메서드입니다.

### 숫자로 변환 (Number, parseInt, parseFloat)

```jsx
Number("10");       // 10
Number(true);       // 1
parseInt("10.99");  // 10
parseFloat("10.99");// 10.99
parseInt("101", 2); // 5  (2진수)
```

- **`Number()`**: 모든 값에 적용, 실패 시 `NaN`
- **`parseInt()`**: 문자열을 *정수*로, 진법 지정 가능
- **`parseFloat()`**: 문자열을 *부동소수점*으로

### 문자열로 변환 (String, toString, 숫자 메서드)

```jsx
String(123);        // "123"
(123).toString();   // "123"
const num = 12345.6789;
num.toExponential(2); // "1.23e+4"
num.toFixed(2);       // "12345.68"
num.toPrecision(6);   // "12345.7"
```

- **`String()`** 는 어떤 값이든 변환 가능
- **`toString()`** 은 `null`, `undefined`에는 사용 불가
- 숫자 객체 메서드로 지수·고정 소수점·유효 자릿수 포맷을 손쉽게 설정

### 불리언으로 변환 (Boolean)

```jsx
Boolean(0);        // false
Boolean("");       // false
Boolean("text");   // true
Boolean(123);      // true
```

“빈 값” (`""`, `0`, `NaN`, `null`, `undefined`)은 `false`, 그 외는 `true`가 됩니다.

------

## Date 객체와 타입 변환

```jsx
String(new Date());      // "Sun May 18 2025 10:00:00 GMT+0900 ..."
new Date().getTime();    // 1747485600000 (1970-01-01 이후 밀리초)
```

- **문자열 변환**: `String()`, `toString()`으로 사람이 읽을 수 있는 형식
- **숫자 변환**: `getTime()`은 타임스탬프, `getFullYear()`·`getMonth()` 등은 부분 값 추출

------

## 타입 변환 주의사항 & 베스트 프랙티스

- **암묵 변환을 예측하기 어렵다면** 명시적 함수로 확실히 변환하세요.
- `==` 보다 `===` **(엄격 비교)**를 사용해 불필요한 형변환을 방지합니다.
- `Number.isNaN()`을 활용해 **NaN 검사를 정확히** 수행합니다.
- 문자열 연산에서 템플릿 리터럴 ( `${value}` )을 사용하면 가독성이 향상됩니다.

------

### 빠른 참고 표

| 변환 도구        | 설명                       | 예시                        |
| ---------------- | -------------------------- | --------------------------- |
| **Number()**     | 숫자로 변환, 실패 시 `NaN` | `Number("123") ⇒ 123`       |
| **parseInt()**   | 문자열 → 정수              | `parseInt("10.5") ⇒ 10`     |
| **parseFloat()** | 문자열 → 실수              | `parseFloat("10.5") ⇒ 10.5` |
| **String()**     | 어떤 값이든 문자열         | `String(true) ⇒ "true"`     |
| **toString()**   | 객체 전용 문자열 변환      | `(255).toString(16) ⇒ "ff"` |
| **Boolean()**    | Truthy/Falsy 판정          | `Boolean("") ⇒ false`       |
| **getTime()**    | Date → 밀리초 숫자         | `new Date().getTime()`      |

------

## 질문 (FAQ)

### Q1. 자바스크립트 타입 변환은 언제 자동으로 발생하나요?

`+`, `==`, 조건문 등의 **연산자·컨텍스트**에서 필요 시 자동(묵시적)으로 일어납니다.

### Q2. `parseInt("08")` 이 8이 아닌 경우가 있던데 왜 그런가요?

두 번째 인자(진법)를 지정하지 않으면 구버전 브라우저가 `0` 접두사를 8진수로 해석했습니다. **`parseInt("08", 10)`** 처럼 진법을 명시하세요.

### Q3. `null` 과 `undefined`를 문자열로 변환하면 어떻게 되나요?

`String(null)` → `"null"`, `String(undefined)` → `"undefined"`입니다. 그러나 `null.toString()` 또는 `undefined.toString()`은 오류가 납니다.

### Q4. `Boolean([])`이 왜 `true`인가요?

빈 배열·객체는 **참조형(객체)** 이라 *truthy*로 평가됩니다. 값의 유무가 아닌 **타입**이 판단 기준입니다.

### Q5. 날짜를 숫자로 변환할 때 `valueOf()`와 `getTime()`의 차이는?

`Date.valueOf()`가 내부적으로 **`getTime()`**을 호출하므로 결과가 같습니다.
