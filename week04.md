# Week04

## 이번 주 큰 흐름
- Bitwise Operator
- Boolean Operator, Relational Operator, and Membership Operator
- vscode
    - vscode 완전 제거하기 (optional)
    - vscode 설치하기 (windows)
    - 기본 terminal 변경하기
    - 기초 사용법 및 단축키.
---



# 1.Bitwise Operator

피연산자로  int 와 bool , 또는 bytes와 bytesarrays의 각 요소 만 사용. 
- bytes 나 bytearrays는 직접 사용이 안되고 각 요소 단위로 꺼내서 처리해야 한다.
- 부호 비트(sign bit, MSB)도 다른 비트들과 동일하게 처리.
-  음수는 2의 보수 사용.

#### 참고 용어 : `2의 보수`

1. 모든 비트를 반전 (0 ↔ 1)
2. +1


## 1.1 Bitwise Operators의 우선순위(⭐기호 암기)
`~` > `<<`, `>>` > `&` > `^` > `|`

### ~ (비트 NOT, complement)
각 bit를 반전시킴. sign bit (MSB) 포함하여 모든 bit 반전

```python
# ~ (NOT)
print(~5)      # -6
```

### <<, >> (시프트 연산자)

#### << (왼쪽 시프트)

모든 비트를 왼쪽으로 이동, 오른쪽은 0으로 채움

```python
# << (왼쪽 시프트)
print(3 << 1)  # 6
```

#### >> (오른쪽 시프트)

- 양수: 왼쪽을 0으로 채움
- 음수: 왼쪽을 1로 채워 sign 유지 (즉, 산술 시프트임) : C++ 등의 논리 시프트랑은 차이가 남.

```python
# >> (오른쪽 시프트)
print(8 >> 1)  # 4
```
```python
x << n  → x × (2^n)
x >> n  → x ÷ (2^n)
```
### & (비트 AND)
두 수의 각 자리 비트를 비교하여 둘 다 1일 때만 1

```python
# & (AND)
print(5 & 3)   # 1
```

### ^ (비트 XOR , Exclusive OR)
두 수의 각 자리 비트를 비교하여 서로 다를 때 1

```python
# ^ (XOR)
print(5 ^ 3)   # 6
```
### | (비트 OR , Inclusive OR)
두 수의 각 자리 비트를 비교하여 하나라도 1이면 1

```python
# | (OR)
print(5 | 3)   # 7
```


## 1.2 bytes 와 bytearray에서의 동작
0b=2진수, 0o=8진수, 0x=16진수, e=지수표기

---

# 2.여러가지 operater
<img width="407" height="173" alt="image" src="https://github.com/user-attachments/assets/c9a8d6a0-b7da-4f43-a6c3-0c14fbcef50f" />



# 2.1 Boolean Operator

- and : and 연산자. (binary op.) : C언어 등에선 &&에 해당.

- or : or 연산자. (binary op.) : || 에 해당.

- not : not 연산자. (unary operator로 operand가 하나임.) : !에 해당.

- 피연산자는 값(truthiness) (⭐ 중요)

```python
print(5 and 10)      # 10
print(0 and 10)      # 0
```
## short-circuit evaluation (⭐ 시험 )
- or의 경우 왼쪽에서 오른쪽으로 evaluation이 이루어지는 도중
하나라도 True가 나오면 뒤에 대해 

- and의 경우는
하나라도 Flase가 나오면 이후 evaluation을 수행하지 않고 False를 반환함.
 

 #### 참고 : (⭐ 중요)
불리언 오퍼레이터는 영어로
비트와이즈 오퍼레이터는 기호로 쓴다.  


# 2.2 Relational Operator(관계연산자, 비교연산자)

값을 비교하는 연산자 (⭐ 시험 )

- `>` : greater than
- `<` : less than
- `>=` : greater than or equal to
- `<=` : less than or equal to
- `==` : equal to
- `!=` : not equal to

## 특징

- 반환하는 값은 Boolean type.
- 피연산자는 numeric type , string
- 일반적으로 lexicographic order (=dictionary ordering, 알파벳순)에 따라 앞에 있는 철자가 작게 처리됨
- 대문자가 소문자보다 작은 값을 가지며, 다른 글자들이 다 같을 경우, 긴문자가 큰 값을 가짐.

```python
print("apple" < "banana")   # True  (a < b)
print("Apple" < "apple")    # True  (대문자 < 소문자)
print("abc" < "abcd")       # True  (짧은 게 작음)
print("abc" < "abd")        # True  (c < d)
```

# 2.3 Membership Operator

포함 여부를 확인하는 연산자.

in 의 뒤에 주어진 collection ( list, dict, str 등)에, 앞에 주어진 object가 포함되어 있는지를 체크함.

- boolean type을 반환값
- 피연산자
    - 왼쪽 : 아무 타입 가능 (비교 가능한 값)
    int,str,float, tuple 등
    - 오른쪽 (⭐ 중요) : 반드시 iterable (반복 가능한 객체, 문자열 (str)리스트 (list)튜플 (tuple)딕셔너리 (dict)집합 (set)

```python
print("plea" in "apple") # False
```
```python
print("" in "apple") # True
```

# 2.3 Identity Operators

is 와 is not 으로 같은 객체를 참조하고 있는지. 같은 메모리 주소를 가져야 True.

(⭐ 중요)
```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True  (값이 같음)
print(a is b)  # False (다른 객체)
print(a is c)  # True  (같은 객체)
```

```python
a = "abc"
b = "abc"

print(a == b)  # True → 값이 같음
print(a is b)  # True(또는 False) → 같은 객체일 수도 있음 (인터닝)
```

## 2.4 그 외 연산자

### del

변수, 요소 삭제
```python
a = [1, 2, 3]
del a[1]     # 리스트 요소 삭제 → [1, 3]

x = 10
del x        # 변수 자체 삭제
```

### . (메소드 혹은 함수)

객체의 속성(attribute)이나 메소드 접근

모듈이든 객체든 . 뒤에는 함수/값/클래스 다 올 수 있다. 모듈 또한 객체. 

```python
a = [1, 2, 3]
a.append(4)   # 리스트의 메소드 호출

s = "abc"
print(s.upper())  # 문자열 메소드 호출
```


---


# 3.vscode

# 3.1 vscode 완전 제거하기 (optional)
# 3.2 vscode 설치하기 (windows)
# 3.3 기본 terminal 변경하기
# 3.4 기초 사용법 및 단축키

## 화면 구성 
- Activity Bar → 메뉴 선택 (Explorer, Search 등)
- Side Bar → 파일/검색 등 표시
- Editor → 코드 작성
- Panel → 터미널 / 출력
- Status Bar → 상태 표시

## Explorer / 파일 관련
- Ctrl + Shift + E → Explorer 열기
- Ctrl + P → 파일 찾기
- Ctrl + Click → 새 창(그룹)에서 열기

## Editor 기본 단축키 
- Ctrl + S → 저장
- Ctrl + C / V / X → 복사 / 붙여넣기 / 잘라내기
- Ctrl + Z / Shift + Z → 실행취소 / 다시실행
- Ctrl + / → 주석 처리
- Ctrl + F → 검색
- Ctrl + H → 바꾸기
- Ctrl + Shift + F → 전체 검색(⭐ 중요)
- ctrl+ ] or [ (or cmd+ ] or [ ): 선택된 블럭 또는 현재 행을 들여쓰기 수행. (⭐ 중요)
- ctrl + / (or cmd + / ): 주석처리 toggle (커서가 위치한 행 or 선택된 영역) (⭐ 중요)

## 탭 / 창 관련
- Ctrl + W → 탭 닫기
- Ctrl + \ → 화면 분할 (새 editor)
- Ctrl + Tab → 파일 이동

## Command Palette (⭐ 중요)
vscode를 command로 제어할 때 사용되는 입력창 (상단 중앙의 검색창과 같은 위치).
- Ctrl + Shift + P → 명령어 실행 창

Perplexity 단축키와 충돌


ctrl (or cmd) + p 로 하고 나서 앞에 > 을 입력하는 방식

## 터미널
- Ctrl + ` → 터미널 열기(⭐ 중요)

## 기타 핵심
- Ctrl + B → 사이드바 토글
- Ctrl + , → 설정 열기
- Ctrl + G → 특정 라인 이동
- Ctrl + Shift + O → 함수/변수 이동

---

# 4. 윤성우의 열혈 파이썬4

### 오차
<img width="146" height="64" alt="image" src="https://github.com/user-attachments/assets/cdf98930-b534-4b39-9f9c-b579422c0498" />


---
### float형으로 변환
<img width="248" height="216" alt="image" src="https://github.com/user-attachments/assets/5ba9863e-1e81-4e7a-a565-387bc698ba42" />


---
### int형으로 변환
<img width="259" height="155" alt="image" src="https://github.com/user-attachments/assets/6774219e-cf5a-48d2-b2c0-841ce3d81cc0" />

---
### 증강할당 연산자 (⭐ 중요)
<img width="266" height="152" alt="image" src="https://github.com/user-attachments/assets/7d69ce84-7b2d-4854-b516-611f44768556" />


- += 는 가능한 경우 기존 객체를 수정 (in-place)
- = 는 항상 새로운 객체 생성
- mutable (리스트 등) → 차이 발생
- immutable (int, str 등) → 거의 동일하게 보임

```python
a = [1, 2]
b = a

a += [3]

print(a)  # [1, 2, 3]
print(b)  # [1, 2, 3]
```

```python
a = [1, 2]
b = a

a = a + [3]

print(a)  # [1, 2, 3]
print(b)  # [1, 2]
```
* truthiness
* Relational / Membership / Identity Operator
* `.` / `:=` / `del`
* VS Code 설치 및 개발 환경 준비
