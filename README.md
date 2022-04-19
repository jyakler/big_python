# PYTHON 빅데이터

주피터 단축키
    
    ctrl + / : 선택한 영역 주석처리/해제
    ctrl + m : 셀 합치기
    ctrl + shift + - : 선택한 부분 기준으로 셀 나누기
    a : 셀 위로 새로운 셀 추가
    b : 셀 아래로 새로운 셀 추기
    dd : 셀 지우기


## 1.urllib 패키지

파이썬 표준 라이브러리

    urllib.request — URL 문자열을 가지고 요청 기능 제공
    urllib.response — urllib 모듈에 의해 사용되는 응답 기능 관련 클래스들 제공
    urllib.parse — URL 문자열을 파싱하여 해석하는 기능 제공
    urllib.error — urllib.request에 의해 발생하는 예외 클래스들 제공
    urllib.robotparser — robots.txt 파일을 구문 분석하는 기능 제공

__urllib.request 모듈__

  urlopen- http.client.HTTPResponse 반환
  
__urllib.parse 모듈__

▪ GET 방식 요청 : Query 문자열
    
   - Query 문자열을 포함하여 요청 ex)urllib.request.urlopen(url)  : url=http://.../..?etc
   
    urllib.request.urlopen(url).info().get_content_charset() : 해당 웹사이트의 meta charset를 알고 싶을때

▪ POST 방식 요청 : 요청 파라미터

   - 요청 바디안에 요청 파라미터를 포함 ex)urllib.request.urlopen(url, data) : data = data.encode(‘ascii’)

    urllib.parse.urlparse()
    urllib.parse.urlencode()

  ***
http.client.HTTPResponse 클래스

    HTTPResponse.read([amt]) - 한글있을경우 decode해줘야함
    HTTPResponse.readinto(b)
    HTTPResponse.getheader(name, default=None)
    HTTPResponse.getheaders()
    HTTPResponse.msg
    HTTPResponse.version
    HTTPResponse.status
    HTTPResponse.reason
    HTTPResponse.closed

## reqeust 패키지
- 딕셔너리 형태로 데이터 전송
- 요청 방식(GET, POST)에 따라서 구현 방법이 달라짐
- request() 함수 호출시 요청 메소드(GET, POST)를 명시하여 요청

        requests.request('GET', url, **kwargs) - [ kwargs ] params – (선택적) 요청 시 전달할 Query 문자열을 지정
        requests.request(‘POST', url, **kwargs) - [ kwargs ] data – (선택적) 요청 시 바디에 담아서 전달할 요청 파라미터 (딕셔너리, 튜플리스트 형식, 바이트)
                                                    json – (선택적) 요청 시 바디에 담아서 전달할 JSON 타입의 객체
 - requests.models.Response  객체
 
 text
 
    ▪ 문자열 형식으로 응답 콘텐츠 추출
    ▪ 추출 시 사용되는 문자 셋은 'ISO-8859-1'이므로 'utf-8' 이나 'euc-kr' 문자 셋으로 작성된 콘텐츠 추출 시 한글이 깨지는 현상 발생
    ▪ 추출 전 응답되는 콘텐츠의 문자 셋 정보를 읽고 r.encoding = 'utf-8'와 같이 설정한 후 추출  (선 - encode 후 -text)

content

    ▪ 바이트열 형식으로 응답 콘텐츠 추출
    ▪ 응답 콘텐츠가 이미지와 같은 바이너리 형식인 경우 사용
    ▪ 한글이 들어간 문자열 형식인 경우 r.content.decode('utf-8')를 사용해서 디코드 해야 함  (선 - content 후 - decode)

## BeautifulSoup

    from bs4 import BeautifulSoup
    #해당 4가지중 하나로 파싱(Parse)해야함 - 다른 파서 이용해도됨
    bs = BeautifulSoup(html_doc, 'html.parser')
    bs = BeautifulSoup(html_doc, 'lxml')
    bs = BeautifulSoup(html_doc, 'lxml-xml')
    bs = BeautifulSoup(html_doc, 'html5lib')
    bs.태그명.태그명. ... 
    bs.태그명.string.strip() -앞뒤 공백 분리문자들 제거해서 보여줌(strip)
    
    find_all(name=None, attrs={}, recursive=True, text=None, limit=None, **kwargs) -bs4.element.ResultSet 객체 리턴
    find(name=None, attrs={}, recursive=True, text=None, **kwargs) - bs4.element.Tag 객체 리턴
    select(selector, namespaces=None, limit=None, **kwargs) - list 객체 리턴

### re
    
    re.compile("정규표현식")- 정규표현식으로 문자열 사용하고자할때 치환할때 

## selenium
다양한 플랫폼과 언어를 지원하는 이용하는 브라우저 자동화 도구 모음

from selenium.webdriver.common.by import By 

    driver = webdriver.Chrome('C:/Temp/chromedriver') - 웹드라이버 객체 생성
    driver.get('http://www.google.com/ncr', 시간) -페이지 가져오기
    
    #id찾기
    driver.find_element_by_id('')
    byId = driver.find_element(by=By.ID, value='')
    
    #class 찾기
    target = driver.find_element_by_class_name('')
    target = driver.find_element(By.CLASS_NAME, "")
    
    #태그명
    byTagName = driver.find_element_by_tag_name('h1') 
    byTagName = driver.find_element(By.TAG_NAME, 'h1')
    
    #링크 텍스트  - <a href="https://www.python.org/">파이썬 학습 사이트</a>
    byLinkText = driver.find_element_by_link_text('파이썬 학습 사이트')
    byLinkText = driver.find_element(By.LINK_TEXT, '파이썬 학습 사이트')
    byLinkText = driver.find_elements_by_partial_link_text('사이트') -부분
    byLinkText = driver.find_element(By.PARTIAL_LINK_TEXT, '사이트') -부분
    
    #css 선택자
    byCss1 = driver.find_element_by_css_selector('') 
    byCss1 = driver.find_element(By.CSS_SELECTOR, 'section>h2')
    
    #xpath
    byXpath1 = driver.find_element_by_xpath('//*[@id="f_subtitle"]')
    byXpath1 = driver.find_element(By.XPATH, '//*[@id="f_subtitle"]')


    # 태그명
    element.tag_name
    # 텍스트 형식의 콘텐츠
    element.text
    # 속성값
    element.get_attribute('속성명')
