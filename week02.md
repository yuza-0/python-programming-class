# Week02
## 이번 주 큰 흐름

- 프로그래밍 언어 기초

- Python 기초
  - 객체, 클래스, 타입
  - 변수, 변수명 규칙
  - statement vs expression 
  - Comments and Docstrings

 
- 윤성우의 열혈 파이썬2
  - 함수와 호출, 인자

# 1. 프로그래밍 언어의 기초

## 1.1 프로그래밍 언어
인간과 컴퓨터 사이의 의사소통을 담당하는 인공적 언어.

## 1.2 프로그래밍 언어 특징
-  엄격한 규칙에 따라 정의(자연어와 다름)
- 컴파일러, 인터프리터 등을 통해 기계가 수행 가능한 기계어(machine language, binary code)로 수행.

## 1.3 프로그래밍 언어의 최소 요건 (⭐ 시험 )
계산 가능한 모든 문제를 풀 수 있는 이론적 요건을 갖추었는지, 즉 **Turing Completeness**를 만족해야 한다.

이를 위해 배워야 하는 것은
- **변수 선언과 할당(variable assignment)**
: 데이터 관리를 위해 변수나 메모리 상태를 갱신하는 기능. 상태 표현.

- **조건과 분기(conditional branching)**
: 데이터 값에 대한 조건문을 실행, 결과에 따라 분기하는 기능.

- **반복(무한 loop, conditional loop)**
: 특정 조건에 따라 반복.

추가로, 함수와 클래스를 만드는 방법도 다룬다.

## 1.4 프로그래밍 언어의 분류

### 1.4.1 추상화 여부에 따른
- **Low-level Language (저급언어)**
: 기계 친화적 언어, 기계가 이해하기 쉬움.

예 : Machine language와 Assembly language

- **High-level Language (고급언어)**
: 추상적이고 인간친화적인 언어. 하드웨어에 대한 직접적 이해 없이도 프로그래밍이 가능.

예 : c, c++, c#, java, **python**, javascript

#### 참고 용어 : `추상화(Abstraction)` (⭐ 중요)
복잡한 대상에 대해 핵심적인 개념이나 기능만을 드러내고, 세부적인 구현이나 수행에 필요하지 않은 요소들을 숨기거나 제거. 

### 1.4.2 작동 방식에 따른
- **Compiler Language** : **Compiler** (고급언어 -> 기계어)를 사용하는 고급 언어. 

프로그램 전체를 읽어들여 이를 object code(목적코드)로 바꿈. 빠르게 전체 프로그램 실행 가능, source code 변경 시 다시 compile.

**구조** : 코드 → 컴파일러(번역) → 기계어(실행파일) → CPU 실행

예 : Fortran, Pascal, Cobol, Ada, C, C++
---
#### 참고 용어 : `compile`
실행 **전**에 코드를 컴퓨터가 이해하게 바꾸는 과정. 

이와 헷갈리는 **런타임**은 프로그램이 실제로 실행되는 순간이다

---

- **Interpreter Language (or Scripting Language)** : **Interpreter**(행, line 단위로 기계어로 번역)에 의해, line 단위로 **컴파일 없이** 실행되는 고급 언어.

Q. 근데 컴파일이 없다기엔 바이트코드 변환은 컴파일 아닌가?

statement 단위의 execution(실행)이 가능하므로 개발 단계에서 적은 양의 수정에 대한 결과를 쉽게 확인 가능. 대화식 프로그래밍이 가능하여 교육용으로 적합.

구조 : 코드 → (바이트코드 변환) → 인터프리터 (해석) → CPU 실행 (간접)

대표적인 예로 **Python**, PHP, Ruby, JavaScript, Perl 

---

#### 참고 용어 : `interpreter`

application 나 commands로 작성된 script 등이
OS를 통해 실행되도록
처리해주는 os 상에서 동작하는 s/w program을 가르킨다.
<img width="595" height="316" alt="image" src="https://github.com/user-attachments/assets/8f440d7f-df3c-4dad-b8e8-b85812e85427" />


---

#### 주의
- 요즘은 컴파일, 인터프리터의 기능을 절반씩 가져와서 사용 
- "컴파일러 언어"라는 표현은 엄밀한 분류라기보다,
컴파일러를 통해 주로 실행되는 프로그래밍 언어를 편의상 가리키는 표현

즉, 컴파일러 언어든 인터프리터 언어든 언어를 실행하기 위한 번역(처리) 방식이다.

### 비교 

<img width="608" height="269" alt="image" src="https://github.com/user-attachments/assets/e3eade43-0417-4a62-858a-ec0335c68a9a" />


#### 참고 용어1 : `scripting language`
general purpose programming language보다 특정 domain에 한정된 DSL(domain-specific language)들을 지칭하는 경우가 많아지면서 특정 task나 환경에 국한된 언어들(이들 대부분이 interpreter방식임)을 가리키는 데 쓰인다.

#### 참고 용어2 : 코드 관련

`Source code (원시코드)`
**programming language**로 작성된 text(텍스트)로서 **인간이 사용하는 문자**로 이루어진 code.

일반적으로 compiler나 interpreter의 도움 없이는 **컴퓨터가 직접 읽고 수행하지 못한다.**

`Bytecode (바이트코드)` (⭐ 중요)

Bytecode는 Virtual Machine이 인식하고 실행할 수 있는 **중간 코드(intermediate code)** 로, 바이트 단위로 처리됨.


특징
- 플랫폼 독립적 **(Portability)**
- 가상 머신(VM)에서 실행
    
    Java에서는 .class 파일 형태로 생성되어 JVM에서 실행되고, Python에서는 .pyc 파일 형태로 생성되어 Python VM에서 실행됨.


#### 참고 용어 2-1 : Python 내부 실행 구조 (PVM)

Python 코드는 바로 CPU에서 실행되지 않고,
인터프리터를 통해 bytecode로 변환된 뒤 PVM에서 실행된다.

```text
Python Source Code (.py / REPL 입력)
        ↓
Interpreter가 컴파일
        ↓
Bytecode 생성
        ↓
interpreter 안의 PVM이 Bytecode 실행
        ↓
CPU가 실제 연산 수행
        ↓
결과 출력 / 객체 생성
```

`Object code (목적코드)`
source code로부터 compile을 수행하여 생성한 code 혹은 파일

특징
- 바이너리 코드
- 다른 오브젝트 코드와 연결되어 실행 가능한 코드가 됨(linking, linker), 이를 완벽한 오브젝트 코드라고 보기도 함.

`Binary code (바이너리코드, 이진코드)`
실제 컴퓨터(정확히는 cpu)가 인식 및 수행할 수 있는 bit pattern.


`Machine code (or Machine language, 기계어)`
Programming language라기보다는 cpu가 직접 이해하고 실행할 수 있는 operation code들.(instruction set)

0과 1로 이루어진 binary code들이며 cpu가 읽고 수행이 가능함.

`Microcode (마이크로코드)`
Microcode는 CPU 내부에서 machine code의 명령어를 실행하기 위해 필요한 더 저수준의 제어 신호를 생성하는 code.

특징
- 복잡한 machine code의 명령어를 더 간단한 hardware code 로 분해함.
- hardware에 내장되거나 firmware 형태로 제공됨.


### 1.4.3 프로그래밍 작성 기법에 따른
- 명령형 프로그래밍 언어 (Imperative Programming Language):
  - 절차적 프로그래밍 언어 (Procedural Programming Language)
    - 구조적 프로그래밍 언어 (Structured Programming Language): procedural을 개선! **
  - 객체지향 프로그래밍 언어 (Object Oriented Programming Language): 일부 declarative요소도 포함가능 ***
- 선언적 프로그래밍 언어 (Declarative Programming Language): SQL
  - 논리형 프로그래밍 언어 (Logic Programming Language): Prolog
  - 함수형 프로그래밍 언어 (Functional Programming Language): Haskell, Erlang, Scala ***


### 명령형, 선언형 차이 (⭐ 중요)

### 선언형 Declarative Programming Language
- 프로그램이 **무엇(what)을 원하는지(원하는 상태), 경과나 관계**를 기술, 선언.

- 그것을 어떻게(how) 계산할지에 대한 절차는 명시하지 않는다.

- 개발자: 결과 또는 관계를 선언
 / 시스템: 결과를 도출하기 위한 실행 절차 결정

- 예: SQL (Structured Query Language), Prolog

### 명령형 Imperative Programming Language
- 프로그램이 **어떻게(how) 동작해야 하는지**를 명시한다. 
- 명시적으로 실행할 instruction들을 순서대로 기재. 
- 프로그램의 제어 흐름(control flow)을 직접 정의.

- 개발자: 어떠 순서로 실행, 어떤 조건에서 분기, 어떤 상태를 변경. / 시스템: 상태변경(state mutation)을 지원.명령이 순차적으로 실행.메모리 갱신이 가능.
- 예: C,**Python**,Java

---
---

## 2. 파이썬 기초

## 2.1 객체, 클래스, 데이터 타입

### 2.1.1 객체 object
**type, value, ID, 그리고 reference count**를
가지고 있는 데이터 덩어리(data chunk) (⭐ 시험 )

Python에선 모든 것이 object임: function, class, 심지어 데이터 타입마저.


- type: 해당 데이터가 무엇인지(종류), 무엇을 할 수 있는지 정의

- id: 자신의 주민등록번호 같은 고유한 값. 주소. 같은 object만이 동일한 id를 가진다. CPython에서는 할당된 memory address.

- value : type에 의해 가질 수 있는 value의 범위가 결정

- reference count: 객체가 얼마나 많이 사용되고 있는지를 숫자로 기록, 필요하지 않을 때(0) 메모리에서 즉시 해제

### 2.1.2 클래스 Class

 동일한 구조(state, 데이터집합)와 동작(behavior)을 공유하는 instance를 생성하기 위한 설계도

#### 참고 용어 : `instance`
class로부터 생성된 개별 object. 각 instance들은 독립적인 state를 가지고 같은 클래스의 instance들은 behavior을 공유.

### 2.1.3 데이터 타입 type (⭐ 중요)
객체가 가져야 하는 4가지 요소 중 하나로 모든 value 혹은 object 들의 종류 (category).

 타입이 결정되면, 해당 object의 **value 집합과 해당 객체를 피연산자로 가지는 연산자**가 결정됨.

 ### Type 확인
```python 
type(obj)
```
### 종류
- Numeric Type : arithmetic 연산자와 사용
  - int : 정수 (integer)
  - float : 실수 (real number, floating point)
  - complex : 복소수 (complex)
  ```python
  >>> c = 1+2j     # complex type
  >>> type(c)
  <class 'complex'>
  ```

파이썬의 숫자형은 primitive가 아닌 boxed type으로, 객체이며 method를 가진다.

---

- Boolean Type : if문, while문 그리고 논리 연산자들과 사용
  - bool : True와 False 만을 값으로 가짐. (boolean)

```python
>>> b = True  # keyword True, False 가 바로 boolean type이 가질 수 있는 값.
>>> type(b)
<class 'bool'>
 
>>> b = False
>>> type(b)
<class 'bool'>
```

```python
>>> i = 1
>>> j = 2
>>> b = i<j  or i==j # boolean expression using logical operator
>>> b
True
>>> type(b)
<class 'bool'>
```

참고 용어 : `truthiness` (⭐ 시험 )

0만을 False로 간주하고, 그 외의 수는 True로 간주하는 관례. 실제로 boolean value가 아니지만 boolean value 로 (implicitly) 다루어지는 경우.

```python
>>> i = 0
>>> b = bool(i)
>>> b
False

>>> f = 8.1
>>> b = bool(f)
>>> b
True
```

다음의 경우들은 False로 다루어짐.

- None
- 0
- 0.0
- an empty str, ""(공백문자는 True)

```python
bool("")    # False
bool(" ")   # True
```
- an empty list, []
- an empty set, set()
- an empty dict, {}`


---

- Sequence Type : 순서가 의미 있는 (⭐ 시험 )
  - str : 글자 하나씩의 관점에서는 sequence이지만, 문자열(문장)을 위해 사용됨. text string 또는 string.   
  
    - **immutable**, **iterable**(⭐ 시험 )
    - multi-line의 string은 three single quote 또는 three double quote로 묶어준다. (역시 시작과 끝이 같아야 함.)

    ```python
    >>> ml = """multiline
    ... line1
    ... line2"""

    >>> type(ml)
    <class 'str'>

    >>> ml
    'multiline\nline1\nline2'  # 내부 모습 그대로
    >>> print(ml) # 실제로 실행 시켜서 출력
    multiline
    line1
    line2
    ```
    \n은 new line이라고 읽고, escape sequence이며, string에서 개행을 의미

  - list : item의 index로 순서를 사용하는 sequence type의 대표. **mutable**임.(⭐ 시험 )
  - tuple : **immutable** list라고 불림.

  ---
- Set Type
  - set : 수학에서의 집합을 abstraction(중복되는 item이 없고, 순서가 의미가 없음). mutable임.
  - frozenset : immutable set에 해당.

  ---

- Dictionary Type (or Mapping Type)
    - dict : key 와 value로 구성된 pair를 item으로 가지는 collection. key를 통해 value에 접근 (순서가 의미 없음).


참고 용어 : `Collection Type`

하나의 이상의 object들을 포함하는 data type.
sequence type (list, tuple) , Set (set, frozenset), Mapping type (dict) 

---

- None Type
    - None : none, void 등에 해당하는 type. "없다"라는 것을 나타낸다.
  - Binary Type
    - bytes: immutable byte sequence. binary data를 위한 tuple이라고 생각하면 쉬움 (하나의 item이 1byte에 해당).
    - bytearray: mutable byte sequence. binary data를 위한 list라고 생각하면 됨.

---

### 2.1.4 class와 object 그리고 type

Python에서 모든 것은 객체임. 따라서 클래스도 객체이며, type에 의해 생성됨. 그리고 여기서 type 또한 객체이며, 자신의 타입이 type이다
즉, type(type) = type


## 2.2 변수, assignment, 변수명 규칙

### 2.2.1 variable
Python에서 Variable은 **Object를 참조하는 Name (=Reference, Identifier)**

파이썬에서는 declaration 없이, 참조대상인 object를 가리키도록 해주는 assignment statement만으로 variable 생성이 가능.

**type을 가지고 있는 것은 object**로,variable은 type을 가지고 있지 않고 그저 이름표일 뿐이다.
따라서 reassignment(재할당)하기가 매우 쉬움.

#### 참고 용어 : `Constant variable`

값이 초기화되고 나서 변하지 않는 variable(변수).

Python의 경우 dynamic language이다 보니, constant를 만들기가 꽤나 까다롭다.
따라서 convention(규약)을 통해 uppercase와 underscore만으로 variable name을 할당하며, 이는 변경하지 말라는 의미가 있다.
```python
PI = 3.141956
```


### 2.2.2 assignment

변수에 값을 연결(할당)하는 것

#### 일반적 형태
`varible = expression`

예:
```python
val = 30
```
30이라는 값을 val이라는 이름으로 참조할 수 있게 함

파이썬에서는 변수 선언과 할당을 동시에 한다. (Definition+assignment = assignment)

수학의 “같다”가 아니라
오른쪽 값을 왼쪽 이름에 연결한다는 의미


### 2.2.3 변수명 규칙과 관례 (⭐ 시험 )

 ### naming rules
- variable은 영어대소문자와 underscore, 숫자 들의 조합 사용 가능 (module도 같은 규칙을 따름)
- 한글 변수명은 지원하지만 사용 권하지 않음
- **keywords는 사용불가**
- **첫글자가 숫자가 올 수 없음.**
숫자로 시작하는 module 의 경우, import등이 되질 않음.
-  variable은 하나의 word로 구성되게 되며, **대소문자를 구분함**
-  공백 문자는 넣지 말자. main script는 사용 가능하지만 그것도 위험.

####  참고 용어: `keyword`
 : Python에서 특별한 단어 (special word)들. reserved word라고도 함.


### naming convention (⭐ 중요)

variable이나 class등의 이름을 짓는 일종의 약속.

- 변수나 함수의 이름은 소문자로 시작
- 둘 이상의 단어 연결은 _언더바 사용

underscore로 시작하는 variable들은 일반적으로 특별한 의미를 가지고 있음

### Camel Naming

- Java나 C++에서 선호
- **variable이나 functoin, method**의 경우엔 

  - name(여러 워드를 붙인 것) 의 맨 처음 : 소문자
  - word : 대문자로 시작 
- 예 : camelCase
- 단, class의 이름이나 structure의 이름은 CamelCase 처럼 맨 처음 글자도 대문자로 표기한다.


### Snake Naming ( 변수나 함수, 모듈)
- word 사이에 underscore `_` 
- 예 : snake_case

참고 : 
`Kebab Naming (or Kebab Case)` : underscore 대신 hyphen `-` 이 사용

`Pascal Naming (or Pascal Case)` : 항상 word의 첫글자를 대문자로 표기함( 주로 클래스 )

### 2.2.4 변수, 객체와 타입

파이썬은 고급언어이고, 인터프리터 언어이며, 명령형 언어이다. 

### dynamically (typed) langauge
변수(variable)가 고정된 타입을 갖지 않으며, assignment 시점에 객체(object)가 타입을 가진다.
타입 정보는 **runtime** 에 object 수준에서 체크 및 관리된다.

유연성이 높고 높은 생산성을 가지나, 코드가 길어질 경우 오류 탐지가 쉽지 않고, 수행속도가 느리다는 단점

### Statically (Typed) Language
**compile time** 에 type에 대한 검사가 이루어짐. 과거에는 compiler lanaguage의 대다수가 static language.

- variable은 특정 type을 갖도록 정의. compile time에 variable의 type이 고정
- explicit casting(명시적 형변환)을 하는 경우를 제외하곤 해당 type이 변하지 않음.

- decalration의 시점에 해당 type에 따른 적절한 크기의 memory location(실제 data가 저장되는 공간)에 binding 됨.
 
파이썬에서 Variable은 가리키는 object를 자유롭게 변경할 수 있고 사전에 Type을 가지고 선언될 필요가 없으나(Dynamically Typed Language),
Object 자체는 한 번 생성되면 자신의 Type을 바꿀 수 없음(Strong Typing).

### strong Typing 

Object가
mutable type이냐 immutable type이냐에 상관없이
implicit type conversion이 엄격하게 제한됨

### trong Typed 라는 관점은 Object에 대한 것으로 그들간의 연산에 적용되는 규칙에 대한 것이며, Dynamic (Typing) Language라는 관점은 Variable에 대한 것이다.







## 2.3 expression vs statement (⭐ 중요)

### 2.3.1 expression
평가(evaluation)을 통해 하나의 값으로 치환(reduce)될 수 있는 코드

여기서 
- evaluation은 expression을 결과 값(value)로 바꾸어주는 동작, 계산 과정을
- reduce는 그 결과가 하나의 값으로 정리되는 상태를
- 값(value)는 정수, 문자열, 리스트 등 프로그램에서 다루는 데이터 자체를 의미한다.
- REPL에서는 expression 결과가 자동으로 보임, script 파일에서는 자동으로 보이지 않음(⭐ 시험 )

### expression의 구성요소
- literal
코드에 직접 적은 값 자체. 숫자, 문자열, boolean, list, tuple, dictionary, none, condition

```python
"hello"
```
- identifier : 변수, 함수, 클래스 등의 이름
```python
>>> x=10   #statement(할당은 expression이 아님)
>>> x      #expression, statement
10
```

**참고** : 변수 ⊂ 식별자

변수는 식별자 중 특별히 값을 저장(참조)하는 식별자

- operator
: 단독으로 expression을 구성하지 못한다.
```python
3 + 5
2 * 10
```

- function call


### expression 평가 - eval()
expression을 나타내는 string 을 argument로 받아, 이 결괏값을 반환하는 함수. (⭐ 시험 )

```
eval("코드")
```
이 안에 들어간 문자열을파이썬이 실제 코드라고 생각하고 실행함. 보안상 위험

```python
eval(1 + 2) → 3
```
### 2.3.2 statement

- 실행되는 코드(executable code) 한 줄. 
- 하나 이상의 expression과 keyword로 구성
- expression을 포함하기 때문에 모든 expression은 statement이다.
- none을 반환하기는 함.(⭐ 시험 )
- REPL에서도 보통 출력 없음. script에서도 출력 없음(⭐ 시험 )

```python
>>> 2+3    #expression, statement
5
>>> x=10   #statement
>>> x      #expresssion, statement
10
```

### statement 평가 - exac()
statement에 해당하는 string을 argument로 받아 실행하는 built-in function임.항상 None을 반환함.(⭐ 시험 )

## 2.4 Comments and Docstrings

### 2.4.1 Comments(#)

해당 code들이 무엇을 위해 존재하는지 등을 기재

### 2.4.2 Docstring(short for documentation string)

function이나 class를 설명해주는 comment

function body부분의 첫 라인에서 three double quotes (""")로 시작하고 여러 line에 걸져 주석이 이루어지고(같은indentation유지) three double quotes로 끝난다.


## 3.윤성우의 열혈 파이썬2

## 3.1 함수와 호출, 인자

### 3.1.1 함수란 (⭐ 중요)
재사용성 과 가독성 을 위해 논리적으로 코드를 나누는(or 그룹화 하는) 기본적인 도구. 

**호출 시 주어진 arguments(인자)** 를 **정의된 parameters(매개변수)에 할당**하여 입력 을 받고,
return을 통해 출력 을 수행

### 3.1.2 함수 정의 
```python
  def  test_func (argument0, argument1) : # function header
    function body # indentation을 통해 구분, 여러 statement
    return 
 ```
 - parameter은 일종의 local variable로 생각할 수 있음.

 - function의 body는 4개의 space 문자로 indentation이 이루어짐.

 - return statement로 종료. 
 
    return value가 None이거나(return의 인자가 없거나 아예 return이 없으면) return 뒤의 인자가 함수가 호출된 위치에서 반환될 수 있음(⭐ 시험 )

 #### 참고 용어 : `Compound Statment (복합문)`
 header + suite(body)를 합쳐서 clauses(절)이라 하며, 1개 이상의 clauses로 이루어짐

- if/elif/else
- for/else
- while/else
- with (context manager)
- def (함수정의)
- class (클래스 정의)
- match/case (3.10+)
- Coroutine (3.8+)

### 3.1.3 Function Call (함수 호출)

정의된 함수를 실행하는 것. 반드시 함수 정의 뒤에 이루어져야 함.


### 기본 형태

```python
ret_v = function_name(arg0, arg1)
```

* `arg` → argument (전달 값, expression)
* `ret_v` → 반환값 저장

### 실행 흐름

1. 함수 호출 발생
2. argument → parameter에 전달
3. 함수 내부 실행
4. return 값 생성
5. 호출 위치로 복귀
6. 값 대체

### Call Stack
```text
함수 호출 , return address 저장
 ↓ 
argument → parameter 전달 
↓ 
stack frame 생성 
↓ 
call stack에 push 
↓ 
함수 내부 실행 
↓ 
return 값 생성 
↓ 
stack frame pop (parameter, local 변수 제거) 
↓ 
return address로 복귀 , 호출 부분 return value로 치환(reduction)
``` 

#### 참고 : 
call stack은 주소부터 해서 매개변수 등을 쌓아올리고 먼저 들어간 것이 가장 나중에 나옴. first in last out(FILO)

### 3.1.4 Parameter and Argument 관련
- default 
- keyword
- positional


```python
# 가장 기본 (default 없음)
def f(a, b):
    print(a, b)

f(1, 2)          # a=1, b=2


# default
def f(a=10):
    print(a)

f()              # a=10 (기본값 사용)
f(5)             # a=5  (값 주면 덮어씀)

# 잘못된 정의 (default 뒤에 non-default)
def f(a=10, b):
# ❌ SyntaxError


# keyword 기본
def f(a, b):
    print(a, b)

f(a=1, b=2)      # a=1, b=2
f(b=2, a=1)      # a=1, b=2 (순서 상관 없음)


# default + keyword
def f(a=0, b=0):
    print(a, b)

f()              # a=0, b=0
f(b=5)           # a=0, b=5


# positional + keyword
def f(a, b, c):
    print(a, b, c)

f(1, 2, c=3)     # a=1, b=2, c=3


# 9. 잘못된 호출 (순서 규칙)
f(a=1, 2, 3)
# ❌ keyword - > positional
```

### 3.1.5 Parameter 의 종류 강제 결정 - /, *

### Parameter의 종류
- 위치 전용 매개변수 - Positional-only Parameters
    / 기호 이전


- 위치 또는 키워드 매개변수 - Positional-or-Keyword Parameters
/와 * 사이, 위치나 키워드로 전달 가능

- 키워드 전용 매개변수 - Keyword-only Parameters, `*` 또는 `*args` 이후

- 기본값이 있는 매개변수 - Parameters with Default Values

- 가변 위치 인자 - Variable Positional Arguments: *args , 추가 위치 인자를 튜플로 수집

- 가변 키워드 인자 - Variable Keyword Arguments: **kwargs, 추가 키워드 인자를 딕셔너리로 수집


```
[ 위치전용 ] / [ 자유구간 ] * [ 키워드전용 ]
   a, b         c             d
   ```

### 예시

```python
def func(a, b, /, c):
    pass

func(1, 2, 3)        # ✅
func(a=1, b=2, c=3)  # ❌ (a, b는 위치전용)
```

```python
def func(a, *, b):
    pass

func(1, b=2)  # ✅
func(1, 2)    # ❌
```

```python
def func(*, a, b=10):
    pass

func(a=1)        # ✅ (b는 기본값 사용)
func(a=1, b=2)   # ✅
func()           # ❌ (a는 필수)
```

```python
def func(*args, **kwargs):
    print(args)    # tuple
    print(kwargs)  # dict

func(1, 2, 3, x=10, y=20)

👉 결과  
- args → (1, 2, 3)  
- kwargs → {'x': 10, 'y': 20}
```

```python
def func(a, b, /, c, d=10, *args, e, f=20, **kwargs):
    pass

func(1, 2, 3, 4, 5, 6, e=7, x=100)

👉 결과  
a, b = 1 2
c, d = 3 4
args = (5, 6)
e, f = 7 20
kwargs = {'x': 100}
```

## 3.2 ppt 주요 예제
<img width="229" height="139" alt="image" src="https://github.com/user-attachments/assets/61570e3a-184a-4223-b389-ae2cb8d7c51e" />

---
### 다양한 return, 출력 방식
<img width="199" height="149" alt="image" src="https://github.com/user-attachments/assets/f870dfc4-280f-4ea7-9e4e-597c337d4d2a" />

<img width="173" height="103" alt="image" src="https://github.com/user-attachments/assets/c091018b-a761-4abe-b7d0-00daf6c8f673" />

---
### main의 사용
<img width="281" height="185" alt="image" src="https://github.com/user-attachments/assets/400b68bd-a70f-4852-8070-d917f12e08f5" />

<img width="168" height="245" alt="image" src="https://github.com/user-attachments/assets/47708e78-4255-4ee0-a886-42cfdcb1f376" />


