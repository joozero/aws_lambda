### Lambda Layers란?

Lambda 함수는 추가 코드와 콘텐츠를 layer의 형태로 가져오도록 구성할 수 있습니다.<br/>
하나의 계층은 라이브러리, 사용자 지정 런타임 또는 그 외 종속성을 포함하는 **ZIP 아카이브**입니다.<br/>
Deployment Package에 라이브러리를 포함시킬 필요 없이 계층을 통해, 함수에서 라이브러리를 사용할 수 있습니다.<br/>

간략한 소개는 아래의 링크를 통해 확인할 수 있습니다.<br/>
https://aws.amazon.com/about-aws/whats-new/2018/11/aws-lambda-now-supports-custom-runtimes-and-layers/?nc1=h_ls

Lambda Layers의 경우, **압축 파일**이며, /opt 폴더에 압축 해제가 되는 것입니다.<br/>
즉, 압축 파일 하나를 /opt 경로에 풀어 준다는 개념으로 이해하면 됩니다. 




참고 자료: https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/configuration-layers.html
