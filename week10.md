# Week10

## 이번 주 큰 흐름

- Binding
- Namespace
- Scope, LEGB
- 함수 호출과 Frame, call stack
- local, global variable / nonlocal(closure), global 키워드
- Context와 전체 실행 흐름
---
- Parameter의 종류와 Slash, Asterisk  
---

# 1. 변수와 객체의 연결 - Binding

```python
x = 10
```
- x 는 name(이름)
- 10 은 object(객체)

즉, x라는 이름을 10이라는 객체에 연결(binding)하는 과정이 **assignment**


---


# 2. Namespace 

## 2.1 Namespace란

변수 이름과 그 값(객체)을 binding하여 저장하는 이름표 보관함.

동일한 identifier라도 namespace가 다르게 할당하면 충돌 없이(name collision) 사용이 가능하다


Python의 경우,
```
function call
↓
function의 local variable들을 포함(paramerter들도 포함됨)하는 namespace 생성
↓
해당 function의 execution 동안 유지, 종료되면 해당 namespace 사라짐.
```

## 2.2 Global Namespace

프로그램(모듈) 전체에서 공유되는 namespace.

```python
x = 10

def f():
    pass
```
여기서 x, f는 global namespace에 저장된다.

## 2.3 Local Namespace

함수 호출 시 생성되는 namespace.

```python
def f():
    a = 1
    b = 2
```
함수 종료 시 보통 사라진다.

### global, local namespace 비교

```python
x = 10  # global variable
 
def foo():
    x = 20  # local variable
    print(x)
 
foo()  # 출력: 20
print(x)  # 출력: 10
```


#### 참고 : 파이썬 제공 namespace
- built-in namespace
- global namespace
- local namespace

---


# 3. Scope : 이름 탐색 규칙

## 3.1 Scope란 (⭐ 중요)
좁은 의미에서는 현재 함수 자신의 영역을 가리키고, 

넓은 의미에서는 현재 위치에서 접근 가능한 범위를 말한다. 

특정 name이 유효한 범위라고도 하는데 이는 특정 name이 실제로 어떤 객체가 무엇이냐를 결정하는 규칙과 관련된다는 것을 의미한다.

#### 참고 : scope 규칙의 종류
- Lexical scope (or static scope)
   - block scope (C, C++등)
   - function scope (**Python**, JavaScript등)
- Dynamic scope

Python이나 C, Java, JavaScript 등의 대중적인 언어의 대부분이 Lexical scope를 따른다. 따라서 dynamic scope는 다루지 않음.

## 3.2 Namespace와 Scope 차이

```python
x = "global"

def outer():
    y = "outer"

    def inner():
        z = "inner"

        print(x)
        print(y)
        print(z)

    inner()

outer()
```

실행 순서
```
[1] 프로그램 시작
    global namespace 생성

[2] x = "global" 실행
    global namespace에 x 저장

[3] def outer(): 실행
    outer 함수 객체 생성
    global namespace에 outer 저장

[4] outer() 호출
    outer frame 생성
    outer local namespace 생성

[5] y = "outer" 실행
    outer local namespace에 y 저장

[6] def inner(): 실행
    inner 함수 객체 생성
    outer local namespace에 inner 저장

[7] inner() 호출
    inner frame 생성
    inner local namespace 생성

[8] z = "inner" 실행
    inner local namespace에 z 저장

[9] print(x)
    inner local에 x 없음
    outer enclosing에 x 없음
    global에서 x 발견
    → global 출력

[10] print(y)
    inner local에 y 없음
    outer enclosing에서 y 발견
    → outer 출력

[11] print(z)
    inner local에서 z 발견
    → inner 출력

[12] inner() 종료
    inner frame 제거

[13] outer() 종료
    outer frame 제거
```

### 3.2.1 namespace 관점
namespace는 이름이 실제로 저장되는 공간이다. 
여기서 함수 이름도 객체이므로 namespace에 저장된다.
- Global Namespace
```
{
    "x": "global",
    "outer": <function>
}
```
- outer()의 Local Namespace, 호출 시 생성
```
{
    "y": "outer",
    "inner": <function>
}
```
- inner()의 Local Namespace, 호출 시 생성
```
{
    "z": "inner"
}
```
### 3.2.2 scope 관점

scope는 현재 위치에서 어떤 namespace까지 접근 가능한가이다.

- global scope에서 보이는 것
```
┌───────────────────────────┐
│ Global Namespace          │
│───────────────────────────│
│ x                         │ ← 보임
│ outer                     │ ← 보임
└───────────────────────────┘

outer namespace 안쪽은 직접 못 봄
inner namespace 안쪽(y, inner,z)도 못 봄
```

- outer scope에서 보이는 것
```
┌───────────────────────────┐
│ outer() Local Namespace   │
│───────────────────────────│
│ y                         │ ← 보임
│ inner                     │ ← 보임
└───────────────────────────┘
inner namespace안쪽 z 볼 수 없음
              │
              │ 바깥도 볼 수 있음
              ▼
┌───────────────────────────┐
│ Global Namespace          │
│───────────────────────────│
│ x                         │ ← 보임
│ outer                     │ ← 보임
└───────────────────────────┘
```

- inner scope에서 보이는 것
```
┌───────────────────────────┐
│ inner() Local Namespace   │
│───────────────────────────│
│ z                         │ ← 보임
└───────────────────────────┘
              │
              │ enclosing scope
              ▼
┌───────────────────────────┐
│ outer() Local Namespace   │
│───────────────────────────│
│ y                         │ ← 보임
│ inner                     │ ← 보임
└───────────────────────────┘
              │
              │ global scope
              ▼
┌───────────────────────────┐
│ Global Namespace          │
│───────────────────────────│
│ x                         │ ← 보임
│ outer                     │ ← 보임
└───────────────────────────┘
```

**(⭐ 중요) 핵심은 안쪽은 바깥쪽을 볼 수 있지만, 바깥쪽은 안쪽을 볼 수 없다.**


## 3.3 LEGB Rule
![alt text](assets/Week09/image.png)

### 예제 코드 1

```python
x = "global"

def outer():
    x = "outer"

    def inner():
        print(x)

    inner()

outer()
```

실행 시:
```
inner local namespace 확인 - 없음
        ↓
outer enclosing : scope 확인 - 발견 
        ↓
global 확인
        ↓
built-in 확인
```


결과 :

```
outer
```

### 예제 코드 2

```python
x = "global"

def outer():

    def inner():
        print(x)

    inner()

outer()
```

```
inner local namespace 확인 - 없음
        ↓
outer enclosing : scope 확인 - 없음
        ↓
global 확인 - 발견
        ↓
built-in 확인
```

결과 :

```
global
```

### 예제 코드 3  (⭐ 중요)
```python
g = "global"

def outer():
    a = "outer"

    def inner():
        b = "inner"

        print(g)
        print(a)
        print(b)

    inner()

    print(b)   # NameError, outer 함수에서 inner local namespace 안 변수 접근 불가

outer()

print(a)       # NameError, global에서 outer local namespace 안 변수 접근 불가
```

---


# 4. 함수 호출과 Frame

## 4.1 Frame 생성

함수 호출 시 새 실행 환경이 만들어지고, 그 실행 환경 객체를 frame이라고 한다. 

즉, frame은 함수 호출 1회의 실행 상태를 의미

## 4.2 Frame 안의 Local Namespace

frame 안에는

- local namespace
- 현재 실행 위치
- 호출 정보

등이 들어있다.

(⭐ 중요) 함수가 정의 시에는 함수 객체가 생성되고, 호출 시에는 frame, namespace가 생성된다.


## 4.4 Call Stack

함수 호출은 frame stack으로 관리되는데

```python
def a():
    b()

def b():
    c()

def c():
    pass
```
가 실행 중일 때

```
c frame
b frame
a frame
```
형태로 stack이 쌓인다.
---


# 5. Variable 구분 / global, nonlocal(closure) 키워드

## 5.1 Local Variable

현재 함수 안의 변수를 의미.

함수 내부에서 정의(lexical scope)되어 그 함수 안(=scope)에서만 유효한 변수

```python
def f():
    x = 1
```

## 5.2 Global Variable

모듈 전체 변수를 의미

함수 외부에서 정의(lexical scope)되어 전역적(global)으로 접근(=scope) 가능한 변수

## 5.3 global 키워드
global 키워드를 통해 전역변수를 가리키도록 지정해두면,

이후 해당 variable은 global namespace에 존재하는 객체를 가리키게 된다.
즉, 함수 안에서도 global variable(전역변수)을 직접 사용한다는 의미이다.

### 예제
```python
num = 10

def func(value):

    result = value + num   # Error 발생

    num = 20               # assignment와 read를 동시에 수행
                           # → Python은 num을 local 변수로 판단함

    print(result)

func(5)

print(num)
```

num = 20 line이 없을 경우에는 아무 문제가 없지만 해당 라인이 추가 되면 에러가 발생하는데,

Python은 함수 호출 전 함수 안에서 
```
num = ...
```
같은 assignment를 발견하면 num이 local변수라 미리 판단하고(namespace와 무관하게) 실제로 호출되었을 때 
```
result = value + num
```
을 계산하기 위해 local 변수를 찾으며, 실제로는 변수에 아직 값이 할당되지 않은 상태이므로 오루가 발생한다.

해결책으로는 
- global 키워드
```python
num = 10

def func(value):

    global num

    result = value + num

    num = 20

    print(result)

func(5)

print(num)

출력:

15
20
```

여기서
```
num = 20
```
은 local variable 생성이 아니라 global variable 자체를 수정

- ```num = 20``` 이 ```result = value + num```보다 먼저 사용


```python
num = 10
def func(value):

    num = 20

    result = value + num

    print(result)

func(5)

print(num)

출력:

25
10
```
여기서는  함수 내부의 num, global의 num 같고 서로 다른 variable.


#### 참고 : ```variable shadowing```
바깥 scope의 변수와 같은 이름의 변수를 안쪽 scope에서 새로 만드는 것

안쪽 scope의 변수가 바깥 변수 이름을 가려버리는 현상이다.


## 5.4 nonlocal 키워드와 closure

## nonlocal 키워드
nonlocal 키워드는 global과 유사하지만, nested function 내부에서
자신을 둘러싸고 있는 **enclosing function의 variable**을 사용하겠다고 명시할 때 사용한다.

- global → global scope 변수 사용
- nonlocal → enclosing scope 변수 사용



### 예제
```python
def outer():

    num = 10

    def inner():

        nonlocal num

        num += 1 # inner()의 local variable이 아니라 outer()의 local variable을 수정

        print(num)

    inner()
    inner()

outer()

출력:

11
12
```

local namespace에 새로운 num을 만들지 않고 enclosing scope의 num을 사용

nonlocal 없이 assignment하면?
```python
def outer():

    num = 10

    def inner():

        num += 1 # UnboundLocalError : assignment로 처리,  local 변수라고 먼저 판단

        print(num)

    inner()

outer()
```
local num에 값이 아직 없는데 읽으려 하기 때문에 오류가 발생

## closure

enclosing(non-local) scope의 variable 상태를 기억하고 있는 nested function


즉 nested function이 바깥 함수의 variable을 계속 유지하고 사용하는 구조이다.

### 예제
```python
def counter():

    count = 0

    def closure_func():

        nonlocal count

        count += 1

        print(f'호출 횟수: {count}')

        return count

    return closure_func

c_func = counter()

c_func()
c_func()
c_func()
c_func()

출력:

호출 횟수: 1
호출 횟수: 2
호출 횟수: 3
호출 횟수: 4
실행 흐름
c_func = counter()
```

실행 시 counter()는 종료되지만 closure_func가 count를 계속 참조하고 있으므로 count 상태가 유지된다.

따라서 c_func()를 여러 번 호출해도 count 값이 계속 누적된다.

---

# 6. Context와 전체 실행 흐름

## 6.1 Execution Context

context는 현재 실행 환경 전체를 의미하는 넓은 개념으로 현재의 frame, 현재의 scope, globals/locals 등을 모두 포함한다.

## 6.2 전체 흐름 연결
```
함수 호출
→ frame 생성
→ local namespace 생성
→ scope(LEGB)로 이름 탐색
→ 필요 시 enclosing scope 유지(closure)
```

--- 

# 7 Parameter의 종류와 Slash,Asterisk 

## 7.1 slash / 와 asterisk *의 사용

parameters 중,

- positional parameters 로만 사용

- positional parameters 또는 keyword parameters(=named parameter) 모두 사용

- keyword parameters(=named parameter) 로만 사용

하는지 알려주는데 사용되는 symbol


- `/` 위치 전용 매개변수 구분자(Positional-only Parameters Separator)
- `*` :키워드 전용 매개변수 구분자(Keyword-only Parameters Separator)
<img width="311" height="259" alt="image" src="https://github.com/user-attachments/assets/d33ed41c-db12-46c5-bec6-8cdb6e077aa9" />

## 7.2 parameter의 종류
- 위치 전용 매개변수`/ 기호 이전에 선언된 매개변수`

- 위치 또는 키워드 매개변수 `/와 * 사이에 선언된 매개변수`

- 키워드 전용 매개변수 `* 또는 *args 이후에 선언된 매개변수`

    - 이후엔 positional argument가 위치할 수 없음

- 기본값이 있는 매개변수

    - 함수 호출 시 인자를 제공하지 않으면 기본값 사용

- 가변 위치 인자 `*args`
    
    - 위치 인자 패킹(Positional Arguments Packing)이라고도 함
    - 추가 위치 인자를 튜플로 수집

- 가변 키워드 인자 `**kwargs`

    - 키워드 인자 패킹(Keyword Arguments Packing)이라고도 함
    - 추가 키워드 인자를 딕셔너리로 수집

## 7.3 예제


### 예제1 
```python
def func(
    a, b, /,
    c, d=10,
    *args,
    e, f=True,
    **kwargs
):
    pass
```
```
[a,b] / [c,d=10] *args → [e,f=True] **kwargs
   ↑         ↑            ↑             ↑
위치전용   일반파라미터   키워드전용   남는 키워드 수집
```

### 예제 2 
```python
def test(a, /, b, *args, c, **kwargs):
    print(a)
    print(b)
    print(args)
    print(c)
    print(kwargs)

test(1, 2, 3, 4, c=5, x=10, y=20)
```

결과
```python
a = 1
b = 2
args = (3,4)
c = 5
kwargs = {'x':10, 'y':20}
```

### 예제 3

```python
def func(
    a, b, /,
    c, d=10,
    *args,
    e, f=True,
    **kwargs
):
    print(f"a = {a}")
    print(f"b = {b}")

    print(f"c = {c}")
    print(f"d = {d}")

    print(f"args = {args}")

    print(f"e = {e}")
    print(f"f = {f}")

    print(f"kwargs = {kwargs}")


func(
    1, 2,              # a, b (positional-only)

    3,                 # c
    4,                 # d

    5, 6, 7,           # *args

    e=8,               # keyword-only
    f=False,           # keyword-only

    x=100,
    y=200              # **kwargs
)
```

결과
```python
a = 1
b = 2

c = 3
d = 4

args = (5, 6, 7)

e = 8
f = False

kwargs = {'x': 100, 'y': 200}
```


# 8. 윤성우의 열혈 파이썬 10

### 인자 전달
<img width="313" height="113" alt="image" src="https://github.com/user-attachments/assets/04593c55-dcf5-451d-8c84-13a89ac51904" />

<img width="222" height="200" alt="image" src="https://github.com/user-attachments/assets/3c789cb5-b9ba-4d41-ad0a-8de4fddbb270" />

<img width="299" height="177" alt="image" src="https://github.com/user-attachments/assets/27cc73de-9dec-461d-a284-7cd0dbe3846a" />



