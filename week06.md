# Week06

## 이번 주 큰 흐름
- if, elif, else statements

- Control Flow 와 Control Structure
    - while statement
    - for statement
    - else (break checker)

- dunder:`__name__`

- Shallow Copy and Deep Copy
    - mutability
    - strong typing
    - dynamic typed language
    - shallow copy vs. deep copy

- 윤성우 ch7


# 1. if, elif, else statements



## 기본 구조

조건에 따라 코드 실행 (flow control)

```python
if condition:
    실행1
elif condition:
    실행2
else:
    실행3
```


## 동작 방식

위에서부터 순서대로 검사

```python
x = 10

if x > 20:
    print("A")
elif x > 5:
    print("B")
else:               # 그 전 if문이 True여서 무시
    print("C") 
```

👉 결과
```
B
```


## condition

조건은 항상 True / False로 평가됨

```python
x = 10

if x > 5 and x < 20:
    print("OK")
```
##elif / else 

```
if → 단독 가능
elif → 단독 불가
else → 단독 불가
```

## 범위 나누기 예제

```python
age = 20

if age < 18:
    print("미성년자")
elif age < 65:
    print("성인")
else:
    print("노인")
```

👉 결과
```
성인
```

## 중첩 (nesting) 과 elif의 차이

### elif (같은 레벨, 하나만 실행)

```python
x = 10

if x > 20:
    print("A")
elif x > 5:
    print("B")
else:
    print("C")
```

👉 결과
```
B
```

### 중첩 if (안에서 또 검사)

```python
x = 10

if x > 0:
    if x > 5:
        print("B")
```

👉 결과
```
B
```

# 2. Control Flow 와 Control Structure

프로그램 실행 흐름을 제어하는 구조

- 기본: 위 → 아래 순차 실행, 제어문으로 흐름 변경 가능

- Control Flow = 실행 경로  
- Control Structure = 그걸 만드는 문법




## 구조 종류

### 순차 구조
```python
print(1)
print(2)
```

👉 그대로 위에서 아래 실행


### 분기 구조 (if)

```python
x = 10

if x > 0:
    print("양수")
else:
    print("음수")
```

👉 조건에 따라 실행 경로 변경


### 반복 구조 (for / while)

```python
for i in range(3):
    print(i)
```

```python
i = 0
while i < 3:
    print(i)
    i += 1
```

같은 코드 반복 실행


##  for vs while

| 구분 | for | while |
|------|-----|-------|
| 기준 | 횟수/데이터 | 조건 |
| 사용 | 반복 횟수 알 때 | 조건 기반 |


## 흐름 제어 키워드

### break
반복 즉시 종료. if 안에 있어도 → while을 끊는다

```python
for i in range(5):
    if i == 3:
        break
    print(i)
```

👉 결과
```
0 1 2
```

---

### continue
현재 반복만 건너뜀. 반복문에만 작용.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

👉 결과
```
0 1 3 4
```

---

### return
👉 함수 종료 + 값 반환

```python
def f():
    return 10
```


# 2.1 while statement



## while 기본 구조

조건이 True인 동안 반복

```python
while 조건:
    실행코드
```


## 예제

```python
a = 1

while a < 5:
    print(a)
    a += 1
```

👉 결과
```text
1
2
3
4
```

`a += 1`이 없으면 조건이 계속 True라서 무한루프가 될 수 있음


##  break

👉 반복문을 즉시 종료

```python
i = 0

while True:
    if i == 3:
        break
    print(i)
    i += 1
```

👉 결과
```text
0
1
2
```

##  continue

👉 현재 반복의 나머지를 건너뛰고 다음 반복으로 이동

```python
i = 0

while i < 5:
    i += 1

    if i == 3:
        continue

    print(i)
```

👉 결과
```text
1
2
4
5
```

---

## do-while 비슷하게 만들기

👉 Python에는 do-while 없음  
👉 `while True + break`로 구현

```python
while True:
    answer = input("종료할까요? y/n: ")

    if answer == "y":
        break
```

최소 1번은 실행됨

---

## continue 예제: 알파벳 개수 세기

```python
s = "a1b2c3"

cnt = 0
idx = 0

while True:
    if idx >= len(s):
        break

    if not s[idx].isalpha():
        idx += 1
        continue

    cnt += 1
    idx += 1

print(cnt)
```

👉 결과
```text
3
```

---

# 2.2 for statement

iterable 객체를 순회하면서 반복 실행

```python
for 변수 in iterable:
    실행코드
```


## 리스트

```python
l = [1, 2, 3]

for x in l:
    print(x)
```

👉 결과
```
1
2
3
```


## 문자열 

```python
s = "abc123"

for c in s:
    if c.isdigit():
        print(c)
```

👉 결과
```
1
2
3
```

## range 

숫자 반복할 때 사용

```python
for i in range(5):
    print(i)
```

👉 결과
```
0 
1 
2 
3 
4
```

### range(start, end, step)

```python
for i in range(0, 10, 2):
    print(i)
```

👉 결과
```
0 
2 
4 
6 
8
```

## zip (여러 개 동시에)

```python
a = [1, 2, 3]
b = ['a', 'b', 'c']

for x, y in zip(a, b):  # zip은 튜플의 묶음.
    print(x, y)
    print(f'{x},{y}')
```

👉 결과
```
1 a
1,a
2 b
2,b
3 c
3,c
```  
짧은 쪽 기준으로 반복


## tuple로 받기

```python
a = [1, 2]
b = ['a', 'b']

for t in zip(a, b):
    print(t)
```

👉 결과
```
(1, 'a')
(2, 'b')
```

## 중첩 for

```python
for i in range(2):
    for j in range(2):
        print(i, j)
```

👉 결과
```
0 0
0 1
1 0
1 1
```

---



# 2.3 else (break checker)

## 조건문에서 else
일반적으로 else의 경우, 앞서의 if 와 elif문들에서 실행된 block이 없는 경우 수행되는 것을 의미한다.

## 반복문에서 else
그런데 python에서는 for와 while과 같은 loop structure 에서도
else를 뒤에 붙여서 break로 해당 loop가 나왔는지를 체크할 수 있다.

앞서의 loop structure에서 break로 종료되지 않은 경우에 수행

# 3. dunder:`__name__`


### 상황1

```python
# adder2.py
def adder(num1, num2):
    return num1 + num2

def main():
    print(adder(5, 3))

main()
```
```python
# test.py
import adder2

print(adder2.adder(10, 20))
```

### 실행 1: adder2.py 실행
```python
# adder2.py
실행 흐름
adder 함수 정의
main 함수 정의
main() 실행
adder(5, 3) → 8 출력
결과
8
```
### 실행 2: test.py 실행
```python
1. test.py 시작
 # test.py
import adder2

2. adder2.py 실행됨 (import 때문에)
# adder2.py
adder 정의
main 정의
❗ main() 실행됨 (# 문제!)
→ 출력: 8

3. 다시 test.py로 돌아옴
print(adder2.adder(10, 20))

→ 출력:30

최종 결과
8(원하지 않음)
30
```

---


### 상황 2: if __name__ == "__main__" 사용

```python
# adder2.py
def adder(num1, num2):
    return num1 + num2

def main():
    print(adder(5, 3))

if __name__ == "__main__":
    main()
```

### 실행 1: adder2.py 실행
```
python adder2.py
내부 상태
__name__ == "__main__"

→ 조건 참 → main() 실행

결과
8
```
### 실행 2: test.py 실행
```
python test.py
내부 상태 (adder2.py 입장)
__name__ == "adder2"

→ 조건 거짓 → main() 실행 안 됨

결과
30
```


# 4. Shallow Copy and Deep Copy


```
= (assignment) → 같은 객체 공유
[:] / copy() → 얕은 복사 (겉만 복사)
deepcopy() → 완전 복사
```

```
mutable → 바뀜 (공유하면 영향 있음)
immutable → 안 바뀜 (공유해도 안전)
```

## 4.1 Assignment - mutable

```python
a = [1, 2, 3]
b = a

b[0] = 100

print(a)  # [100, 2, 3]
```

👉 이유  
- a, b **같은 리스트 가리킴**

 
```
a is b → True
```


## 4.2 Shallow Copy (얕은 복사) - mutable

```python
a = [[1, 2], 3]
b = a[:]

b[0][0] = 999

print(a)  # [[999, 2], 3]
```

👉 이유  
- 겉 리스트는 다름
- **안쪽 리스트는 공유됨**

📌 핵심  
```
a is b → False
a[0] is b[0] → True
```


##  4.3 Deep Copy (완전 복사)

```python
import copy

a = [[1, 2], 3]
b = copy.deepcopy(a)

b[0][0] = 999

print(a)  # [[1, 2], 3]
```

이유  
- 내부까지 전부 새로 생성



## 4.4 Immutable (변경 불가)

👉 대표: int, float, str, tuple

```python
a = (1, 2, 3)
b = a

print(a is b)  # True
```

👉 같은 객체지만 문제 없음

---

### 수정 시

```python
b += (4,)
```

👉 결과

- b → 새 객체 생성
- a → 그대로

---

### copy 관점 정리
mutable 함수는 공유하고 복사하면 같이 바뀌기 때문에 이를 방지하기 위해 deep copy 사용, immutable은 공유해도 복사하면 같이 안바뀜.




# 5. 윤성우의 열혈 파이썬 7,8

### 진실성


---
### 이중 for
![alt text](image-52.png)
