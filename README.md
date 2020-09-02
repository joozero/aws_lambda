# aws_lambda
* 서버를 프로비저닝하거나 관리할 필요 없이 코드를 실행할 수 있는 서비스
* 사용한 컴퓨팅 시간에 대해서만 비용 지불

## AWS Lambda Examples

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


* * * 
### S3 트리거를 이용한 서버리스 이미지 리사이즈 
1. S3 버킷 생성
<pre>
   전세계적으로 유일한 이름 필요
   예: {your_name}-transformed-images
</pre>
2. AWS Lambda > Functions 생성 클릭, AWS SAR(Serverless App Repository)에서 **resize** 검색 후, resize 애플리케이션 배포 

<img width="1229" alt="Screen Shot 2020-09-02 at 10 32 54 PM" src="https://user-images.githubusercontent.com/59524380/91990121-5239ec00-ed6c-11ea-9a05-d270f3178172.png">

3. 애플리케이션 이름 입력 후, 1번에서 생성한 S3 버킷명을 destBucket에 입력

sourceBucket에는 리사이징할 이미지를 저장할 버킷명을 입력(단, sourceBucket은 SAR를 통해 자동으로 생성되는 버킷)

![Screen Shot 2020-09-02 at 10 40 09 PM](https://user-images.githubusercontent.com/59524380/91991021-5f0b0f80-ed6d-11ea-93eb-c24c6af8157c.png)

4. AWS Lambda > Functions 생성 클릭, AWS SAR에서 **uploader** 검색 후, uploader 애플리케이션 배포 

![Screen Shot 2020-09-02 at 11 26 39 PM](https://user-images.githubusercontent.com/59524380/91997752-6504ee80-ed75-11ea-913b-d8dc70f6638f.png)

5. 애플리케이션 이름 입력 후, 3번 작업(sourceBucket)을 통해 생성된 버킷명을 입력

![Screen Shot 2020-09-02 at 11 27 56 PM](https://user-images.githubusercontent.com/59524380/91997845-79e18200-ed75-11ea-8f67-e7bf98501e95.png)

6. 배포 후, AWS Lambda > Applications를 확인하면 선택한 애플리케이션이 배포된 것을 확인할 수 있음

그리고 Functions 메뉴에서 **uploader** 함수를 클릭하면 배포한 Lambda 함수는 API Gateway에 의해 트리거되는 함수임을 파악할 수 있음

![Screen Shot 2020-09-02 at 11 29 27 PM](https://user-images.githubusercontent.com/59524380/91997991-a6959980-ed75-11ea-8419-fde47699f7c0.png)

<img width="1264" alt="Screen Shot 2020-09-02 at 11 30 33 PM" src="https://user-images.githubusercontent.com/59524380/91998052-bad99680-ed75-11ea-9074-f36d003514e8.png">

7. API Gateway 콘솔 > API Gateway 목록에서 serverlessrepo로 시작되는 API Gateway 선택

8. 사이드바 메뉴에서 settings 항목에서 Binary Media Types 항목에 \*/* 값이 있는지 확인 

9. API를 배포하여 외부에서 접근이 가능하도록 설정

![Screen Shot 2020-09-02 at 11 47 37 PM](https://user-images.githubusercontent.com/59524380/91998836-b19cf980-ed76-11ea-8968-53b8ec0900f0.png)

10. API를 Prod 환경에 배포

![Screen Shot 2020-09-02 at 11 48 50 PM](https://user-images.githubusercontent.com/59524380/91998983-db562080-ed76-11ea-931b-66474657312c.png)

11. 배포된 API URL 복사

![Screen Shot 2020-09-02 at 11 50 32 PM](https://user-images.githubusercontent.com/59524380/91999203-19534480-ed77-11ea-8b79-c49e7020b0a8.png)

12. 복사된 URL로 이동하면 아래의 화면과 같은 페이지가 나오고 JPG 이미지 파일을 드래그하여 이동

<img width="325" alt="Screen Shot 2020-09-02 at 11 52 19 PM" src="https://user-images.githubusercontent.com/59524380/91999444-57e8ff00-ed77-11ea-9883-099bcbdfd260.png">

13. Source S3 버킷에 가면 드래그한 파일이 저장되고 처음 1번에서 생성한 버킷에 가면 리사이징된 파일이 저장된 것을 확인

14. API 콘솔을 통해, GET 및 POST 요청시, 실행되는 Lambda 함수를 확인

