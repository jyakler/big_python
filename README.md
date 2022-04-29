# PYTHON 빅데이터

주피터 단축키
    
    ctrl + / : 선택한 영역 주석처리/해제
    ctrl + m : 셀 합치기
    ctrl + shift + - : 선택한 부분 기준으로 셀 나누기
    a : 셀 위로 새로운 셀 추가
    b : 셀 아래로 새로운 셀 추기
    dd : 셀 지우기

파이썬 정규표현식

![정규표현식](https://user-images.githubusercontent.com/49812691/164121211-c70b463b-52a2-4715-8f37-843bc10a7d21.PNG)


## 1.urllib 패키지

파이썬 표준 라이브러리

    urllib.request — URL 문자열을 가지고 요청 기능 제공
    urllib.response — urllib 모듈에 의해 사용되는 응답 기능 관련 클래스들 제공
    urllib.parse — URL 문자열을 파싱하여 해석하는 기능 제공
    urllib.error — urllib.request에 의해 발생하는 예외 클래스들 제공
    urllib.robotparser — robots.txt 파일을 구문 분석하는 기능 제공

__urllib.request 모듈__

      urlopen- http.client.HTTPResponse 반환
      urlretrieve(url,"경로") - url내용을 경로에 저장 
  
__urllib.parse 모듈__

▪ GET 방식 요청 : Query 문자열
    
   - Query 문자열을 포함하여 요청 ex)urllib.request.urlopen(url)  : url=http://.../..?etc
   
    urllib.request.urlopen(url).info().get_content_charset() : 해당 웹사이트의 meta charset를 알고 싶을때
    urllib.request.Request(url) - url을 get,post로 받아온 형태를 리턴
    urllib.request.urlopen(geturl) -get으로 받아온 geturl을 내용으로 추출한것을 리턴
    
▪ POST 방식 요청 : 요청 파라미터

   - 요청 바디안에 요청 파라미터를 포함 ex)urllib.request.urlopen(url, data) : data = data.encode(‘ascii’)

    urllib.parse.urlparse()
    urllib.parse.urlencode()
    urllib.parse.quote_plus() : 한글을 encode식으로 변환
    
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

## BeautifulSoup -정적

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

## selenium -동적
다양한 플랫폼과 언어를 지원하는 이용하는 브라우저 자동화 도구 모음

브라우저 띄우지 않기
    
    options = webdriver.ChromeOptions()
    options.add_argument('headless')
    options.add_argument('window-size=1920x1080') -사이즈 조절

from selenium.webdriver.common.by import By 

    driver = webdriver.Chrome('C:/Temp/chromedriver',options=옵션) - 웹드라이버 객체 생성 (옵션은 선택)
    driver.implicitly_wait(숫자) - 견고성 확보
    driver.get('http://www.google.com/ncr') -페이지 가져오기
    
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
    
실행

    #클릭
    driver.execute_script("arguments[0].click();", 개체)
    개체.click() 
    #스크롤
    driver.execute_script("var su = arguments[0]; var dom=document.querySelectorAll(); dom.scrollIntoView();", 개체)
    #캡처
    driver.get_screenshot_as_file('경로')


### pandas

    df.drop(행열이름 또는 배열, axis=0/1) - 행/열 삭제 0=행 1=열
    df.rename(index={기존인덱스:새로운인덱스},columns={기존이름:새이름}) - 이름바꾸기 - 원본에서도 저장할거면 inplace=True 해줘야함
    
    #행 선택
    df.loc[행인덱스이름,열] - 행만을 검색할때는 [[행인덱스이름]] 사용
    df.iloc[행인덱스,열]

    #열의 값을 인덱스로 바꾸기
    df.set_index(열이름',inplace=True)
    #인덱스 초기화
    df.reset_index()
    
    #정렬
    df.sort_index(ascending=True)
    df.sort_values(by='칼럼이름',ascending=True)
    
    #객수 확인
    df.count() - 열의 데이터 개수 확인
    df['열이름'].value_counts() - 열이름 열의 고유 값의 개수 확인

    #plot
    df.plot() / series.plot()- 그래프 작성 (바그래프일경우  matplotlib보다 이거쓰는게 편함)
    plot.set_xticklabels()- x축이름 변경
    
    #결측치 제거
    df.dropna(axis=0,thresh=숫자) - na값이 숫자 이상 포함되어있는 axis=0(행) axis=1(열) 제거
    df.fillna(method=) -결측치를 무엇으로 채울지
    
    #중복값 찾기
    df.duplicated() -중복되있는 행은 true로 반환
    df.drop_duplicates(subset=[]) - 중복값 제거 (subset기준으로 중복행 제거)
    
    #자료형 변환
    df.astype(자료형)
    
    #데이터 분할
    result=pd.cut(x=df,
                  bins=[경계값리스트],
                  labels=[bin 이름],
                  include_lowest=True) - 첫 경계값 포함
                  
    #더미 변수
    pd.get_dummies(df) - 범주형 데이터를 더미변수로 변환
    
    #날짜
    타임스탬프.to_period(freq=단위) - timestamp 를 period로 변환
    pd.date_range(시작날짜,periods=몇개,freq=단위,tz=시간대) - 배열형태의 시간데이터 만들기
    
    #함수 매핑
    series.apply(매핑함수) - 시리즈에 함수 적용
    df.applymap(함수) - 데이터프레임에 함수 적용
    df.apply(함수,axis=0) -axis=0(열) axis=1(행) 
    df.pipe(함수) - 데이터프레임 !객체! 에 함수전달
   #### map
   ![map](https://user-images.githubusercontent.com/49812691/165461456-1a432a3c-7b9d-4e01-9b28-cadbb5fccc3c.jpg)
   #### applymap
   ![applymap](https://user-images.githubusercontent.com/49812691/165461577-cf436cb8-b7fa-4fc7-81bc-9fdd72dd1fc0.jpg)
   #### apply
   ![apply](https://user-images.githubusercontent.com/49812691/165461595-744a05c6-20b2-4cfe-aac0-0edb67adac7c.jpg)

    #그룹화
    df.groupby(기준이되는열)- 열기준으로 그룹화
    
    #데이터 집계
    group객체.mean()
    max/min/sum/count/size/var/std/describe/info/first/last
    agg(사용자정의함수) - 사용자 정의함수를 적용하고싶을때 사용 -집계연산
    transform()
    filter(조건) - 조건이 참인 그룹만 남김
    apply()- 매핑함수를 개별원소에 일대일로 매핑

    #검색
    group객체.xs(찾을이름, level=칼럼이름) - 칼럼에서 찾을이름을 검색함
    
   #### pivot
       pdf1 = pd.pivot_table(df,              # 피벗할 데이터프레임
                         index='',    # 행 위치에 들어갈 열
                         columns='',    # 열 위치에 들어갈 열
                         values='',     # 데이터로 사용할 열
                         aggfunc='')   # 데이터 집계 함수(디폴트)
                     
   ![pivot_table](https://user-images.githubusercontent.com/49812691/165674321-6b6acf92-e8e6-4e3d-aeda-a9c85a3e2348.jpg)

   
### numpy

    count,경계값리스트 = np.histogram(df,bins=3) - df를 3개의 bins으로 구분할 경계값의 리스트 구하기(3개를 나눠서 4개의 값이 나옴)
    np.array() / np.mat()
    np.min() / np.max()  - axis=0 (열기준) axis=1(행기준)
    
    
### matplotlib - 시각화 라이브러리 
   한글폰트 등록예시
   
    import sys                                               ## 파이썬 엔진에 대한 정보를 관리하는 모듈을 사용한다. 
    from matplotlib import font_manager, rc                  ## 폰트를 관리하는 함수와 설정 함수를 사용한다. 

    if sys.platform  == 'darwin':                             ## MAC OS의 이름을 확인한다.
        path = '.....'  
    elif sys.platform == 'win32':                             ## Windows 이름을 확인한다.
        path = "font/MaplestoryBold.ttf"
    else:
        print('Unknown system... sorry~~~~') 
    
    font_name = font_manager.FontProperties(fname=path).get_name()        ##  폰트가 있는지를 확인한다. 
    rc('font', family=font_name)                                          ## 한글 폰트를 시각화 환경에 세팅한다. 
    plt.rcParams['axes.unicode_minus'] = False 

  치트시트
  
![제목 없음](https://user-images.githubusercontent.com/49812691/165009322-20914cb8-7e60-4932-8af4-b16e7bcb01eb.png)

### plt.plot(*args, scalex=True, scaley=True, data=None, **kwargs)
#### plot([x], y, [fmt], *, data=None, **kwargs)
#### plot([x], y, [fmt], [x2], y2, [fmt2], ..., **kwargs)
<span style="color:red">fmt = '[marker][line][color]'</span>
##### plot(x, y)        # plot x and y using default line style and color
##### plot(x, y, 'bo')  # plot x and y using blue circle markers
##### plot(y)           # plot y using x as index array 0..N-1
##### plot(y, 'r+')     # ditto, but with red plusses

    matplotlib.pyplot.savefig('경로') - plot저장하기
    matplotlib.pyplot.plot(인덱스,값) - plot
    

![mpl7](https://user-images.githubusercontent.com/49812691/165020010-bee49789-e0a1-4cb1-aa29-9218b540095c.png)

## folium - 지도를 다루는 라이브러리 (leaflet.js기반)

        map=folium.Map(location=[],zoom_start=숫자,tiles='') - 지도 만들기
        display(map) - 지도 표시
        map.save(경로.html) - 지도를 파일로 저장 
        folium.Marker([위도,경도],popup=팝업).add_to(지도) - '지도'에 마커 추가 popup은 클릭했을때 뭐가 뜨게할건지 
        folium.CircleMarker([위도,경도],radius=,color=,fill=True,fill_color=,fill_opacity=,popup=).add_to() - 원 마커 추가 
        
        folium.Choropleth(geo_data=,    # 지도 경계
                 data = ,      # 표시하려는 데이터
                 columns = ,  # [지도 데이터와 매핑할 데이터, 시각화 하고려는 데이터]
                 fill_color='YlOrRd', fill_opacity=0.7, line_opacity=0.3, #색 지정
                 threshold_scale=[범위], #범주 스케일 지정             
                 key_on='', # 지도 데이터파일에서 데이터파일과 매핑할 값
                 legend_name=, # 칼라 범주 이름
                 ).add_to(map) #map 에다가 해당 choropleth를 추가
                 
        fmap=folium.Choropleth()...
        fmap.geojson.zoom_on_click = False # 클릭 할때 줌인 안되게
        fmap.geojson.add_child(
             folium.features.GeoJsonTooltip(['name'],labels=False) #마우서 호버하였을때 정보 나오게
             folium.features.GeoJsonPopup(['name'],labels=False) #마우스 클릭시 팝업 나오게
        )

## seaborn

    heatmap() - 히트맵
    중요! relplot()
        https://seaborn.pydata.org/generated/seaborn.relplot.html
    중요! catplot(x,y,hue,data,kind='',...)
        https://seaborn.pydata.org/generated/seaborn.catplot.html#seaborn.catplot
    
## Image   (PIL 패키지)

    Image.open('사진.JPG') - 이미지 파일 읽어오기

# 문자열

![string1](https://user-images.githubusercontent.com/49812691/165894898-d0a6a651-2c7e-4785-8c11-9dc31269caea.jpg)

