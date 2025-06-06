---
layout: single
title: "부동소수점·Infinity·NaN"
categories: javaScript
author_profile: false
toc: true
---

**자바스크립트 Number 객체**는 웹 개발에서 숫자를 다룰 때 꼭 이해해야 하는 핵심 개념입니다. 이 글에서는 64비트 부동소수점 구조부터 `Infinity`, `NaN`, 진법 변환, `Number` 래퍼 객체까지 **Number 객체**의 모든 것을 한눈에 정리했습니다.

---

## Number 객체란?

자바스크립트의 모든 숫자는 **64비트 부동소수점(IEEE 754)** 형식으로 저장됩니다.

| 비트 구분 | 내용           |
| --------- | -------------- |
| 1비트     | 부호(Sign)     |
| 11비트    | 지수(Exponent) |
| 52비트    | 가수(Mantissa) |

> 정수는 최대 15자리, 소수는 약 17자리까지 정확하지만, 그 이상은 오차가 발생할 수 있습니다.

```jsx
let exact = 999_999_999_999_999; // ✔ 정확
let inexact = 9_999_999_999_999_999; // ❌ 10000000000000000
```

---

## 부동소수점 정밀도와 오차 해결법

0.1 + 0.2 문제를 통해 오차를 확인해봅니다.

```jsx
let sum = 0.1 + 0.2; // 0.30000000000000004
let fix = (0.1 * 10 + 0.2 * 10) / 10; // 0.3
```

- **원인**: 2진수에서 0.1, 0.2를 정확히 표현할 수 없음
- **해결**: **정수화 → 연산 → 다시 나누기**(스케일링) 또는 `toFixed`, `BigInt`·사설 라이브러리 활용

---

## toString()으로 손쉽게 진법 변환

```jsx
const num = 256;
num.toString(2); // "100000000"  (2진수)
num.toString(8); // "400"        (8진수)
num.toString(16); // "100"        (16진수)
```

> toString(진법)은 문자열로 변환만 할 뿐, 실제 숫자 타입은 변하지 않습니다.

---

## Infinity와 NaN 제대로 이해하기

### Infinity

```jsx
10 / 0; //  Infinity
1 / Infinity; //  0
```

- 0으로 나누거나 **표현 범위**를 초과하면 무한대(`Infinity`)가 반환됩니다.

### NaN (Not-a-Number)

```jsx
100 - "text"; // NaN
0 / 0; // NaN
isNaN(NaN); // true
```

- **수학적으로 정의되지 않은 결과**
- `Number.isNaN()`을 사용하면 _암묵 변환_ 없이 정확히 검사 가능

---

## null·undefined·Number 객체 구분하기

| 값          | 의미         | `typeof` 결과 | 불리언 변환 |
| ----------- | ------------ | ------------- | ----------- |
| `null`      | “값 없음”    | `"object"`    | `false`     |
| `undefined` | “정의 안 됨” | `"undefined"` | `false`     |
| `NaN`       | 숫자 아님    | `"number"`    | `false`     |
| `Infinity`  | 무한대       | `"number"`    | `true`      |

```jsx
const a = 100; // 숫자 리터럴
const b = new Number(100); // Number 객체

typeof a; // "number"
typeof b; // "object"

a == b; // true
a === b; // false
```

> Number 객체는 래퍼 객체라서 성능·가독성 측면에서 추천되지 않습니다.

---

## 핵심 요약

- **부동소수점**: 15 ~ 17자리만 정확, 오차 발생 가능
- **진법 변환**: `num.toString(2)` 등으로 문자열 출력
- **Infinity**: 무한대, 0으로 나눌 때 등장
- **NaN**: 계산 불가능한 숫자
- **null·undefined**: “값 없음” vs “정의 안 됨”
- **Number 객체**: 특별한 경우 외엔 사용 지양

---

## 질문 정리

### Q1. 0.1 + 0.2 오차를 항상 방지하려면?

**A.** 정수 변환(스케일링)·`BigInt`·소수 지원 라이브러리를 사용하거나 `toFixed()` 등으로 보정합니다.

### Q2. `parseInt("08")`이 8이 아닌 경우가 있던데?

**A.** ES5 이전 브라우저에서 **8진수로 해석**될 수 있습니다. 반드시 `parseInt("08", 10)`처럼 **기수(10)**를 명시하세요.

### Q3. `Number.MAX_SAFE_INTEGER`의 값은?

**A.** `9 007 199 254 740 991` (2^53 − 1)로, 그 이상부터는 정수 오차가 발생합니다.

### Q4. `isNaN()`과 `Number.isNaN()`의 차이점은?

**A.** `isNaN()`은 **암묵 변환** 후 검사, `Number.isNaN()`은 **엄격 검사**(NaN만 true)로 더 안전합니다.

### Q5. `Infinity`를 비교 연산에 사용해도 괜찮나요?

**A.** 가능합니다. 모든 유한한 숫자보다 크거나 작다는 성질을 이용해 **경계값** 체크를 간단히 구현할 수 있습니다.
