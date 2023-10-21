Bash Syntax 정리
===================

### 정수형 변수 계산하기
* 괄호 한번 더 써서 묶어준다.
```sh
#!/bin/bash
current=123
target=$(($current+100))

echo $target
223
```

### 조건문
* 분기처리를 위한 조건문.

#### if
```sh
if [조건]; then
    # 이후 액션
fi
```
#### elif
```sh
if [조건1]; then
    # 조건1이 True일 경우
elif [조건2]; then
    # 조건2가 True일 경우
else
    # 조건1, 조건2 둘 다 해당 안되는 경우
fi
```

### 비교 연산자
두 가지 변수를 비교할 때, 왼쪽 기준.
* `-eq` (equal) : 같음 ( `==` )
* `-ne` (not equal) : 같지 않음 ( `!=` )
* `-gt` (greater than) : 크다 ( `>` )
* `-lt` (less than) : 작다 ( `<` )
* `-ge` (greater than or equal) : 크거나 같다 ( `>=` )
* `-le` (less than or equal) : 작거나 같다 ( `<=` )

### 논리 연산자
* `&&` : AND
* `||` : OR
* `!` : NOT
```sh
if [조건1] || [조건2]; then
    # 조건1, 조건2 중 하나라도 True인 경우
fi
```
```sh
if ! [조건]; then
    # 조건의 반대일 경우
fi
```