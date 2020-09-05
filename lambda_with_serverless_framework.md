### serverless framework로 lambda 구성하기 
serverless는 lambda를 개발하고 aws 배포까지 손쉽게 할 수 있도록 도와주는 프레임 워크입니다.
<pre>
> npm i -g serverless
> sls --version
</pre>

<pre>
> serverless config credentials --provider aws --key [access_key_id] --secret [secret_access_key]
> sls create -t # 에러 발생과 함께 아래에 만들 수 있는 템플릿 종류 나열 됨
> sls create -t aws-python3 web-crawling-serverless # 템플릿 목록 생성할 폴더 명
</pre>

![Screen Shot 2020-09-05 at 8 38 19 PM](https://user-images.githubusercontent.com/59524380/92304316-e5b32d00-efb7-11ea-988f-fba858068404.png)

web-crawling-serverless 경로에 **handler.py** 및 **serverless.yaml** 파일이 생성된 것을 확인할 수 있습니다.<br/>
아래의 명령어를 통해, serverless를 통하여 함수가 잘 작동하는지 확인할 수 있습니다.<br/>
이때, **invoke** 명령어를 사용합니다. 
<pre>
> serverless invoke local --function hello # 로컬에서 함수 테스트 가능 
</pre>

serverless.yaml 파일 수정을 합니다.
아래의 입력을 통해 stage(배포 상태) 및 region을 설정하고, API Gateway와 연결할 수 있습니다.
<pre>
provider:
  name: aws
  runtime: python3.8
  stage: dev
  region: ap-northeast-2

functions:
  hello:
    handler: handler.hello
    events: 
      - http:
          path: api/test
          method: get
</pre>

함수를 배포할 때는 **sls deploy** 명령어를 사용합니다.
<pre>
sls deploy
</pre>

생성 과정에서 나타는 endpoint를 통해 API 요청을 보내면 결과 값을 확인할 수 있습니다.<br/>
AWS lambda 콘솔 창에서도 생성한 lambda를 확인할 수 있습니다. 
