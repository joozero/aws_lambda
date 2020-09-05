### serverless framework로 lambda 구성하기 
serverless는 lambda를 개발하고 aws 배포까지 손쉽게 할 수 있도록 도와주는 프레임 워크입니다.
<pre>
> npm i -g serverless
> sls --version
</pre>

<pre>
> serverless config credentials --provider aws --key [access_key_id] --secret [secret_access_key]
> sls create -t # 에러 발생과 함께 아래에 만들 수 있는 템플릿 종류 나열 됨
> sls create -t aws-python3 web-crawling-serverless
> serverless invoke local --function hello # 로컬에서 함수 테스트 가능 
</pre>
