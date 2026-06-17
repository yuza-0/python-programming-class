# Week13

## 이번 주 큰 흐름
- OOP and Programming Paradigm
- OOP Details
    - Abstraction (추상화) : Class and Instance
    - Encapsulation (and Data Hiding)
    - Inheritance (상속)
    - Polymorphism (다형성)
- Exception
    - Debug: Error and Exception
    - Exception 처리
- Stack
- Queue

- 과제
- 윤성우의 열혈 파이썬 14

  ---

  # Week13

## 이번 주 큰 흐름

* OOP and Programming Paradigm

* OOP Details

  * Abstraction (추상화) : Class and Instance
  * Encapsulation (캡슐화) and Data Hiding
  * Inheritance (상속)
  * Polymorphism (다형성)

* Exception

  * Debug : Error and Exception
  * Exception 처리

* Stack

* Queue

* 과제

* 윤성우의 열혈 파이썬 14

# 1. OOP and Programming Paradigm

## 1.1 Programming Paradigm

프로그래밍 패러다임이란 프로그램을 어떻게 바라보고, 어떻게 구성할 것인지에 대한 사고 방식이다.

대표적인 프로그래밍 패러다임에는 다음이 있다.

* Structured Programming
* Object Oriented Programming
* Functional Programming

## 1.2 OOP란?

OOP는 **Object Oriented Programming**의 약자이다.

즉, 객체 지향 프로그래밍을 의미한다.

OOP는

* Object에 기반하여
* Object를 이용하고
* Object를 만들고
* Object들을 조합하여

프로그램을 구성하는 프로그래밍 패러다임이다.

즉, 프로그램을 단순한 명령어의 나열이 아니라 **객체들의 상호작용**으로 보는 방식이다.

## 1.3 OOP의 핵심 관점

OOP에서는 현실 세계의 대상을 프로그램 안에서 객체로 표현한다.

예를 들어

```text
강아지
```

라는 대상을 프로그램에서 표현한다면

```text
상태 : 이름, 나이, 색깔
동작 : 짖기, 걷기, 먹기
```

처럼 나눌 수 있다.

이를 코드로 표현하면

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print("멍멍")
```

## 1.4 OOP Language가 되기 위한 조건 (⭐ 중요)

어떤 언어가 OOP 언어라고 불리려면 최소한 다음 3가지 특성을 가져야 한다.

* Encapsulation
* Inheritance
* Polymorphism

추가로 OOP를 이해하기 위해서는 Abstraction도 중요하다.

따라서 OOP의 핵심 개념은 보통 다음과 같이 정리한다.

```text
Abstraction
Encapsulation
Inheritance
Polymorphism
```

# 2. Abstraction

## 2.1 Abstraction의 의미

Abstraction은 추상화를 의미한다.

한자로 보면

```text
抽 : 뽑아낼 추
像 : 모양 상
```

즉, 추상화란 어떤 대상으로부터 **필요한 특징만 뽑아내는 것**이다.

## 2.2 프로그래밍에서의 추상화

프로그래밍에서 추상화란 복잡한 대상을 그대로 표현하는 것이 아니라, 문제 해결에 필요한 핵심 특징만 뽑아 단순화하는 것이다.

즉,

```text
복잡한 현실 대상 → 필요한 특징만 선택 → 코드로 표현
```

하는 과정이다.

예를 들어 사람을 표현한다고 해서 모든 정보를 다 넣을 필요는 없다.

```text
이름
나이
직업
걷기
말하기
```

처럼 현재 문제에 필요한 정보만 뽑아낸다.

## 2.3 OOP에서의 추상화

OOP에서 추상화는 대상을 Class로 정의하는 것이다.

즉,

```text
어떤 대상 → 필요한 특징 추출 → Class로 표현
```

하는 과정이다.

OOP에서 대상의 특징은 크게 두 가지로 나뉜다.

* Attribute
* Behavior

## 2.4 Attribute and Behavior (⭐ 중요)

OOP에서 Object의 특징은 다음과 같이 나눌 수 있다.

```text
Attribute = Data = State = Field = Member Variable
Behavior = Operation = Method = Member Function
```

예를 들어 강아지 객체를 생각하면

```text
Attribute : 이름, 나이, 색깔
Behavior : 짖기, 걷기, 먹기
```

이다.

Python 코드로 표현하면 다음과 같다.

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        print("멍멍")
```

여기서

```python
self.name
self.age
```

는 attribute이고,

```python
bark()
```

는 method이다.

## 2.5 Class란?

Class는 표현 대상에 대한 추상화의 결과물이다.

즉, Class는 어떤 Object가 가져야 할

* data
* behavior

를 정의한 type 또는 template이다.

정리하면 다음과 같다.

```text
Class = concept = type = template
```

예를 들어

```python
class Dog:
    pass
```

는 Dog라는 새로운 type을 정의한 것이다.

## 2.6 Instance란?

Instance는 Class가 실제로 메모리에 생성되어 사용할 수 있는 상태가 된 것이다.

즉,

```text
Class → Instance 생성
```

이다.

예시는 다음과 같다.

```python
class Dog:
    pass

d1 = Dog()
d2 = Dog()
```

여기서

```python
Dog
```

는 class이고,

```python
d1
d2
```

는 Dog class로부터 생성된 instance이다.

## 2.7 Class vs Instance (⭐ 중요)

```text
Class = 붕어빵틀
Instance = 붕어빵
```

같은 붕어빵틀에서 여러 개의 붕어빵을 만들 수 있듯이, 하나의 class에서 여러 instance를 만들 수 있다.

정리하면 다음과 같다.

```text
class = object의 구조와 동작을 정의한 type 또는 template
instance = 특정 class로부터 생성된 구체적인 object
object = 실행 중 존재하는 구체적인 대상
```

좁은 의미에서 object는 instance를 의미하는 경우가 많다.

```text
Object = Instance of Class
```

## 2.8 Python에서의 특이점 : 동적 Attribute 생성

Python에서는 instance attribute를 나중에 동적으로 추가할 수 있다.

```python
class Samp:
    def get_x(self):
        return self.x

s = Samp()
s.x = 23
print(s.get_x())
```

출력은 다음과 같다.

```text
23
```

하지만 다음처럼 `s.x = 23`이 없다면 에러가 발생한다.

```python
class Samp:
    def get_x(self):
        return self.x

s = Samp()
print(s.get_x())
```

이유는 `self.x`가 아직 만들어지지 않았기 때문이다.

따라서 Python에서는 가급적 생성자 `__init__`에서 사용할 instance attribute를 미리 초기화하는 것이 좋다.

```python
class Samp:
    def __init__(self):
        self.x = 0

    def get_x(self):
        return self.x
```

# 3. Encapsulation and Data Hiding

## 3.1 Encapsulation이란?

Encapsulation은 캡슐화를 의미한다.

캡슐화란 서로 관련 있는

* data
* data를 다루는 method

를 하나의 object 안에 묶는 것이다.

그리고 외부에서는 내부 data에 직접 접근하지 못하게 하고, 정해진 method를 통해서만 접근하게 한다.

## 3.2 Data Hiding

Data Hiding은 데이터 은닉을 의미한다.

객체 내부의 중요한 data를 외부에서 직접 건드리지 못하게 숨기는 것이다.

즉,

```text
내부 data는 숨기고
외부에는 interface만 공개
```

하는 것이다.

## 3.3 Encapsulation의 구조

캡슐화는 다음과 같은 구조를 가진다.

```text
Object 내부
- Attribute
- Method

외부 공개
- Method 중심의 Interface
```

즉, 외부 사용자는 내부 구현을 몰라도 method만 사용하면 된다.

예를 들어 자동차를 운전할 때 엔진 내부 구조를 몰라도

```text
핸들
브레이크
엑셀
```

만 알면 운전할 수 있다.

## 3.4 Encapsulation의 장점

캡슐화의 장점은 다음과 같다.

* 사용자는 interface만 알고 있어도 객체를 사용할 수 있다.
* 내부 구현이 바뀌어도 외부 사용 코드의 변화가 줄어든다.
* 설계자가 의도한 방식으로 객체를 사용하게 만들 수 있다.
* 잘못된 직접 접근을 막을 수 있다.

## 3.5 Encapsulation의 단점

단점은 다음과 같다.

* 직접 접근보다 코드가 길어질 수 있다.
* getter, setter 같은 method를 추가해야 할 수 있다.

## 3.6 Python에서의 Encapsulation

C++이나 Java는 접근 제어자가 엄격하다.

예를 들어

```text
private
public
protected
```

같은 접근 제어자를 통해 data hiding을 강하게 구현할 수 있다.

하지만 Python은 상대적으로 느슨하다.

Python에서는 관례적으로 `_` 또는 `__`를 사용한다.

```python
class Person:
    def __init__(self, name):
        self.__name = name

    def get_name(self):
        return self.__name
```

여기서

```python
self.__name
```

은 외부에서 직접 접근하지 말라는 의미가 강하다.

## 3.7 property

Python에서는 `property`를 이용해 getter와 setter를 더 자연스럽게 사용할 수 있다.

```python
class Person:
    def __init__(self, age):
        self.__age = age

    @property
    def age(self):
        return self.__age

    @age.setter
    def age(self, value):
        if value >= 0:
            self.__age = value
```

사용은 다음과 같다.

```python
p = Person(20)
print(p.age)

p.age = 21
print(p.age)
```

## 3.8 Encapsulation 정리 (⭐ 중요)

Encapsulation은

```text
Attribute와 Method를 묶고,
Attribute에 직접 접근하지 못하게 하며,
Method를 통해서만 다루도록 하는 것
```

이다.

즉,

```text
Encapsulation = Data + Method + Data Hiding
```

# 4. Inheritance

## 4.1 Inheritance란?

Inheritance는 상속을 의미한다.

상속은 기존 class의 attribute와 method를 새로운 class가 물려받는 것이다.

즉,

```text
부모 class의 기능을 자식 class가 재사용하는 것
```

이다.

## 4.2 상속의 목적

상속을 사용하는 이유는 다음과 같다.

* 공통 기능을 부모 class에 모아둘 수 있다.
* 여러 자식 class에서 중복 코드를 줄일 수 있다.
* class 사이의 관계를 명확하게 표현할 수 있다.
* 기존 class를 수정하지 않고 기능을 확장할 수 있다.

## 4.3 상속 관계 용어 (⭐ 중요)

상속 관계에서 사용하는 용어는 다음과 같다.

```text
parent class = superclass = base class = 상위 클래스
child class = subclass = derived class = 하위 클래스
```

예를 들어

```python
class Human:
    pass

class Warrior(Human):
    pass
```

여기서

```text
Human = parent class = superclass = base class
Warrior = child class = subclass = derived class
```

이다.

## 4.4 is-a 관계

상속은 보통 is-a 관계를 만든다.

예를 들어

```text
Warrior is a Human
Knight is a Warrior
Knight is a Human
```

이라고 말할 수 있다.

따라서 상속은 계층 구조를 만든다.

## 4.5 상속 예제

```python
class Human:
    def __init__(self, name):
        self.name = name
        self.job = None

    def introduce(self):
        print(f"제 이름은 {self.name}입니다.")
        print(f"제 직업은 {self.job}입니다.")

class Warrior(Human):
    def __init__(self, name):
        super().__init__(name)
        self.job = "Warrior"

    def bash(self):
        print("강타 능력")

class Healer(Human):
    def __init__(self, name):
        super().__init__(name)
        self.job = "Healer"

    def healing(self):
        print("치료 능력")
```

사용 예시는 다음과 같다.

```python
h = Human("김아무개")
w = Warrior("이아무개")
he = Healer("박아무개")

h.introduce()
w.introduce()
he.introduce()

w.bash()
he.healing()
```

## 4.6 super() (⭐ 중요)

`super()`는 부모 class의 method에 접근할 때 사용한다.

특히 생성자에서 자주 사용한다.

```python
class Warrior(Human):
    def __init__(self, name):
        super().__init__(name)
        self.job = "Warrior"
```

여기서

```python
super().__init__(name)
```

은 부모 class인 Human의 생성자를 호출한다.

즉, 부모가 가진 초기화 과정을 먼저 수행하고, 자식 class에서 필요한 내용을 추가한다.

## 4.7 Method Overriding (⭐ 중요)

Overriding은 부모 class의 method를 자식 class에서 다시 정의하는 것이다.

```python
class Dog:
    def bark(self):
        print("멍멍")

class Poodle(Dog):
    def bark(self):
        print("왈왈")
```

사용하면 다음과 같다.

```python
d = Dog()
p = Poodle()

d.bark()
p.bark()
```

출력은 다음과 같다.

```text
멍멍
왈왈
```

같은 `bark()`라는 이름의 method이지만, 실제 객체의 class에 따라 다르게 실행된다.

## 4.8 Overriding vs Overloading

Overriding과 Overloading은 다른 개념이다.

```text
Overriding
= 부모 class의 method를 자식 class에서 다시 정의하는 것

Overloading
= 같은 이름의 함수나 method를 parameter 차이에 따라 여러 개 정의하는 것
```

Python은 전통적인 의미의 overloading을 엄격하게 지원하지 않는다.

예를 들어 다음처럼 같은 이름의 함수를 두 번 정의하면 뒤의 함수가 앞의 함수를 덮어쓴다.

```python
def func(a):
    print(a)

def func(a, b):
    print(a, b)
```

## 4.9 Multiple Inheritance

Multiple Inheritance는 다중 상속을 의미한다.

즉, 하나의 class가 두 개 이상의 부모 class를 상속받는 것이다.

```python
class Knight:
    def riding(self):
        print("말타기")

class Healer:
    def healing(self):
        print("치료하기")

class Paladin(Knight, Healer):
    pass
```

사용 예시는 다음과 같다.

```python
p = Paladin()
p.riding()
p.healing()
```

## 4.10 Diamond Problem

다중 상속은 편리하지만 충돌 위험이 있다.

예를 들어 여러 부모 class에 같은 이름의 method가 있으면 어떤 부모 class의 method를 먼저 사용할지 문제가 생길 수 있다.

이를 Diamond Problem이라고 한다.

Python에서는 MRO에 따라 method 탐색 순서를 결정한다.

## 4.11 MRO

MRO는 Method Resolution Order의 약자이다.

즉, method를 찾는 순서이다.

Python에서는 `mro()`로 확인할 수 있다.

```python
print(Paladin.mro())
```

예를 들어

```python
class Paladin(Knight, Healer):
    pass
```

이면 Python은 왼쪽에 있는 class를 더 먼저 탐색한다.

즉,

```text
Paladin → Knight → Healer → object
```

순서로 method를 찾는다.

# 5. Polymorphism

## 5.1 Polymorphism이란?

Polymorphism은 다형성을 의미한다.

다형성이란 서로 다른 type의 object들이 동일한 방식의 message 또는 method 호출에 대해 각자 다른 방식으로 반응할 수 있는 성질이다.

간단히 말하면

```text
같은 명령
다른 실행
```

이다.

## 5.2 Polymorphism 예제

```python
class Dog:
    def bark(self):
        print("멍멍")

class Poodle(Dog):
    def bark(self):
        print("왈왈")

class Samoyed(Dog):
    def bark(self):
        print("컹컹")
```

사용 예시는 다음과 같다.

```python
dogs = [Poodle(), Samoyed(), Dog()]

for d in dogs:
    d.bark()
```

출력은 다음과 같다.

```text
왈왈
컹컹
멍멍
```

같은 코드로

```python
d.bark()
```

를 호출했지만 실제 실행 결과는 object의 실제 class에 따라 달라진다.

## 5.3 Polymorphism과 Overriding

다형성은 method overriding과 연결된다.

부모 class에 있는 method를 자식 class들이 각자 방식으로 overriding하면, 같은 method 호출이 서로 다른 결과를 낼 수 있다.

```text
Dog.bark()
Poodle.bark()
Samoyed.bark()
```

는 모두 `bark()`라는 같은 이름을 가지지만, 실제 동작은 다르다.

## 5.4 isinstance()

`isinstance()`는 어떤 object가 특정 class의 instance인지 확인하는 함수이다.

```python
p = Poodle()

print(isinstance(p, Poodle))
print(isinstance(p, Dog))
```

출력은 다음과 같다.

```text
True
True
```

`Poodle`은 `Dog`를 상속받았기 때문에 `p`는 Poodle이면서 Dog이기도 하다.

## 5.5 issubclass()

`issubclass()`는 어떤 class가 다른 class의 subclass인지 확인하는 함수이다.

```python
print(issubclass(Poodle, Dog))
```

출력은 다음과 같다.

```text
True
```

## 5.6 Duck Typing

Python은 Duck Typing을 통해 다형성을 구현하는 경우가 많다.

Duck Typing은 다음 문장으로 설명된다.

```text
오리처럼 걷고, 오리처럼 꽥꽥거리면 오리로 본다.
```

즉, 객체의 실제 type보다 필요한 method를 가지고 있는지가 더 중요하다.

```python
class Dog:
    def speak(self):
        print("멍멍")

class Cat:
    def speak(self):
        print("야옹")

animals = [Dog(), Cat()]

for a in animals:
    a.speak()
```

여기서 Dog와 Cat은 같은 부모 class를 상속하지 않아도 `speak()`라는 method가 있기 때문에 같은 방식으로 사용할 수 있다.

## 5.7 Polymorphism 정리 (⭐ 중요)

Polymorphism은

```text
서로 다른 객체들에게 같은 방식으로 명령을 내릴 수 있고,
각 객체가 자기 방식대로 그 명령을 수행하는 것
```

이다.

# 6. SOLID 원칙

## 6.1 SOLID란?

SOLID는 OOP에서 소프트웨어를 더 유지보수하기 쉽고 확장하기 쉽게 만들기 위해 제안된 다섯 가지 원칙이다.

2000년대 초 Robert C. Martin이 정리한 원칙이다.

각 원칙의 앞글자를 따서 SOLID라고 부른다.

## 6.2 SRP

SRP는 Single Responsibility Principle이다.

하나의 class는 하나의 책임만 가져야 한다는 원칙이다.

```text
하나의 class가 너무 많은 일을 하면 수정하기 어려워진다.
```

## 6.3 OCP

OCP는 Open-Closed Principle이다.

소프트웨어 entity는 확장에는 열려 있고, 변경에는 닫혀 있어야 한다.

즉,

```text
기존 코드를 직접 수정하지 않고 기능을 확장할 수 있어야 한다.
```

## 6.4 LSP

LSP는 Liskov Substitution Principle이다.

자식 class는 부모 class를 대체할 수 있어야 한다.

즉,

```text
부모 class가 사용되는 자리에 자식 class를 넣어도 문제가 없어야 한다.
```

이는 다형성과 관련이 깊다.

## 6.5 ISP

ISP는 Interface Segregation Principle이다.

Client는 자신이 사용하지 않는 interface에 의존하면 안 된다.

즉, 너무 큰 interface 하나보다 작고 구체적인 interface 여러 개로 나누는 것이 좋다.

## 6.6 DIP

DIP는 Dependency Inversion Principle이다.

고수준 모듈과 저수준 모듈이 구체적인 구현에 직접 의존하지 말고, 추상화에 의존해야 한다는 원칙이다.

즉,

```text
구체적인 구현보다 abstraction에 의존하라.
```

# 7. Error and Exception

## 7.1 Error와 Exception

Python에서 무엇인가 정상 흐름에서 벗어난 경우 exception이 발생할 수 있다.

Exception은 예외를 의미한다.

즉, 정상적인 프로그램 흐름에서 벗어난 특별한 상황이다.

반면 Error는 프로그램이 기대한 동작을 하지 못하고 문제를 일으킨 상태를 의미한다.

## 7.2 Exception

Exception은 반드시 명백한 코드 오류만을 의미하지 않는다.

예를 들어

```text
사용자가 숫자를 입력해야 하는데 문자를 입력함
파일을 열려고 했는데 파일이 없음
0으로 나누려고 함
```

같은 경우도 exception이 발생할 수 있다.

## 7.3 Error

Error는 보통 명확한 문제 상황을 가리킨다.

Python에서 `Error`로 끝나는 예외 class들은 대부분 프로그래밍 오류나 실행 중 문제와 관련된다.

예를 들어

```text
SyntaxError
TypeError
ValueError
ZeroDivisionError
FileNotFoundError
```

등이 있다.

## 7.4 Syntax Error

Syntax Error는 문법적 에러이다.

source code가 Python 문법에 어긋나는 경우 발생한다.

예시는 다음과 같다.

```python
if True
    print("hello")
```

`if True` 뒤에 `:`가 없기 때문에 SyntaxError가 발생한다.

## 7.5 Logical Error

Logical Error는 논리적 에러이다.

문법적으로는 맞지만 알고리즘이나 의도 자체가 잘못된 경우이다.

이런 오류를 bug라고 부르는 경우가 많다.

```python
def average(a, b):
    return a + b / 2
```

위 코드는 문법적으로는 맞지만 평균을 구하려면 다음처럼 써야 한다.

```python
def average(a, b):
    return (a + b) / 2
```

## 7.6 Debugging

Debugging은 bug를 찾아 고치는 과정이다.

```text
bug = 프로그램의 논리적 오류
debugging = bug를 찾아 수정하는 과정
```

# 8. Python Exception Hierarchy

## 8.1 BaseException

`BaseException`은 Python의 모든 예외에 대한 최상위 class이다.

Python에서 발생하는 모든 예외는 BaseException을 상속받는다.

## 8.2 Exception

`Exception`은 일반적으로 프로그래머가 처리할 수 있는 대부분의 예외를 추상화한 class이다.

일반적인 예외 처리는 보통 다음처럼 작성한다.

```python
try:
    ...
except Exception as e:
    ...
```

## 8.3 Exception이 아닌 특수 예외

다음 예외들은 `Exception`이 아니라 `BaseException`을 직접 상속한다.

```text
SystemExit
KeyboardInterrupt
GeneratorExit
```

이들은 일반적인 프로그램 오류라기보다는 프로그램 실행 흐름 자체를 중단하거나 제어하기 위한 예외이다.

## 8.4 주요 예외 종류

대표적인 예외는 다음과 같다.

```text
BaseException
 ├── SystemExit
 ├── KeyboardInterrupt
 ├── GeneratorExit
 └── Exception
      ├── ArithmeticError
      │    └── ZeroDivisionError
      ├── LookupError
      │    ├── IndexError
      │    └── KeyError
      ├── ValueError
      ├── TypeError
      ├── OSError
      │    └── FileNotFoundError
      └── Warning
```

## 8.5 자주 보는 Exception

```text
ValueError
= 값이 잘못된 경우

TypeError
= type이 잘못된 경우

ZeroDivisionError
= 0으로 나눈 경우

IndexError
= list 등에서 잘못된 index를 사용한 경우

KeyError
= dictionary에 없는 key를 사용한 경우

FileNotFoundError
= 파일을 찾을 수 없는 경우
```

# 9. Exception Handling

## 9.1 Exception 발생 시 기본 동작

Python에서 exception이 발생하면 프로그램은 더 이상 정상적으로 진행하지 못하고 종료된다.

이런 비정상 종료를 crash라고도 한다.

Exception은 발생한 위치에서 함수 호출 stack을 따라 상위 호출자에게 전달된다.

이를 Exception Propagation이라고 한다.

최종적으로 처리되지 않은 exception은 Python interpreter에게 전달되고, 프로그램이 종료된다.

## 9.2 Exception Handling

Exception Handling은 발생한 exception을 처리하여 프로그램이 비정상적으로 종료되지 않도록 하는 것이다.

Python에서는 `try`와 `except`를 사용한다.

## 9.3 try-except 기본 구조 (⭐ 중요)

```python
try:
    exception이 발생할 수 있는 코드
except 처리할_Exception as 별칭:
    exception 발생 시 실행할 코드
finally:
    exception 발생 여부와 관계없이 항상 실행할 코드
```

예시는 다음과 같다.

```python
try:
    x = int(input("number? "))
    print(10 / x)
except ValueError as ve:
    print("숫자를 입력해야 합니다.")
except ZeroDivisionError as ze:
    print("0으로 나눌 수 없습니다.")
finally:
    print("프로그램 종료")
```

## 9.4 except

`except`는 특정 exception이 발생했을 때 실행되는 block이다.

```python
try:
    n = int("abc")
except ValueError as e:
    print(e)
```

여기서 `e`는 발생한 exception object를 가리키는 alias이다.

## 9.5 여러 except 사용

발생할 수 있는 exception이 여러 종류라면 `except`를 여러 개 사용할 수 있다.

```python
try:
    a = int(input("a? "))
    b = int(input("b? "))
    print(a / b)
except ValueError:
    print("정수를 입력해야 합니다.")
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
```

## 9.6 모든 Exception 처리

모든 일반적인 exception을 처리하려면 다음처럼 쓸 수 있다.

```python
try:
    ...
except Exception as e:
    print("Exception occurred")
```

하지만 모든 exception을 한 번에 처리하는 방식은 권장되지 않는다.

이유는 어떤 문제가 발생했는지 구체적으로 알기 어려워지기 때문이다.

## 9.7 except: 와 except Exception: 의 차이

```python
except:
```

는 `BaseException`까지 잡을 수 있다.

즉, `KeyboardInterrupt`, `SystemExit` 같은 특수 예외까지 잡을 수 있다.

반면

```python
except Exception:
```

은 일반적으로 프로그래머가 처리하는 예외만 잡는다.

따라서 보통은 `except:`보다 `except Exception:`이 더 적절하다.

## 9.8 raise

`raise`는 exception을 직접 발생시키거나, 처리한 exception을 다시 밖으로 전달할 때 사용한다.

```python
raise ValueError("잘못된 값입니다.")
```

예시는 다음과 같다.

```python
try:
    age = -1
    if age < 0:
        raise ValueError("나이는 음수가 될 수 없습니다.")
except ValueError as e:
    print(e)
```

## 9.9 finally

`finally`는 exception 발생 여부와 관계없이 항상 실행된다.

```python
try:
    print(10 / 0)
except ZeroDivisionError:
    print("0으로 나눌 수 없음")
finally:
    print("항상 실행")
```

출력은 다음과 같다.

```text
0으로 나눌 수 없음
항상 실행
```

주로 파일 닫기, 자원 정리 같은 작업에 사용된다.

## 9.10 else

`else` block은 `try` block에서 exception이 발생하지 않았을 때만 실행된다.

```python
try:
    x = int(input("number? "))
except ValueError:
    print("잘못된 입력")
else:
    print("입력 성공")
finally:
    print("종료")
```

정리하면 다음과 같다.

```text
try
= 예외 발생 가능 코드

except
= 예외 발생 시 실행

else
= 예외가 발생하지 않았을 때 실행

finally
= 예외 발생 여부와 관계없이 항상 실행
```

## 9.11 Exception 처리 예제

```python
def divide(a, b):
    return a / b

def main():
    try:
        a = int(input("numerator? "))
        b = int(input("denominator? "))

        result = divide(a, b)
        print(f"result = {result}")

    except ValueError as ve:
        print(ve)
        print("Check your inputs")

    except ZeroDivisionError as ze:
        print(ze)
        print("denominator can not be zero!")

    else:
        print("There is no error!")

    finally:
        print("This python script is finished.")

main()
```

# 10. Stack

## 10.1 Stack이란?

Stack은 자료구조의 하나이다.

Stack은 LIFO 또는 FILO 방식으로 동작한다.

```text
LIFO = Last-In-First-Out
FILO = First-In-Last-Out
```

즉, 마지막에 들어온 데이터가 가장 먼저 나간다.

## 10.2 Stack 비유

Stack은 접시 쌓기로 비유할 수 있다.

접시를 쌓을 때 나중에 올린 접시가 가장 위에 있고, 가장 먼저 꺼내진다.

```text
먼저 들어온 것 → 나중에 나감
나중에 들어온 것 → 먼저 나감
```

## 10.3 Stack 주요 용어

```text
Element
= Stack에 저장되는 데이터 단위

Push
= Stack에 데이터를 넣는 동작

Pop
= Stack에서 데이터를 꺼내는 동작

Top
= Stack의 가장 위에 있는 데이터
```

## 10.4 Stack 동작

예를 들어 순서대로 A, B, C를 push하면 다음과 같다.

```text
Push A
Push B
Push C
```

Stack 구조는 다음과 같다.

```text
Top → C
      B
      A
```

이 상태에서 pop하면 C가 먼저 나온다.

```text
Pop → C
Pop → B
Pop → A
```

## 10.5 Python list로 Stack 구현

Python에서는 list를 stack처럼 사용할 수 있다.

```python
stack = []

stack.append("A")
stack.append("B")
stack.append("C")

print(stack.pop())
print(stack.pop())
print(stack.pop())
```

출력은 다음과 같다.

```text
C
B
A
```

여기서

```python
append()
```

는 push 역할을 하고,

```python
pop()
```

은 pop 역할을 한다.

## 10.6 Stack 활용 예시

Stack은 다음과 같은 곳에서 사용된다.

* 함수 호출 관리
* 메모리 관리
* 괄호 검사
* 수식 계산
* DFS
* 실행 취소 기능
* Reverse Polish Notation 구현

## 10.7 Function Call Stack

함수가 호출될 때도 stack 구조가 사용된다.

```python
def a():
    b()

def b():
    c()

def c():
    print("hello")

a()
```

호출 순서는 다음과 같다.

```text
a() 호출
→ b() 호출
→ c() 호출
```

하지만 종료는 반대 순서로 이루어진다.

```text
c() 종료
→ b() 종료
→ a() 종료
```

즉, 함수 호출도 LIFO 구조이다.

# 11. Queue

## 11.1 Queue란?

Queue는 자료구조의 하나이다.

Queue는 FIFO 방식으로 동작한다.

```text
FIFO = First-In-First-Out
```

즉, 먼저 들어온 데이터가 먼저 나간다.

## 11.2 Queue 비유

Queue는 줄서기로 비유할 수 있다.

먼저 줄 선 사람이 먼저 나가고, 새로 온 사람은 줄의 맨 뒤에 선다.

```text
먼저 들어온 것 → 먼저 나감
나중에 들어온 것 → 나중에 나감
```

## 11.3 Queue 주요 용어

```text
Element
= Queue에 저장되는 데이터 단위

Enqueue
= Queue의 뒤쪽에 데이터를 추가하는 동작

Dequeue
= Queue의 앞쪽에서 데이터를 제거하는 동작

Front
= Queue에서 가장 먼저 들어온 요소

Rear
= Queue에서 가장 최근에 들어온 요소
```

## 11.4 Queue 동작

예를 들어 A, B, C를 순서대로 enqueue하면 다음과 같다.

```text
Front → A → B → C ← Rear
```

이 상태에서 dequeue하면 A가 먼저 나온다.

```text
Dequeue → A
Dequeue → B
Dequeue → C
```

## 11.5 Python list로 Queue 구현

Python list로 간단하게 queue를 구현할 수 있다.

```python
queue = []

queue.append("A")
queue.append("B")
queue.append("C")

print(queue.pop(0))
print(queue.pop(0))
print(queue.pop(0))
```

출력은 다음과 같다.

```text
A
B
C
```

여기서

```python
append()
```

는 enqueue 역할을 하고,

```python
pop(0)
```

은 dequeue 역할을 한다.

단, list의 `pop(0)`은 앞 요소를 제거한 뒤 나머지 요소들을 이동시켜야 하므로 효율이 좋지 않다.

## 11.6 deque 사용

Python에서는 queue를 구현할 때 `collections.deque`를 사용하는 것이 더 좋다.

```python
from collections import deque

queue = deque()

queue.append("A")
queue.append("B")
queue.append("C")

print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
```

출력은 다음과 같다.

```text
A
B
C
```

## 11.7 Queue 활용 예시

Queue는 다음과 같은 곳에서 사용된다.

* 프로세스 스케줄링
* 프린터 대기열
* 네트워크 트래픽 관리
* BFS
* 작업 대기열
* 이벤트 처리

## 11.8 Queue의 종류

Queue의 종류는 다음과 같다.

```text
일반 Queue
= 기본적인 FIFO 구조

Circular Queue
= Queue의 끝이 다시 처음으로 연결된 구조

Priority Queue
= 요소마다 우선순위를 부여하여 우선순위가 높은 요소가 먼저 처리되는 구조
```

## 11.9 Priority Queue

Priority Queue는 들어온 순서가 아니라 우선순위에 따라 처리되는 Queue이다.

예를 들어 병원 응급실에서는 먼저 온 사람보다 더 위급한 사람이 먼저 치료받을 수 있다.

Priority Queue는 보통 Heap 자료구조를 이용해 구현한다.

# 12. Stack vs Queue

## 12.1 Stack과 Queue 비교 (⭐ 중요)

| 구분        | Stack                     | Queue                           |
| --------- | ------------------------- | ------------------------------- |
| 동작 방식     | LIFO / FILO               | FIFO                            |
| 비유        | 접시 쌓기                     | 줄서기                             |
| 삽입        | Push                      | Enqueue                         |
| 삭제        | Pop                       | Dequeue                         |
| 나가는 데이터   | 마지막에 들어온 데이터              | 먼저 들어온 데이터                      |
| Python 구현 | list.append(), list.pop() | deque.append(), deque.popleft() |

## 12.2 핵심 정리

```text
Stack
= 나중에 들어온 것이 먼저 나간다.

Queue
= 먼저 들어온 것이 먼저 나간다.
```


