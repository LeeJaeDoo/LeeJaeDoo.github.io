---
date: 2020-07-07 18:40:40
layout: post
title: 자바 8 인 액션
subtitle: 8. 리팩토링, 테스팅, 디버깅
description: 8. 리팩토링, 테스팅, 디버깅
image: https://leejaedoo.github.io/assets/img/java8.png
optimized_image: https://leejaedoo.github.io/assets/img/java8.png
category: java
tags:
  - java
  - 책 정리
paginate: true
comments: true
---
# 가독성과 유연성을 개선하는 리팩토링
람다, 메서드 레퍼런스  스트림 등의 기능을 활용하여 가독성 좋고 유연한 코드로 리팩토링하는 방법을 설명한다.
## 코드 가독성 개선
자바8에서는 다음과 같은 기능을 통해 코드 가독성을 높일 수 있다.
* 코드의 장황함을 줄여 쉽게 이해할 수 있는 코드를 구현한다.
* 메서드 레퍼런스와 스트림 API를 이용해서 코드의 의도(코드가 무엇을 수행하려는 것인지)를 쉽게 표현할 수 있다.

## 익명 클래스를 람다 표현식으로 리팩토링하기
익명 클래스는 코드를 장황하게 만들고 쉽게 에러를 일으킬 수 있기 때문에 람다 표현식을 사용하여 간결하고 가독성을 높인다.<br>
하지만 익명 클래스를 람다 표현식으로 변환하기 위한 조건이 몇 가지 있다.
### 익명 클래스에서 사용한 this와 super는 람다 표현식에서 다른 의미를 갖는다.
익명 클래스에서 this는 익명 클래스 자신을 가라키지만 람다에서 this는 람다를 감싸는 클래스를 가리킨다.
### 익명 클래스는 감싸고 있는 클래스의 변수를 가릴 수 있다.: shadow variable
하지만 람다 표현식으로는 변수를 가릴 수 없다.
 * ex.
 
```java
int a = 10;
Runnable r1 = () -> {
    int a = 2;          //  Variable 'a' is already defined in the scope(컴파일 에러 발생)
    System.out.println(a);
};
        
Runnable r2 = new Runnable() {
    @Override
    public void run() {
        int a = 2;      //  정상 동작!
        System.out.println(a);
    }
};
```
### 익명 클래스를 람다 표현식으로 바꾸면 컨텍스트 오버로딩에 따른 모호함이 초래될 수 있다.
익명 클래스는 인스턴스화할 때 명시적으로 형식이 정해지는 반면, 람다의 형식은 컨텍스트에 따라 달라지기 때문이다.

* ex.

```java
    public interface Task {
        public void execute();
    }

    private static void doSomething(Runnable r) {
        r.run();
    }

    private static void doSomething(Task a) {
        a.execute();
    }

    doSomething(new Task() {    //  익명 클래스 : 아무런 문제 없음
        @Override
        public void execute() {
            System.out.println("Danger danger!!");
        }
    });

    /* Ambiguous method call. Both doSomething (Runnable) in Main and doSomething (Task) in Main match
       아래와 같이 람다 표현식을 구현하면 위 두 함수 중 어느것을 구현한 것인지 알 수 없게 된다. 
    */
    doSomething(() -> System.out.println("Danger danger!!"));

    //  명시적 형변환 (Task)를 이용해 모호함을 제거할 수 있다.
    doSomething((Task) () -> System.out.println("Danger danger!!"));
```
## 람다 표현식을 메서드 레퍼런스로 리팩토링하기
람다 표현식도 간결한 코드지만 대신 메서드 레퍼런스를 활용하면 좀 더 가독성을 높일 수 있다.

* 람다 표현식

```java
Map<CaloricLevel, List<Dish>> dishesByCaloricLevel = 
    menu.stream()
        .collect(
            groupingBy(dish -> {
                if (dish.getCalories() <= 400)  return CaloricLevel.DIET;
                else if (dish.getCalories() <= 700) return CaloricLevel.NORMAL;
                else    return CaloricLevel.FAT;
            })
        );
```

* 메서드 레퍼런스

```java
Map<CaloricLevel, List<Dish>> dishesByCaloricLevel = 
    menu.stream().collect(groupingBy(Dish::getCaloricLevel));

//  Dish 클래스에 getCaloricLevel 메서드를 구현해야 한다.
public class Dish {
    ...
    public CaloricLevel getCaloricLevel() {
        if (dish.getCalories() <= 400)  return CaloricLevel.DIET;
        else if (dish.getCalories() <= 700) return CaloricLevel.NORMAL;
        else    return CaloricLevel.FAT;
    }
}
```
## 명령형 데이터 처리를 스트림으로 리팩토링하기
## 코드 유연성 개선
### 함수형 인터페이스 적용
### 조건부 연기 실행
### 실행 어라운드
# 람다로 객체지향 디자인 패턴 리팩토링하기
## 전략
### 람다 표현식 사용
### 템플릿 메서드
### 람다 표현식 사용
## 옵저버
### 람다 표현식 사용하기
## 의무 체인
### 람다 표현식 사용
## 팩토리
### 람다 표현식
# 람다 테스팅
## 보이는 람다 표현식의 동작 테스팅
## 람다를 사용하는 메서드의 동작에 집중하라
## 복잡한 람다를 개별 메서드로 분할하기
## 고차원 함수 테스팅
# 디버깅
## 스택 트레이스 확인
### 람다와 스택 트레이스
## 정보 로깅
# 요약