## BeautifulSoup
BeautifulSoup(뷰티풀솝)은 데이터를 추출하는데 필요한 기능이 들어있는 라이브러리 입니다.
* 반도체공장(모래) = BeautifulSoup(html)

뷰티풀솝은 텍스트를 단계별로 접근을 할 수 있게 데이터를 구조화 시켜줍니다.

## 라이브러리(library)
라이브러리(library)는 도서관이라는 뜻입니다. 책이 여러권 있는 곳이 도서관인데 여러가지 기능들이 있는 코드 묶음을 라이브러리라고 합니다.
* 많이 사용하는 기능들을 다른 사람 또는 회사가 만들어서 올려놓은 것입니다.
* 라이브러리는 import를 해서 사용 합니다.
* 내장 라이브러리와 외장 라이브러리가 있습니다.
* 내장 라이브러리는 import해서 사용하고 외장 라이브러리는 설치한 후 import해서 사용합니다.

## 라이브러리 설치 하는 방법
* Settings(Preferance) -> interpreter검색
* +를 누르고 설치하고 싶은 라이브러리 검색 ex)bs4, numpy 등   


###  BeautifulSoup 사용법
```python
from bs4 import BeautifulSoup
html_str = '<html><div>hello</div></html>'
bs_obj = BeautifulSoup(html_str, "html.parser")

print(bs_obj)
print(bs_obj.find("div"))
print(bs_obj.find("div").text)
```

결과
```text
<html><div>hello</div></html>
<div>hello</div>
hello
```

BeautifulSoup() 함수에 받은 데이터를 넣으면 텍스트 형식으로 된 데이터를 구조화 시켜서 우리가 데이터를 비교적 쉽게 뽑아 낼 수 있도록 오브젝트를 리턴합니다.

```html
<html><div>hello</div></html>
```
위 코드는 html형식의 문서를 가장 단순하게 만들어본 코드 입니다.

html.parser는 인터넷에 있는 대부분의 문서가 html로 되어 있기 때문에 "html.parser"를 사용합니다.


위 코드를 그냥 실행 하면 모듈이 없다는 에러가 납니다.
그래서 bs4를 설치 해야 합니다.

.find("div")이 부분이 가장 중요 합니다. html문서에서 가장 먼저 등장하는 div를 뽑으라는 명령입니다. 위 예제에서는 한개만 있기 때문에 바로 나오네요.

### 크롤링이란?
인터넷 주소로 서버에 데이터를 요청해서 받아오는 것(콘솔에 출력하는 것)
서버에 리퀘스트(request)를 보내서 서버가 준 response를 받는 것
* 라이브러리 : urlopen

### 파싱이란?
크롤링한 데이터에서 값을 뽑아내는 것
* 라이브러리:bs4 BeautifulSoup 뷰티풀솝

### 크롤링의 과정
1. 페이지를 불러온다.
    - 어떻게 불러올 것인가?
    - urllib.request를 써서 불러온다.
    - urlopen(url)을 쓴다.
2. 파싱을 한다.
    - BeautifulSoup으로 파싱한다.
    - 개발자 도구를 켜서 원하는 데이터가 있는 위치를 찾는다.


### 태그란?
html문서를 표현 할 때 쓰는 화면 구성을 하는 표시들.

문서에 있는 특정 부분에 꼬리표를 붙여준다는 뜻으로 tag라고 쓴다.
```html
<html>, <div>, <ul>, <li>, <a>, <span> 등이 있다.
```

### ul태그 뽑아내기
위 소스코드는 <div>태그를 뽑아내는 예제였습니다. 이 예제는 ul태그를 뽑아내는 예제 입니다.

모든 데이터는 태그 안에 들어있습니다.

예를 들면 뉴스 기사 들은 아래와 같이 데이터가 들어가 있습니다.

```html
<ul>
	<li>000가 000를 했다</li>
	<li>111가 222를 했다</li>
</ul>
```
웹에 표시되는 데이터는 태그로 감싸져 있습니다.

```json
[
	{"title":"000가 000를 했다"},
	{"title":"111가 222를 했다"}
]
```
이러한 리스트 구조와 비슷합니다. 이건 json이라고 하는데 뒤에 배웁니다. 모양이 비슷하기 때문에 넣어놓았습니다.

"""따옴표 3개로 감싸주면 변수에 여러줄을 넣을 수 있습니다.
```python
import bs4

html_str = """
<html>
    <body>
        <ul>
            <li>hello</li>
            <li>bye</li>
            <li>welcome</li>
        </ul>
    </body>
</html>
"""
bsObj = bs4.BeautifulSoup(html_str, "html.parser")

ul = bsObj.find("ul")
print(ul)

```

결과
```text
<ul>
<li>hello</li>
<li>bye</li>
<li>welcome</li>
</ul>
```


### li를 찾아내기
```python
import bs4

html_str = """
<html>
    <body>
        <ul>
            <li>hello</li>
            <li>bye</li>
            <li>welcome</li>
        </ul>
    </body>
</html>
"""

bs_obj = bs4.BeautifulSoup(html_str, "html.parser")

ul = bs_obj.find("ul")
li = ul.find("li")
print(li)
```
hello만 출력할려면 어떻게 해야 할까요?
ul.find("li")를 해주면 됩니다.

결과
```text
<li>hello</li>
```

### text속성 사용하기
```python
import bs4

html_str = """
<html>
    <body>
        <ul>
            <li>hello</li>
            <li>bye</li>
            <li>welcome</li>
        </ul>
    </body>
</html>
"""
bs_obj = bs4.BeautifulSoup(html_str, "html.parser")

ul = bs_obj.find("ul")
li = ul.find("li")
print(li.text)
```
결과
```text
hello
```

.text를 이용해 태그 안에 있는 내용을 뽑아낼 수 있습니다.


### class이용해서 세부사항 추출하기
class를 이용하면 같은 태그가 있을 때 특정 블럭을 선택해서 뽑아낼 수 있습니다.

```python
import bs4

html_str = """
<html>
    <body>
        <ul class="greet">
            <li>hello</li>
            <li>bye</li>
            <li>welcome</li>
        </ul>
        <ul class="reply">
            <li>ok</li>
            <li>no</li>
            <li>sure</li>
        </ul>
    </body>
</html>
"""

bs_obj = bs4.BeautifulSoup(html_str, "html.parser")

ul = bs_obj.find("ul", {"class":"reply"})
print(ul)
```

결과
```text
<ul class="reply">
<li>ok</li>
<li>no</li>
<li>sure</li>
</ul>
```
