# Week12

## 이번 주 큰 흐름
- class 만들기
- class Definition and Object Model
- 윤성우 열혈 파이썬 13

---


# 1. Python에서 Class란?

Class는 객체지향 프로그래밍(OOP)의 기본 단위이다.

```text
Class = State + Behavior
```

- State = 객체가 가지는 데이터
- Behavior = 객체가 수행하는 동작

역할

```text
동일한 구조와 동작을 가지는 Instance를 생성하기 위한 설계도
```

Python에서는 **모든 것이 객체(Object)** 이다.  
숫자, 함수, 리스트뿐 아니라 **Class도 객체**이다.

```python
class CustomClass:
    pass
```

위 코드는 단순히 설계도를 만드는 것이 아니라

→ 실행 시점(Runtime)에 `CustomClass` 라는 **객체가 생성됨**

즉,

```text
Class 정의 = Runtime에 객체 생성
```

---

## 1.1 type, class, instance (⭐ 중요 )

`type(obj)` 는 obj가 어떤 type의 instance인지 확인

예시

```python
x = 10
print(type(x))

class A:
    pass

print(type(A))
```

결과

```python
<class 'int'>

<class 'type'>
```

이때, type은 함수가 아니라 Class이다


```text
Class를 생성하는 Class = Metaclass
```

Instance = Class로부터 생성된 개별 객체(Object)

```python
class CustomClass:
    pass

print(type(CustomClass))
```

결과

```python
<class 'type'>
```

의미

```text
CustomClass는 객체(Object)이다.
CustomClass의 타입(type)은 type이다.
```

구조

```text
type → CustomClass → instance
```

- `type` : 클래스를 생성하는 metaclass
- `CustomClass` : class object
- `instance` : class로 생성한 객체

---

# 2. Instance 생성

클래스 이름을 함수처럼 **호출**하면 instance가 생성된다.

```python
ins = CustomClass() # CustomClass() : instance 생성

print(type(ins))
```

결과

```python
<class '__main__.CustomClass'>
```



- ins: CustomClass 클래스의 instance이다.


- CustomClass(): constructor(생성자) 역할을 한다.

## 2.1 Class Definition 실행 시 생성되는 것 (⭐ 중요 )
예시

```python
class Person:

    species = "Human"

    def greet(self):
        print("Hello")
```

실행 시 생성되는 것

```text
1. Class Object : Person

2. Class Attribute : species

3. Function Object : greet
```


## 2.2 생성되지 않는 것 (⭐ 중요 )

아직 생성되지 않는 것

```text
1. Instance

2. Instance Attribute
```

즉

```text
Class 정의만으로 Instance는 생성되지 않는다
```

---

# 3. Attribute

Attribute는 객체가 가지는 속성

예시

- 변수
- 함수(method)

Python 객체는 **동적으로 attribute 추가/삭제 가능**

---

## 3.1 동적 Attribute 추가 (⭐ 중요 )

Python에서는 Variable이 type을 가지지 않는다. 이는 단순히 객체를 가리키는 이름일 뿐, Object만 type을 가진다. static field가 존재하지 않는다고 할 수 있다.

```python
class CustomClass:
    pass

ins = CustomClass()

ins.dynamic_attribute = 100
print(ins.dynamic_attribute)

del ins.dynamic_attribute
```

Python의 사용자 정의 class는 모두 객체이기 때문에 attribute 변수 추가가 가능하다.

이는 class 구조가 고정되는 java와 차이가 있다.


---

# 4. Attribute 종류


- Data Attribute
    - Class Attribute
    - Instance Attribute
- Method Attribute
    - Instance Method
    - Class Method
    - Static Method


## 4.1 Data Attribute

데이터를 저장하는 attribute



### 4.1.1 Class Attribute (⭐ 중요 )

Class 객체 자체가 가지는 변수

```python
class Student:
    school = "ABC"

print(Student.school)
```


모든 instance가 공유한다.

구조

```text
Student
 └ school = "ABC"

a → Student 참조
b → Student 참조
```

---

### 4.1.2 Instance Attribute (⭐ 중요 )

각 instance가 개별적으로 가지는 변수. 주로 이 방식이 권장된다.

보통 `__init__()` 에서 생성

```python
class Student:

    def __init__(self):
        self.name = None
        self.age = None

s1 = Student()
s2 = Student()
```

구조

```text
s1 → name, age

s2 → name, age
```

각 객체마다 독립적이다.

## 4.2 Method Attribute

객체의 동작(behavior)을 정의하는 callable attribute

## 4.2.1 Instance Method (⭐ 중요 )

일반적인 method

첫 번째 parameter

```python
self
```

예시

```python
class A:

    def func(self):
        print(self)

obj = A() 
obj.func() # A.func(obj)
```


## 4.2.2 Class Method (⭐ 중요 )

Class 자체를 받는 method

데코레이터 필요

```python
@classmethod
```

첫 번째 parameter

```python
cls
```

예시

```python
class A:

    value = 10

    @classmethod
    def show(cls):
        print(cls.value)

A.show() # A.show(A)
```


---

## 4.2.3 Static Method

Class 내부에 묶어두는 일반 함수

데코레이터 필요

```python
@staticmethod
```

예시

```python
class A:

    @staticmethod
    def add(a, b):
        return a + b

A.add(1, 2)
```

특징

```text
self 자동 전달 X
cls 자동 전달 X
```

---

# 5. Attribute 탐색 순서 (⭐ 중요 )

instance에서 attribute 접근 시

Python은 다음 순서로 찾는다.

```text
1. Instance Namespace 탐색
2. Class Namespace 탐색
```

예시


```python
class A:
    x = 10

obj = A()

obj.x = 20

print(obj.x)
```

결과

```python
20
```

# 6. Python Class Attribute   vs Java Static Variable 차이

Java

```java
static int count;
```

Python

```python
class A:
    count = 0
```

비슷하지만 내부 구조 다름

Java

```text
언어 차원의 static 문법 존재
```

Python

```text
class object가 가지는 일반 attribute
```

즉

```text
Python에는 진짜 static variable 개념이 없음
```

---

# 9. 권장되는 Class 작성법 (⭐ 중요 )

```python
class CustomClass:

    # class attribute
    class_var = None

    @classmethod
    def class_method(cls):
        print(cls.class_var)

    def __init__(self):
        self.instance_var = None

    def instance_method(self):
        print(self.instance_var)

    @staticmethod
    def static_method():
        print(CustomClass.class_var)
```

원칙

```text
1. 모든 instance attribute는 __init__ 에서 초기화

2. 모든 instance가 공유하는 변수는 class attribute 사용

3. 동적 attribute 추가는 피할 것
```

---


#  Python Class Definition and Object Model

# 1. `__init__()` 의 역할 ⭐ 중요

`__init__()` 는 생성자가 아니다.

정확히는

```text
생성된 Instance를 초기화하는 Method
```

과정

```text
1. Instance 생성

2. __init__() 호출

3. Attribute 초기화
```

예시

```python
class Person:

    def __init__(self, name):
        self.name = name
```

생성

```python
p = Person("Alice")
```

---

⭐ 중요


- Instance Attribute는 __init__ 에서 정의되는 것이 아니다


정확히는

```text
Assignment(할당) 되는 순간 생성된다
```

예시

```python
self.name = name
```

이 순간

```text
name attribute 생성
```

---

-  __init__는 필수가 아니다

가능

```python
class A:
    pass

a = A()
```

결과

```text
Instance는 생성됨
Attribute는 없음
```
---

- Python은 Open Object Model을 가진다 ⭐ 중요

Python 객체 구조는 열려 있다.

의미

```text
생성 후에도 attribute 추가 가능
```

예시

```python
class A:
    pass

a = A()

a.age = 20
```

가능

---

- `__init__` 밖에서도 추가 가능

```python
p = Person("Alice")

p.age = 30
```

가능한 이유

```text
Python은 Open Structure 구조이기 때문
```





# 2. Duck Typing

Python은 Duck Typing 기반이다.

개념

```text
Class보다 Object의 기능이 중요하다
```

원칙

```text
오리처럼 걷고

오리처럼 울면

오리다
```

즉

```text
같은 Method를 가지면 같은 방식으로 사용 가능
```

상속 필요 없음

---

# 3. `__dict__` : Attribute 저장 공간 ⭐ 중요

Python Object는 Attribute를 내부 Dictionary에 저장한다.

이 공간이

```python
__dict__
```

이다.

---

## 3.1 예시

```python
class A:

    kind = "demo"

    def __init__(self):
        self.x = 10
```

생성

```python
a = A()
```

확인

```python
print(A.__dict__)
print(a.__dict__)
```

결과

```text
A.__dict__ → kind 저장

a.__dict__ → x 저장
```

즉

```text
Class와 Instance는 서로 다른 __dict__ 를 가진다
```

---

# 4. Attribute Lookup Rule ⭐ 중요

Attribute 접근 시 검색 순서

```text
Instance → Class → Parent Class
```

---

## 4.1 예시

```python
class A:
    x = 10

a = A()

print(a.x)
```

Python 내부

```text
1. a.__dict__ 확인

2. A.__dict__ 확인
```

---

## 4.2 충돌하면?

```python
class A:
    x = 10

a = A()

a.x = 20
```

결과

```python
print(a.x)
```

출력

```python
20
```

왜?

```text
Instance가 먼저 검색되기 때문
```

---

# 5. `__slots__`

Python은 원래 Attribute를 자유롭게 추가 가능하다.

이를 제한하는 기능

```python
__slots__
```

예시

```python
class Point:

    __slots__ = ("x","y")

    def __init__(self):
        self.x = 1
        self.y = 2
```

문제 발생

```python
p = Point()

p.z = 3
```

결과

```python
AttributeError
```


효과

```text
1. 허용된 Attribute만 사용 가능

2. __dict__ 생성 안됨

3. Memory 절약 가능
```

---


