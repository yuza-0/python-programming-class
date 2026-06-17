# Week11

## 이번 주 큰 흐름

- 모듈(module)
- import
- module serach path
- dictionary
---
- 윤성우의 열혈 파이썬 11, 12
- 과제 

# 1. 모듈(module)

## 1.1 모듈이란
python 코드로 이뤄진 source code file. `.py` 파일을 의미.

하나의 module 안에는 변수, 함수, 클래스 등이 들어갈 수 있다.

```python
# calculator.py 

def add(a, b):
    return a + b
```
이때 calculator.py 파일 자체가 하나의 module이다.

## 1.2 특징
- import 구문을 이용하여 다른 모듈에서 참조될 수 있음.
- module의 naming은 variable 과 같은 규칙으로 작성되어야 함.

## 1.3 namespace 관점에서 module
Module은 import될 때 자신만의 namespace를 가진다.

즉, module 안에 있는 함수나 변수는 그냥 흩어져 있는 것이 아니라, 그 module 이름 아래에 묶여 있음.

```python
# calculator.py
def add(a, b):
    return a + b
```

```python
# main.py
import calculator

print(calculator.add(1, 2))
```

여기서
```
calculator = module namespace
add = calculator namespace 안에 있는 function
```

그래서 add()가 아니라 calculator.add()로 접근

## 1.4 Main Script와 Module의 관계

Python 파일은 상황에 따라 두 가지 역할을 할 수 있다.

직접 실행되는 파일 → main script
import되는 파일 → module

예를 들어

```
main.py
calculator.py
```

가 있을 때,
```python
# main.py
import calculator
```
이면 main.py는 직접 실행되는 main script이고,
calculator.py는 import되는 module이다.

## 1.5 package

### package란

Package는 여러 module을 하나의 계층적 namespace 아래에 묶어 관리하는 directory 기반 module이다.

쉽게 말하면
```
module = .py 파일
package = module들이 들어 있는 folder
```
구조
```
function / variable / class
        ↓
      module
        ↓
      package
        ↓
      library
```

### package 사용 이유

같은 이름의 파일이 있어도 package가 다르면 구분할 수 있다.
```
project/

 ├── main.py          ← 실행 파일

 ├── farith/           ← package 1
 │      └── ds_cal.py    ← module

 └── ftri/             ← package 2
        └── ds_cal.py    ← module
```

```python
import farith.ds_cal as arith 
# farith package 안에 있는 ds_cal module을 가져와서 arith라 부름

import ftri.ds_cal as tri # ftri package 안에 있는 ds_cal module을 가져와서 tri라고 부름
```
사용할 때는

```python
arith.ds_addition(1, 2)
tri.ds_cos(3.14)
```

처럼 package 경로를 포함해서 구분한다.

### namespace package 

물리적으로 나뉜 package들을 하나의 논리적 package처럼 다루는 것


---

# 2. import

## 2.1 import란
다른 module 안에 정의된 변수, 함수, 클래스 등을 현재 파일에서 사용할 수 있게 하는 문장이다.

```python
import calculator
```

### 2.1.1 모듈 import 시 과정
```
1. calculator라는 module을 찾음
2. calculator.py를 실행함
3. calculator module object를 생성함
4. 현재 파일에서 calculator라는 이름으로 접근 가능하게 함
```

즉,
```
import = module 찾기 + 실행하기 + namespace 연결하기
```
이며 현재 파일에 calculator라는 module object를 가리키는 namespace가 생긴다.

따라서 다음처럼 사용할 수 있다.
```python
calculator.add(1, 2) 
# calculator라는 module namespace 안에서 add라는 함수를 찾아 호출
```

### 2.1.2 모듈의 반복 사용
같은 module을 여러 번 import해도 실제 실행은 최초 한 번만 일어난다.

```python
import echo
import echo
```

이미 import된 module이 메모리에 저장되어 있기 때문에 첫 번째 import 때만 실행되고, 두 번째 import 때는 다시 실행되지 않는다.



#### 관련되는 객체 : `sys.modules`

이미 import된 module들을 저장하는 dictionary


## 2.2 import의 방식 ( 문법 기준 )

### 2.2.1 Explicit Import

전체 module을 import하는 방식이다.

```python
import calculator

calculator.add(1, 2)
```

- module 이름을 prefix로 붙여야 하고
- namespace 충돌이 적음
- 모듈의 이름이 길어지면 불편.

#### 참고 용어 : `prefix` 
모듈 이름 앞에 붙어서 "어느 패키지 소속인지" 알려주는 경로 이름

### 2.2.2 Aliased Import

module 이름이 길 때 별칭을 붙이는 방식이다.

```python
import calculator as cal

cal.add(1, 2)
```

```python
import numpy as np
import matplotlib.pyplot as plt
```


### 2.2.3 Selective Import

module 전체가 아니라 필요한 attribute만 가져오는 방식이다.

```python
from calculator import add

add(1, 2)
```
from 에서는 pakcage 또는 module 의 경로가 기재되고,
import 뒤에는 해당 package나 module에 속한 submodule이나 class, function, variable 등이 기재됨(⭐ 중요)

이 경우 module 이름 prefix가 필요 없다.
```python
calculator.add() --- X
add() --- O
```
### 2.2.4 Wildcard Import / Global Import

module 안의 이름들을 한꺼번에 가져오는 방식이다.

```python
from calculator import *
```
이 방식은 편하지만 일반적으로 추천되지 않는다.

이유는 어떤 이름들이 현재 namespace로 들어오는지 알기 어렵고, 이름 충돌이 발생하기 쉽기 때문이다.


예를 들어 다른 곳에도 add라는 함수가 있으면 어떤 add인지 헷갈릴 수 있다.

## 2.3  `__name__`과 `__main__`

### 2.3.1 `__name__`
special global variable. 파일이 어떻게 실행되었는지에 따라 값이 달라짐.

### 직접 실행된 경우

```python
python main.py
```
이면

```python
__name__ == "__main__"
```

### import된 경우

```python
import calculator
```

이면 calculator.py 안에서

```python
__name__ == "calculator"
```
가 된다.


### 2.3.2 직접 실행 시 활용 코드

```python
if `__name__` == `"__main__"`:
    main()
```

이 파일이 직접 실행될 때만 main()을 실행

참고 용어 : `Dunder`

`__name__`, `__main__`, `__init__`, `__all__`처럼 앞뒤에 double underscore가 붙은 이름을 dunder라고 한다.

이런 이름들은 Python 언어에서 특별한 의미로 사용된다.

## 2.4 import 문제점 - reassignment

Python에서는 module 안의 attribute를 쉽게 바꿀 수 있다.

```python
import math

print(math.pi)

math.pi = 72

print(math.pi)
```

이렇게 하면 현재 Python session 안에서는 math.pi가 72를 가리키게 된다.

하지만 실제 math.py 파일이 수정되는 것은 아니다.

이것은 Python에서 상수를 완전히 고정할 수 없다는 단점과 연결된다.




---
# 3. module serach path 

import를 하려면 Python은 먼저 해당 module 파일을 찾아야 하는데, 이때 참고하는 경로 목록이 Module Search Path이다.
<img width="476" height="350" alt="image" src="https://github.com/user-attachments/assets/fa5c55a8-d6fc-469b-81d0-ed702b7083e1" />


## 3.1 Module Search Path의 우선순위

Python은 다음 순서로 module을 찾는다.

```
1. main script가 있는 위치 
   또는 Python이 실행된 current working directory

2. PYTHONPATH 환경변수에 지정된 directory / zip file

3. Python Standard Library directory

4. site module이 추가하는 site-specific directory
   - site-packages
   - site-packages 안의 .pth 파일에 적힌 path
```

중요한 점은

**앞쪽 경로에서 먼저 발견된 module이 우선 import된다.**

## 3.2 최우선 경로

Python은 import할 때 가장 먼저 특정 경로부터 찾음.
```
python main.py → main.py 위치가 우선

python -m → 현재 작업 폴더가 우선
```

## 3.3 PYTHONPATH

추가 검색 경로 지정 환경변수
Python이 import할 때 원래 경로 외에 추가로 찾게 함.

예시
```
export PYTHONPATH="/home/test0:/home/test1"
```
의 의미는
```
/home/test0 도 찾아라
/home/test1 도 찾아라
```


#### 운영체제 구분자

Windows `;`

Linux `:`

## 3.4 Standard Library와 site-packages

### Standard Library
Python 설치하면 기본 제공됨.

예시
```python
import math
import os
import sys
```


### site-packages

외부 라이브러리 설치 위치

예시
```python
pip install numpy
```

설치 위치
```
site-packages
```
## 3.5.pth 파일

추가 경로 저장 파일

예시
```python
site-packages/config.pth
```
내용
```
/home/myproject
```
뜻
```
/home/myproject도 import 검색 경로에 추가
```

.pth 파일에 적힌 경로는 Python 시작 시 sys.path에 추가된다.


## 3.6 sys.path와 sys.modules (⭐ 중요)

Module 검색과 관련해서 가장 중요한 객체는 두 가지이다.

### 3.6.1 sys.path

Python이 새 module을 찾을 때 확인하는 경로 목록이다. 어느 폴더에서 찾을지를 의미.

```python
import sys
print(sys.path)
```
Module Search Path가 저장된 list임.

### 3.6.2 sys.modules

이미 import된 module들이 저장된 dictionary이다.

```python
import sys
print(sys.modules)
```
### 차이
|             | 의미        |
| ----------- | --------- |
| sys.path    | 찾을 위치     |
| sys.modules | 이미 불러온 모듈 |


## 3.7 Absolute Import와 Relative Import ( 경로 기준 )

### 3.7.1 Absolute Import

전체 package 경로 작성
```python
import package0.package1.module0
```

예시 구조
```
project/

   package0/
      package1/
         module0.py
```


### 3.7.2 Relative Import

현재 package 기준 import
```python
from . import module1

```
#### `.` 의미
```
.   = 현재 package
..  = 상위 package
```

예시 구조
```python
mypackage/

   module0.py
   module1.py
```

module0.py
```python
from . import module1
```
현재 package 안의 module1 가져와라

### 3.7.3 Relative Import 주의점

직접 실행
```python
python module0.py
```

Python은 module0.py 를 main script로 판단

```python
__name__ = "__main__"
```
현재 package 정보가 사라짐.

그래서
```python
from . import module1
```
오류 발생 가능.


#### 해결 방법
```python
python -m mypackage.module0
```


# 정리

#### 1. 파일 만들기
```python
# calculator.py

def add(a,b):
    return a+b

x = 10
```
#### 2. main.py에서 import 

```python
# main.py

import calculator
```


Python은 이 코드를 보면 먼저
calculator.py 어디 있지?
찾아야 함.

#### 3. sys.path = 찾을 폴더 목록

Python 내부에는 목록이 있음.

```python
# sys.path
[
 현재 폴더
 site-packages
 python 기본 라이브러리 폴더
]
```
Python은 여기서 찾음.
calculator.py 있나? 아직 함수 실행 아님. namespace 없음.

#### 4. Python이 calculator.py를 읽는다

찾았으면 파일 내용을 읽음.

```python
def add(a,b):
    return a+b

x = 10
```

Python은 이 코드를 실행해야 함.

근데 그냥 실행하면 값들을 저장할 공간이 필요함.



#### 5. calculator namespace 생성

```python
# calculator namespace

{
}
```
읽고 난 후 
```python
# calculator namespace

{
  add : 함수
  x   : 10
}
```

#### 6. main.py namespace에도 저장

```python
# main namespace

{
   calculator : (calculator module)
}
```


#### 7. calculator.add()
```
calculator.add(1,2)
```
Python은 두 번 찾는다.

1. main namespace에서 calculator 어디 있지?

2. calculator = calculator module 안에서 add 어디 있지?

3. 실행


---

# 4. dictionary

## 4.1 Dictionary란?

Dictionary (`dict`) 는 Python의 자료형 중 하나로,
`key-value pair` 를 item으로 가지는 **collection 자료형**이다.
<img width="308" height="169" alt="image" src="https://github.com/user-attachments/assets/e08e8188-0b7e-488b-af8a-e0e8f9c8f40f" />


---

## 4.2 Dictionary의 특징

### 4.2.1 key-value pair 구조

데이터를 단순히 순서대로 저장하는 것이 아니라

```text
key : value
```

형태로 저장한다.

예시

```python
student = {
    "name": "Kim",
    "age": 20
}
```

구조

```text
"name" → "Kim"
"age"  → 20
```

list가 위치(index)를 기준으로 값을 저장한다면

dictionary는 key를 기준으로 값을 저장하며, 따라서 접근할 때도 key를 이용한다.
```python
a = {
   "name":"Kim"
}
```

접근

```python
a["name"] # key로 접근
```

결과

```text
Kim
```

---

### 4.2.2 unordered

Dictionary는 list처럼 index 순서가 중요한 자료형이 아니다.

#### List

```python
a = [10,20,30]
```

저장 구조

```text
0 → 10
1 → 20
2 → 30
```

#### Dictionary

```python
a = {
   "x":10,
   "y":20
}
```

저장 구조

```text
"x" → 10
"y" → 20
```

즉 dictionary는

```text
몇 번째인가? (X)

어떤 key인가? (O)
```

가 중요하다.

#### 참고
dic은 원래 순서를 보장하지 않으므로 출력 순서가 실행할 때마다 달라질 수 있었다.

하지만 Python 3.7부터입력한 순서가 유지된다.

#### 참고 용어 : `OrderedDict`

삽입 순서를 명확하게 보장하는 dictionary

```python
collections.OrderedDict
```


### 4.2.3 mutable (⭐ 중요 )

Dictionary는 생성 후 수정이 가능하다.

예시

```python
a = {
   "age":20
}
```

값 변경

```python
a["age"] = 30
```

결과

```python
{'age':30}
```

새로운 item 추가도 가능하다.
- collection 자료형



### 4.2.4 Collection
<img width="386" height="169" alt="image" src="https://github.com/user-attachments/assets/5b8a6404-dcc9-4786-a760-d2bd3c502457" />

Dictionary는 여러 개의 데이터를 하나의 객체 안에 저장한다.

예시

```python
person = {
   "name":"Lee",
   "age":21,
   "major":"EE"
}
```

### 4.2.5 Hashing

추가 메모리를 사용해서 검색 시간을 줄이는 방식

Dictionary는 list보다 검색 속도가 매우 빠르다.

list

```python
a = [10,20,30,40]
```

30을 찾으려면

```text
10 확인

20 확인

30 확인
```

처럼 하나씩 확인해야 한다.

---

dictionary

```python
a = {
   "name":"Kim"
}
```

검색

```python
a["name"]
```

Python은 바로 해당 값을 찾는다.



## 4.3 Key의 조건 (⭐ 시험 )

Dictionary에서 key는 몇 가지 조건이 있다.

---

### 4.3.1 Key는 Unique 해야 한다

같은 key를 두 번 사용할 수 없다.

예시

```python
a = {"age":20,"age":30}
```

결과

```python
{'age':30}
```

Python은 같은 key가 있으면 뒤의 값으로 덮어쓴다.

---

### 4.3.2 Key는 Immutable Object만 가능하다 (⭐ 중요 )

Key는 변경되지 않는 객체만 사용할 수 있다.

가능한 객체

```python
int
float
str
bool
tuple
```

예시

```python
a = {
   "name":"Kim",
   10:"hello"
}
```

가능하다.

---

변경 가능한 객체는 key가 될 수 없다.

예시

```python
a = {
   [1,2] : "hello"
}
```

오류 발생


---

## 4.4 Dictionary 생성

기본적으로 5가지 방법이 있음.

```python
d1 = {'a':1, 'b':2, 'c':3}

d2 = dict([('a':1), ('b':2), ('c':3)])

d3 = dict([['a':1], ['b':2], ['c':3]])

d4 = dict(a=1,b=2,c=3) # 이 경우엔 key가 무조건 str

k = ["a", "b", "c"]
v = [1, 2, 3]
d5 = dict(zip(k,v))
```

비어있는 curly bracket은 보통 dic임.
```python
d = {}
print(f"{type(d) = }") # <class 'dict'>
```
## 4.5 추가, 수정, 삭제, 확인

Dictionary는 기본적으로

```text
square bracket [ ] + key
```

를 이용해서 item에 접근한다.

---

### 4.5.1 key-value 추가

존재하지 않는 key에 값을 대입하면 새로운 item이 추가된다.

```python
a = {"name":"Kim"}
```

```python
a["age"] = 20
```

실행 후

```python
{
   'name':'Kim',
   'age':20
}
```


### 4.5.2 value 수정

이미 존재하는 key에 값을 대입하면 기존 value가 교체된다.

```python
{'name':'Kim'}
```

```python
a["name"] = "Lee"
```

실행 후

```python
{'name':'Lee'}
```

---

### 4.5.3  key-value 삭제

Dictionary에서 삭제는 `del` 을 사용한다.

기본 구조

```python
a = {"name":"Kim","age":20}
```

삭제

```python
del a["age"]
```

결과

```python
{'name':'Kim'}
```
key-value 모두 삭제

---


#### 참고 : 존재하지 않는 key를 삭제하면 오류 발생


### 4.5.4 key 확인 : Membership Operator `in`

Dictionary에서도 `in` 연산자를 사용할 수 있다.

key를= 확인하는 데 쓰임.(value는 안됨)

```python
>>> dict = {'gachon': 100, 'bme': 200, 'elec': 300}
>>> 'bme' in dict
True
>>> 300 in dict
False
```



## 4.6 Dictionary's methods

<img width="310" height="158" alt="image" src="https://github.com/user-attachments/assets/305b7e0a-69d6-476d-ad29-d8ae4931b18b" />

- 모두 삭제 : dic.clear()

- 값 반환: dic.get(key) (⭐ 중요 )
    ```
    → key 없으면 None
    → key 있으면 기존 값 반환
    ```
    square bracket을 통한 indexing보다 권장되는데, key가 없어도 오류가 안나기 때문

- dic.get(key,default_value)

- 반환과 제거 : dic.pop(key) : value 반환 + 해당 key-value 제거(⭐ 중요 )

- dic.pop(key, default_value)

- dic.setdefault(key)

```
→ key 없으면 추가 
→ key 있으면 기존 값 반환
```

- dic.setdefault(key,value)

- dic.update(other_dic)

- 업데이트 : dic.update(other_dic) (⭐ 중요 )
dic.update(other_dic)

예시
```python
a = {"x":1,"y":2}

b = {"y":10,"z":20}

a.update(b)
```

결과
```
{
   "x":1,
   "y":10,
   "z":20
}
```

```
같은 key  → 값 변경

없는 key  → 새로 추가

원래 key → 유지
```

- loop
<img width="65" height="23" alt="image" src="https://github.com/user-attachments/assets/b436e79a-bc91-4658-8b21-1d4d21f7c0cd" />

<img width="78" height="25" alt="image" src="https://github.com/user-attachments/assets/4ba29d82-d066-47b4-b4ba-55af209f4d06" />

<img width="80" height="28" alt="image" src="https://github.com/user-attachments/assets/c17cd298-49f9-4317-b497-ec466b2322cf" />


이 메서드들은 list를 바로 반환하는 것이 아닌
```
dict_keys

dict_values

dict_items
```

라는 special object를 반환한다.
이 객체들은 반복(for문) 가능하다.


# 윤성우 열혈 파이썬 11

### import
<img width="292" height="170" alt="image" src="https://github.com/user-attachments/assets/a1863d18-acc3-4493-90c9-4dd1c5d7426a" />

<img width="322" height="230" alt="image" src="https://github.com/user-attachments/assets/ff028227-cb4f-42b3-aec5-c0d33c919a5c" />

<img width="296" height="196" alt="image" src="https://github.com/user-attachments/assets/4244c8dd-480a-4e0c-9a7d-59b86068f9f1" />

<img width="233" height="110" alt="image" src="https://github.com/user-attachments/assets/9582230a-add0-4034-9086-e459a43552c4" />

<img width="314" height="232" alt="image" src="https://github.com/user-attachments/assets/bc55311f-31d3-40d0-9ebc-6c14a1df9393" />

<img width="317" height="248" alt="image" src="https://github.com/user-attachments/assets/6949c205-1946-4982-a645-ce0832ba7a1c" />

<img width="208" height="116" alt="image" src="https://github.com/user-attachments/assets/41c2086d-17cb-4f98-9d3d-7316d843203e" />

# 윤성우 열혈 파이썬 12

### dic

<img width="294" height="167" alt="image" src="https://github.com/user-attachments/assets/4af5a331-4157-48c0-a9c3-13c1cbf2fb2c" />

### 같은 key 불가
<img width="152" height="143" alt="image" src="https://github.com/user-attachments/assets/fa6b4761-21b5-4ef3-b351-5d641aa1dc4c" />

### loop
<img width="312" height="221" alt="image" src="https://github.com/user-attachments/assets/a10e2dfa-2bf2-4051-a897-0f79dc7e3632" />



# 과제

