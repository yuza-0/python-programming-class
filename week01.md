# Week01

## 이번 주 큰 흐름
- Python 실행 환경
  - REPL
  - IPython
  - Jupyter Notebook / Colab 
  - 터미널, IDE

- python의 실행 방식
  - REPL 방식
  - Script 실행 방식 (.py)
  - Module 실행 방식 (-m)

- 매직 커맨드와 OS 명령어
  - 매직 커맨드 (% 계열)
  - OS 명령어 (! 계열)

- Python 설치
  - CPython 설치 튜토리얼
  - Semantic Versioning
  - 패키지, 패키지 매니저

- 윤성우의 열혈 파이썬 1
  - print문

---

# 1. 파이썬 실행환경
```
내가 코드를 쓰고 싶다
 
  ↓

어디서 할까?  (작업 도구 / 창)

기본 환경
- Python REPL (python)
- IPython

노트북 환경
- Jupyter Notebook
- Google Colab

IDE / 에디터
- VSCode
- PyCharm

터미널 / 쉘
- cmd (Windows)
- bash / zsh (Linux, macOS)

기타 (참고용)
- 온라인 실행기 (repl.it 등)
- Python Shell (IDLE)

 ↓

누가 실제로 실행하나?  (실행기)
- Python

↓

어떻게 실행하나?  (사용 방식)
- shell을 통한 REPL 방식 (=shell execution)
- script 파일(.py확장자)을 이용한 방식 (=script execution)
- -m 옵션을 통한 module로 수행
```

여기서
Interactive mode면 **python shell, prompt(>>>)** 이 보인다고 하고, 그 상태로 계속 작업하는 상태를 **Interactive session**이라 한다.

#### 참고 용어1 : `shell`

사용자와 OS (정확히는 kernel) 사이에 위치하면서 사용자가 OS를 사용하도록 돕는 프로그램을 가르킨다.
#### 참고 용어2 : `prompt`

사용자에게 컴퓨터가 다음 명령을 입력받을 준비가 되었음 을 알려줌.

# 1.1 REPL

- Python 인터프리터 실행 후 `>>>` 상태

```python
>>> python
>>>
```
- 한 줄 입력 → 즉시 실행

## 1.2 IPython

- REPL의 확장 버전
- 자동완성, 매직 커맨드(⭐ 중요) 등 추가 기능 제공

## 1.3 Jupyter Notebook / Colab 

- 셀 단위로 코드 실행
- 코드 + 결과 + 설명 함께 작성 가능
REPL 방식 기반

## 1.4 터미널, IDE

- 터미널(cmd, bash): Python 실행, script 실행 가능
- IDE(VSCode 등): 코드 작성 + 실행 환경 제공

# 2. python의 실행 방식

## 2.1 REPL 방식 (⭐ 중요)

한 줄 입력 → 즉시 실행 → 결과 출력

**Read → Eval → Print → Loop**(⭐ 중요)
- **Read** : 사용자가 python shell의 prompt에 입력한 statements를 읽고
- **Evaluate** : 평가하여 실행시키고
- **Print** : 해당 결과를 즉시 출력하고
- **Loop**: 다시 prompt를 통해 사용자의 입력을 대기, 위 과정을 반복하는 **실행방식**.

**interactive mode(execution)** 라고도 부른다.
그냥 계산기라 생각하면 편하다.

## 2.2 Script execution (.py) (⭐ 중요)

```python
python <main_script_file>.py
```

Python 인터프리터가 지정된 <main_script_file>.py 파일을 읽어 하나의 프로그램으로 실행하는 방식.

실행할 main sciprt file은 PATH로 지정

## 2.3 Module Execution (⭐ 중요)

```python
python -m <module_name>
```

Python 인터프리터가 sys.path(정확히는 module search path)에서 <module_name>이라는 이름을 가지는 모듈을 찾아 해당 모듈을 __main__ 컨텍스트로 실행하는 방식.

#### 참고 용어 : 
`python -c`는 문자열로 전달된 코드를 파일 없이 즉시 실행하는 방식이며, 여러 문장은 ;로 구분한다.

주로 간단한 테스트나 sys.path 확인 같은 짧은 코드 실행에 사용된다.

`python -i script.py`는 script를 먼저 실행한 뒤 종료하지 않고 REPL(인터랙티브 모드)로 진입하는 방식이다.
즉, 실행 결과 상태를 유지한 채 이어서 직접 코드 실행이 가능하다.

`sys.path`는 Python이 module을 찾는 경로 목록이며, 현재 실행 중인 디렉토리는 항상 포함된다.


---

# 3. 매직 커맨드와 OS 명령어
IPython은 Python에서 shell 명령어를 사용할 수 있게 해줌

## 3.1 매직 커맨드 (% 계열)
- %automagic on : magic commands가 % prefix 없이 수행가능

- %augomagic off : % prefix를 붙여야 함
## 3.2 OS 명령어 (! 계열)
OS에서 지원하는 shell commands를 실행

---

# 4. Python 설치와 설치 매니저,  Semantic Versioning, 패키지와 패키지 매니저

## 4.1 Python 설치
python.org 웹사이트에 가서 Downloads를 선택하여 최신 release를 다운로드.

"Install launcher for all users" 또는 "Add Python to PATH" 옵션을 선택하면

Python Launcher for Windows 라고 불리는 py.exe 가 함께 설치됨:

## 4.2 python 설치 매니저

py = PIM (설치 + 실행 + 관리)
Python 3.14부터 도입
Python 3.16부터 표준

## 4.3 Semantic Versioning

소프트웨어 버전을 체계적으로 비교하고 관리하는 규칙

### 기본 구조
```MAJOR.MINOR.PATCH```
```
1 → 큰 변화
2 → 기능 추가
3 → 버그 수정
```

### 버전 우선순위

```dev < a(alpha) < b(beta) < rc < release < post```
```
a = alpha
b = beta
rc = release candidate (출시 직전)
dev → 실험 중
release → 완성
```

```1.0.0.dev1 < 1.0.0a1 < 1.0.0b1 < 1.0.0rc1 < 1.0.0 < 1.0.0.post1```

### epoch
```1!1.0.0 > 3.0.0 ```
### local
`+` 기호 뒤에 나타나며, 버전 비교에서 주요 우선순위에 영향을 주지 않음


## 4.4 패키지와 패키지 매니저 (⭐ 중요)

### 4.4.1 pip란
pip는 Python에서 패키지를 설치, 업그레이드, 삭제할 때 사용하는 패키지 매니저이다. numpy, pandas, requests 같은 외부 라이브러리를 설치할 때 주로 사용한다.
### 4.4.2 package
여러 구성요소를 하나로 묶은 것을 의미한다.

python과 os에서의 package는 다른 의미를 가진다.

- 파이썬에서의 패키지: 여러 모듈(.py 파일)과 관련 코드들을 묶어둔 것.
예 : request, numpy, pandas

- os에서의 패키지: 설치 가능한 프로그램 단위.프로그램 실행 파일, 설정 파일, 의존성 정보 등을 포함한 묶음

즉, 여러 패키지가 함께 묶여서 설치되기 때문에 이를 효율적으로 설치 관리하기 위해 패키지 매니저가 필요하다. 

### 4.4.3 package manager
패키지 매니저는 소프트웨어(또는 라이브러리)를 설치 / 업데이트 / 제거 / 의존성 관리해주는 도구이다.
예시는 다음과 같다.
Python: pip
JavaScript: npm
Ubuntu/Linux: apt
macOS: brew

### 4.4.4 pip 설치 및 확인 과정
pip는 대부분 Python 설치 시 함께 설치되므로, 별도로 설치할 일이 많지 않다.
따라서 먼저 pip가 설치되어 있는지 확인하는 과정이 필요하다.

### pip 설치 여부 + 버전 확인
```python -m pip --version```
```pip --version```

### pip 업그레이드
```python -m pip install --upgrade 패키지명```

```python -m pip install --upgrade pip```
### pip 삭제
```python -m pip uninstall 패키지명```

### pip 목록 확인
```python -m pip list```

### 여러 개 설치
```python -m pip install -r requirements.txt```

### 현재환경 저장
```python -m pip freeze > requirements.txt```

### 설치할 패키지의 Version 지정
== : 정확히 일치하는 버전 설치 
~= : 지정된 버전 이상을 설치하되 메이저 버전은 유지.
>= : 이상 설치
<= : 이하 설치

### 추가

-quiet 옵션을 활용하면, 설치 과정에서 출력되는 log를 최소화함.

-r 은 --requirement 옵션과 같은 뜻임.

---

# 5. 윤성우의 열혈 파이썬 1

## 5.1 print문

Python의 built-in 함수로, 표준 출력(stdout) 에 메시지나 데이터를 문자열 형태로 출력하는 기능을 제공.

### 특징
- 콤마로 구분하여 여러 parameter의 사용
- 모든 타입을 str로 변환 후 출력

#### 참고 용어 : `프로그래밍에서의 stream`

- 입력 스트림(Input Stream):
데이터를 프로그램으로 가져오는 stream (예: 키보드입력, 파일 읽기, 네트워크 수신)
  - stdin 
  - 숫자로 0 
  - Python에선 sys.stdin 으로 표준 입력스트림을 가리킴.

- 출력 스트림(Output Stream):
데이터를 외부로 보내는 흐름 (예: 파일 쓰기, 네트워크 전송)
   - sys.stdout 이 표준 출력스트림을 가리킴.
  - 숫자로 1

### 5.1.1 예제
```python
print("Hello, world!")  # 출력: Hello, world!
```

```python
name = "Alice"
age = 25
print("Name:", name, "Age:", age)  # 출력: Name: Alice Age: 25
```

### 5.1.2 주요 매개 변수
- print(변수)
- print(sep=' ') : 구분문자
- print( end='\n') : 줄바꿈 대신 사용 문자 (⭐ 중요)

### 5.1.3 포맷팅을 사용한 출력 (f-string, format(), % 연산자)

### f-string (Python 3.6 이상)

{} 안에는 expression이 들어갈 수 있고 해당 expression이 evaluation된 값이 문자열에서 해당 {} 부분이 치환되어 완성됨.

```python
a = "문자열"
b = 7.0
s = f'이것은 f-String 입니다. a={a}, b={b+3} 입니다.'
print(s)
```
```
이것은 f-String 입니다. a=문자열, b=10.0 입니다.
```
#### variable들의 값을 확인하는 기능

```python
a = 'test'
b = 8.0
c = 3
 
print(f"New f-string\'s function : {a=}, {b=}, and {c=}.")
```
```
New f-string's function : a='test', b=8.0, and c=3
```


### str.format() 메서드
```
"Hello, {}!".format(name)
```

### % 연산자 (구버전 스타일)
```
"Hello, %s %s!" % (fname,lname)
```
## 5.2 ppt 주요 예제
<img width="160" height="211" alt="image" src="https://github.com/user-attachments/assets/08bca7b8-8c8c-4a19-a4af-de71b04b6928" />


튜플 패킹 후 언패킹으로 동시에 할당이 이루어진다
