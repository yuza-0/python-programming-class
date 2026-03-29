# Week 3

## 1. Function (함수)

함수(function)는 **재사용성**과 **가독성**을 위해 코드를 논리적으로 나누는 기본적인 도구이다.
같은 처리를 여러 번 반복해야 할 때 코드를 매번 다시 작성하지 않고, 하나의 함수로 묶어서 필요할 때마다 호출하여 사용할 수 있다.

함수는 procedure(절차)의 추상화라고 볼 수 있으며, 입력(input)을 받아 처리한 뒤 결과(output)를 반환하는 구조를 가진다.


## 2. 함수의 기본 구조

Python에서 함수는 `def` 키워드를 사용하여 정의한다.

예

```python
def test_func(argument0, argument1):
    result = argument0 + argument1
    return result
```

이때 함수의 윗부분을 **function header**라고 하며, 아래 들여쓰기 된 부분을 **function body**라고 한다.

### 함수 정의 시 중요한 점

* `def` 로 시작한다.
* 함수 이름 뒤에는 소괄호 `()` 가 온다.
* 괄호 안에는 parameter(매개변수)를 적는다.
* header 끝에는 반드시 `:`(colon)이 붙는다.
* body는 **들여쓰기(indentation)** 를 해야 한다.

Python에서는 들여쓰기가 문법의 일부이므로 매우 중요하다.


## 3. Function Call (함수 호출)

함수를 만들었다고 해서 바로 실행되는 것은 아니다.
실제로 사용하려면 **함수 호출(function call)** 을 해야 한다.

예

```python
def add(a, b):
    return a + b

x = add(3, 5)
print(x)
```

결과

```python
8
```

이때 `add(3, 5)` 부분이 함수 호출이다.

함수 호출 시에는 괄호 안에 **argument(인자)** 를 넣는다.
이 argument가 함수 정의에 있는 parameter에 전달된다.


## 4. Parameter와 Argument

예

```python
def add(a, b):
    return a + b

add(3, 5)
```

여기서

* `a`, `b` → **parameter**
* `3`, `5` → **argument**

즉,

* parameter는 함수 정의 시 적는 입력 자리
* argument는 실제 호출할 때 넣는 값

이다.


## 5. 함수 실행 흐름과 Call Stack

일반적으로 Python 코드는 위에서 아래로 순서대로 실행된다.
하지만 함수 호출이 일어나면 **제어(control)** 가 함수 쪽으로 넘어간다.

실행 흐름은 다음과 같다.

```text
함수 호출
→ 함수로 제어 이동
→ 함수 body 실행
→ return 수행
→ 원래 호출된 위치로 복귀
```

예

```python
def add(a, b):
    return a + b

x = add(3, 5)
print(x)
```

이 경우 `add(3, 5)` 가 먼저 실행되고, 그 결과값 `8` 이 반환된 후 다시 원래 자리로 돌아온다.

즉, 위 코드는 개념적으로 다음처럼 생각할 수 있다.

```python
x = 8
print(x)
```

처럼 함수 호출 부분이 **return value로 reduction(축약)** 되는 것이다.


## 6. Call Stack

함수 호출이 일어날 때 Python은 내부적으로 **call stack** 을 사용한다.

함수 호출 시 저장되는 것들:

* 귀환 주소(return address)
* parameter
* local variable(지역 변수)

함수 수행이 끝나면 stack에서 제거된다.

즉,

* 함수 안에서 만든 변수는 함수가 끝나면 사라짐
* 함수 밖에서는 접근할 수 없음

이때 함수 내부에서만 존재하는 변수를 **local variable** 이라고 한다.


## 7. return

함수는 `return` 을 통해 결과를 반환할 수 있다.

예

```python
def square(x):
    return x * x
```

```python
print(square(3))
```

결과

```python
9
```

### return이 없는 경우

```python
def say_hello():
    print("hello")
```

이 경우 함수는 명시적으로 값을 반환하지 않으므로 `None` 을 반환한다.

즉, 반환값이 없는 `return` 은 생략해도 동일하다.

```python
return
```

과

아무것도 쓰지 않는 것

은 같은 의미이다.


## 8. 여러 값 반환

Python에서는 여러 값을 반환하는 것처럼 보일 수 있다.

예

```python
def test():
    return 1, 2
```

하지만 실제로는 **두 개의 값을 반환하는 것이 아니라 tuple 객체 하나를 반환** 하는 것이다.

```python
x = test()
print(x)
```

결과

```python
(1, 2)
```


## 9. Default Argument

함수의 parameter에는 기본값(default value)을 줄 수 있다.

예

```python
def ds_print(message='my default message'):
    print(message)
```

```python
ds_print("hello")
ds_print()
```

결과

```python
hello
my default message
```

### 주의할 점

기본값이 있는 parameter는, 기본값이 없는 parameter 뒤에 와야 한다.

예를 들어 다음은 가능하다.

```python
def func(a, b=0):
    return a + b
```

하지만 아래처럼 쓰면 오류가 난다.

```python
def func(a=0, b):
    return a + b
```


## 10. Keyword Argument

함수 호출 시 argument를 이름으로 지정할 수도 있다.

예

```python
def ds_subtract(a=0, b=0):
    return a - b

print(ds_subtract(b=5))
```

이 경우 `a` 는 기본값 0을 사용하고, `b` 에만 5를 넣는다.

keyword argument를 사용하면 가독성이 좋아질 수 있지만, parameter 이름을 정확히 알고 있어야 한다.


## 11. input()

`input()` 함수는 사용자로부터 값을 입력받는 함수이다.

예

```python
name = input("이름을 입력하세요: ")
print(name)
```

### 중요한 점

`input()` 으로 입력받은 값은 **항상 문자열(str)** 이다.

예

```python
x = input("숫자 입력: ")
print(type(x))
```

결과

```python
<class 'str'>
```

즉, 숫자로 사용하려면 형변환(type casting)이 필요하다.

예

```python
x = int(input("숫자 입력: "))
print(x + 3)
```


## 12. eval() 과 exec()

### eval()

`eval()` 은 문자열을 받아 **expression으로 평가(evaluation)** 하여 값을 반환한다.

예

```python
print(eval("3 + 5"))
```

결과

```python
8
```

즉, 문자열 `"3 + 5"` 를 실제 계산식처럼 해석한다.

### exec()

`exec()` 는 문자열을 **코드 자체로 실행** 한다.

예

```python
exec("x = 10")
print(x)
```

결과

```python
10
```

### 차이

* `eval()` → 값을 계산해서 반환
* `exec()` → 코드를 실행

⚠ `eval()` 과 `exec()` 는 편리하지만, 외부 입력을 그대로 넣으면 매우 위험할 수 있다.


## 13. for 문

`for` 문은 반복문(loop)의 한 종류이다.

예

```python
for i in [1, 2, 3]:
    print(i)
```

결과

```python
1
2
3
```

이때

* `for`, `in` 은 Python의 **keyword**
* `i` 는 **loop variable**

이다.

즉, 리스트 안의 각 요소를 하나씩 꺼내어 `i` 에 대입하며 반복한다.


## 14. range()

반복문에서 자주 사용하는 것이 `range()` 이다.

예

```python
for i in range(1, 10):
    print(i)
```

결과

```python
1
2
3
4
5
6
7
8
9
```

### range의 형태

```python
range(start, stop, step)
```

또는

```python
range(stop)
range(start, stop)
```

예

```python
range(5)
```

→ 0, 1, 2, 3, 4

### 주의할 점

`step` 에 음수가 들어갈 경우 시작값이 끝값보다 커야 한다.

예

```python
for i in range(10, 0, -1):
    print(i)
```


## 15. Literal

Literal은 **소스 코드 상에서 직접 적는 고정된 값** 을 의미한다.

예

```python
10
3.14
"hello"
True
```

이들은 모두 literal이다.

Programming에서 값을 지정하는 방법은 크게 두 가지이다.

1. Literal 사용
2. Variable 사용


## 16. Constant와 Variable

### Variable

변수(variable)는 값을 가리키는 이름이다.

예

```python
x = 10
```

### Constant

constant는 **값이 변하지 않는 변수** 를 의미한다.

Python은 dynamic language라서 진짜 의미의 constant를 강제하기 어렵기 때문에, 보통 **convention(관례)** 으로 표현한다.

예

```python
PI = 3.141592
```

이처럼 대문자와 underscore만 사용하면
“이 변수는 상수처럼 사용하자” 라는 의미가 된다.


## 17. Arithmetic Operators

Arithmetic Operators는 숫자형 데이터에 대해 수학적 계산을 수행하는 연산자이다.

### 기본 사칙연산

```python
+
-
*
/
```

예

```python
print(3 + 5)
print(10 - 2)
print(4 * 3)
print(8 / 2)
```


## 18. 정수 나눗셈과 나머지

### Integer Division (floor division)

```python
//
```

예

```python
print(12 // 10)
```

결과

```python
1
```

### Modulo (remainder)

```python
%
```

예

```python
print(10 % 3)
```

결과

```python
1
```


## 19. Augmented Assignment

증강 할당 연산자는 기존 값을 다시 자기 자신에 연산하여 저장하는 방식이다.

예

```python
x = 5
x += 3
print(x)
```

결과

```python
8
```

이는 아래와 같은 의미이다.

```python
x = x + 3
```


## 20. Data Type

Type은 Programming에서 **값이나 객체의 종류(category)** 를 의미한다.

어떤 object의 type이 결정되면 다음이 함께 결정된다.

1. 그 object가 가질 수 있는 값의 범위
2. 그 object에 사용할 수 있는 연산자와 기능

예를 들어 문자열은 나눗셈 `/` 의 피연산자가 될 수 없다.


## 21. Python에서 Type 확인

Python에서는 `type()` 함수를 이용하여 타입을 확인할 수 있다.

예

```python
print(type(3))
print(type(3.14))
print(type("hello"))
```

결과

```python
<class 'int'>
<class 'float'>
<class 'str'>
```


## 22. Python의 주요 Type 분류

### Numeric Type

* `int` : 정수
* `float` : 실수
* `complex` : 복소수

예

```python
x = 10
y = 3.14
z = 2 + 3j
```

Python에서는 복소수에서 `i` 대신 `j` 를 사용한다.

---

### Boolean Type

* `True`
* `False`

예

```python
print(True)
print(False)
```

Boolean type에는 다음과 같은 논리 연산이 가능하다.

```python
and
or
not
```

예

```python
print(True and False)
print(True or False)
print(not True)
```

### 참고

Programming에서는 보통 **0을 False**, 그 외의 수를 **True** 로 간주하는 관례가 있다.

예

```python
print(bool(0))
print(bool(5))
```

결과

```python
False
True
```

---

### Sequence Type

#### str

문자열을 나타내는 type이다.

```python
s = "hello"
```

#### list

순서가 있고, 변경 가능한(mutable) 자료형이다.

```python
a = [1, 2, 3]
```

#### tuple

순서가 있지만, 변경 불가능한(immutable) 자료형이다.

```python
t = (1, 2, 3)
```

### Set Type

#### set

중복이 없고, 순서가 없는 자료형이다.

```python
s = {1, 2, 3}
```

중복 제거 등에 자주 사용된다.

#### frozenset

변경 불가능한 set이다.


### Dictionary Type

#### dict

key와 value의 쌍으로 이루어진 자료형이다.

```python
d = {"name": "jihye", "age": 20}
```

* 순서보다 key를 통해 접근
* key는 중복될 수 없음


### None Type

```python
None
```

값이 없음을 의미한다.

예

```python
x = None
```

---

## 23. sys 모듈

`sys` 는 Python 인터프리터와 상호작용하기 위한 모듈이다.

즉, Python VM(or Interpreter)에 의해 사용되거나 유지되는 변수들과, 인터프리터와 밀접한 기능에 접근할 수 있도록 해준다.

예

```python
import sys
```


## 24. sys.argv

`sys.argv` 는 **명령줄(command line)로 전달된 argument list** 를 저장하는 리스트이다.

예를 들어 CMD에서 다음과 같이 입력한다고 하자.

```bash
python gugudan.py 3
```

그러면 Python 내부에서는 다음과 같이 저장된다.

```python
['gugudan.py', '3']
```

즉,

* `argv[0]` → script file 이름
* `argv[1]` → 첫 번째 입력값

이다.

### 실행 흐름

```text
CMD 입력
↓
python.exe 실행
↓
gugudan.py + 3 전달
↓
Python 내부에서 sys.argv에 저장
↓
스크립트 실행
```

예

```python
import sys
print(sys.argv)
```

CMD에서

```bash
python test.py 5
```

실행 시 결과

```python
['test.py', '5']
```

즉, `sys.argv` 는 **CMD에서 넘긴 인자들을 리스트 형태로 저장하는 변수** 라고 볼 수 있다.


## 25. sys 관련 기타 기능

### sys.executable

현재 실행 중인 Python interpreter의 절대 경로를 나타낸다.

```python
import sys
print(sys.executable)
```


### sys.exit()

Python interpreter에게 종료를 지시한다.

```python
import sys
sys.exit(0)
```

보통 `0` 은 정상 종료를 의미하고,
다른 숫자는 비정상 종료를 의미한다.


### sys.path

Python이 모듈이나 패키지를 찾을 때 참조하는 경로들의 리스트이다.

즉, import할 때 Python이 어디를 뒤지는지를 보여준다.

```python
import sys
print(sys.path)
```


### sys.modules

현재 로딩되어 있는 모듈들을 저장하는 dictionary이다.

Python이 `import` 를 수행할 때 중요한 역할을 한다.

동작 방식은 다음과 같다.

1. `import` 문을 만나면 먼저 `sys.modules` 에 이미 있는지 확인
2. 없으면 `sys.path` 등을 통해 모듈을 찾음
3. 찾은 모듈을 로딩 후 `sys.modules` 에 저장

즉, 같은 모듈을 여러 번 import해도 보통 한 번만 로딩된다.

---


## 26. Module, Package, Library

### Module

함수, 클래스, 변수 등을 **파일 단위로 정리한 것** 이 module이다.

즉, Python의 `.py` 파일 하나가 모듈이 될 수 있다.

예

```text
helper.py
math_tools.py
gugudan.py
```


### Package

관련 있는 여러 모듈을 **폴더 단위로 묶은 것** 이 package이다.

예

```text
mypackage/
    __init__.py
    helper.py
    math_tools.py
```


### Library

패키지나 모듈들을 하나의 **재사용 가능한 도구** 로 배포한 것을 보통 library라고 부른다.

즉,

* 파일 단위 → module
* 폴더 단위 → package
* 배포/사용 목적 단위 → library

라고 볼 수 있다.


## 27. Package Manager

Package Manager는 여러 패키지를 설치, 제거, 관리하는 도구이다.

### OS 수준의 Package Manager 예시

* Linux: `apt`, `apt-get`
* macOS: `homebrew`
* Windows: `winget`

이들은 OS 수준에서 소프트웨어를 설치하고 관리하는 역할을 한다.


## 28. pip

`pip` 는 Python에서 사용하는 대표적인 **package management system** 이다.

즉, Python에서 사용할 라이브러리나 패키지를 설치/제거/관리하는 도구이다.

Python 3.4부터는 보통 Python 설치 시 함께 설치된다.


## 29. pip 기본 사용법

### pip 업그레이드

```bash
python -m pip install --upgrade pip
```


### 패키지 설치

```bash
pip install numpy
```

또는

```bash
python -m pip install numpy
```


### 패키지 제거

```bash
pip uninstall numpy
```


### 설치된 패키지 목록 확인

```bash
pip list
```


## 30. requirements.txt

여러 패키지를 한 번에 관리하기 위해 사용하는 파일이다.

예를 들어 `requirements.txt` 안에 다음처럼 적을 수 있다.

```text
numpy
pandas
matplotlib
```

설치

```bash
pip install -r requirements.txt
```


## 31. 버전 지정

패키지 설치 시 버전을 지정할 수 있다.

예

```bash
pip install numpy==1.26.0
```

### 자주 사용하는 기호

* `==` : 정확히 같은 버전
* `>=` : 이상
* `<=` : 이하
* `~=` : 특정 범위 허용


## 32. Python 실행 구조 정리

이번 주차에서 중요한 Python 실행 구조는 다음과 같이 정리할 수 있다.

```text
사용자 (CMD)
↓
python.exe (인터프리터)
↓
main.py 실행
↓
import 모듈들
↓
sys로 실행 환경 접근
↓
프로그램 동작
```

즉,

* Python 코드는 인터프리터에 의해 실행되며
* 모듈과 패키지를 import하여 기능을 확장하고
* sys를 통해 실행 환경에 접근할 수 있다.

---

## 정리

이번 수업에서는 다음 내용을 학습하였다.

* 함수의 정의와 호출
* parameter와 argument
* return과 call stack
* input, eval, exec
* for문과 range
* literal, constant, arithmetic operator
* Python의 다양한 data type
* sys 모듈과 sys.argv
* module, package, library의 차이
* pip와 requirements.txt
* Python 프로그램의 전체 실행 구조

