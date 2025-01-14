---
date: 2021-10-15 01:40:40
layout: post
title: 객체지향의 사실과 오해
subtitle: 2. 이상한 나라의 객체
description: 2. 이상한 나라의 객체
image: https://leejaedoo.github.io/assets/img/object.png
optimized_image: https://leejaedoo.github.io/assets/img/object.png
category: object
tags:
- object
- 책 정리
paginate: true
comments: true
---

객체지향을 직관적이고 이해하기 쉬운 패러다임이라고 말하는 이유는, 객체지향이 세상을 자율적이고 독립적인 객체들로 분해할 수 있는 인간의 기본적인 인지 능력에 기반을 두고 있기 때문이다.<br>

객체지향 패러다임은 인간이 인지할 수 있는 다양한 객체들이 모여 현실 세계를 이루는 것처럼, 소프트웨어의 세계 역시 인간이 인지할 수 있는 다양한 소프트웨어 객체들이 모여 이뤄져 있다는 믿음에서 출발한다.

# 객체, 그리고 소프트웨어 세상

> 객체란, 식별 가능한 개체 또는 사물. 객체는 구별 가능한 식별자, 특징적인 행동, 변경 가능한 상태를 갖는다. 소프트웨어 안에서 객체는 저장된 상태와 실행 가능한 코드를 통해 구현된다.

객체는 `상태(State)`, `행동(Behavior)`, `식별자(Identity)`를 지닌 실체로 본다.

## 상태

행동의 결과는 과거에 어떤 행동들이 일어났었느냐에 의존한다. 인간은 행동의 과정과 결과를 단순하게 기술하기 위해 `상태`라는 개념을 고안했다.<br>
상태를 이용하면 과거에 얽매이지 않고 현재를 기반으로 객체의 행동 방식을 이해할 수 있다.

### 상태와 프로퍼티

모든 객체의 상태는 단순한 값과 객체의 조합으로 표현할 수 있다. 이 때, 객체의 상태를 구성하는 모든 특징을 통틀어 객체의 `프로퍼티(property)`라고 한다.(ex. 키, 위치 등)<br>
일반적으로 프로퍼티는 변경되지 않고 고정되는 정적 값이다. 반면, 프로퍼티 값(property value)은 시간의 흐름에 따라 변경되기 때문에 동적이다.

객체와 객체 사이의 의미있는 연결을 `링크(link)`라고 한다. 객체와 객체 사이에는 링크가 존재해야지만 요청을 보내고 받을 수 있다. 즉, 링크를 통해서만 메시지를 주고 받을 수 있다.<br>
링크는 객체가 다른 객체를 `참조`할 수 있다는 것을 의미하며, 이것은 일반적으로 한 객체가 다른 객체의 식별자를 알고 있는 것으로 표현된다.

> `상태`는 특정 시점에 객체가 가지고 있는 정보의 집합으로 객체의 구조적 특징을 표현한다. 객체의 상태는 객체에 존재하는 정적인 프로퍼티와 동적인 프로퍼티 값으로 구성된다. 객체의 프로퍼티는 단순한 값과 다른 객체를 참조하는 링크로 구분할 수 있다.

객체는 자율적인 존재로써, 다른 객체의 상태를 직접적으로 접근하거나 상태를 변경할 수 없다. 자율적인 객체는 스스로 자신의 상태를 책임져야 한다.<br>
외부의 객체가 직접적으로 다른 객체를 주무를 수 없다면, 간접적으로 객체의 상태를 변경하거나 조회할 수 있는 방법이 필요한데 이를 `행동`이라는 개념을 활용하여 접근할 수 있다.<br>
객체지향의 기본 사상은 상태와 상태를 조작하기 위한 행동을 하나의 단위로 묶는 것이다. 객체는 스스로의 행동에 의해서만 상태가 변경되는 것을 보장함으로써 객체의 자율성을 유지한다.

## 행동

### 상태와 행동

객체의 상태는 저절로 변하지 않는다. 객체가 어떠한 행동을 함으로써 상태가 변경되게 되는데 이는 행동이 `부수 효과(side effect)`를 초래한다는 것을 의미한다. 부수 효과를 이용하여 객체의 행동을 상태 변경의 관점에서 쉽게 기술할 수 있다.

객체의 행동은 객체의 상태를 변경시키지만, 행동의 결과는 객체의 상태에 의존적이다. 즉, 상태와 행동 사이에는 다음과 같은 관계가 있을 수 있다.

- 객체의 행동은 상태에 영향을 받는다.
- 객체의 행동은 상태를 변경시킨다.

### 협력과 행동

객체는 자신에게 주어진 책임을 완수하기 위해 다른 객체를 이용하고 다른 객체에게 서비스를 제공한다. 객체가 다른 객체와 협력하는 유일한 방법은 다른 객체에게 요청을 보내는 것이다.<br>
또한, 객체는 협력에 참여하는 과정에서 자기 자신의 상태뿐만 아니라 다른 객체의 상태 변경을 유발할 수 있다.

정리하면, 객체의 행동으로 인해 발생하는 결과는 두 가지 관점에서 설명할 수 있다.

- 객체 자신의 상태 변경
- 행동 내에서 협력하는 다른 객체에 대한 메시지 전송

> `행동`이란 외부의 요청 또는 수신된 메시지에 응답하기 위해 동작하고 반응하는 활동이다. 행동의 결과로 객체는 자신의 상태를 변경하거나 다른 객체에게 메시지를 전달할 수 있다. 객체는 행동을 통해 다른 객체와의 협력에 참여하므로 행동은 외부에 가시적이어야 한다.

### 상태 캡슐화

현실 세계의 객체와 객체지향 세계의 객체 사이에 차이점 중 하나는 현실 세계에서의 객체는 능동적인 객체와 수동적인 객체가 모두 존재하지만, 객체지향 세계에서의 모든 객체는 자신의 상태를 스스로 관리하는 자율적인 존재라는 것이다.<br>
여기서 캡슐화 개념이 나온다. 객체는 상태를 캡슐 안에 감춰둔 채로 외부로 노출하지 않기 때문에 외부에서 객체에 접근할 수 있는 유일한 방법은 행동을 통한 방법 뿐이다.<br>
객체의 행동을 유발하는 것은 외부로부터 전달된 메시지지만 `객체의 상태를 변경할지 여부는 객체 스스로 결정`한다.<br>
외부의 객체는 메시지를 수신하는 객체의 상태가 변경된다는 사실 조차 알지 못한다. 메시지 송신자는 단지 자신의 요구를 메시지로 포장해서 전달할 뿐이고 메시지를 해석하고 그에 반응하여 상태를 변경할지 여부는 수신자의 자율적 판단에 따른다.

상태를 외부에 노출시키지 않고 행동을 경계로 캡슐화하는 것은 결과적으로 객체의 자율성을 높인다. 자율적인 객체는 스스로 판단하고 스스로 결정하기 때문에 객체의 자율성이 높아질수록 객체의 지능도 높아진다. 지능이 높아질수록 객체 간 협력은 유연하고 간결해진다. 이것이 캡슐화를 하는 이유다.

## 식별자

객체가 식별 가능하다는 것은 객체를 서로 구별할 수 있는 특정한 프로퍼티가 객체 안에 존재한다는 것을 의미한다. 이 프로퍼티를 `식별자`라고 한다. 모든 객체는 식별자를 가지며 식별자를 이용해 객체를 구별할 수 있다.

모든 객체가 식별자를 가진다는 의미는 반대로 얘기하면 객체가 아닌 단순한 값은 식별자를 갖지 않는다는 것을 의미한다.<br>
값과 객체의 가장 큰 차이점은 값은 식별자를 갖지 않지만 객체는 식별자를 갖는다는 점이다.

`값(Value)`은 숫자, 문자열, 날짜, 시간, 금액 등과 같이 변하지 않는 양을 모델링한다. 흔히 값의 상태는 변하지 않기 때문에 불변 상태(Immutable State)를 가진다고 말한다.<br>
값이 같은 지 여부는 상태가 같은지를 이용해 판단한다. 이렇게 상태를 이용해 두 값이 같은지 판단할 수 있는 성질을 `동등성(equality)`라고 한다.

`객체`는 시간에 따라 변경되는 상태를 포함하며, 행동을 통해 상태를 변경한다. 따라서 객체는 가변 상태(Mutable State)를 가진다고 말한다. 타입이 같은 두 객체의 상태가 완전히 똑같더라도 두 객체는 독립적인 별개의 객체로 다뤄야 한다.<br>
객체는 두 객체의 상태가 다르더라도 식별자가 같다면 두 객체를 같은 객체로 판단할 수 있다. 이처럼 식별자를 기반으로 객체가 같은지를 판단할 수 있는 성질을 `동일성(Identical)`이라 한다.

# 행동이 상태를 결정한다.

객체지향 설계 시, 상태를 먼저 결정한 후 행동을 나중에 결정하는 방법으로 설계 할 경우 다음과 같은 부작용이 발생할 수 있다.

1. 상태를 먼저 결정할 경우 캡슐화가 저해된다.
   
상태에 초점을 맞출 경우 상태가 객체 내부로 캡슐화되지 못하고 외부에 노출될수 있다.

2. 객체를 협력자가 아닌 고립된 섬으로 만든다.
   
다른 객체와의 협력이 어려운 구조가 될 수 있다.

3. 객체의 재사용성을 저해한다.

객체의 재사용성은 협력에서 나오는데 2번에서와 같이 협력이 어려운 구조가 되므로 재사용성도 저하될 수 있다.

협력 안에서 객체의 행동은 결국 객체가 협력에 참여하면서 완수해야 하는 책임을 의미한다. 따라서 어떤 책임이 필요한가를 결정하는 과정이 전체 설계를 주도해야 한다.<br>
즉, `책임 주도 설계`라는 개념은 객체의 행동을 생각하도록 도움으로써 응집도 높고 재사용 가능한 객체를 만들 수 있게 한다.

> 행동이 상태를 결정한다.

# 은유와 객체

객체지향이란 현실 세계의 모방이라는 잘못된 얘기가 하나 있다. 객제지향 세계는 단순한 현실 세계의 모방으로 표현하기에는 부족한 부분들이 많다.

## 의인화

현실 속의 객체와 소프트웨어 객체 사이의 가장 큰 차이점은 현실 속에서의 객체는 수동적이었던 것이 소프트웨어 세계에서는 능동적으로 변한다는 것이다.<br>
이는 소프트웨어 객체가 현실 객체의 부분적인 특징을 모방하는 것이 아니라 현실 객체가 가지지 못한 추가적인 능력을 보유하게 됨을 의미한다.

현실의 객체보다 더 많은 일을 할 수 있는 소프트웨어 객체의 특징을 `의인화`라고 한다.

소프트웨어 안에 구축되는 객체지향 세계는 현실을 단순히 모방하는 것이 아닌 현실의 모습을 조금 참조할 뿐, 궁극적인 목적은 현실과 다른 새로운 세계를 창조하는 것이다.

## 은유

위에서 말했지만 그렇다고 객체지향 세계와 현실 세계 사이가 전혀 상관이 없는 것은 아니다. 모방이나 추상화의 수준이 아닐 뿐이지 다른 관점에서 유사성을 가지는 것이다.<br>
현실 세계와 객체지향 세계 사이의 관계를 더 정확하게 나타내는 용어로 `은유`가 있다.

은유는 객체지향 세계에서 현실 세계 객체의 이름을 그대로 사용함으로써 소프트웨어 세계의 구조를 더 쉽게 예측할 수 있는 용도로 사용되는 것이다. 

