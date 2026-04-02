# Week 4

## 1. int형과 float형

Python에서 숫자형 데이터는 크게 `int` 와 `float` 로 나눌 수 있다.

* `int` : 정수(integer)
* `float` : 실수(floating point number)

예

```python
x = 10
y = 3.14
```

### int형

정수형은 소수점이 없는 숫자를 표현한다.

예

```python
a = 3
b = -10
c = 0
```

Python의 `int` 는 C언어처럼 고정 크기가 아니라, **가변 길이 정수** 이므로 매우 큰 정수도 표현할 수 있다.

예

```python
print(999999999999999999999999999999999999)
```

---

### float형

실수형은 소수점이 있는 숫자를 표현한다.

예

```python
x = 3.14
y = -0.5
z = 2.0
```

float는 내부적으로 **근삿값(approximation)** 으로 저장되기 때문에, 계산 과정에서 오차가 발생할 수 있다.

예

```python
print(0.1 + 0.2)
```

결과

```python
0.30000000000000004
```

즉, float는 수학적 실수를 완벽하게 저장하는 것이 아니라, **컴퓨터가 표현 가능한 가장 가까운 값** 으로 저장한다.

### 참고

* 매우 큰 수와 매우 작은 수를 함께 계산할 때
* 소수 계산을 여러 번 반복할 때

오차가 누적될 가능성이 커진다.

---

## 2. type()

`type()` 은 Python의 **built-in function(빌트인 함수)** 이며, 어떤 object의 type을 확인할 수 있다.

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

### 추가 개념

Python에서 `type` 은 단순한 확인 함수이기도 하지만, 동시에 **class를 다루는 개념** 과도 연결된다.
Python에서는 object의 type을 class로 표현하며, class조차 object로 취급한다.

즉, Python은 object 중심으로 동작하는 언어라는 점을 다시 확인할 수 있다.

---

## 3. Bitwise Operator

Bitwise Operator는 정수를 **비트(bit) 단위로 나누어 연산** 하는 연산자이다.

일반적인 Python 프로그래밍에서는 자주 쓰이지 않지만,

* low-level 연산
* binary data 처리
* Tensor / element-wise 연산

등에서 중요하게 사용될 수 있다.

### 사용 가능한 operand

주로 다음에 사용한다.

* `int`
* `bool`
* `bytes`, `bytearray` 의 **각 요소**

즉, `bytes` 나 `bytearray` 는 전체를 한 번에 비트 연산하는 것이 아니라, **각 요소별로 꺼내서 처리** 해야 한다.

---

## 4. Bitwise Operator 종류

### 4.1 비트 NOT : `~`

각 비트를 반전시킨다.

```python
print(~5)
```

5를 8비트 기준으로 보면

```text
00000101
```

이를 반전시키면

```text
11111010
```

이 값은 `-6` 으로 해석된다.

즉,

```python
~x = -(x + 1)
```

이 성질이 성립한다.

예

```python
print(~5)   # -6
print(~0)   # -1
```

### 주의

이 개념은 **2의 보수(two’s complement)** 표현과 관련된다.

---

### 4.2 왼쪽 시프트 : `<<`

비트를 왼쪽으로 이동시키고, 오른쪽은 0으로 채운다.

예

```python
print(5 << 1)
```

5는

```text
00000101
```

왼쪽으로 1칸 이동하면

```text
00001010
```

즉 10이 된다.

결과

```python
10
```

### 의미

보통 `<< 1` 은 **2배** 와 비슷하게 생각할 수 있다.

---

### 4.3 오른쪽 시프트 : `>>`

비트를 오른쪽으로 이동시킨다.

예

```python
print(10 >> 1)
```

10은

```text
00001010
```

오른쪽으로 1칸 이동하면

```text
00000101
```

즉 5가 된다.

결과

```python
5
```

### 특징

* 양수: 왼쪽을 `0` 으로 채움
* 음수: 왼쪽을 `1` 로 채워 sign 유지

즉, Python의 `>>` 는 **산술 시프트(arithmetic shift)** 의 성격을 가진다.

---

### 4.4 비트 AND : `&`

두 비트를 비교해서 **둘 다 1일 때만 1** 이 된다.

예

```python
print(5 & 3)
```

```text
5 = 0101
3 = 0011
------------
    0001
```

결과

```python
1
```

---

### 4.5 비트 XOR : `^`

두 비트를 비교해서 **서로 다를 때만 1** 이 된다.

예

```python
print(5 ^ 3)
```

```text
5 = 0101
3 = 0011
------------
    0110
```

결과

```python
6
```

### 읽는 법

`^` 는 **caret(캐럿)** 이라고 읽는다.

---

### 4.6 비트 OR : `|`

두 비트를 비교해서 **하나라도 1이면 1** 이 된다.

예

```python
print(5 | 3)
```

```text
5 = 0101
3 = 0011
------------
    0111
```

결과

```python
7
```

### 읽는 법

`|` 는 **vertical bar** 라고 부른다.

---

## 5. Bitwise Operator 우선순위

Bitwise 연산자의 우선순위는 다음과 같다.

```text
~  >  <<, >>  >  &  >  ^  >  |
```

즉, 여러 개를 섞어서 쓸 때는 precedence를 주의해야 하며,
헷갈릴 경우 괄호를 사용하는 것이 좋다.

---

## 6. bytes 와 bytearray에서의 bitwise 연산

Python에서는 `bytes` 나 `bytearray` 를 전체 단위로 바로 비트 연산하는 것이 아니라, **각 요소별(element-wise)** 로 처리해야 한다.

예

```python
a = bytes([0b10101010])
b = bytes([0b11001100])

res = bytes([a[0] | b[0]])
print(bin(res[0]))
```

결과

```python
0b11101110
```

즉, 각 바이트를 하나씩 꺼내서 연산한 뒤 다시 `bytes` 로 묶는다.

### 여러 바이트 처리

```python
a = bytes([0b11001100, 0b10101010])
b = bytes([0b11110000, 0b00001111])

res = bytes([x & y for x, y in zip(a, b)])
print([bin(byte) for byte in res])
```

결과

```python
['0b11000000', '0b0']
```

이 부분은 수업에서 설명되었지만, 시험엔 나오지 않을 예정이다.

---

## 7. 진법 표현

Python에서는 숫자를 다른 진법으로 표현할 수 있다.

* `0b` : binary (2진수)
* `0o` : octal (8진수)
* `0x` : hexadecimal (16진수)

예

```python
print(0b1010)   # 10
print(0o12)     # 10
print(0xA)      # 10
```

---

## 8. Boolean Operators

Boolean Operators는 **참/거짓(Boolean value)** 에 대해 동작하는 연산자이다.

Python에서는 영어 단어 형태로 사용한다.

```python
and
or
not
```

즉,

* `and`, `or`, `not` → Boolean Operator
* `&`, `|`, `~` → Bitwise Operator

이다.

### 중요한 구분

> 영어로 쓰면 Boolean
> 기호로 쓰면 Bitwise

즉, 비슷해 보여도 **의미가 완전히 다르다**.

---

## 9. Boolean Operator 종류

### 9.1 `and`

둘 다 True일 때만 True

예

```python
print(True and True)
print(True and False)
```

결과

```python
True
False
```

---

### 9.2 `or`

하나라도 True이면 True

예

```python
print(True or False)
print(False or False)
```

결과

```python
True
False
```

---

### 9.3 `not`

참/거짓을 반전시킨다.

예

```python
print(not True)
print(not False)
```

결과

```python
False
True
```

---

## 10. Short-circuit Evaluation

Boolean Operator는 **short-circuit evaluation(단락 평가)** 를 수행한다.

즉, 결과가 이미 정해졌다면 뒤를 더 계산하지 않는다.

---

### 10.1 `or` 의 경우

왼쪽에서 오른쪽으로 평가하다가 **하나라도 True가 나오면**, 뒤는 평가하지 않는다.

예

```python
print(True or (3 / 0))
```

결과

```python
True
```

`3 / 0` 은 원래 오류가 나야 하지만,
앞의 `True` 만으로 이미 전체 결과가 결정되므로 뒤를 계산하지 않는다.

---

### 10.2 `and` 의 경우

왼쪽에서 오른쪽으로 평가하다가 **하나라도 False가 나오면**, 뒤는 평가하지 않는다.

예

```python
print(False and (3 / 0))
```

결과

```python
False
```

즉,

* `or` → True를 만나면 멈춤
* `and` → False를 만나면 멈춤

이다.

---

## 11. Python의 Truthiness

Python에서는 실제 Boolean type이 아니더라도, **Boolean처럼 해석되는 값들** 이 있다.
이를 **truthiness** 라고 한다.

예를 들어 다음 값들은 False처럼 취급된다.

* `0`
* `0.0`
* `""` (빈 문자열)
* `[]` (빈 리스트)
* `()` (빈 튜플)
* `{}` (빈 딕셔너리)
* `set()` (빈 집합)
* `None`

예

```python
print(bool(0))
print(bool(""))
print(bool([]))
```

결과

```python
False
False
False
```

반대로, 비어 있지 않거나 0이 아닌 값은 보통 True처럼 취급된다.

예

```python
print(bool(5))
print(bool("hello"))
print(bool([1, 2]))
```

결과

```python
True
True
True
```

즉, Python에서는 “비어 있음 / 없음 / 0” 을 False처럼 다루는 경향이 있다.

---

## 12. Relational Operators (비교 연산자)

Relational Operators는 두 값을 비교하여 **Boolean type** 을 반환하는 연산자이다.

예

```python
<
<=
>
>=
==
!=
```

---

### 예시

```python
print(3 < 5)
print(10 == 10)
print(7 != 2)
```

결과

```python
True
True
True
```

### 특징

* 숫자형끼리 비교 가능
* 문자열끼리 비교 가능
* 결과는 항상 Boolean type

---

## 13. 문자열 비교

문자열 비교는 일반적으로 **lexicographic order** 에 따라 수행된다.

즉, 사전 순서(알파벳 순)처럼 비교된다.

예

```python
print("apple" < "banana")
print("cat" > "car")
```

결과

```python
True
True
```

### 비교 방식

문자열을 앞에서부터 한 글자씩 비교하다가,
처음 다른 문자가 나오면 그 문자 기준으로 비교한다.

만약 끝까지 같으면, **짧은 문자열이 더 작다**.

예

```python
print("abc" < "abcd")
```

결과

```python
True
```

즉, 비교할 것이 더 이상 없으면 **문자가 없는 쪽이 더 작다**.

---

## 14. Membership Operator

Membership Operator는 어떤 object가 collection 안에 **포함되어 있는지 여부** 를 확인하는 연산자이다.

```python
in
not in
```

결과는 Boolean type이다.

---

### 예시 1: 리스트

```python
print(3 in [1, 2, 3, 4])
print(5 in [1, 2, 3, 4])
```

결과

```python
True
False
```

---

### 예시 2: 문자열

```python
print("a" in "apple")
print("z" in "apple")
```

결과

```python
True
False
```

### 참고

문자열은 sequence type 중에서도 비교적 복잡하게 동작할 수 있으므로,
예외적인 경우나 세부 동작은 나중에 더 자세히 다룰 수 있다.
문자열에서의 membership은 한 번 더 복습해둘 필요가 있다.

---

## 15. Identity Operator

Identity Operator는 두 변수가 **같은 객체(object)를 참조하는지** 확인하는 연산자이다.

```python
is
is not
```

즉, 값이 같은지를 보는 것이 아니라 **“같은 객체냐?”** 를 보는 것이다.

---

### 예시

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)
print(a is b)
print(a is c)
```

결과

```python
True
False
True
```

### 의미

* `a == b` → 값이 같은가?
* `a is b` → 같은 객체인가?
* `a is c` → 같은 객체인가?

즉,

* `a` 와 `b` 는 값은 같지만 서로 다른 object
* `a` 와 `c` 는 같은 object

이다.

### 중요한 포인트

리스트처럼 mutable object에서는 이 차이가 특히 중요하다.

```python
a = [1, 2]
c = a
c.append(3)

print(a)
```

결과

```python
[1, 2, 3]
```

즉, 같은 object를 가리키고 있으면 서로 영향을 준다.

---

## 16. 문자열과 intern

문자열(str)의 경우에는 경우에 따라 **같은 객체처럼 보이는 상황** 이 생길 수 있다.
이는 Python의 **interning** 과 관련된다.

예

```python
a = "hello"
b = "hello"

print(a is b)
```

어떤 경우에는 `True` 가 나올 수 있다.

즉, 문자열에서는 Python이 메모리 효율을 위해 같은 문자열 object를 재사용할 수 있다.

### 주의

따라서 문자열 비교는 보통 `is` 가 아니라 `==` 로 하는 것이 안전하다.

---

## 17. `.` 연산자

`.` 도 Python에서 중요한 연산자이다.

예

```python
import sys
print(sys.argv)
```

여기서 `.` 은 앞의 object나 module 안에서 **attribute를 찾는 역할** 을 한다.

즉,

```python
sys.argv
```

는

```text
sys 모듈 안의 argv attribute
```

를 의미한다.

예를 들어

```python
"hello".upper()
```

에서는 문자열 object의 `upper` 라는 기능을 찾는 것이다.

즉, `.` 은 Python에서 object-oriented 구조를 이해할 때 매우 중요하다.

---

## 18. `:=` (Walrus Operator)

`:=` 는 **assignment와 expression의 기능을 동시에 수행** 하는 연산자이다.

즉, 값을 할당하면서 동시에 그 값을 사용할 수 있다.

예

```python
if (n := len("hello")) > 3:
    print(n)
```

결과

```python
5
```

### 의미

* `n = len("hello")` 를 하면서
* 동시에 그 결과를 비교에 사용

즉, **할당 + 값 반환** 을 동시에 수행한다.

---

## 19. `del`

`del` 은 변수나 collection의 요소를 삭제하는 데 사용된다.

예

```python
x = 10
del x
```

이후 `x` 에 접근하면 오류가 난다.

### 리스트 요소 삭제

```python
a = [1, 2, 3]
del a[1]
print(a)
```

결과

```python
[1, 3]
```

### 의미

`del` 은 단순히 “지운다”기보다
**reference를 제거하는 것** 으로 이해하는 것이 더 정확하다.

즉, 어떤 object를 가리키는 reference가 사라지며,
reference count가 0이 되면 Python VM의 garbage collection 대상이 될 수 있다.

다만, object가 “즉시 메모리에서 완전히 사라진다”기보다는
**더 이상 접근할 수 없게 된다** 는 쪽으로 이해하는 것이 좋다.

---

## 20. VS Code

이번 주 실습에서는 **Visual Studio Code (VS Code)** 설치와 사용 환경 설정을 진행하였다.

### VS Code란?

VS Code는 Microsoft에서 제공하는 **code editor** 이다.

Visual Studio와 달리, 기본적으로는 가볍고 확장 가능한 editor이며,
필요한 기능은 **extension(확장 프로그램)** 을 설치하여 개발 환경처럼 사용할 수 있다.

즉,

* Visual Studio → 전형적인 IDE
* VS Code → editor 중심, extension으로 확장

이라고 볼 수 있다.

---

## 21. VS Code와 IDLE 비교

### IDLE

Python 학습용으로 제공되는 간단한 환경이다.

* REPL 사용 가능
* 간단한 script 작성 가능
* 교육용으로는 충분함

하지만 실제 개발 환경으로는 기능이 제한적이다.

---

### VS Code

VS Code는 다음과 같은 장점이 있다.

* 여러 파일 관리 가능
* 확장 프로그램 설치 가능
* 코드 자동완성
* 터미널 사용 가능
* Python 개발 환경으로 확장 가능

즉, 학습 단계를 넘어서 **실제 작업용 환경** 으로 더 적합하다.

---

## 22. VS Code 설치

Windows 기준 설치 과정은 다음과 같다.

1. 공식 사이트 접속
   https://code.visualstudio.com/

2. 설치 파일 다운로드

3. 설치 파일 실행

4. 설치 옵션 선택 후 설치 진행

5. 설치 완료 후 실행

수업에서는 설치 이후 Python 관련 extension을 추가하고,
실제로 Python 파일을 열고 실행하는 실습까지 진행하였다.

---

## 23. 정리

이번 수업에서는 다음 내용을 학습하였다.

* `int` 와 `float` 의 차이
* float의 근삿값 오차
* `type()` 의 의미
* Bitwise Operator
* Boolean Operator
* short-circuit evaluation
* truthiness
* Relational / Membership / Identity Operator
* `.` / `:=` / `del`
* VS Code 설치 및 개발 환경 준비
