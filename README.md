# aws_lambda
* 서버를 프로비저닝하거나 관리할 필요 없이 코드를 실행할 수 있는 서비스
* 사용한 컴퓨팅 시간에 대해서만 비용 지불
* AWS Lambda Quotas
AWS Lambda의 할당량의 경우, 주기적으로 개선되고 있기에 아래의 링크에서 확인하는 것이 보다 정확합니다.<br/>
참고 자료: https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/gettingstarted-limits.html
* 각 파일에 lambda와 관련된 내용이 기술되어 있습니다. 

* * *

### CloudWatch Event와 Lambda를 이용한 자동화
AWS 리소스 또는 사용자의 애플리케이션에 상태 변경이 발생했을 때, Event를 **CloudWatch Event**에 보낼 수 있습니다.
<pre>
사용자는 CloudWatch Event에 규칙을 생성하여 특정 이벤트가 발생했을 경우, 후속 작업을 수행할 수 있습니다.

CloudWatch Event Rule
- 생성한 규칙과 일치한 이벤트가 발생할 경우, 후속 작업을 Lambda를 이용하여 자동화할 수 있습니다.
- 예: 미션 크리티컬한 EC2 인스턴스가 Stop될 경우, 운영자 개입 없이 Lambda를 이용하여 자동으로 시작시키는 프로세스
</pre>

1. **Lambda**가 EC2를 실행할 수 있는 **IAM 역할** 생성
2. EC2를 시작하는 Lambda 생성
3. **CloudWatch Event**에서 EC2가 중단되는 경우에 실행되는 규칙 생성
4. 테스트 인스턴스 생성 후, 인스턴스 상태를 stop으로 변경 > 인스턴스의 재시작 확인
5. **CloudWatch Logs**를 통해, Lambda의 수행 확인 및 실행 시간 확인 
