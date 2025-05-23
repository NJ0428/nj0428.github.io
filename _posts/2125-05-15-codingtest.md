---
layout: single
title: "분수 계산"
categories: codingtest
author_profile: false
sidebar:
  nav: "docs"
---

# 분수 계산

### **💡 Java서 분수(유리수) 계산 정리**

Java는 기본적으로 **정수형(int, long) 연산은 정수로, 실수형(double, float) 연산은 실수로 처리**합니다.

분수를 다루려면 **기본 연산 방법, 최대공약수(GCD) 활용, 기약분수 변환**을 이해해야 합니다.

---

## **🔹 1. 기본적인 분수 연산**

### ✅ **(1) 분수의 덧셈, 뺄셈, 곱셈, 나눗셈 공식**

1. **덧셈(A/B + C/D)**

   ```java
   (A * D + B * C) / (B * D)
   ```

2. **뺄셈(A/B - C/D)**

   ```java
   (A * D - B * C) / (B * D)
   ```

3. **곱셈(A/B × C/D)**

   ```java
   (A * C) / (B * D)
   ```

4. **나눗셈(A/B ÷ C/D)**

   ```java
   (A * D) / (B * C)
   ```

---

## **🔹 2. Java 코드 구현**

### **(1) 분수 연산 함수 만들기**

```java
import java.util.Scanner;

class FractionCalculator {
    // 최대공약수(GCD) 계산 - 분수 기약분수 변환에 사용
    private static int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // 분수 덧셈
    public static int[] addFractions(int num1, int den1, int num2, int den2) {
        int numerator = num1 * den2 + num2 * den1; // 분자 계산
        int denominator = den1 * den2; // 분모 계산
        return simplifyFraction(numerator, denominator); // 기약분수 변환
    }

    // 분수 뺄셈
    public static int[] subtractFractions(int num1, int den1, int num2, int den2) {
        int numerator = num1 * den2 - num2 * den1;
        int denominator = den1 * den2;
        return simplifyFraction(numerator, denominator);
    }

    // 분수 곱셈
    public static int[] multiplyFractions(int num1, int den1, int num2, int den2) {
        int numerator = num1 * num2;
        int denominator = den1 * den2;
        return simplifyFraction(numerator, denominator);
    }

    // 분수 나눗셈
    public static int[] divideFractions(int num1, int den1, int num2, int den2) {
        int numerator = num1 * den2;
        int denominator = den1 * num2;
        return simplifyFraction(numerator, denominator);
    }

    // 분수 기약분수 변환 (최대공약수 사용)
    public static int[] simplifyFraction(int numerator, int denominator) {
        int gcdValue = gcd(Math.abs(numerator), Math.abs(denominator)); // 절댓값으로 GCD 계산
        numerator /= gcdValue;
        denominator /= gcdValue;

        // 음수가 분모에 있으면 분자로 이동
        if (denominator < 0) {
            numerator = -numerator;
            denominator = -denominator;
        }
        return new int[]{numerator, denominator};
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // 사용자 입력
        System.out.print("첫 번째 분수의 분자 입력: ");
        int num1 = scanner.nextInt();
        System.out.print("첫 번째 분수의 분모 입력: ");
        int den1 = scanner.nextInt();

        System.out.print("두 번째 분수의 분자 입력: ");
        int num2 = scanner.nextInt();
        System.out.print("두 번째 분수의 분모 입력: ");
        int den2 = scanner.nextInt();

        // 연산 수행
        int[] sum = addFractions(num1, den1, num2, den2);
        int[] diff = subtractFractions(num1, den1, num2, den2);
        int[] product = multiplyFractions(num1, den1, num2, den2);
        int[] quotient = divideFractions(num1, den1, num2, den2);

        // 결과 출력
        System.out.println("덧셈 결과: " + sum[0] + "/" + sum[1]);
        System.out.println("뺄셈 결과: " + diff[0] + "/" + diff[1]);
        System.out.println("곱셈 결과: " + product[0] + "/" + product[1]);
        System.out.println("나눗셈 결과: " + quotient[0] + "/" + quotient[1]);

        scanner.close();
    }
}
```

---

## **🔹 3. 실행 예시**

### ✅ **입력**

```
첫 번째 분수의 분자 입력: 1
첫 번째 분수의 분모 입력: 2
두 번째 분수의 분자 입력: 1
두 번째 분수의 분모 입력: 3
```

### ✅ **출력**

```
복사편집
덧셈 결과: 5/6
뺄셈 결과: 1/6
곱셈 결과: 1/6
나눗셈 결과: 3/2
```

---

## **🔹 4. 주요 개념 요약**

| 개념                           | 설명                                          |
| ------------------------------ | --------------------------------------------- |
| `gcd(a, b)`                    | 최대공약수를 구해서 분수를 기약분수로 변환    |
| `addFractions(A/B + C/D)`      | `(A*D + B*C) / (B*D)`                         |
| `subtractFractions(A/B - C/D)` | `(A*D - B*C) / (B*D)`                         |
| `multiplyFractions(A/B × C/D)` | `(A*C) / (B*D)`                               |
| `divideFractions(A/B ÷ C/D)`   | `(A*D) / (B*C)`                               |
| `simplifyFraction(n, d)`       | `n`과 `d`를 최대공약수로 나눠 기약분수로 변환 |

---

## **✅ 최종 정리**

- **덧셈**: `(A * D + B * C) / (B * D)`
- **뺄셈**: `(A * D - B * C) / (B * D)`
- **곱셈**: `(A * C) / (B * D)`
- **나눗셈**: `(A * D) / (B * C)`
- **최대공약수(GCD)를 사용하여 기약분수 변환**
- **음수 처리: 분모가 음수일 경우 부호를 조정**
