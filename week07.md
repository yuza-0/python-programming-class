# Week07

## 이번 주 큰 흐름
- tuple
- range and enumerate
- while statement
- comprehension
- scope: LEGB
- 윤성우의 열혈 파이썬9

---



# 1. tuple

순서가 있는 여러 개의 값을 묶은 것

```python
t = (1, 2, 3)
```


## 특징
- seauence
- 변경 불가 → 값 수정 ❌
- list보다 메모리 적음
- dict key로 사용 가능

---

## 생성 방법

```python
t1 = (1, 2, 3)
t2 = 1, 2, 3        # 괄호 없어도 tuple
```


## 한 개짜리 tuple (⭐ 중요)

```python
t = (1,)   # ⭕ tuple
t = (1)    # ❌ int
```

## 인덱싱

```python
t = (10, 20, 30)

print(t[0])  # 10
```

읽기만 가능


## 수정 불가

```python
t = (1, 2, 3)
t[0] = 100   # ❌ 에러
```


## 연산

```python
t = (1, 2) + (3, 4)
print(t)  # (1, 2, 3, 4)
```

```python
t = (1, 2) * 3
print(t)  # (1, 2, 1, 2, 1, 2)
```

항상 **새 객체 생성**


## tuple unpacking (⭐ 중요 )

```python
a, b = 1, 2
print(a, b)  # 1 2
```

👉 사실은:

```
(1, 2) → unpacking
```

---

### 값 교환

```python
a, b = 1, 2
a, b = b, a

print(a, b)  # 2 1
```

---

## 리스트로

```python
l = [1, 2, 3]
t = tuple(l)
```

---

##  비교 (⭐ 중요)

```python
a = (1, 2, 3)
b = (1, 2)

print(a > b)  # True
```

앞에서부터 비교


# 2 range and enumerate

## 2.1 range 

**숫자 sequence를 “메모리 없이” 만드는 객체**.
- lazy iterable (필요할 때 하나씩 생성)
- list처럼 다 저장 안 함 → 효율적

### 기본 사용

```python
range(5)
```

의미
```
0, 1, 2, 3, 4
```


### 구조

```python
range(start, stop, step)
```

| 파라미터 | 의미 |
|----------|------|
| start | 시작 |
| stop | 끝 (포함 안됨⭐ 중요) |
| step | 간격 |


### 예제

```python
list(range(1, 10, 2))
```

👉 결과
```
[1, 3, 5, 7, 9]
```

## 🔹 4. 음수 step

```python
list(range(5, 0, -1))
```

👉 결과
```
[5, 4, 3, 2, 1]
```


### for와 같이 사용

```python
for i in range(3):
    print(i)
```

결과
```
0 1 2
```

---

## 2.2 enumerate (⭐ 중요)
반복 가능한(iterable) 객체를 입력받아, 
각 item(요소)를 순회하면서

index와 함께 item를 묶은 tuple을 반환하는
enumerate 객체를 생성

```python
a = ['a', 'b', 'c']

for idx, val in enumerate(a):
    print(idx, val)
```

👉 결과
```
0 a
1 b
2 c
```


### 시작 인덱스 변경

```python
for idx, val in enumerate(a, 1):
    print(idx, val)
```

👉 결과
```
1 a
2 b
3 c
```

---

### enumerate 내부 구조

```python
list(enumerate(['a','b']))
```

👉 결과
```
[(0, 'a'), (1, 'b')]
```

tuple 반환


---

# 3 comprehension


## 3.1  List Comprehension 
한 줄로 list를 생성하는 expression


shorthand expression으로 중첩된 여러 반복문(loop) 및 조건문(if)으로 collection을 생성하는 것을 한 줄로 작성가능하게 해준다.

## 3.2 흐름
```
하나씩 꺼냄 → 조건 검사 → True면 변환 → 리스트에 추가
```


## 🔹 예제

```python
[x*2 for x in [1,2,3,4] if x % 2 == 0]
```
흐름
```
1 → 조건 False → 버림
2 → 조건 True → 2*2 → 추가
3 → 조건 False → 버림
4 → 조건 True → 4*2 → 추가
```

👉 결과
```
[4, 8]
```

## 3.3 예제
```python
# src_list를 shallow copy. 
# ret_list = src_list.copy() 또는 ret_list = src_list[:] 와 같은 결과임.
# 이 경우엔 comprehension을 사용하는 건 상대적으로 비효율적이라 이런 방식으로 거의 사용되지 않음.
ret_list = [x for x in src_list]
 
# non-negative filter를 적용하여 ret_list를 생성.
ret_list = [x for x in src_list if x >= 0]
 
# 3제곱 (cube of a number) 처리를 한 ret_list생성.
ret_list = [x**3 for x in src_list]
 
# 역수(valid reciprocal) 처리 (단 0으로 나누어지는 경우 제외)
ret_list = [1/x for x in src_list if x != 0]
 
# multi_line text로 구성된 file을 읽어들여 공백 line을 제거.
ret_lit = [line for line in [l.strip() for l in infile] if line != ""]
```

---
기본 예제

```python
a = [1, 2, 3]

b = [x * 2 for x in a]

print(b)
```

👉 결과
```
[2, 4, 6]
```


## 3.4 일반 for문과 비교

### 일반 코드

```python
result = []

for x in [1,2,3]:
    result.append(x*2)
```

---

### comprehension

```python
result = [x*2 for x in [1,2,3]]
```


## 중첩 for

```python
result = [(i, j) for i in range(2) for j in range(2)]

print(result)
```

👉 결과
```
[(0,0), (0,1), (1,0), (1,1)]
```

---

## 3.5 다른 comprehension

### tuple (⭐ 중요)

```python
t = (x*2 for x in [1,2,3])
```

👉 결과
```
generator 객체 (tuple 아님)
```

---

# 4. scope: LEGB
<img width="281" height="244" alt="image" src="https://github.com/user-attachments/assets/032d2e3d-7fcf-4113-be68-3030633c0fb5" />

## 4.1 Scope
scope는

특정 name이 유효한 범위를 가리키는데
이는 namespace와 관련이 깊어서
namespace로 바꿔 애기해도 많은 부분에서 통용된다.



# 3. 윤성우의 열혈 파이썬 9
