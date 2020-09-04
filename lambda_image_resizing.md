### S3 트리거를 이용한 서버리스 이미지 리사이즈 
1. S3 버킷 생성을 생성합니다.
<pre>
   전세계적으로 유일한 이름 필요
   예: {your_name}-transformed-images
</pre>
2. AWS Lambda > Functions 생성 클릭, AWS SAR(Serverless App Repository)에서 **resize** 검색 후, resize 애플리케이션 배포합니다.

<img width="1229" alt="Screen Shot 2020-09-02 at 10 32 54 PM" src="https://user-images.githubusercontent.com/59524380/91990121-5239ec00-ed6c-11ea-9a05-d270f3178172.png">

3. 애플리케이션 이름 입력 후, 1번에서 생성한 S3 버킷명을 destBucket에 입력합니다.

sourceBucket에는 리사이징할 이미지를 저장할 버킷명을 입력합니다(단, sourceBucket은 SAR를 통해 자동으로 생성되는 버킷)

![Screen Shot 2020-09-02 at 10 40 09 PM](https://user-images.githubusercontent.com/59524380/91991021-5f0b0f80-ed6d-11ea-93eb-c24c6af8157c.png)

4. AWS Lambda > Functions 생성 클릭, AWS SAR에서 **uploader** 검색 후, uploader 애플리케이션 배포합니다.

![Screen Shot 2020-09-02 at 11 26 39 PM](https://user-images.githubusercontent.com/59524380/91997752-6504ee80-ed75-11ea-913b-d8dc70f6638f.png)

5. 애플리케이션 이름 입력 후, 3번 작업(sourceBucket)을 통해 생성된 버킷명을 입력합니다.

![Screen Shot 2020-09-02 at 11 27 56 PM](https://user-images.githubusercontent.com/59524380/91997845-79e18200-ed75-11ea-8f67-e7bf98501e95.png)

6. 배포 후, AWS Lambda > Applications를 확인하면 선택한 애플리케이션이 배포된 것을 확인할 수 있습니다.

그리고 Functions 메뉴에서 **uploader** 함수를 클릭하면 배포한 Lambda 함수는 API Gateway에 의해 트리거되는 함수임을 파악할 수 있습니다. 

![Screen Shot 2020-09-02 at 11 29 27 PM](https://user-images.githubusercontent.com/59524380/91997991-a6959980-ed75-11ea-8419-fde47699f7c0.png)

<img width="1264" alt="Screen Shot 2020-09-02 at 11 30 33 PM" src="https://user-images.githubusercontent.com/59524380/91998052-bad99680-ed75-11ea-9074-f36d003514e8.png">

7. API Gateway 콘솔 > API Gateway 목록에서 serverlessrepo로 시작되는 API Gateway 선택합니다.

8. 사이드바 메뉴에서 settings 항목에서 Binary Media Types 항목에 \*/* 값이 있는지 확인합니다. 

9. API를 배포하여 외부에서 접근이 가능하도록 설정합니다.

![Screen Shot 2020-09-02 at 11 47 37 PM](https://user-images.githubusercontent.com/59524380/91998836-b19cf980-ed76-11ea-8968-53b8ec0900f0.png)

10. API를 Prod 환경에 배포합니다.

![Screen Shot 2020-09-02 at 11 48 50 PM](https://user-images.githubusercontent.com/59524380/91998983-db562080-ed76-11ea-931b-66474657312c.png)

11. 배포된 API URL 복사합니다.

![Screen Shot 2020-09-02 at 11 50 32 PM](https://user-images.githubusercontent.com/59524380/91999203-19534480-ed77-11ea-8b79-c49e7020b0a8.png)

12. 복사된 URL로 이동하면 아래의 화면과 같은 페이지가 나오고, JPG 이미지 파일을 드래그하여 이동합니다.

<img width="325" alt="Screen Shot 2020-09-02 at 11 52 19 PM" src="https://user-images.githubusercontent.com/59524380/91999444-57e8ff00-ed77-11ea-9883-099bcbdfd260.png">

13. Source S3 버킷에 가면 드래그한 파일이 저장되고 처음 1번에서 생성한 버킷에 가면 리사이징된 파일이 저장된 것을 확인합니다.

14. API 콘솔을 통해, GET 및 POST 요청시, 실행되는 Lambda 함수를 확인합니다.
![Screen Shot 2020-09-02 at 11 57 54 PM](https://user-images.githubusercontent.com/59524380/92000128-1f95f080-ed78-11ea-8cd9-f58a78fdaf34.png)

15. 해당 함수를 클릭하면 API Gateway를 통해, URL로 접근할 때, 실행되는 소스 코드를 확인할 수 있습니다. 



