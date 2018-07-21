# 크롤링3

### 웹크롤링 과제점검

* html 문서에서 가장 첫번째 테이블을 데이터프레임으로 가져오기

  ```
  df = pd.read_html(url,flavor='html5lib')[0]
  ```

* 앞뒤 공백제거

  ```
  text = "    aaa b cc ddddd   "
  print(text.strip())
  ```

  > aaa b cc ddddd

* 중간에 있는 공백 제거

  ```
  text.replace('\n', '').replace('\r', '')
  ```

* 실무에서 큰 프로젝트일수록 프로젝트가 망하거나 중단되는 경우가 많음. 잘 망하려면 중요한 것은 해놓고 망하는 것이다..(?) 

* 한글 -> 데이터타입을 컴퓨터가 인식할 수 있는 것으로 인식

* 문장 옆에 주석을 달때 두칸을 띄워줌

* 웹크롤러를 하나 만들면 내가 아무것도 안해도 매일 자동으로 크롤이 되어 좋다..

  * 게시글 올라올때마다 pdf박제, 소스다운로드. 한달 후에 만약 삭제되었으면 수상하다해서 보관함
  * 박제된채로 남아있는 게시물들은 상당수가 법적으로 문제가 있는 게시물일 수 있음. 따로 보관해서 나중에 수사기관에 넘긴다던가 함

## CSS 셀렉트

* select_one(태그이름)처럼 보이지만, select_one() <- 인자는 일종의 문법이다. 

  ```
  title = bs.select_one('title').text
  ```

### CSS 문법

* 비슷한 속성끼리 묶을때는 class로

* 클래스찾기 `.class`

  ```
  .classname {}
  ```

* id찾기 `#id`

  ```
  #idname {}
  ```

* p이면서 highlight 클래스가 있는 요소를 모두 찾아줌

  ```
  p.hightlight {}
  ```

* ul 혹은 ul의 자식이면서 hightlight 클래스인것

  ```
  ul .hightlight {}
  ```

* ul중에 highlight 클래스인것

  ```
  ul.highlight {}
  ```

* ul 혹은 ul의 자식중 li 이면서 highlight 클래스인것

  ```
  ul li.highlight {}
  ```

-> 공백이 없으면 해당 element들 중 해당 속성들

-> 공백이 있으면 본인과 자식을 포함하는 element들 중 해당 속성들을 불러옴

* 자식 selector `>`

  ```
  body > .highlight {}  
  ```

  * body의 바로 밑에 자식(직계자식) 중 highlight 클래스인것
  * body의 자식의 자식중 hightlight 클래스인것은 해당 안됨
  * 

* goodsList 클래스와 goodsList_list 클래스를 둘다 가진 div태그

  ```
  <div class="goodsList goodsList_list">
  ```

  * goodsList 클래스에도 포함되고 goodsList_list 클래스에도 포함된다

## Beautiful Soup 실습

* Yes24 사이트에서 '파이썬'으로 검색했을때 나온 결과 중

* div의 클래스가 goodsList인 것의 하위 자식중 p의 클래스가 goods_name인 것의 anchor 태그에서 strong 안에있는 text 추출하기 => 책 제목만 추출

  ```
  title_elements = bs.select('div.goodsList p.goods_name a strong')  # 도서이름만 추출하기
  titles = []
  for t in title_elements:
    titles.append(t.text)
  titles
  ```

  

