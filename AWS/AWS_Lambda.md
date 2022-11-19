💻 [AWS] AWS Lambda
=================
# 💡 AWS Lambda
* Serverless
* 함수 호출 방식 : 요청이 있을 때만 코드가 실행되어 요청을 처리하고 종료
* 장점
    * 서버 관리 필요가 없음(보안 패치나 OS 업데이트 등)
    * 상대적으로 비용이 저렴
        * 항상 가동중인 서버와 달리 요청이 있을 때만 작동하기 때문에 사용자가 적은 새벽 시간대에 는 코드 실행이 되는 횟수가 줄어들기 때문에 비용이 절감됨

## 📌 Function
* 실행할 함수

## 📌 Layer
* 사용할 라이브러리 모음집

## 📌 Trigger
* API GateWay : 어떤 URL로 접속했을 때 Function을 실행할지 결정 가능
* S3 : 파일 업로드, 수정 등의 Event발생 시 Function 실행
* Eventbridge : 특정 이벤트 발생시 Function 실행

# 📌 Lambda 디버깅
* Function Code를 수정할 때 마다 새로운 Log Stream이 생성되며 그 곳에 로그가 작성됨
    * CloudWatchlogs 관련 권한들이 필요한 이유 되시겠다.

## 📌 Lambda 기본 코드
```python
# Function Name : lambda_handler(Reserved)
# Two Parameter (event, context)

def lambda_handler(event, context):
    print(event) # Log에 데이터를 찍어볼 수 있음.
    return event['left'] * event['right']
```

