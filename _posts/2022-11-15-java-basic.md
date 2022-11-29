---
title: OOP 개념 정리
date: 2022-11-15 +09:00
categories: [Java, OOP]
tags: [java, oop, basic]
---

# OOP

###  __추상화(Abstraction) 와 일반화__  
    : 객체(Object)의 필요 속성, 기능 등을 추출하여 단순화
 
    + 클래스(Class)  
  
### __캡슐화(Encapsulation)__  
    : 정보 은닉(information hiding)
    접근제한자(private)를 사용하여 구현부를 외부에 노출시키지 않는다.

### __상속(Inheritance)__  
    : 상위클래스의 속성을 하위클래스에서 사용, 재정의(overriding)
    일반적인 개념 -> 구체적인 개념으로 확장(extends)

    + is a, 직접적 관계

### __다형성(Polymorphism)__  
    : 하나의 변수 또는 함수가 상황에 따라 다른 결과를 나타내는 것
    조상타입으로 자손타입의 객체들을 접근 가능

# Basic

## overloading, overriding

- overriding  
: 선언부 동일, 구현부 수정
> ex. modify, change 개념
{: .prompt-info }

- overloading
: 선언부 수정, 새로운 메서드
> ex. new 개념
{: .prompt-info }

## abstract Class

선언부만 존재, 구현부가 없이 상속을 염두하고 만든 메서드

## interface

클래스에 기능을 제공하는 구조, 생성자를 가질 수 없다.
표준 제시, 다형성 개념 적용

## lambda

익명함수(Anonymous function) 생성.
> 람다식 = 매개변수를 가진 코드 블럭 = 익명(Anonymous) 내부 객체

( 매개변수 ) -> { 실행문; }  : 매개변수와 매개변수를 이용한 실행문
```java
(int x, int y) -> {return x + y;}
```

    - 매개변수가 두개 이상인 경우 괄호 생략 불가
```java
        x, y -> {System.out.println(x+y);}  // error
```

    - 매개변수가 하나인 경우 자료형과 괄호 생략 가능
```java
        x -> {System.out.println(x);}
```

    - 실행문이 한 문장인 경우 중괄호 생략 가능
```java
        x -> System.out.println(x);
```

    - 실행문이 한 문장이라도 return문(반환문)은 중괄호 생략 불가
```java
        x -> return x.length(); //error
```

    - 실행문이 한 문장의 반환문인 경우엔 return과 중괄호를 모두 생략 가능
```java
        (x, y) -> x+y;
        x -> x.length();
```
