# Week05

## 이번 주 큰 흐름
- list , list의 메소드
- string, string의 메소드
-  Escape Sequence
- CR(Carriage Return)과 LF(Line Feed)
- 윤성우의 열혈 5,6
---


# 1. list , list의 메소드

## 1.1 list

sequence type 중에서 유일 mutable 객체.

sequen

### 특징

- list = **순서 있음 (ordered)** + **변경 가능 (mutable)**
- 다양한 타입 혼합 가능 (heterogeneous)

#### 참고 용어 : `Mutability`

객체의 value를 변경할 수 있는지. Variable이 자유롭게 다른 object를 가르키도록(refer to) 할 수 있는 것이지 object 자체는  type 변경 불가한 strong typed임.

- list : mutable sequence

-  tuple : immutable sequence

-  string : immutable text sequence
sequen

### 인덱싱

```python
a = [10, 20, 30]

print(a[0])   # 10
print(a[-1])  # 30
```
### 값 변경
- 인덱싱
```python
st = [1, 2, 3, 4, 5]

st[0] = 10
st[4] = 50

print(st)
```

결과
```
[10, 2, 3, 4, 50]
```


- 슬라이싱
```python
st = [1, 2, 3, 4, 5]

st[1:3] = [100, 200]

print(st)
```

결과
```
[1, 100, 200, 4, 5]
```
- 슬라이싱 + 삭제 느낌
```python
st = [1, 2, 3, 4, 5]

st[1:4] = []

print(st)
```

결과
```
[1, 5]
```


### 슬라이싱

```python
a = [0, 1, 2, 3, 4]

print(a[1:3])   # [1, 2]
print(a[:2])    # [0, 1]
print(a[2:])    # [2, 3, 4]
```
### Slicing - 값으로 사용(새로운 객체)
```python
a = [1, 2, 3]
b = a[:]

b[0] = 100

print(a)  # [1, 2, 3]
print(b)  # [100, 2, 3] # 새로운 리스트 생성 (shallow copy)**
```

```python
st = [1, 2, 3]

st[:] = [0]  # 기존 리스트 유지 (내용만 변경)
```
---
### Slicing - 변경만(기존 객체 유지)
모두 대체
```python
st = [1, 2, 3, 4, 5]

st[:] = [0, 0, 0, 0, 0]

print(st)
```

결과
```
[0, 0, 0, 0, 0]
```
---

하나로 대체
```python
st = [1, 2, 3, 4, 5]

st[:] = [0]

print(st)
```

결과
```
[0]
```
없애는 느낌으로
```python
st = [1, 2, 3, 4, 5]

st[:] = []

print(st)
```

결과
```
[]
```
---

### + and * operation
```python
a = [1, 2]
b = [3, 4]

print(a + b)  # [1, 2, 3, 4]
```

```python
a = [1, 2]

print(a * 3)  # [1, 2, 1, 2, 1, 2]
```

### in membership operation

```python
a = [1, 2, 3]

print(2 in a)    # True
print([2,3] in a) # False
```

### 정렬(sorted)

```python
a = [3, 1, 2]
b = sorted(a)

print(a)  # [3, 1, 2]
print(b)  # [1, 2, 3]
```

### sort (원본 변경)

```python
a = [3, 1, 2]
a.sort() # sort()는 반환값이 없음

print(a)  # [1, 2, 3]
```

## 1.2 list의 메소드

일반적으로 object에 대해 method를 호출할 경우,해당 object의 관련 attribute의 값이 바뀌고 None을 반환하는 경우가 많다.

반환값으로 해당 list의 object를 다시 할당시 None이 되는 문제가 발생하지 않도록 주의해야 한다.

<img width="302" height="130" alt="image" src="https://github.com/user-attachments/assets/eaaae62d-47ba-4014-a4ff-724c88d09dfb" />


## clear()
리스트 모든 요소 삭제 (빈 리스트 됨, 반환값 없음)

```python
l = [1, 2, 3]
l.clear()

print(l)  # []
```


## pop()
리스트의 마지막 요소를 반환하면서 삭제 

```python
l = [1, 2, 3]
x = l.pop()

print(x)  # 3
print(l)  # [1, 2]
```

## append() (⭐ 시험 )
마지막에 요소 하나 추가 (반환값 없음)

```python
l = [1, 2]
l.append(3)

print(l)  # [1, 2, 3]
```

## insert()
특정 위치에 요소 삽입 (반환값 없음)

```python
l = [1, 3]
l.insert(1, 2)

print(l)  # [1, 2, 3]
```


## extend()
리스트 뒤에 여러 요소 추가 (반환값 없음)

```python
l = [1, 2]
l.extend([3, 4])

print(l)  # [1, 2, 3, 4]
```

## remove()
값으로 요소 삭제 (첫 번째 것만)

```python
l = [1, 2, 2, 3]
l.remove(2)

print(l)  # [1, 2, 3]
```

없으면 에러 발생


## del
인덱스로 요소 삭제

```python
l = [1, 2, 3]
del l[1]

print(l)  # [1, 3]
```

## index()
값의 위치 반환 (없으면 에러)

```python
l = [1, 2, 3]
print(l.index(2))  # 1
```

## count()
특정 값 개수 반환

```python
l = [1, 2, 2, 3]
print(l.count(2))  # 2
```

## reverse()
순서 뒤집기 (반환값 없음)

```python
l = [1, 2, 3]
l.reverse()

print(l)  # [3, 2, 1]
```

## sort()
리스트 정렬 (원본 변경, 반환값 없음)

```python
l = [3, 1, 2]
l.sort()

print(l)  # [1, 2, 3]
```

```python
l.sort(reverse=True)  # 내림차순
```
## 주의사항

```
append, insert, extend, clear, reverse, sort → 반환값 없음 (None) (⭐ 시험 )
pop, index, count → 값 반환 (⭐ 시험 )
```


# 2. string, string의 메소드

## 2.1 string

문자열 (text데이터)을 처리하기 위해 사용되는 type.

str은 immutable이므로,
method 결과로 새로운 str 객체가 생성됨.

### 인덱싱
```python
s = "SIMPLEST"

print(s[2])
```

결과
```
'M'
```
### 슬라이싱

```python
s = "SIMPLEST"

print(s[2:5])
```

결과
```
'MPL'
```


## 2.2 string의 메서드

## 대소문자 변환

문자열 형태 변환 (새 문자열 반환)

```python
s = "hello world"

print(s.upper())      # HELLO WORLD
print(s.lower())      # hello world
print(s.capitalize()) # Hello world
print(s.title())      # Hello World
print(s.swapcase())   # HELLO WORLD → hello world 반대
```


## 체크 메서드

문자열 상태 확인 (True / False 반환)

```python
s = "Hello123"

print(s.islower())   # False
print(s.isupper())   # False
print(s.isdigit())   # False
print(s.isalpha())   # False
print(s.isalnum())   # True
```

```python
s = "   \n\t"
print(s.isspace())  # True
```

```python
s = "hello world"
print(s.startswith("he"))  # True
print(s.endswith("ld"))    # True
```

## 공백 제거

앞/뒤 공백 제거 (새 문자열 반환)

```python
s = "  hello  "

print(s.strip())   # "hello"
print(s.lstrip())  # "hello  "
print(s.rstrip())  # "  hello"
```

특정 문자 제거

```python
s = "xxhelloxx"
print(s.strip("x"))  # "hello"
```


## split / join

### split
문자열 → 리스트

```python
s = "a,b,c"
print(s.split(","))  # ['a', 'b', 'c']
```

기본: 공백 기준

```python
s = "a b c"
print(s.split())  # ['a', 'b', 'c']
```

###  join
리스트 → 문자열

```python
l = ['a', 'b', 'c']
print(",".join(l))  # "a,b,c"
```

## count / index / find

```python
s = "hello hello"

print(s.count("lo"))  # 2
print(s.index("lo"))  # 3
print(s.find("lo"))   # 3
```

차이  
- index → 없으면 ❌ 에러  
- find 인덱스 반환 → 없으면 -1  

## replace

문자열 치환 (원본 변경 안됨)

```python
s = "hello world"
print(s.replace("world", "python"))  # "hello python"
```

---

##  정렬 같은 (정렬 아님, 정렬처럼 보이게)

```python
s = "hi"

print(s.center(10))  # 가운데 정렬
print(s.ljust(10))   # 왼쪽 정렬
print(s.rjust(10))   # 오른쪽 정렬
```

## 주요 사항

```
문자열은 immutable → 항상 새 문자열 반환
split → 문자열 → 리스트
join → 리스트 → 문자열
index vs find → 에러 vs -1
```

---

# 3. Escape Sequence(backslash)

## 3.1 기본 Escape Sequence

`\` (backslash)는 **escape 문자** (⭐ 시험 )

| 문자 | 의미 |
|------|------|
| \n | 줄바꿈 (newline) |
| \t | 탭 (tab) |
| \r | 캐리지 리턴 |

```python
print("Hello\nWorld")
# Hello
# World
```
## 3.2 백슬래시 출력

`\` 자체를 출력하려면 `\\`

```python
print("\\n")  # \n
```

## 3.3 Raw String (⭐ 중요) - 정규 표현식에서 사용

`r""` → escape 무시 (그대로 출력)

```python
print('\\n')   # \n
print(r'\n')   # \n
```

둘 다 결과 같음


# 4. CR(Carriage Return)과 LF(Line Feed)

## 4.1 기본 개념

줄바꿈 방식 (newline 처리)

| 방식 | 의미 | 문자 |
|------|------|------|
| CR | 커서를 맨 앞으로 이동 | \r |
| LF | 다음 줄로 이동 | \n |
| CRLF | 둘 다 사용 | \r\n |

## 4.2 동작 차이

```python
print("Hello\rWorld")
```

 출력 (덮어쓰기 느낌)
```
World
```
---
```python
print("Hello\nWorld")
```
 출력
```
Hello
World
```

---

## 4.3 운영체제별 차이

| OS | 줄바꿈 |
|----|--------|
| Windows | \r\n |
| Linux / Unix / macOS | \n |

# 5. 윤성우의 열혈 5

### 문자열은 변경 불가
<img width="293" height="134" alt="image" src="https://github.com/user-attachments/assets/158bbd35-42f0-4784-b3d1-4b7655c659e8" />


---
### 문자열도 순회 가능
<img width="165" height="80" alt="image" src="https://github.com/user-attachments/assets/eb84529a-7eb6-48ed-a007-896166fddd5b" />


--- 
### len
<img width="146" height="115" alt="image" src="https://github.com/user-attachments/assets/c63796bd-95b0-4276-ada4-05046b5a5172" />


---
### return의 역할
<img width="139" height="142" alt="image" src="https://github.com/user-attachments/assets/6d54b59b-ada5-4ac7-82bb-d158ad312b6f" />


# 6. 윤성우의 열혈 6

### 리스트 메소드
<img width="229" height="150" alt="image" src="https://github.com/user-attachments/assets/072ad05a-09bc-4c30-8a45-4b7d5ff9180a" />

<img width="295" height="124" alt="image" src="https://github.com/user-attachments/assets/f52f7fca-9b27-49d5-afa2-80be8ad547d5" />

---
### 이스케이프
<img width="245" height="187" alt="image" src="https://github.com/user-attachments/assets/b4a36080-2c9a-4314-89d4-434abb6e29ea" />

---

### del : 함수가 아닌 키워드
<img width="277" height="224" alt="image" src="https://github.com/user-attachments/assets/bb34ba49-afb0-4cea-aeb9-e7bfeea9f192" />



