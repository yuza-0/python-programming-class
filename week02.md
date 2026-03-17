# Week 2

## 1. Programming Language란?

프로그래밍 언어는 **주어진 문제를 해결하기 위해 인간과 컴퓨터 사이의 의사소통을 가능하게 하는 인공적인 언어**이다.

- 프로그래밍 언어 자체를 CPU가 직접 이해하는 것은 아니다.
- CPU는 **machine language(기계어)** 만 직접 이해할 수 있다.
- 따라서 프로그래밍 언어로 작성된 코드는 **compiler** 또는 **interpreter**를 통해 기계가 수행할 수 있는 형태로 변환되어 실행된다.
- 자연어와 달리, 프로그래밍 언어는 **정해진 규칙에 따라 엄격하게 정의**된다.


## 2. 범용 프로그래밍 언어의 조건

계산 가능한 모든 문제를 해결할 수 있는 이론적 요건을 갖춘 언어를 **범용 프로그래밍 언어(general purpose programming language)** 라고 한다.

범용 프로그래밍 언어가 되기 위해 필요한 요소는 다음과 같다.

1. **Variable assignment**
   - 상태를 저장하고 변경할 수 있어야 한다.
   - 변수 선언, 변수 읽기, 입력 처리 등이 포함된다.

2. **Loops**
   - 반복을 수행할 수 있어야 한다.
   - iteration(반복) 또는 recursion(재귀)이 가능해야 한다.

3. **Conditions**
   - 조건에 따라 다른 동작을 수행할 수 있어야 한다.
   - conditional branching(조건 분기)이 필요하다.

즉, **상태 표현, 반복(또는 재귀), 조건 분기**가 계산에 필요한 핵심 요소이다.

수업에서는 이 3가지를 중심으로 학습하고, 추가로 함수와 클래스를 만드는 방법도 배운다.


## 3. 프로그래밍 언어의 분류

### 3.1 추상화 수준에 따른 분류

#### 저급 언어 (Low-level Language)
저급 언어는 컴퓨터 하드웨어의 물리적 동작과 가까운 언어이다.

- 기계가 이해하기 쉽다.
- 실행 속도가 빠를 수 있다.
- 사람이 이해하기는 어렵다.
- 하드웨어에 대한 지식이 많이 필요하다.

예:
- Machine language
- Assembly language

#### 고급 언어 (High-level Language)
고급 언어는 사람이 이해하기 쉽도록 추상화가 적용된 언어이다.

- 하드웨어를 직접 이해하지 않아도 프로그래밍이 가능하다.
- 변수 이름을 이용해 데이터를 다룰 수 있다.
- 자연어에 가까운 표현을 사용한다.

예:
- Python
- C
- Java

---

### 추상화 (Abstraction)

추상화란 **복잡한 대상에서 핵심적인 개념이나 기능만 드러내고, 세부 구현은 숨기거나 제거하여 쉽게 사용할 수 있도록 하는 것**을 의미한다.

즉, 필요한 것만 가져와서 사용하는 개념이다.

---

### 3.2 작동 방식에 따른 분류

#### Compiler Language
프로그램 전체를 한 번에 읽어서 **object code** 또는 실행 파일로 변환하는 방식이다.

특징:
- 전체를 한 번에 번역한다.
- 번역 후 실행 속도가 빠를 수 있다.
- 소스 코드를 수정하면 다시 컴파일해야 한다.

예:
- C
- C++
- Fortran
- Pascal

#### Interpreter Language
코드를 한 줄 또는 statement 단위로 읽고 실행하는 방식이다.

특징:
- 작성 후 바로 실행 결과를 확인하기 쉽다.
- 대화형 프로그래밍에 적합하다.
- 교육용이나 빠른 테스트에 유리하다.

예:
- Python
- JavaScript
- Ruby
- PHP

최근에는 인터프리터 언어도 VM을 사용하여 성능을 개선하고 있다.  
예를 들어 Python은 **PVM(Python Virtual Machine)** 을 통해 bytecode를 실행한다.


### 3.3 작성 방식에 따른 분류

#### 명령형 프로그래밍 (Imperative Programming)
프로그램이 **어떻게 동작해야 하는지**를 순서대로 기술하는 방식이다.

특징:
- 상태 변경
- 명령의 순차 실행
- 메모리 갱신

예:
- C
- Python
- Java

#### 선언형 프로그래밍 (Declarative Programming)
프로그램이 **무엇을 원하는지**를 기술하는 방식이다.

특징:
- 결과나 관계를 선언한다.
- 실제 절차는 시스템이 결정한다.

예:
- SQL
- Prolog

### 요약 : 명령형과 선언형의 차이

- **명령형**: 어떻게 실행할지 직접 작성
- **선언형**: 무엇이 필요한지만 작성


## 4. Compiler와 Interpreter 관련 용어

### Source Code
사람이 프로그래밍 언어로 작성한 텍스트 코드이다.

### Object Code
컴파일러가 source code를 번역하여 만든 결과물이다.

### Bytecode
Virtual Machine이 이해하고 실행할 수 있는 중간 코드이다.

예:
- Java의 `.class`
- Python의 `.pyc`

### Binary Code
CPU가 이해할 수 있는 0과 1의 패턴으로 된 코드이다.

### Machine Language
CPU가 직접 이해하고 실행할 수 있는 명령어 집합이다.

### Microcode
CPU 내부에서 machine code를 더 낮은 수준으로 분해하여 제어 신호를 만드는 코드이다.


## 5. Dynamic Typing과 Static Typing

### Dynamic Typing
변수의 타입이 **실행 시점(runtime)** 에 결정되는 방식이다.

특징:
- 변수 자체는 고정된 타입을 가지지 않는다.
- 실제로는 **변수가 참조하는 object가 타입을 가진다**.
- 유연성이 높다.
- 생산성이 좋다.
- 실행 중 타입 오류가 날 수 있다.

예:
- Python
- JavaScript
- PHP
- Ruby

### Static Typing
변수의 타입이 **컴파일 시점(compile time)** 에 결정되는 방식이다.

특징:
- 변수 타입이 미리 정해진다.
- 타입 오류를 초기에 발견할 수 있다.
- 최적화된 실행 코드 생성에 유리하다.

예:
- C
- C++
- Java


## 6. Strong Typing과 Weak Typing

### Strong Typing
타입 규칙을 엄격하게 적용하는 방식이다.

- 서로 다른 타입 사이의 암묵적 변환이 제한된다.
- 타입 불일치 시 오류가 발생한다.

Python은 **dynamic language이면서 strongly typed language**이다.

즉:
- 변수는 타입을 가지지 않는다.
- object는 타입을 가진다.
- object의 타입은 쉽게 바뀌지 않는다.

### Weak Typing
타입 변환이 비교적 자유로운 방식이다.

- 자동 형변환이 자주 허용된다.
- 타입 안전성이 상대적으로 약하다.

예:
- C
- PHP


## 7. Python에서 Variable과 Object

### Variable
Python에서 variable은 **메모리에 존재하는 object를 가리키는 이름(name,reference,identifier)** 이다.

Python에서는 **변수 자체가 타입을 가지는 것이 아니라, 변수가 가리키는 object가 타입을 가진다.**


### Object
Python에서 object는 다음 요소를 가지는 데이터 덩어리이다.

- **type**
- **value**
- **id**
- **reference count**

CPython에서는 `id`가 보통 메모리 주소와 관련되어 설명된다.

즉, object는 단순한 값이 아니라 **타입과 값, 식별 정보 등을 가진 실체**라고 볼 수 있다.


## 8. Variable Naming Rules

Python에서 변수명은 다음 규칙을 따른다.

- 영어 대소문자, underscore(`_`), 숫자의 조합을 사용할 수 있다.
- 첫 글자에 숫자가 올 수 없다.
- keyword는 사용할 수 없다.
- 대소문자를 구분한다.
- 한글 변수명도 technically 가능하지만 사용하지 않는 것이 좋다.

예:
```python
my_name = "jihyun"
score1 = 100
```

## 9. Naming Convention

### Camel Naming (or Camel Case)

한 name을 구성하는 word의 시작을 대문자로 기재하고 붙여쓴다.

- 보통, variable이나 functoin, method의 경우엔 name의 맨 처음은 소문자이지만, 이후 word의 시작은 대문자로 기재한다. : camelCase
- 단, class의 이름이나 structure의 이름은 CamelCase 처럼 맨 처음 글자도 대문자로 표기한다.

Java나 C++(MFC나 windows 대상인 경우)등에서는 Camel Naming 가 선호된다.

참고로 Pascal Naming (or Pascal Case) 의 경우엔, 항상 word의 첫글자를 대문자로 표기하는 경우를 지칭한다. class의 이름으로 주로 쓰임.

### Snake Naming (or Snake Case)

- Snake naming의 경우, word 사이에 underscore `_` 가 들어간다.  : snake_case
- Camel Naming보다 읽기 쉽지만, 좀더 이름이 길게 되는 경우가 많다.

Python이나 Linux 및 Unix 대상의 C, C++ 프로그래머들은 Snake Naming을 선호하는 편이다.
참고로 Kebab Naming (or Kebab Case)의 경우, underscore 대신 hyphen `-` 이 사용됨. Python 변수명에는 사용할 수 없고, 주로 블로그나 마크다운 문서에서 많이 보인다.

## 10. Python Script와 Module

### Script

Python 코드를 파일로 저장하고 한 번에 실행하는 방식이다.

예:

python gugudan.py

### Module

Python 파일을 다른 곳에서 불러와 재사용할 수 있는 형태이다.

예:

import math

수업에서는 REPL, script 실행, module 실행 방식의 차이를 실습하였다.

## 11. input 함수

input() 함수는 표준 입력(stdin) 으로부터 데이터를 입력받는 함수이다.

CLI 프로그램에서는 보통 다음과 같이 동작한다.

입력: stdin

출력: stdout

예:
```name = input("이름을 입력하세요: ")
print(name)
```
주의할 점은 input()의 반환값은 기본적으로 문자열(str) 이다.
따라서 숫자로 사용하려면 형변환이 필요하다.

예:
```
num = int(input("숫자를 입력하세요: "))
```
## 12. 함수 정의 기초

함수는 반복적으로 사용되는 코드를 하나로 묶은 것이다.

예:
```python
def greet():
    print("Hello")
```

### 함수 정의 시 주의할 점

- 함수의 머리(head)는 : 로 끝난다.
- 함수의 몸통(body)은 들여쓰기를 해야 한다.
- 들여쓰기에서 space와 tab을 섞어 쓰면 오류가 발생할 수 있다.
- REPL에서는 함수의 body를 끝내기 위해 빈 줄을 입력한다.

## 13. Parameter와 Argument

Parameter: 함수 정의에서 사용하는 변수

Argument: 함수 호출 시 실제로 전달하는 값

예:
```python
def greet(name):   # name은 parameter
    print(name)

greet("jihyun")    # "jihyun"은 argument
```
## 14. 이번 주 실습 내용

이번 주에는 다음 내용을 실습하였다.

REPL 실행
Python script 파일 실행
module 형태로 실행
input()을 이용한 사용자 입력 처리
구구단 출력 프로그램 작성
함수 정의와 호출 기초

## 정리

이번 수업에서는 프로그래밍 언어의 개념과 분류, compiler와 interpreter의 차이, Python의 typing 특성, variable과 object의 개념, 변수명 규칙과 naming convention 등을 학습하였다.
또한 Python에서 REPL, script, module 방식으로 코드를 실행하는 방법을 실습하였고, input() 함수와 함수 정의 기초도 함께 배웠다.
특히 Python에서는 변수가 타입을 가지는 것이 아니라 object가 타입을 가진다는 점이 중요하다.
