# Week9

## 이번 주 큰 흐름

- 시험 확인


# 문제 1
```python
def main():
    print("Hello,World")
if __name__ =='__main__':
    main()
```


# 문제 2 
parameter를 통해 하나의 str 객체를 전달 받아 이를 총 3회 출력하는 함수를 작성하시오.

```python
# 내 답안
def give_par(name):
    return name

for i in range(3):
    print(give_par("지현"))
```


```python
# 교수님 답안1
def print_str(para):
    tmp = para
    print(tmp)
    print(tmp)
    print(tmp)

    return # 혹은 안해도 됨

print_str("인자다.")
```

```python
# 교수님 답안2
def print_str(para):
    for _ in range(3):
        print(para)

    return # 혹은 안해도 됨

print_str("test.")
```

```python
# 교수님 답안3
def print_str(para):
    cnt=0
    while cnt < 3:
        print(para)
        cnt+=1

    return # 혹은 안해도 됨

print_str("qqqq.")
```



# 문제 3
구구단을 출력하는 파이썬 모듈을 작성. 사용자로부터 출력할 구구단을 입력받고, 해당 단을 출력하는 형태로 작성. 입력, 처리, 출력을 담당하는 함수를 각각 만들어야 함.

```python
dan = input("출력할 단?")
dan = int(dan)          # dan = int(input("출력할 단?")) 도 가능

for i in range(1,10):
    ret = dan * i 
    print(ret)  # print(f"{dan}*{i}={ret}")
```
