# Week 5

## 1. print() 함수

`print()` 는 Python의 built-in function이다.
값을 표준 출력(stdout)으로 출력할 때 사용한다.

예를 들어 다음과 같이 사용할 수 있다.

```python id="qvtj1s"
print("Hello")
print(3 + 5)
print("3+5 =", 3 + 5)
```

`print()` 는 여러 개의 argument를 받을 수 있으며,
기본적으로 각 값 사이에는 공백이 들어간다.

---

## 2. keyword argument

함수에 값을 전달할 때, 위치로 전달하는 방식 외에도
**이름을 지정해서 전달하는 방식** 이 있다. 이를 **keyword argument** 라고 한다.

`print()` 함수에서는 대표적으로 다음과 같은 keyword argument를 사용한다.

* `sep`
* `end`

예

```python id="ec1i0v"
print("a", "b", "c", sep="-")
```

결과

```python id="v0agum"
a-b-c
```

여기서 `sep` 는 각 값 사이를 무엇으로 구분할지를 의미한다.

또한

```python id="knv23x"
print("Hello", end=" ")
print("World")
```

처럼 `end` 를 사용하면 출력 후 줄바꿈 대신 다른 문자를 넣을 수 있다.

즉,

* `sep` → 값과 값 사이
* `end` → 출력 끝

을 의미한다.

---

## 3. help와 함수 정보 확인

Python에서는 함수의 도움말을 확인할 수 있다.

함수 도움말을 보면 다음과 같은 정보를 볼 수 있다.

* parameter 이름
* 기본값(default value)
* 타입 힌트(type hint)
* 반환값 관련 정보

예를 들어 도움말에서 다음과 같은 표현을 볼 수 있다.

```text id="0ndxhm"
sep: str
end: str
```

이는

* `sep` 에는 문자열이 들어가야 하고
* `end` 에도 문자열이 들어가야 한다

는 뜻이다.

즉, 도움말을 보면 함수가 어떤 값을 받아들이는지 파악할 수 있다.

---

## 4. 문자열 포매팅 (String Formatting)

문자열 안에 값을 넣어 표현하는 방법이다.

Python에서는 여러 가지 문자열 포매팅 방식을 사용할 수 있다.

### 4.1 f-string

문자열 앞에 `f` 를 붙이고,
중괄호 `{}` 안에 값을 넣는 방식이다.

예

```python id="78u4ff"
name = "jihye"
age = 20

print(f"My name is {name}")
print(f"I am {age} years old")
```

이 방식은 직관적이고 읽기 쉬워서 자주 사용된다.

---

### 4.2 format() 메서드

문자열의 메서드인 `format()` 을 이용하는 방식이다.

예

```python id="ngnkk6"
name = "jihye"
print("My name is {}".format(name))
```

---

### 4.3 `%` 연산자

예전 방식으로, `%` 기호를 이용해서 문자열 안에 값을 넣는 방식이다.

예

```python id="lj1i0f"
name = "jihye"
print("My name is %s" % name)
```

하지만 이 방식은 현재는 잘 사용하지 않는다.

즉, 문자열 포매팅은 가능하면 **f-string** 으로 익히는 것이 좋다.

---

## 5. list

`list` 는 Python의 대표적인 sequence type 중 하나이다.

특징은 다음과 같다.

* 여러 값을 저장할 수 있다.
* 순서가 있다.
* 여러 타입의 데이터를 함께 담을 수 있다.
* 변경 가능하다 (mutable)

예

```python id="mjlwmr"
a = [1, 2, 3]
b = [1, "hello", 3.14]
```

또한 리스트 안에 다른 리스트를 넣을 수도 있다.

예

```python id="ql8sfe"
a = [1, 2, [3, 4]]
print(a)
```

결과

```python id="1s2h5g"
[1, 2, [3, 4]]
```

즉, 리스트는 다양한 데이터를 묶어서 다룰 수 있는 매우 중요한 자료형이다.

---

## 6. mutable / immutable

Python에서는 객체가 **변경 가능한지 여부** 에 따라
mutable / immutable 로 나눌 수 있다.

### mutable

객체 자체를 바꿀 수 있는 경우

예: `list`

```python id="qq0e5m"
a = [1, 2, 3]
a[0] = 100
print(a)
```

결과

```python id="k7tbyo"
[100, 2, 3]
```

즉, 리스트는 mutable이다.

---

### immutable

객체 자체를 바꿀 수 없는 경우

예: `tuple`, `str`

```python id="3p9fwf"
t = (1, 2, 3)
```

```python id="7zjlwm"
t[0] = 100
```

→ 오류 발생

즉, tuple은 immutable이다.

문자열도 마찬가지로 immutable이다.

```python id="0o3trf"
s = "hello"
```

```python id="ysjlwm"
s[0] = "H"
```

→ 오류 발생

### 중요한 점

중요한 것은 **변수가 mutable / immutable 한 것이 아니라**,
**객체(object)가 mutable / immutable 하다는 것** 이다.

즉, 변수는 단지 객체를 가리키는 이름일 뿐이다.

---

## 7. tuple과 list

`tuple` 과 `list` 는 구조적으로 매우 비슷하다.

공통점:

* sequence type
* 순서가 있음
* indexing 가능
* slicing 가능

차이점:

* `list` → mutable
* `tuple` → immutable

즉, tuple은 **변경 불가능한 list처럼** 생각할 수 있다.

---

## 8. Indexing

인덱싱(indexing)은 sequence type에서
특정 위치의 값을 가져오는 방법이다.

예

```python id="n7q2cs"
a = [10, 20, 30]
print(a[0])
print(a[1])
```

결과

```python id="djlwmr"
10
20
```

Python에서는 인덱스가 **0부터 시작** 한다.

---

### 음수 인덱싱

Python에서는 뒤에서부터 접근할 때 음수 인덱스를 사용할 수 있다.

예

```python id="z9vmq1"
a = [10, 20, 30]
print(a[-1])
print(a[-2])
```

결과

```python id="fjlwmr"
30
20
```

즉,

* `-1` → 마지막 요소
* `-2` → 뒤에서 두 번째 요소

를 의미한다.

---

## 9. Slicing

슬라이싱(slicing)은 sequence의 일부 구간을 잘라내는 방법이다.

기본 형태는 다음과 같다.

```python id="2jlwmr"
sequence[start:stop]
```

예

```python id="njlwmr"
a = [10, 20, 30, 40]
print(a[1:3])
```

결과

```python id="jlwmr1"
[20, 30]
```

즉,

* `start` 는 포함
* `stop` 은 포함하지 않음

이다.

---

### 생략 슬라이싱

`start` 나 `stop` 을 생략할 수도 있다.

예

```python id="jlwmr2"
a[:]
a[:3]
a[2:]
```

의미는 각각 다음과 같다.

* `a[:]` → 전체
* `a[:3]` → 처음부터 3 전까지
* `a[2:]` → 2부터 끝까지

---

### step 인덱싱

슬라이싱에는 step도 넣을 수 있다.

예

```python id="jlwmr3"
a[::2]
```

→ 두 칸씩 건너뛰며 가져옴

즉, 인덱싱은 크게 다음 세 가지로 구분해서 익히면 된다.

* 기본 인덱싱
* 음수 인덱싱
* 슬라이싱 / step 인덱싱

---

## 10. 문자열(str)

문자열(`str`)도 sequence type이다.

즉,

* indexing 가능
* slicing 가능

하다.

예

```python id="jlwmr4"
s = "hello"
print(s[0])
print(s[1:4])
```

또한 문자열의 길이는 `len()` 으로 구할 수 있다.

```python id="jlwmr5"
print(len("hello"))
```

### 중요한 점

공백도 문자 1개로 센다.

예

```python id="jlwmr6"
print(len("a b"))
```

결과는 `3` 이다.

즉, 문자열 길이를 셀 때 공백도 포함된다.

---

## 11. len()

`len()` 은 대표적인 built-in function이다.

길이를 구할 때 사용한다.

예

```python id="jlwmr7"
print(len([1, 2, 3]))
print(len("python"))
```

특징:

* 반환값은 항상 `int`
* list, tuple, str 등 sequence type에서 자주 사용

---

## 12. min(), max()

`min()` 과 `max()` 도 built-in function이다.

예

```python id="jlwmr8"
print(min([3, 1, 7]))
print(max([3, 1, 7]))
```

즉,

* `min()` → 최솟값
* `max()` → 최댓값

을 구한다.

---

## 13. 함수와 메서드

Python에서는 함수(function)와 메서드(method)를 구분해야 한다.

### 함수

객체와 독립적으로 사용하는 것

예

```python id="jlwmr9"
print("hello")
len([1, 2, 3])
input()
```

---

### 메서드

객체에 종속되어, 객체 뒤에 `.` 을 붙여 사용하는 것

예

```python id="jlwmr10"
a.append(3)
s.upper()
```

즉,

* `print()`, `len()` → 함수
* `append()`, `upper()` → 메서드

이다.

---

## 14. list 메서드

리스트는 mutable 객체이므로
상태를 바꾸는 다양한 메서드를 가진다.

이 부분은 실습이 중요하다.

---

### 14.1 append()

리스트 맨 뒤에 값을 하나 추가한다.

예

```python id="jlwmr11"
a = [1, 2]
a.append(3)
print(a)
```

결과

```python id="jlwmr12"
[1, 2, 3]
```

즉, 값을 **그냥 하나 통째로 넣는다.**

---

### 14.2 extend()

리스트 끝에 여러 값을 이어 붙인다.

예

```python id="jlwmr13"
a = [1, 2]
a.extend([3, 4])
print(a)
```

결과

```python id="jlwmr14"
[1, 2, 3, 4]
```

즉, `extend()` 는 인자로 받은 iterable을 **풀어서 넣는다.**

---

### append와 extend 차이

```python id="jlwmr15"
a = [1, 2]
a.append([3, 4])
print(a)
```

결과

```python id="jlwmr16"
[1, 2, [3, 4]]
```

```python id="jlwmr17"
a = [1, 2]
a.extend([3, 4])
print(a)
```

결과

```python id="jlwmr18"
[1, 2, 3, 4]
```

즉,

* `append()` → 통째로 하나 넣기
* `extend()` → 풀어서 넣기

이다.

이 둘의 차이는 중요하다.

---

### 14.3 insert()

원하는 위치에 값을 삽입한다.

예

```python id="jlwmr19"
a = [1, 2, 3]
a.insert(1, 100)
print(a)
```

결과

```python id="jlwmr20"
[1, 100, 2, 3]
```

형태는 다음과 같다.

```python id="jlwmr21"
insert(위치, 값)
```

---

### 14.4 clear()

리스트를 비운다.

예

```python id="jlwmr22"
a = [1, 2, 3]
a.clear()
print(a)
```

결과

```python id="jlwmr23"
[]
```

즉, 빈 리스트로 만든다.

---

### 14.5 pop()

리스트에서 값을 꺼내고,
그 값을 반환한다.

예

```python id="jlwmr24"
a = [10, 20, 30]
x = a.pop()
print(a)
print(x)
```

결과

```python id="jlwmr25"
[10, 20]
30
```

즉, `pop()` 은

* 리스트에서는 제거되고
* 꺼낸 값은 반환된다.

---

### 14.6 remove()

리스트에서 특정 값을 제거한다.

예

```python id="jlwmr26"
a = [1, 2, 3, 2]
a.remove(2)
print(a)
```

결과

```python id="jlwmr27"
[1, 3, 2]
```

즉, **처음 등장한 값 하나만 제거** 한다.

또한 `remove()` 는 리스트를 바꾸지만
반환값은 없다.

---

### 14.7 count()

리스트 안에서 특정 값이 몇 번 나오는지 센다.

예

```python id="jlwmr28"
a = [1, 2, 2, 3, 2]
print(a.count(2))
```

결과

```python id="jlwmr29"
3
```

---

### 14.8 index()

리스트 안에서 특정 값이 처음 등장하는 위치를 찾는다.

예

```python id="jlwmr30"
a = [10, 20, 30, 20]
print(a.index(20))
```

결과

```python id="jlwmr31"
1
```

즉, 가장 먼저 나오는 위치를 반환한다.

---

## 15. 문자열 메서드

문자열도 다양한 메서드를 가진다.

문자열은 immutable이기 때문에,
대부분의 문자열 메서드는 **새 문자열을 반환** 한다.

즉, 원본 문자열 자체를 직접 바꾸는 것이 아니라
새로운 문자열을 만들어 돌려준다.

---

### 15.1 count()

문자열 안에서 특정 문자나 부분 문자열이 몇 번 등장하는지 센다.

예

```python id="jlwmr32"
print("banana".count("a"))
print("banana".count("an"))
```

---

### 15.2 lower(), upper()

소문자 / 대문자로 바꾼다.

예

```python id="jlwmr33"
s = "Hello"
print(s.lower())
print(s.upper())
```

중요한 점은
문자열은 immutable이므로 원본이 바뀌는 것이 아니라
**새 문자열이 반환** 된다는 것이다.

즉, 실제로 바꿔 쓰려면

```python id="jlwmr34"
s = s.lower()
```

처럼 다시 대입해야 한다.

---

### 15.3 strip(), lstrip(), rstrip()

문자열 양끝의 공백 등을 제거한다.

예

```python id="jlwmr35"
s = "   hello   "
print(s.strip())
print(s.lstrip())
print(s.rstrip())
```

즉,

* `strip()` → 양쪽
* `lstrip()` → 왼쪽
* `rstrip()` → 오른쪽

이다.

---

### 15.4 replace()

문자열의 일부를 다른 문자열로 바꾼다.

예

```python id="jlwmr36"
s = "banana"
print(s.replace("a", "o"))
```

또한 횟수를 지정할 수도 있다.

```python id="jlwmr37"
print(s.replace("a", "o", 2))
```

즉, `replace()` 는

* 무엇을
* 무엇으로
* 몇 번

바꿀지 지정할 수 있다.

---

### 15.5 split()

문자열을 기준 문자열로 나누어 리스트로 만든다.

예

```python id="jlwmr38"
s = "a,b,c"
print(s.split(","))
```

결과

```python id="jlwmr39"
['a', 'b', 'c']
```

즉, 문자열을 쪼개서 list로 바꿀 때 사용한다.

---

### 15.6 find(), rfind()

문자열 안에서 특정 문자의 위치를 찾는다.

예

```python id="jlwmr40"
s = "banana"
print(s.find("a"))
print(s.rfind("a"))
```

즉,

* `find()` → 앞에서부터 찾기
* `rfind()` → 뒤에서부터 찾기

이다.

---

## 16. Escape Sequence

문자열 안에서 `\`(백슬래시)는
뒤 문자와 결합하여 특별한 의미를 만드는 escape sequence의 시작 문자이다.

대표적인 예는 다음과 같다.

* `\n` → 줄바꿈
* `\t` → 탭
* `\'` → 작은따옴표
* `\"` → 큰따옴표
* `\\` → 백슬래시 자체

예

```python id="jlwmr41"
print("hello\nworld")
print("hello\tworld")
print("\\")
```

---

## 17. Raw String

백슬래시를 escape sequence로 해석하지 않고
있는 그대로 사용하고 싶을 때는 raw string을 사용한다.

문자열 앞에 `r` 을 붙인다.

예

```python id="jlwmr42"
print(r"C:\Users\jihye")
```

즉, Windows 경로처럼 백슬래시가 많이 들어가는 문자열에서 편리하다.

---

## 18. del

`del` 은 삭제를 수행하는 문법 요소이다.

함수처럼 보이지만 함수는 아니다.

예

```python id="jlwmr43"
a = [1, 2, 3]
del a[1]
print(a)
```

결과

```python id="jlwmr44"
[1, 3]
```

또한

```python id="jlwmr45"
del a
```

→ 변수 자체 삭제

```python id="jlwmr46"
del a[:]
```

→ 리스트 안의 요소만 삭제

즉,

* `del a` → 변수 제거
* `del a[:]` → 내용만 제거

이다.

---

## 19. Sequence Type 정리

대표적인 sequence type은 다음과 같다.

* `list` : mutable sequence
* `tuple` : immutable sequence
* `str` : immutable text sequence

공통점:

* 순서가 있음
* indexing 가능
* slicing 가능

차이점:

* 변경 가능 여부

---

## 20. 슬라이싱의 특징

Python의 기본 `list` 에서 슬라이싱은
새로운 객체를 만든다.

즉,

```python id="jlwmr47"
a = [1, 2, 3, 4]
b = a[:]
```

에서 `b` 는 `a` 와 값은 같지만
다른 객체이다.

즉, 슬라이싱은 기본적으로 **새로운 리스트를 생성하는 방식** 이다.

---

## 21. `+` 와 `*` 연산

Python에서는 같은 연산자라도
type에 따라 다르게 동작할 수 있다.

### 리스트에서 `+`

```python id="jlwmr48"
[1, 2] + [3, 4]
```

→ 리스트 연결

### 문자열에서 `+`

```python id="jlwmr49"
"hello" + "world"
```

→ 문자열 연결

### 리스트에서 `*`

```python id="jlwmr50"
[1, 2] * 3
```

→ 반복

### 문자열에서 `*`

```python id="jlwmr51"
"ha" * 3
```

→ 반복

즉, 같은 기호라도 operand type에 따라 의미가 달라질 수 있다.

---

## 22. 정렬

### 22.1 sorted()

`sorted()` 는 built-in function이다.

정렬된 **새 객체를 반환** 한다.

즉, 원본은 바뀌지 않는다.

---

### 22.2 sort()

`.sort()` 는 list의 메서드이다.

리스트 자체를 정렬한다.

즉,

* `sorted()` → 새 객체 반환
* `.sort()` → 원본 변경 / 반환값 없음

이다.

---

## 23. if문

`if` 문은 조건에 따라 실행 여부를 결정하는 문장이다.

조건문을 이해하려면 먼저 **Boolean expression** 을 이해해야 한다.

예

```python id="jlwmr52"
x = 10

if x > 0:
    print("positive")
```

즉,

* 조건이 True이면 body 실행
* 조건이 False이면 body는 실행되지 않음

이다.

---

## 24. 핵심 구조 복습

범용 프로그래밍 언어가 되기 위해 필요한 핵심 요소는 다음과 같다.

1. 변수와 값 읽기 / 저장
2. 반복문
3. 조건문

즉, 이번 주에 배운 내용도
이 큰 흐름 안에서 이해하면 된다.

---

## 25. 정리

이번 주차에서는 다음 내용을 정리하였다.

* `print()` 함수와 keyword argument
* 함수 도움말 보기
* 문자열 포매팅
* list, tuple, string
* mutable / immutable
* indexing / slicing
* `len()`, `min()`, `max()`
* 함수와 메서드의 차이
* list 메서드
* 문자열 메서드
* escape sequence / raw string
* `del`
* sequence type 정리
* `+`, `*` 연산
* 정렬 (`sorted()`, `.sort()`)
* `if` 문

