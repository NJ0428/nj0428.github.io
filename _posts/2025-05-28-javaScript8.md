---
layout: single
title: "객체 속성(Property) & 메소드(Method) 정리"
categories: javaScript
author_profile: false
toc: true
---

**자바스크립트 객체 속성과 메소드**는 데이터를 구조화하고 동작을 정의할 때 필수 개념입니다. 이번 글에서는 프로토타입 체계부터 `hasOwnProperty()`·`getter`·`setter` 등 실무에서 자주 쓰이는 기능까지 한눈에 살펴봅니다.

---

## 객체와 프로토타입 기본 개념

### 모든 객체는 `Object.prototype`을 상속합니다

자바스크립트의 모든 객체는 최상위 `Object` → `Object.prototype` 체인을 따라 **속성(property)** 과 **메소드(method)** 를 물려받습니다.

덕분에 `toString()`, `valueOf()` 같은 기본 메소드를 별도 선언 없이 사용할 수 있습니다.

```jsx
// 모든 배열 객체에 last() 메소드 추가
Array.prototype.last = function () {
  return this[this.length - 1];
};
console.log([1, 2, 3].last()); // 3
```

과도한 프로토타입 확장은 충돌 위험이 있으니 *라이브러리 내부*에서만 사용하세요.

---

## 자주 쓰이는 객체 메소드 6선

### 1. `hasOwnProperty()` — 직접 정의된 속성 판별

```jsx
function Animal(name) {
  this.name = name;
}
const dog = new Animal("Buddy");

dog.hasOwnProperty("name"); // true
dog.hasOwnProperty("toString"); // false (상속 메소드)
```

- **상속 프로퍼티** 를 거르고 객체 **자체 속성**만 확인할 때 유용합니다.

### 2. `propertyIsEnumerable()` — 열거 가능 여부 확인

```jsx
const cat = { color: "white", age: 2 };
Object.defineProperty(cat, "color", { enumerable: false });

cat.propertyIsEnumerable("color"); // false
cat.propertyIsEnumerable("age"); // true
```

- `for...in`·`Object.keys()` 순회 대상인지 즉시 판별할 수 있습니다.

### 3. `isPrototypeOf()` — 프로토타입 체인 검사

```jsx
const arr = [];
Array.prototype.isPrototypeOf(arr); // true
Object.prototype.isPrototypeOf(arr); // true
```

- 상속 구조를 디버깅하거나 타입 가드를 만들 때 활용합니다.

### 4. `Object.isExtensible()` — 새 속성 추가 가능 여부

```jsx
const user = { name: "Lee" };
Object.isExtensible(user); // true

Object.preventExtensions(user);
Object.isExtensible(user); // false
```

- 확장 금지(불변) 객체를 쉽게 확인·관리할 수 있습니다.

### 5. `toString()` — 객체 → 문자열

```jsx
[1, 2, 3].toString(); // "1,2,3"
```

- 배열·날짜·에러 객체 등에서 **디버깅용 문자열**을 빠르게 얻을 때 유용합니다.

### 6. `valueOf()` — 객체의 원시값 반환

```jsx
function Counter(n) {
  this.count = n;
}
const c = new Counter(5);

c + 1; // "[object Object]1"

Counter.prototype.valueOf = function () {
  return this.count;
};
c + 1; // 6
```

- **산술·비교 연산**에서 객체가 자연스럽게 동작하도록 커스터마이즈할 수 있습니다.

---

## Getter & Setter (접근자 프로퍼티)

### Getter — 읽기 시 실행되는 함수

```jsx
const person = { age: 20 };
Object.defineProperty(person, "koreanAge", {
  get() {
    return this.age + 1;
  },
});
console.log(person.koreanAge); // 21
```

### Setter — 쓰기 시 실행되는 함수

```jsx
const person = { age: 20 };
Object.defineProperty(person, "ageReducer", {
  set(n) {
    this.age -= n;
  },
});
person.ageReducer = 3;
console.log(person.age); // 17
```

- **데이터 은닉**·**유효성 검사**·**계산된 값** 정의에 효과적입니다.

---

## 실전 활용 & 베스트 프랙티스

1. **속성 검사**는 `hasOwnProperty()` + `Object.keys()` 조합으로 빠짐없이!
2. **열거 제어**가 필요할 땐 `Object.defineProperty()`의 `enumerable` 플래그를 적극 활용합니다.
3. **프로토타입 오염**을 방지하려면 공용 객체(`Array.prototype` 등)에 메소드를 추가할 때 네임스페이스를 명확히 하세요.
4. **불변 패턴**이 필요한 경우 `Object.preventExtensions()` · `Object.freeze()`를 사용해 의도치 않은 속성 추가·변경을 막습니다.

---

## 요약 표

| 메소드/기술                | 기능 한 줄 요약                |
| -------------------------- | ------------------------------ |
| **hasOwnProperty()**       | 직접 정의된 속성인지 판별      |
| **propertyIsEnumerable()** | 열거 가능 속성인지 확인        |
| **isPrototypeOf()**        | 프로토타입 체인 포함 여부 확인 |
| **isExtensible()**         | 새 속성 추가 가능 여부 검사    |
| **toString()**             | 객체를 문자열로 변환           |
| **valueOf()**              | 연산 시 사용할 원시값 반환     |
| **Getter / Setter**        | 읽기·쓰기 시 커스텀 로직 실행  |

---

## 질문 정리

1. **`for...in` 반복에서 상속된 속성을 제외하려면?**

   `if (obj.hasOwnProperty(key)) { ... }` 조건으로 필터링하세요.

2. **`Object.freeze()`와 `preventExtensions()`의 차이점은?**

   `freeze`는 **추가·삭제·수정** 모두 금지, `preventExtensions`는 **추가만 금지**합니다.

3. **프로토타입 메소드 추가가 왜 위험할 수 있나요?**

   서드파티 코드·브라우저 기본 API와 **이름 충돌**이 발생해 예기치 않은 버그를 유발할 수 있습니다.

4. **Getter에서 비동기 로직을 실행해도 되나요?**

   가능하지만 *동기식 접근자*가 **Promise**를 반환하면 예측이 어려워집니다. 계산 비용이 큰 경우 **메소드**를 별도 정의하세요.

5. **`valueOf()` 커스터마이즈 시 주의할 점은?**

   예상치 못한 암묵 변환을 막기 위해 **명확한 문맥**(산술·비교)에만 사용하도록 테스트를 충분히 진행하세요.
