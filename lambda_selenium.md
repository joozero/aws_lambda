본 실습은 Selenium을 AWS Lambda Layers에 넣어 웹 크롤링을 수행하는 방식에 대해서 기술했습니다. 


### selenium이란?

Selenium이란 주로 웹 애플리케이션 자동화 테스트를 위한 프레임워크입니다.

우리가 웹 크롤링을 하다 보면 여러 가지 이슈와 직면하게 됩니다.<br/>
예를 들어, 웹 사이트가 로그인을 요구하거나 프로그램을 통한 접근을 허용하지 않는 경우가 그 예입니다.

그럴 때는 단순히 **requests** 라이브러리만으로는 원하는 작업을 수행할 수 없습니다.<br/>
이때 사용할 수 있는 방법이 selenium을 이용하는 것입니다.<br/>
selenium은 실제 웹 브라우저가 동작하기 때문에 JS로 렌더링이 완료된 후의 DOM 결과물에 대한 접근이 가능합니다.

1. pip을 통해 selenium을 설치합니다. 
<pre>
pip install selenium
</pre>

2. 웹 드라이버를 설치합니다.
주로 사용하는 브라우저 및 해당 브라우저의 버전을 확인한 다음 맞는 드라이버를 선택합니다.
크롬 웹 드라이버: https://chromedriver.chromium.org/

+ 추가 자료<br/>
**PhantomJS webdriver**는 cli 서버 환경에서 테스트를 진행할 경우 사용하기 적합합니다.

* * *

### AWS Lambda Layer

Lambda 함수는 추가 코드와 콘텐츠를 layer의 형태로 가져오도록 구성할 수 있습니다.<br/>
하나의 계층은 라이브러리, 사용자 지정 런타임 또는 그 외 종속성을 포함하는 ZIP 아카이브입니다.<br/>
Deployment Package에 라이브러리를 포함시킬 필요 없이 계층을 통해, 함수에서 라이브러리를 사용할 수 있습니다. 


참고 자료: https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/configuration-layers.html
