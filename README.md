# aws_lambda
* 서버를 프로비저닝하거나 관리할 필요 없이 코드를 실행할 수 있는 서비스
* 사용한 컴퓨팅 시간에 대해서만 비용 지불

## AWS Lambda Examples

### CloudWatch Event와 Lambda를 이용한 자동화

AWS 리소스 또는 사용자의 애플리케이션에 상태 변경이 발생했을 때, Event를 **CloudWatch Event**에 보낼 수 있습니다.

사용자는 CloudWatch Event에 규칙을 생성하여 특정 이벤트가 발생했을 경우, 후속 작업을 수행할 수 있습니다.

Rule을 설정하여 해당 Rule과 일치한 Event가 발생할 경우, 후속 작업을 Lambda를 이용하여 자동화 할 수 있습니다. 


### S3 트리거를 이용한 서버리스 이미지 리사이즈 
