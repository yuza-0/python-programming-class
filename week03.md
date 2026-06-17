# Week03
## 이번 주 큰 흐름

- 리터럴, 키워드

- 산술연산자, 데이터 타입, object

- 모듈과 sys 모듈

- 윤성우의 열혈 파이썬3
    - input 함수


# 1. literal, keyword

## 1.1 literal (⭐ 시험 )
소스 코드 상에서 고정된 값. 할당문에서 주로 우항에 위치. 참고로 literal도 객체


프로그래밍 언어에서 값을 지정하는 방법은 1. literal 사용과 2. variable 사용 2가지가 있다.

### 1.1.1 literal 특징

 literal도 object(객체)이다.

### 1.1.2 literal 예시
```python
x = 9
```
9가 literal

```python
v_bool = True
if v_bool:
    print('v_bool is True')
```

여기서 True가 literal. 

### 1.1.3 데이터 타입에 따른 literal

literal은 데이터 타입에 따라 표기 방식이 다르다. 

- 정수 (int): 10, -3, 0
- 실수 (float): 3.14, -0.5, 2.0
- **문자열 (string)**: "hello", 'a', "123"

    -> 코드에 그냥 적으면 literal이 될 수 없음(⭐ 중요)
- 불리언 (boolean): True, False
- None 타입: None


### 1.1.4 literal, variable, expression의 차이 

리터럴, 변수 ⊂ 표현식


## 1.2 keyword

Python에서 특별한 단어 (special word)들. reserved word라고도 함.
### 1.2.1 다양한 키워드

![](image-3.png)

### 1.2.2 Soft Keywords
 특정 맥락 안에서만 키워드.
 
 예: match나 case , underscore _ 는 match compound statement의 context에서만 keywords로 처리

#### 확인 방법

1.import keyword

2.print(keyword.kwlist)

---

# 2. Arithmetic in Python and Augmented Assignment

## 2.1 Arithmetic operator
먼저, **연산자**란
변수(variable)나 값(value)에 대해 **연산(operation)을 수행하는 기호** 또는 키워드를 말한다. 

연산자 종류는 다음과 같다.

- 산술 연산자: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- 비교 연산자: `==`, `!=`, `>`, `<`, `>=`, `<=`
- 논리 연산자: `and`, `or`, `not`
- 할당 연산자: `=`, `+=`, `-=`, `*=`, `/=`
- 기타: `in`, `not in`, `is`, `is not`

이 중 **산술연산자**는 수학적 계산을 하는 연산자이다.


#### 참고 용어 : `operand(피연산자)`
연산의 대상이 되는 값

### 2.1.1 연산자 우선순위

 `**` > `-(negation)` > `*` ,`/` ,`//` ,`%` > `+` ,`-`(subtraction)(⭐ 시험 )
 
 헷갈리면 괄호를 사용할 것.





### 2.1.2 연산자 종류

### unary operator(단항 연산자) : 피연산자 1개, 음수 표현

```python
>>> -2
-2
>>> --2
2
>>> ---2
-2
>>> ---2.
-2.0
```
### binary operator(이항 연산자) : 피연산자 2개

- ### `**`

- ### 사칙연산

결과는 피연산자 중 하나라도 실수형이면 실수형, 모두 정수형이면 정수이다.

나눗셈은 항상 실수형을 결과값으로 가진다.

Q. 값을 반환한다 와 생성한다. 가진다 등등의 차이는 무엇인가?

**곱하기** :*(asterisk, 아스터리스크) - (⭐ 중요)



```python
>>> 4/2
2.0
>>> 2.+3  # float
5.0
```

- ### 몫의 연산 `//` (⭐ 중요)
결과가 항상 정수처럼 보이도록 반환. floor(내림)연산을 사용

#### 결과 type
- 피연산자 중 하나라도 float이면 → 결과는 float
- 둘 다 int이면 → 결과는 int

```python
>>> -12//10   # floor(-1.2) = -2 ,작은 정수값이 답임.
-2
>>> -9//10
-1
>>> -19//10   # floor(-1.9) 이며 이는 -2가 됨.
-2
>>> 12.//10   # 하나라도 float면 결과도 float: floor(1.2)= 1.0
1.0
>>> 12//10.
1.0
```

- ### 나머지 연산 `%` (⭐ 중요)
결괏값의 sign(부호)이 항상 나누어주는 수(divisor)의 sign 을 따름 (0은 sign이 없음)

`a % b = a − (a // b) ∗ b` (⭐ 중요)

#### 결과 type
- 피연산자 중 하나라도 float이면 → 결과는 float
- 둘 다 int이면 → 결과는 int

#### 쉽게 계산하기

1. 결과는 항상 b와 같은 부호
2. 결과의 절댓값은 항상 |b|보다 작음
3. 범위 들어오면 즉시 종료

```python
# b > 0 (결과는 0,1,2,3 중 하나)
print(9 % 4)    # 1 , 2번 뺄셈
print(-9 % 4)   # 3 , 3번 덧셈

# b < 0 (결과는 0,-1,-2,-3 중 하나)
print(9 % -4)   # -3 , 3번 덧셈
print(-9 % -4)  # -1 , 2번 뺄셈

# float 포함
print(6.5 % 3)  # 0.5
```

## 2.2 Augmented Assignment(증강 할당 연산자)

Assignment + arithmetic operation. 즉 할당과 산술 연산을 동시에 함.

- `x += y` → `x = x + y`
- `x -= y` → `x = x - y`
- `x *= y` → `x = x * y`
- `x /= y` → `x = x / y`
- `x //= y` → `x = x // y`
- `x %= y` → `x = x % y`
- `x **= y` → `x = x ** y`

---

# 4. 모듈과 sys 모듈

## 4.1 모듈
함수/클래스/변수들을 source code file = 모듈 (⭐ 중요)

→
관련 있는 모듈 여러 개를 폴더로 묶으면 = 패키지

→
그 패키지/모듈들을 하나의 재사용 가능한 도구로 배포하면 = 라이브러리

* `mylib/`

  * `__init__.py` (모듈)
  * `helper.py` (모듈)
  * `math/` (패키지)
    * `__init__.py` (모듈)
    * `add.py`(모듈)
    * `sub.py`(모듈)
  * `text/` (패키지)
    * `__init__.py`(모듈)
    * `format.py`(모듈)

#### 참고 : class와의 차이
한가지 일만 할 때  module, 상속을 사용할 때 class

Q. 상속??

## 4.2 모듈의 특징
-   import 구문을 이용하여 다른 모듈(=다른 source code file)에서 참조되어 질 수 있음. 
- module의 naming은 variable 과 같은 규칙으로 작성되어야 함.

## 4.3 sys 모듈

파이썬이 미리 만들어둔 내장 모듈로,  인터프리터의 실행환경과 그 내부 상태에 직접 연결된 정보/기능을 다루는 도구. 

- 인터프리터가 가지고 있고 사용하거나 유지되는 변수
= data attribute

- 인터프리터와 밀접한 함수
= function attribute, method

#### 참고
function은 앞에 아무것도 없거나 모듈
method는 앞에 오브젝트(호출한 오브젝트에 엮여있음)


에 대한 접근을 제공한다.

#### 참고 용어 : `attribute (전체)`
 - data attribute (값)
 -  method (함수)

 ## 4.4 sys.argv (⭐ 시험 )

command line에서 전달된 값들을 담는 리스트. 모든 요소는 문자열(str)

### 코드
```
# test.py import sys 
print(sys.argv)
```
### 터미널
```python
>>> python test.py 10 hi
['test.py', '10', 'hi']
```

이때 argv[0]은 파일 이름을, argv[1]은 전달한 값들을 인덱스한다.

```python
>>> int(sys.argv[1])
10
```

## 4.5 sys.exit()
프로그램을 종료하는 함수

```python
# test1.py 
import sys 
print("A") 
sys.exit() # sys.exit(0)과 동일
print("B")
```
```python
>>> python test1.py
A
```

```python
# test3.py
import sys

print("A")
sys.exit(1)
print("B")
```
```python
>>> python test3.py
A # 에러 종료
```

# 5. 윤성우의 열혈 파이썬3

## 5.1 input 함수


표준 입력 스트림(stdin)으로부터 데이터를 입력받는 함수

```text
[키보드] → (stdin) → [프로그램] → (stdout) → [화면]
```
 
### 5.1.1 예제
```python
a = input()
```

input()함수가 호출되면 아무 출력이 없이 사용자의 입력을 대기 (blocking mode로 동작)

```python
b = input('Enter your input:')
```
문자열 argument,
해당 문자열을 prompt 문자열이라고 부르며 이 문자열이 출력되고 나서 사용자의 입력을 대기

### 5.2.2 특징

 input()의 반환값은 항상 문자열

### 5.2.3 여러 값의 입력을 한번에 처리하기

str의 method인 split 등을 통해 공백문자나 separator (or delimiter) 문자를 통해
복수개의 입력을 한번에 받을 수도 있음.

unpacking을 이용하기 때문에 반드시 입력되는 변수의 숫자를 맞게 입력

### 5.2.4 가변길이 입력 처리 방식


## 5.2 주요 예제

### 문자열 덧셈
<img width="253" height="80" alt="image" src="https://github.com/user-attachments/assets/69c43953-6735-4119-ac69-5bbc7763c8c0" />


### for
<img width="146" height="194" alt="image" src="https://github.com/user-attachments/assets/45521a92-7368-432d-b656-ea1b2b1432ef" />
<img width="249" height="226" alt="image" src="https://github.com/user-attachments/assets/e3d220c8-11d3-45f9-ae3e-6744a1cb2b21" />

