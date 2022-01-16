# 03장. 프로그램의 구조를 쌓는다! 제어문

집을 지을 때 나무, 돌, 시멘트 등은 재료가 되고, 철근은 집의 뼈대가 된다.

프로그램을 만드는 것도 집 짓기와 매우 비슷한 면이 있다.

나무, 돌, 시멘트와 같은 재료는 자료형이 되고, 집의 뼈대를 이루는 철근은 제어문에 해당한다.

3장에서는 자료형을 바탕으로 제어문을 이용해서 프로그램의 구조를 만든다.





## 03-2. while문

### 1. while문의 기본 구조

- while문의 기본 구조

```python
while <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
```

**while문은 조건문이 참인 동안에 while문 아래의 문장이 반복해서 수행됨**





`"10번 찍어 안 넘어가는 나무 없다."`

```python
>>> treeHit = 0
>>> while treeHit < 10:
        treeHit = treeHit + 1
        print("나무를 %d번 찍었습니다." % treeHit)
        if treeHit == 10:
            print("나무 넘어갑니다.")
나무를 1번 찍었습니다.
나무를 2번 찍었습니다.
나무를 3번 찍었습니다.
나무를 4번 찍었습니다.
나무를 5번 찍었습니다.
나무를 6번 찍었습니다.
나무를 7번 찍었습니다.
나무를 8번 찍었습니다.
나무를 9번 찍었습니다.
나무를 10번 찍었습니다.
나무 넘어갑니다.            
```

위 예에서 조건문은 `treeHit < 10` 이므로 treeHit가 10보다 작은 동안에 while문 안의 문장을 계속 수행함

제일 먼저 `treeHit = treeHit + 1` 로 treeHit 값이 계속해서 1씩 증가하고, 나무를 treeHit번만큼 찍었음을 알리는 문장을 출력함

treeHit가 10이 되면 "나무 넘어갑니다."라는 문장을 출력함

그 후에는 `treeHit < 10` 조건문이 거짓이 되므로 while문을 빠져나가게 됨







### 2. while문 만들기

- 여러 가지 선택지 중 하나를 선택해서 입력받는 예제

먼저 여러 줄짜리 문자열을 입력

```python
>>> prompt = """
    1. Add
    2. Del
    3. List
    4. Quit
    Enter number: """
```

number 변수에 0을 입력해놓음. 이렇게 변수를 먼저 설정해놓지 않으면 다음에 나올 while문의 조건문인 `number != 4`에서 변수가 존재하지 않는다는 오류가 발생함

```python
>>> number = 0
>>> while number != 4:
        print(prompt)
        number = int(input())
    1. Add
    2. Del
    3. List
    4. Quit
    Enter number:       
```

number가 4가 아닌 동안 prompt를 출력하고 사용자로부터 번호를 입력받음

사용자가 4를 입력하지 않으면 계속해서 prompt를 출력

```python
Enter number: 
1

1. Add
2. Del
3. List
4. Quit
Enter number: 
```

사용자가 4를 입력하면 조건문이 거짓이 되어 while문을 빠져나가게 됨

```python
Enter number: 
4
```







### 3. while문 강제로 빠져나가기

while문은 조건문이 참인 동안 계속해서 while문 안의 내용을 반복적으로 수행함

**강제로 while문을 빠져나가고 싶을 때 break문을 사용함**





(예시) 커피 자판기

![image-20210915225244258](/Users/moominie/Library/Application Support/typora-user-images/image-20210915225244258.png)

```python
>>> coffee = 10
>>> money = 300
>>> while money:
        print("돈을 받았으니 커피를 줍니다.")
        coffee = coffee - 1
        print("남은 커피의 양은 %d개입니다." % coffee)
        if coffee == 0:
            print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
            break
```

money가 300으로 고정되어 있으므로 `while money:` 에서 조건문인 money는 항상 True(참)이 되어 무한히 반복되는 무한 루프를 돌게 됨

while문의 내용을 한 번 수행할 때마다 `coffee = coffee - 1` 에 의해서 coffee의 개수가 1개씩 줄어들다가 만약 coffee가 0이 되면 `if coffee == 0:` 문장이 참이 되어 `"커피가 다 떨어졌습니다. 판매를 중지합니다."` 가 수행되고 break문이 호출되어 while문을 빠져나가게 됨





실제 자판기의 작동 과정과 비슷하게 만들기

```python
>>> coffee = 10
>>> while True:
        money = int(input("돈을 넣어 주세요: "))
        if money == 300:
            print("커피를 줍니다.")
            coffee = coffee - 1
        elif money > 300:
            print("거스름돈 %d를 주고 커피를 줍니다." % (money - 300))
            coffee = coffee - 1
        else:
            print("돈을 다시 돌려주고 커피를 주지 않습니다.")
            print("남은 커피의 양은 %d개입니다." % coffee)
        if coffee == 0:
            print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
            break
```







### 4.while문의 맨 처음으로 돌아가기

while문 안의 문장을 수행할 때 입력 조건을 검사해서 조건에 맞지 않으면 while문을 빠져나감

이때, **while문을 빠져나가지 않고 while문의 맨 처음(조건문)으로 다시 돌아가게 만들고 싶은 경우 continue문을 사용함**





1부터 10까지의 숫자 중에서 홀수만 출력하기

```python
>>> a = 0
>>> while a < 10
        a = a + 1
        if a % 2 == 0: continue
        print(a)
1
3
5
7
9        
```

a가 10보다 작은 동안 a는 1만큼씩 계속 증가함

`if a % 2 == 0:` 에서 a를 2로 나눈 나머지가 0인 경우, 즉, a가 짝수이면 continue문장을 수행함

continue문은 while문의 맨 처음인 조건문 `a < 10` 으로 돌아가게 하는 명령어이므로, a가 짝수일 때에는 `print(a)` 문장은 수행되지 않음

따라서 a가 1부터 10까지의 숫자 중에서 홀수일 때에만 출력됨







### 4. while문의 맨 처음으로 돌아가기

### 5. 무한 루프

> **무한 루프(Loop)**
>
> 무한히 반복한다





- 무한 루프의 기본 형태

```python
while True:
    수행할 문장1
    수행할 문장2
    ...
```

while문의 조건문이 True이므로 항상 참이 되어 while문 안의 문장들이 무한하게 수행됨





```python
>>> while True:
        print("무한 루프")
무한 루프
무한 루프
무한 루프
...
```

