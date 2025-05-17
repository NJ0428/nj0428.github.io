---
layout: single
title: "자바스크립트 객체 다루기"
categories: javaScript
author_profile: false
toc: true
---

# 자바스크립트 객체 다루기 완벽 가이드

웹 애플리케이션의 핵심 자료형 **자바스크립트 객체 다루기**(JavaScript Object Handling)는 “데이터 + 동작”을 하나로 묶어 코드의 **재사용성**·**유지보수성**을 높여 줍니다. 이번 글에서는 `this` 키워드부터 프로퍼티 삭제·순회·비교까지 실무에 바로 쓰이는 팁을 정리했습니다.

------

## this 키워드 이해하기

`this` 는 *함수가 실행되는 맥락* 에 따라 가리키는 대상이 바뀝니다.

- **메서드 내부** → 메서드를 소유한 객체
- **생성자 함수** → 새로 생성되는 인스턴스
- **전역 컨텍스트** → 브라우저에선 `window`, Node.js에선 `global`

```jsx
function Dog(name){
  this.name = name;
}
const myDog = new Dog("마루");
console.log(myDog.name); // "마루"
```

> Tip : 화살표 함수는 자신만의 this 를 갖지 않으므로, 메서드로 사용할 때 주의하세요.

------

## 프로퍼티 삭제하기 – `delete`

객체에 더 이상 필요 없는 값이 있다면 **`delete`** 로 이름까지 제거합니다.

```jsx
const puppy = { color: "흰색", name: "마루", age: 1 };
delete puppy.age;
console.log(puppy.age); // undefined
```

- 삭제된 키는 **열거**에서도 제외됩니다.
- 배열 요소에 `delete`를 쓰면 *빈 칸*만 남으므로, **`splice()`** 가 더 안전합니다.

------

## 객체 프로퍼티를 효율적으로 순회

| 메서드                             | 반환값 | 특징                     |
| ---------------------------------- | ------ | ------------------------ |
| **`for...in`**                     | key    | 상속·열거 가능한 모든 키 |
| **`Object.keys()`**                | 배열   | *자신* 의 열거 가능한 키 |
| **`Object.getOwnPropertyNames()`** | 배열   | 열거 불가 포함 *모든* 키 |

```jsx
const pet = { color: "흰색", name: "마루", age: 1 };
Object.defineProperty(pet, "color", { enumerable: false });

console.log(Object.keys(pet));              // ["name", "age"]
console.log(Object.getOwnPropertyNames(pet)); // ["color", "name", "age"]
```

> Checklist
>
> - JSON 직렬화 전에는 열거 불가 프로퍼티가 제외됩니다.
> - 키·값을 함께 필요할 땐 **`Object.entries()`** 를 활용하세요.

------

## `Object.defineProperty()`로 속성 제어

프로퍼티를 추가하거나 **열거 가능(enumerable)**·**쓰기 가능(writable)**·**재정의 가능(configurable)** 속성을 세밀하게 설정합니다.

```jsx
const dog = {};
Object.defineProperty(dog, "name", {
  value: "마루",
  enumerable: false,
  writable: true
});
console.log(Object.keys(dog)); // []
console.log(dog.name);         // "마루"
```

- 라이브러리 내부 **비공개 속성** 구현 시 유용
- 다수의 프로퍼티는 **`Object.defineProperties()`** 로 일괄 정의

------

## 객체 비교와 레퍼런스 관리

```jsx
const dog1 = { name: "마루" };
const dog2 = { name: "마루" };

console.log(dog1 === dog2); // false – 주소 다름
const dog3 = dog1;
console.log(dog1 === dog3); // true  – 같은 참조
```

- **`===`** 비교는 *메모리 참조* 를 검사합니다.
- 내용 비교가 필요하면 **깊은 비교**(deep equal) 라이브러리를 사용하거나, `JSON.stringify()` 후 문자열을 비교하세요.

------

## 실전에서 객체 다루기를 안전하게 하는 법

1. **`this` 컨텍스트** 확인 → 이벤트 핸들러에선 `bind` / 화살표 함수를 적재적소에 사용
2. **프로퍼티 상태** 점검 → `delete` 대신 값 `null` / `undefined` 할당이 더 빠를 때도 있음
3. **열거 가능 여부** 설정 → 내부 API용 속성은 `enumerable:false`
4. **참조 복사 주의** → 얕은 복사 시 불변 업데이트 패턴(스프레드, `structuredClone`) 활용

------

## 질문(FAQ)

1. **`this`가 `undefined`로 찍히는 이유는?**

   strict mode에서 일반 함수 호출 시 `this`가 전역 객체가 아닌 `undefined`가 됩니다.

2. **왜 `for...in` 대신 `Object.keys()`를 권장하나요?**

   상속받은 프로퍼티까지 순회하면 예상치 못한 키가 포함돼 버그가 생길 수 있습니다.

3. **프로퍼티를 읽기 전용으로 만들 수 있나요?**

   `Object.defineProperty(obj, "key", { writable:false })`로 설정하면 됩니다.

4. **객체를 깊은 복사할 때 가장 간단한 방법은?**

   최신 브라우저·Node ≥17이라면 `structuredClone(obj)`를 추천드립니다.

5. **`Object.freeze()`와 `defineProperty()`의 차이점은?**

   `freeze`는 객체 전체를 *불변*으로, `defineProperty`는 개별 프로퍼티를 세밀하게 제어합니다.
