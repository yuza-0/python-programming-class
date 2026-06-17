# Week14

## 이번 주 큰 흐름

* File Handling

  * file: open and close
  * Text File: read and write
  * Binary File: write and read
  * Text mode vs. Binary mode: File open
  * Binary File의 특별한 사용: pickle (Serialization)
  * File 및 Directory 처리

    * os 모듈의 함수들 : file과 directory 관련
  * venv : Python Virtual Environment

# 1. File Handling

## 1.1 File Handling이란?

File Handling은 Python에서 파일을 읽고 쓰고 관리하는 작업을 의미한다.

즉,

```text
파일 열기
파일 읽기
파일 쓰기
파일 닫기
파일/디렉토리 경로 처리
```

등을 포함한다.

## 1.2 File Object

Python에서 파일을 처리하려면 먼저 파일에 접근할 수 있는 object를 얻어야 한다.

이 object는 여러 이름으로 불린다.

```text
file object
file handler
file descriptor
```

Python에서는 보통 **File Object**라는 표현을 많이 사용한다.

## 1.3 File Descriptor

File Descriptor는 OS에서 열린 파일에 대해 할당하는 int형 id이다.

즉, OS 입장에서 열린 파일을 구분하기 위한 번호라고 볼 수 있다.

Python에서는 직접 file descriptor를 다루기보다는 `open()`으로 얻은 file object를 사용한다.

# 2. File Open and Close

## 2.1 File Open

파일을 open한다는 것은 OS에게 해당 파일에 대한 입출력 stream을 생성해달라고 요청하는 것이다.

Python에서는 `open()` 함수를 사용한다.

```python
f = open("test.txt", "wt")
```

여기서

```text
test.txt = file path
wt = file open mode
```

이다.

## 2.2 Stream

Stream은 데이터가 연속적으로 흐르는 방식으로 입출력되는 개념이다.

파일을 open하면 Python은 file object를 통해 stream interface를 제공한다.

즉, file object를 이용해 파일 내용을 순차적으로 읽거나 쓸 수 있다.

## 2.3 File Close

파일을 close한다는 것은 파일 작업을 끝내고 OS 자원을 반환하는 것이다.

```python
f.close()
```

파일을 닫을 때 이루어지는 일은 다음과 같다.

* buffer에 남아 있는 데이터를 디스크에 기록
* file descriptor 반환
* OS resource 해제

## 2.4 파일을 닫지 않으면 생길 수 있는 문제

파일을 닫지 않으면 다음과 같은 문제가 생길 수 있다.

* buffer에 남은 데이터가 디스크에 기록되지 않을 수 있음
* file descriptor가 반환되지 않음
* 너무 많은 파일이 열린 상태가 될 수 있음
* `Too many open files` 오류가 발생할 수 있음

따라서 파일 작업 후에는 반드시 close하는 것이 좋다.

# 3. open() 함수

## 3.1 기본 구조

```python
f = open("file_path", "mode")
```

예시는 다음과 같다.

```python
f = open("test.txt", "wt")
```

여기서

```text
file_path = 열고자 하는 파일의 경로
mode = 파일을 어떤 방식으로 열 것인지 지정
```

이다.

## 3.2 File Path

File Path는 파일의 위치를 나타내는 문자열이다.

파일 경로에는 두 가지가 있다.

```text
Absolute Path
= 절대 경로

Relative Path
= 상대 경로
```

## 3.3 Absolute Path

Absolute Path는 현재 작업 위치와 관계없이 파일의 절대적인 위치를 나타내는 경로이다.

예를 들어 Windows에서는 다음과 같은 형태를 가진다.

```text
C:\Users\user\Desktop\test.txt
```

## 3.4 Relative Path

Relative Path는 현재 작업 디렉토리, 즉 cwd를 기준으로 하는 경로이다.

```python
open("test.txt", "rt")
```

라고 하면 현재 작업 디렉토리에서 `test.txt`를 찾는다.

## 3.5 cwd

cwd는 Current Working Directory의 약자이다.

즉, 현재 작업 디렉토리이다.

Python에서 확인하려면 다음과 같이 한다.

```python
import os

print(os.getcwd())
```

# 4. File Open Mode

## 4.1 mode란?

mode는 파일을 어떤 방식으로 열 것인지 지정하는 문자열이다.

mode는 보통 다음 두 부분으로 구성된다.

```text
첫 번째 문자 : 작업 방식
두 번째 문자 : 파일 종류
```

예를 들어

```python
open("test.txt", "wt")
```

에서

```text
w = write mode
t = text mode
```

이다.

## 4.2 첫 번째 문자 : 작업 방식

| mode | 의미                 | 설명         |
| ---- | ------------------ | ---------- |
| r    | read               | 읽기 모드      |
| w    | write              | 쓰기 모드      |
| a    | append             | 파일 끝에 추가   |
| x    | exclusive creation | 새 파일 생성 전용 |

## 4.3 r mode

`r`은 read mode이다.

기존에 존재하는 파일을 읽기 위해 연다.

```python
f = open("test.txt", "r")
```

주의할 점은 파일이 없으면 `FileNotFoundError`가 발생한다.

## 4.4 w mode

`w`는 write mode이다.

파일을 쓰기 위해 연다.

```python
f = open("test.txt", "w")
```

파일이 없으면 새로 생성된다.

하지만 파일이 이미 존재하면 기존 내용은 모두 삭제된다.

## 4.5 a mode

`a`는 append mode이다.

파일 끝에 내용을 추가한다.

```python
f = open("test.txt", "a")
```

파일이 없으면 새로 생성된다.

기존 내용은 삭제되지 않는다.

## 4.6 x mode

`x`는 새 파일 생성 전용 mode이다.

```python
f = open("test.txt", "x")
```

파일이 없을 때만 새로 생성한다.

이미 파일이 존재하면 `FileExistsError`가 발생한다.

## 4.7 두 번째 문자 : 파일 종류

| mode | 의미          | 설명              |
| ---- | ----------- | --------------- |
| t    | text mode   | text file로 처리   |
| b    | binary mode | binary file로 처리 |

`t`는 기본값이므로 생략할 수 있다.

즉, 다음 둘은 거의 같은 의미이다.

```python
open("test.txt", "r")
open("test.txt", "rt")
```

## 4.8 + mode

`+`는 update mode이다.

즉, 읽기와 쓰기를 모두 가능하게 한다.

```text
r+
w+
a+
x+
```

단, 읽기와 쓰기가 모두 가능하다는 뜻이지 동시에 수행된다는 뜻은 아니다.

상황에 따라 `seek()` 또는 `flush()`가 필요할 수 있다.

## 4.9 r+

```python
open("test.txt", "r+")
```

특징은 다음과 같다.

* 파일이 반드시 존재해야 함
* 파일이 없으면 FileNotFoundError 발생
* 기존 내용 삭제 안 됨
* file pointer는 파일 처음에 위치
* write하면 현재 위치부터 기존 내용을 덮어씀

## 4.10 w+

```python
open("test.txt", "w+")
```

특징은 다음과 같다.

* 읽기와 쓰기 가능
* 파일이 없으면 생성
* 파일이 이미 있으면 기존 내용 모두 삭제
* file pointer는 파일 처음에 위치

## 4.11 a+

```python
open("test.txt", "a+")
```

특징은 다음과 같다.

* 읽기와 쓰기 가능
* 파일이 없으면 생성
* 파일이 이미 있으면 기존 내용 유지
* write는 항상 파일 끝에 추가
* read하려면 보통 `seek()`로 위치를 조정해야 함

## 4.12 x+

```python
open("test.txt", "x+")
```

특징은 다음과 같다.

* 파일이 없을 때만 생성
* 파일이 이미 있으면 FileExistsError 발생
* 읽기와 쓰기 가능

# 5. Context Manager

## 5.1 Context Manager란?

Context Manager는 특정 구간에서 resource를 얻고, 해당 구간이 끝나면 resource를 자동으로 반환하게 해주는 기능이다.

파일 처리에서는 `with` statement를 사용한다.

## 5.2 with statement

파일을 처리할 때 가장 권장되는 방식은 `with`를 사용하는 것이다.

```python
with open("test.txt", "wt") as f:
    f.write("hello")
```

위 코드는 block이 끝나면 자동으로 파일을 닫는다.

즉, `close()`를 직접 쓰지 않아도 된다.

## 5.3 with의 동작

`with` block에 들어갈 때는 resource를 얻고, block을 나갈 때는 resource를 반환한다.

파일의 경우

```text
with block 진입 → file open
with block 종료 → file close
```

이다.

## 5.4 직접 close와 with 비교

직접 close하는 방식은 다음과 같다.

```python
f = open("test.txt", "wt")
f.write("hello")
f.close()
```

with를 사용하면 다음과 같다.

```python
with open("test.txt", "wt") as f:
    f.write("hello")
```

둘 다 파일을 닫지만, `with` 방식이 더 안전하고 권장된다.

# 6. Text File: Write

## 6.1 Text File

Text File은 사람이 읽을 수 있는 문자로 구성된 파일이다.

Python에서 text file을 읽고 쓸 때는 `str` 객체를 사용한다.

Text mode로 열면 Python은 encoding/decoding을 자동으로 수행한다.

## 6.2 Text File 열기

```python
with open("test.txt", "wt", encoding="utf-8") as f:
    f.write("hello")
```

여기서

```text
wt = write text
encoding="utf-8" = 문자 인코딩 지정
```

이다.

## 6.3 encoding

Text file은 내부적으로 bytes로 저장되지만, 사람이 읽을 수 있는 문자로 해석하려면 encoding 방식이 필요하다.

대표적인 encoding은 다음과 같다.

```text
utf-8
ascii
cp949
```

보통 Python에서는 `utf-8`을 많이 사용한다.

## 6.4 print()로 쓰기

`print()` 함수는 기본적으로 standard output에 출력한다.

하지만 `file` parameter를 지정하면 파일에 출력할 수 있다.

```python
with open("test.txt", "wt", encoding="utf-8") as f:
    print("Hello Python", file=f)
```

`print()`는 기본적으로 끝에 newline을 추가한다.

## 6.5 write()로 쓰기

`write()` method는 문자열을 파일에 쓴다.

```python
with open("test.txt", "wt", encoding="utf-8") as f:
    cnt = f.write("Hello Python")
    print(cnt)
```

text mode에서 `write()`는 쓴 character 수를 반환한다.

## 6.6 print()와 write() 차이 (⭐ 중요)

| 구분      | print()  | write()     |
| ------- | -------- | ----------- |
| 기본 대상   | stdout   | file object |
| newline | 기본적으로 추가 | 자동 추가 안 함   |
| 반환값     | None     | 쓴 글자 수      |
| 여러 값 출력 | 가능       | 문자열 하나 필요   |

예를 들어

```python
with open("test.txt", "wt") as f:
    print("hello", file=f)
    f.write("python")
```

`print()`는 newline을 붙이고, `write()`는 붙이지 않는다.

## 6.7 여러 줄 쓰기

여러 줄 문자열을 쓸 수 있다.

```python
txt = """First line
Second line
Third line"""

with open("test.txt", "wt", encoding="utf-8") as f:
    f.write(txt)
```

## 6.8 큰 파일 쓰기

큰 문자열을 한 번에 쓰기보다 chunk로 나눠서 쓸 수 있다.

```python
txt = "abcdefghijklmnopqrstuvwxyz"

with open("test.txt", "wt") as f:
    chunk = 5
    offset = 0

    while offset < len(txt):
        f.write(txt[offset:offset + chunk])
        offset += chunk
```

# 7. Text File: Read

## 7.1 Text File 읽기

Text file을 읽을 때는 보통 `rt` mode를 사용한다.

```python
with open("test.txt", "rt", encoding="utf-8") as f:
    txt = f.read()
```

## 7.2 read()

`read()`는 파일 전체를 한 번에 읽거나, 지정한 글자 수만큼 읽는다.

```python
with open("test.txt", "rt") as f:
    txt = f.read()
```

argument 없이 사용하면 전체 파일을 읽는다.

```python
with open("test.txt", "rt") as f:
    txt = f.read(10)
```

argument를 주면 해당 글자 수만큼 읽는다.

EOF에 도달하면 empty string을 반환한다.

```python
""
```

## 7.3 readline()

`readline()`은 한 줄씩 읽는다.

```python
with open("test.txt", "rt") as f:
    line = f.readline()
```

반환된 문자열은 줄 끝의 newline을 포함할 수 있다.

반복해서 읽으려면 다음과 같이 한다.

```python
with open("test.txt", "rt") as f:
    while line := f.readline():
        print(line, end="")
```

## 7.4 readlines()

`readlines()`는 파일의 여러 line을 한 번에 읽고, 각 line을 item으로 가지는 list를 반환한다.

```python
with open("test.txt", "rt") as f:
    lines = f.readlines()

print(lines)
```

각 item에는 newline이 포함될 수 있다.

## 7.5 File Object는 Iterator

File object 자체는 iterator처럼 사용할 수 있다.

따라서 for문으로 한 줄씩 읽을 수 있다.

```python
with open("test.txt", "rt") as f:
    for line in f:
        print(line, end="")
```

이 방식은 파일을 한 줄씩 처리할 수 있어 메모리 측면에서 유리하다.

## 7.6 Text File 읽기 정리

| method        | 의미               | 반환        |
| ------------- | ---------------- | --------- |
| read()        | 전체 또는 지정 글자 수 읽기 | str       |
| readline()    | 한 줄 읽기           | str       |
| readlines()   | 모든 줄을 list로 읽기   | list[str] |
| for line in f | 한 줄씩 순회          | str       |

# 8. Binary File

## 8.1 Binary File이란?

Binary File은 데이터를 text 형식이 아니라 이진 형식으로 저장하는 파일이다.

즉, 사람이 읽을 수 있는 문자 중심이 아니라 bytes 중심으로 저장된다.

예를 들면 다음과 같다.

```text
이미지 파일
음악 파일
동영상 파일
실행 파일
pickle 파일
```

## 8.2 Binary File의 특징

Binary file은 다음과 같은 특징이 있다.

* 사람이 직접 읽기 어렵다.
* 특정 프로그램이 해석해야 의미가 있다.
* text encoding/decoding이 자동으로 수행되지 않는다.
* `str`이 아니라 `bytes` 또는 `bytearray`를 사용한다.

## 8.3 bytes와 bytearray

Binary file에서는 주로 `bytes`와 `bytearray`를 사용한다.

```text
bytes
= immutable

bytearray
= mutable
```

예시는 다음과 같다.

```python
b1 = bytes([65, 66, 67])
b2 = bytearray([65, 66, 67])

print(b1)
print(b2)
```

출력은 다음과 같다.

```text
b'ABC'
bytearray(b'ABC')
```

## 8.4 Binary File 쓰기

Binary file을 쓸 때는 `wb` mode를 사용한다.

```python
bin_data = bytearray(range(0, 32))

with open("bfile.bin", "wb") as f:
    cnt = f.write(bin_data)
    print(f"{cnt} bytes is written")
```

binary mode에서 `write()`는 쓴 byte 수를 반환한다.

## 8.5 Binary File 읽기

Binary file을 읽을 때는 `rb` mode를 사용한다.

```python
with open("bfile.bin", "rb") as f:
    data = f.read()

print(data)
```

chunk 단위로 읽을 수도 있다.

```python
r_bin = bytes()

with open("bfile.bin", "rb") as f:
    chunk = 5

    while buf := f.read(chunk):
        r_bin += buf

print(len(r_bin))
print(list(map(int, r_bin)))
```

EOF에 도달하면 empty bytes를 반환한다.

```python
b""
```

# 9. Text Mode vs Binary Mode

## 9.1 Text Mode

Text mode는 파일을 문자 기반으로 처리한다.

```python
open("test.txt", "rt")
open("test.txt", "wt")
```

Text mode의 특징은 다음과 같다.

* `str`을 사용한다.
* encoding/decoding이 자동으로 수행된다.
* 사람이 읽을 수 있는 문자 파일을 다룰 때 사용한다.
* 기본 mode이다.

## 9.2 Binary Mode

Binary mode는 파일을 bytes 기반으로 처리한다.

```python
open("file.bin", "rb")
open("file.bin", "wb")
```

Binary mode의 특징은 다음과 같다.

* `bytes` 또는 `bytearray`를 사용한다.
* encoding/decoding이 자동으로 수행되지 않는다.
* byte 값을 그대로 읽고 쓴다.
* 이미지, 동영상, 실행 파일, pickle 파일 등에 사용한다.

## 9.3 핵심 차이 (⭐ 중요)

| 구분                | Text Mode             | Binary Mode           |
| ----------------- | --------------------- | --------------------- |
| mode              | t                     | b                     |
| 기본 자료형            | str                   | bytes                 |
| 단위                | 문자                    | byte                  |
| encoding/decoding | 자동 수행                 | 수행 안 함                |
| 예시                | txt, csv              | image, bin, pkl       |
| open 예시           | `open("a.txt", "rt")` | `open("a.bin", "rb")` |

## 9.4 encoding error

Text mode로 파일을 열 때, 지정한 encoding으로 해석할 수 없는 byte가 있으면 `UnicodeDecodeError`가 발생할 수 있다.

```python
with open("file.txt", "rt", encoding="ascii") as f:
    txt = f.read()
```

ascii로 해석할 수 없는 byte가 있으면 오류가 발생한다.

이때 다음처럼 처리할 수도 있다.

```python
with open("file.txt", "rt", encoding="ascii", errors="ignore") as f:
    txt = f.read()
```

`errors="ignore"`는 해석할 수 없는 byte를 무시한다.

# 10. Pickle

## 10.1 Serialization

Serialization은 객체를 저장하거나 전송할 수 있도록 연속적인 bytes 형태로 변환하는 과정이다.

즉,

```text
Python object → bytes 형태
```

로 바꾸는 것이다.

반대로 bytes 형태의 데이터를 다시 객체로 복원하는 것을 deserialization이라고 한다.

```text
bytes 형태 → Python object
```

## 10.2 pickle이란?

`pickle`은 Python 객체를 직렬화하고 역직렬화하기 위한 module이다.

즉, Python object를 파일에 저장하고 다시 읽어올 수 있게 해준다.

```text
pickle.dump()
= 객체 저장

pickle.load()
= 객체 읽기
```

## 10.3 pickle의 특징

pickle은 binary serialization이다.

즉, text가 아니라 binary 형태로 객체를 저장한다.

따라서 pickle 파일은 보통 binary mode로 연다.

```text
쓰기 : wb
읽기 : rb
```

## 10.4 pickle로 객체 저장

```python
import pickle

data = {
    "name": "Alice",
    "age": 25,
    "scores": [95, 88, 92]
}

with open("data.pkl", "wb") as f:
    pickle.dump(data, f)
```

## 10.5 pickle로 객체 읽기

```python
import pickle

with open("data.pkl", "rb") as f:
    loaded_data = pickle.load(f)

print(loaded_data)
```

## 10.6 전체 흐름 예제

```python
import pickle

example_object = {
    "id": 123,
    "name": "John Doe",
    "attributes": ["smart", "kind", "friendly"],
    "scores": {"math": 90, "science": 88}
}

with open("example.pkl", "wb") as f:
    pickle.dump(example_object, f)

with open("example.pkl", "rb") as f:
    loaded_object = pickle.load(f)

print(loaded_object)
```

## 10.7 pickle 주의 사항 (⭐ 중요)

pickle은 신뢰할 수 없는 데이터를 load하면 보안 위험이 있다.

악의적인 코드가 포함된 pickle 데이터를 읽으면 문제가 생길 수 있다.

따라서 다음을 기억해야 한다.

```text
pickle.load()는 반드시 신뢰할 수 있는 파일에만 사용한다.
```

## 10.8 pickle protocol

pickle은 여러 protocol 버전을 지원한다.

현재 사용 가능한 가장 높은 protocol은 다음과 같이 확인할 수 있다.

```python
import pickle

print(pickle.HIGHEST_PROTOCOL)
print(pickle.DEFAULT_PROTOCOL)
```

최신 protocol을 사용하려면 다음처럼 쓴다.

```python
with open("data.pkl", "wb") as f:
    pickle.dump(data, f, protocol=pickle.HIGHEST_PROTOCOL)
```

## 10.9 pickle 정리

```text
Serialization
= object를 저장/전송 가능한 형태로 변환

pickle
= Python object를 binary 형태로 저장하고 복원하는 module

dump
= 저장

load
= 읽기

pickle 파일
= binary mode로 처리
```

# 11. os Module

## 11.1 os Module이란?

`os` module은 운영체제와 상호작용하기 위한 Python built-in module이다.

파일과 디렉토리 관련 작업을 할 때 자주 사용한다.

```python
import os
```

## 11.2 os.path

`os.path`는 path를 다루기 위한 기능을 제공한다.

path는 파일이나 디렉토리의 위치를 나타내는 문자열이다.

## 11.3 os.path.exists()

경로가 실제로 존재하는지 확인한다.

```python
import os

print(os.path.exists("test.txt"))
```

존재하면 `True`, 존재하지 않으면 `False`를 반환한다.

## 11.4 os.path.isfile()

해당 경로가 파일인지 확인한다.

```python
print(os.path.isfile("test.txt"))
```

파일이면 `True`, 아니면 `False`를 반환한다.

## 11.5 os.path.isdir()

해당 경로가 디렉토리인지 확인한다.

```python
print(os.path.isdir("my_dir"))
```

디렉토리이면 `True`, 아니면 `False`를 반환한다.

## 11.6 os.path.join() (⭐ 중요)

여러 path 조각을 합쳐 하나의 경로를 만든다.

```python
path = os.path.join("folder", "subfolder", "test.txt")
print(path)
```

운영체제에 맞는 구분자를 사용해 path를 만들어준다.

## 11.7 os.path.abspath()

absolute path를 반환한다.

```python
abs_path = os.path.abspath("test.txt")
print(abs_path)
```

## 11.8 os.path.basename()

경로의 마지막 이름을 반환한다.

```python
print(os.path.basename("/home/user/test.txt"))
```

출력은 다음과 같다.

```text
test.txt
```

## 11.9 os.path.dirname()

파일을 포함하는 directory path를 반환한다.

```python
print(os.path.dirname("/home/user/test.txt"))
```

출력은 다음과 같다.

```text
/home/user
```

## 11.10 os.path.split()

path를 directory 부분과 마지막 이름으로 나눈다.

```python
print(os.path.split("/home/user/test.txt"))
```

출력은 다음과 같다.

```text
('/home/user', 'test.txt')
```

## 11.11 os.path.getsize()

파일 크기를 반환한다.

```python
print(os.path.getsize("test.txt"))
```

# 12. os Module: File and Directory

## 12.1 os.getcwd()

현재 작업 디렉토리를 반환한다.

```python
import os

print(os.getcwd())
```

## 12.2 os.chdir()

현재 작업 디렉토리를 변경한다.

```python
os.chdir("new_folder")
```

## 12.3 os.listdir()

디렉토리 안의 파일과 subdirectory 목록을 list로 반환한다.

```python
print(os.listdir("."))
```

## 12.4 os.mkdir()

디렉토리를 생성한다.

```python
os.mkdir("new_dir")
```

단, 중간 경로가 없으면 생성되지 않는다.

이미 존재하는 디렉토리를 만들려고 하면 `FileExistsError`가 발생한다.

## 12.5 os.makedirs()

중간 디렉토리까지 한 번에 생성한다.

```python
os.makedirs("a/b/c", exist_ok=True)
```

`exist_ok=True`를 지정하면 이미 디렉토리가 있어도 에러가 발생하지 않는다.

## 12.6 os.remove()

파일을 삭제한다.

```python
os.remove("test.txt")
```

## 12.7 os.rmdir()

비어 있는 디렉토리를 삭제한다.

```python
os.rmdir("empty_dir")
```

주의할 점은 비어 있지 않은 디렉토리는 삭제할 수 없다.

## 12.8 os.rename()

파일이나 디렉토리 이름을 변경한다.

```python
os.rename("old.txt", "new.txt")
```

## 12.9 os.replace()

`os.replace()`도 이름 변경과 비슷하지만, 대상이 존재하면 덮어쓴다.

```python
os.replace("old.txt", "new.txt")
```

## 12.10 os.system()

OS의 shell 명령어를 실행한다.

```python
os.system("dir")
```

하지만 일반적으로는 `os.system()`보다 `subprocess` module 사용이 권장된다.

# 13. 자주 쓰는 os 함수 정리

## 13.1 경로 확인

```python
os.getcwd()
os.chdir(path)
```

## 13.2 존재 여부 확인

```python
os.path.exists(path)
os.path.isfile(path)
os.path.isdir(path)
```

## 13.3 경로 만들기 및 분리

```python
os.path.join(a, b)
os.path.abspath(path)
os.path.basename(path)
os.path.dirname(path)
os.path.split(path)
```

## 13.4 디렉토리 생성/삭제

```python
os.mkdir(path)
os.makedirs(path, exist_ok=True)
os.rmdir(path)
```

## 13.5 파일 처리

```python
os.remove(path)
os.rename(old, new)
os.replace(old, new)
```

## 13.6 목록 확인

```python
os.listdir(path)
```

# 14. pathlib 참고

## 14.1 pathlib

`pathlib`은 path를 문자열이 아니라 객체로 다루기 위한 Python 표준 library이다.

`os.path`는 문자열 중심이고, `pathlib.Path`는 객체 중심이다.

```python
from pathlib import Path

p = Path("folder") / "test.txt"
print(p)
```

시험에서는 `os` 중심으로 나오더라도, `pathlib`이 있다는 정도는 알아두면 좋다.

# 15. venv

## 15.1 venv란?

`venv`는 Python Virtual Environment를 만들기 위한 Python standard library이다.

즉, Python 가상환경을 만드는 module이다.

Python 3.3부터 기본 내장되어 있다.

## 15.2 Virtual Environment란?

Virtual Environment는 프로젝트마다 독립적인 Python 실행 환경을 만드는 것이다.

즉, 프로젝트마다 필요한 package를 따로 관리할 수 있다.

```text
Project A → package A, B 사용
Project B → package C, D 사용
```

이렇게 서로 영향을 주지 않도록 분리할 수 있다.

## 15.3 venv를 사용하는 이유

venv를 사용하는 이유는 다음과 같다.

* 프로젝트별 package 관리 가능
* host system Python 환경을 오염시키지 않음
* package version 충돌 방지
* 개발 환경 재현이 쉬움

## 15.4 가상환경 생성

가상환경은 다음 명령어로 생성한다.

```bash
python -m venv 환경이름
```

예를 들어

```bash
python -m venv myenv
```

를 실행하면 `myenv`라는 directory가 생성된다.

## 15.5 가상환경 활성화 : Linux / macOS

```bash
source myenv/bin/activate
```

또는

```bash
. myenv/bin/activate
```

## 15.6 가상환경 활성화 : Windows cmd

```bash
.\myenv\Scripts\activate.bat
```

## 15.7 가상환경 활성화 : Windows PowerShell

```bash
.\myenv\Scripts\Activate.ps1
```

만약 PowerShell에서 실행이 막히면 실행 정책 문제일 수 있다.

## 15.8 package 설치

가상환경을 활성화한 상태에서 `pip`를 사용한다.

```bash
pip install package_name
```

예를 들어

```bash
pip install numpy
```

가상환경 안에 package가 설치된다.

## 15.9 가상환경 비활성화

가상환경에서 빠져나올 때는 다음 명령어를 사용한다.

```bash
deactivate
```

## 15.10 가상환경 삭제

가상환경을 삭제하려면 생성된 환경 directory를 통째로 삭제하면 된다.

예를 들어 `myenv`라는 환경을 만들었다면 `myenv` 폴더를 삭제하면 된다.

