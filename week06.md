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

👉 결과
```
[10, 2, 3, 4, 50]
```


- 슬라이싱
```python
st = [1, 2, 3, 4, 5]

st[1:3] = [100, 200]

print(st)
```

👉 결과
```
[1, 100, 200, 4, 5]
```
- 슬라이싱 + 삭제 느낌
```python
st = [1, 2, 3, 4, 5]

st[1:4] = []

print(st)
```

👉 결과
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

👉 결과
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

👉 결과
```
[0]
```
없애는 느낌으로
```python
st = [1, 2, 3, 4, 5]

st[:] = []

print(st)
```

👉 결과
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

![alt text](image-40.png)

## 🔹 clear()
리스트 모든 요소 삭제 (빈 리스트 됨, 반환값 없음)

```python
l = [1, 2, 3]
l.clear()

print(l)  # []
```


## 🔹 pop()
리스트의 마지막 요소를 반환하면서 삭제 

```python
l = [1, 2, 3]
x = l.pop()

print(x)  # 3
print(l)  # [1, 2]
```

## 🔹 append()
마지막에 요소 하나 추가 (반환값 없음)

```python
l = [1, 2]
l.append(3)

print(l)  # [1, 2, 3]
```

## 🔹 insert()
특정 위치에 요소 삽입 (반환값 없음)

```python
l = [1, 3]
l.insert(1, 2)

print(l)  # [1, 2, 3]
```


## 🔹 extend()
리스트 뒤에 여러 요소 추가 (반환값 없음)

```python
l = [1, 2]
l.extend([3, 4])

print(l)  # [1, 2, 3, 4]
```

## 🔹 remove()
값으로 요소 삭제 (첫 번째 것만)

```python
l = [1, 2, 2, 3]
l.remove(2)

print(l)  # [1, 2, 3]
```

⚠️ 없으면 에러 발생


## 🔹 del
인덱스로 요소 삭제

```python
l = [1, 2, 3]
del l[1]

print(l)  # [1, 3]
```

## 🔹 index()
값의 위치 반환 (없으면 에러)

```python
l = [1, 2, 3]
print(l.index(2))  # 1
```

## 🔹 count()
특정 값 개수 반환

```python
l = [1, 2, 2, 3]
print(l.count(2))  # 2
```

## 🔹 reverse()
순서 뒤집기 (반환값 없음)

```python
l = [1, 2, 3]
l.reverse()

print(l)  # [3, 2, 1]
```

## 🔹 sort()
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
append, insert, extend, clear, reverse, sort → 반환값 없음 (None)
pop, index, count → 값 반환
```
