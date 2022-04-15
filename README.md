# PYTHON 빅데이터

## 1.urllib 패키지

파이썬 표준 라이브러리

    urllib.request — URL 문자열을 가지고 요청 기능 제공
    urllib.response — urllib 모듈에 의해 사용되는 응답 기능 관련 클래스들 제공
    urllib.parse — URL 문자열을 파싱하여 해석하는 기능 제공
    urllib.error — urllib.request에 의해 발생하는 예외 클래스들 제공
    urllib.robotparser — robots.txt 파일을 구문 분석하는 기능 제공

urllib.request 모듈

  urlopen- http.client.HTTPResponse 반환
  
  ***
http.client.HTTPResponse 클래스

    HTTPResponse.read([amt])
    HTTPResponse.readinto(b)
    HTTPResponse.getheader(name, default=None)
    HTTPResponse.getheaders()
    HTTPResponse.msg
    HTTPResponse.version
    HTTPResponse.status
    HTTPResponse.reason
    HTTPResponse.closed
