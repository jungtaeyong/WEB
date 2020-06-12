# HTML (Hyper Text Mark-up Language)

- 문서의 내용 이외에도 문서의 구조나 서식 등을 포함한다.

- DOM(Document Object Model) 구조
  
  - html을 루트로 head, body등 트리구조로 이루어짐
  
- 서버에서 보내오는 정적인 정보를 그대로 그려내는 것에 강하지만, 동적인 화면구성에 약함. 따라서 동적인 입력에 반응하는 것은 JS(AJAX 등)가 처리
  
  [HTML/CSS/JS 연습사이트](https://jsbin.com/?html,output)
  
  

## Index

- [태그](#태그)

- [폼](#폼)

- [시맨틱 태그](#시맨틱-태그)

- [검색 엔진 최적화(SEO)](#검색-엔진-최적화)



## 태그

| 태그명  | 내용                                                         |
| :-----: | ------------------------------------------------------------ |
|  html   | HTML DOM 구조의 루트격 태그. 보통 head와 body로 나뉨         |
|  head   | HTML 문서의 속성을 지정하기 위한 태그. title, meta(utf8, description, style)등을 사용 |
|  body   | HTML 문서의 본 모양(내용)을 나타내기 위한 태그               |
| h[1~6]  | 제목, 부제 등에 사용되는 태그                                |
|    p    | 일반 text                                                    |
|   img   | 이미지 `<img src="주소 or 파일위치" alt="산 이미지"(값 못불러왔을때)> ` |
| iframe  | 새로운 프레임(사이트) `<iframe width="너비" height="높이" src="주소">` 대형 사이트에서는 보안상의 이유로 전체 주소는 막아놨다. |
|    b    | 굵게(Bold)                                                   |
|    i    | 기울임꼴(italic)                                             |
| strong  | 강한강조                                                     |
|   em    | 약한강조                                                     |
| ins, s  | 밑줄(insert)                                                 |
| del, u  | 취소선(delete)                                               |
|   sup   | 위첨자                                                       |
|   sub   | 아래첨자                                                     |
|  small  | 작게                                                         |
|   br    | 줄바꿈                                                       |
|   hr    | 가로줄                                                       |
|   ul    | 순서 없는 목록(unordered list) li로 하위요소 표기            |
|   ol    | 순서 있는 목록(ordered list) li로 하위요소 표기              |
|    a    | 링크 `<a href="https://www.naver.com" target="_black"(새창) title="네이버"(툴팁표기)>` 형태로 작성 |
|  table  | 테이블의 시작태그                                            |
|   tr    | 행의 시작                                                    |
|   th    | 행의 요소중 제목을 위한 태그(굵은 글씨)                      |
|   td    | 행의 요소                                                    |
| rowspan | 행병합 td또는 th에 `<td rowspan="2">`형태로 사용             |
| colspan | 열병합 td또는 th에 `<td colspan="3">` 형태로 사용            |



## 폼

|     태그명     | 내용                                                         |
| :------------: | ------------------------------------------------------------ |
|      form      | 폼의 시작태그 `<form action="www.naver.com" method="post" autocomplete="on"(자동완성 기능. 특정 요소마다 off도 가능)>` 형태로 사용 |
|     input      | 입력값 요소를 지정                                           |
|      text      | 한 줄 짜리 문자열 값 `<input type="text(형식)" name="key값" id="id값" value="defalut값" required(반드시 입력받아야 함)>`의 형태로 사용 |
|     number     | 숫자 `<input type="number" min="10" max="15">` 형태로 사용   |
|     email      | 이메일                                                       |
|      tel       | 전화번호                                                     |
|      url       | url                                                          |
|    checkbox    | 체크박스 `<input type="checkbox" name="key값" value="value값" checked>` 형태 |
|     radio      | 라디오 버튼 `<input type="radio" name"key값(다른 radio버튼도 name을 같은 값으로 준다면 자동 그룹핑) checked>"` 형태 |
|     submit     | 제출 버튼                                                    |
|     reset      | 리셋 버튼                                                    |
|      file      | 파일 업로드                                                  |
|     hidden     | 입력값을 수정하지 않고 곧바로 보낼 때 쓰임. `<input type="hidden" name="key값" value="value값" > ` |
|     image      | 제출버튼 이미지 입히기 `<input type="image" src="주소 또는 파일명" alt="이미지 로드 실패시 문구" title="툴팁">`형태로 사용 |
|    textarea    | 텍스트 여러 줄 입력시 사용`<textarea cols="열 사이즈" rows="행 사이즈" placeholder="미입력시 희미하게 예시 텍스트기재"></textarea>`형태로 사용 |
|     button     | `<button>버튼 이름</button>` 또는 `<input type="button" value="버튼이름">` |
|     select     | `<select name="key"> <option value="value값" selected="selected(초기선택)">텍스트 표기</option>`형태로 사용 |
| optgroup label | select안에서 `<optgroup label="내부 카테고리명">..여러 option.. </optgroup>` |
|    fieldset    | 폼 요소를 그룹으로 묶어줌 (네모난 선으로 둘러줌)             |
|     legend     | 그룹에 제목 부여 (fieldset에 제목 표기)                      |
|     range      | 범위 설정 `<input type="range" min="0" max="10">`형태로 사용 |

JS, HTML 모두 유효성검사가 가능하지만, JS는 좀 더 디테일한 부분에 사용된다. ex) 비밀번호 특수문자, 영문자, 숫자 조합 검사 등.. 그러나 유효성검사는 조금만 수정하면 무시할 수 있기 때문에 보안적인 측면에서 신뢰할 수 없다. 따라서 서버단에서 반드시 검사를 해주어야한다.



## 시맨틱 태그

HTML5에서는 시맨틱 웹을 중요시한다. 시맨틱 웹이란 실제적인 기능은 없지만 레이아웃 구조에 맞는 태그로 묶어줌으로써 HTML을 보다 구조화해서 표현할 수 있다. 다음과 같은 장점이 있다.

- 구조화로 인한 가독성
- 검색 노출의 용이성
  - 시맨틱 태그를 사용한 레이아웃을 컴퓨터가 해석할 수 있다. 어디가 내용인지 알 수 있기때문에, 검색시 해당 부분을 노출시킨다.

| 태그명  | 내용                                                         |
| :-----: | ------------------------------------------------------------ |
| header  | 제목, 상단바 등 컨텐츠의 윗부분                              |
|   nav   | 네비게이션. 사이트를 안내하는 요소. 보통 ul을 넣어 목록 형태로 사용 |
|  main   | 문서의 주된 컨텐츠 1번만 쓸수 있음(but, I에서 지원 안됨....) |
| article | 독립적으로 재사용 할 수 있는 (기사부분 등)섹션에 사용        |
| section | 의미적으로 각각 파트를 구분하기 위해 쓰는 태그               |
|  aside  | 부수적인 부분 (광고, 사이드바)                               |
| footer  | 컨텐츠의 가장 아랫부분에 위치. (가장 아래의 주소, 연락처, 회사정보) |



## 검색 엔진 최적화

**HTML페이지를 구성할 때, 왜 사용자에게 보여지는 부분뿐만 아니라 보여지지 않는 부분에 대해서도 의미에 맞게, 규칙에 맞게 구현을 해야할까?**

크롬, IE 등의 브라우저는 각각 검색 엔진을 포함하고 있다. 이러한 검색 엔진은 사용자가 어떠한 키워드를 검색했을 때, 수 많은 페이지의 HTML을 분석해서 가장 알맞은 정보를 포함하고 있는 페이지 별로 순위를 매겨 페이지 상단에 띄운다. 따라서 검색 엔진을 제대로 활용하면 그만큼 많은 사용자에게 노출될 수 있고, 검색 엔진을 신경쓰지 않는다면, 오히려 스팸으로 간주되어 멀리 밀려나게 된다. 이러한 검색 엔진 최적화를 Search Engine Optimization(SEO)라고 부른다.



- 페이지마다 title 태그에 제목 선정 (제목 그대로 검색결과가 반영됨)

- meta 태그의 description 표기. 그러나 무분별한 description은 검색엔진이 웹스팸으로 판별할 수 있음.

- URL구조 개선
  - 단어사용
  - 단순구조

- 다수의 페이지, 같은 컨텐츠의 경우 301리다이렉션 또는 head태그 안에 rel="canonical" 옵션 설정
  - 301리다이렉션 : 서버사이드나 클라이언트 단에서 어떤 코드도 수행하지 않고 바로 리다이렉션함. 다음과 같은 2가지 경우에 사용. 301은 요청한 정보가 새로운 주소로 영구적으로 옮겨갔다는 의미, 302는 일시적으로 옮겨갔다는 의미. 육안으로 구별할 수 없으나, 검색엔진 크롤러에서 차이를 파악해 검색엔진 최적화에 영향을 미침.
    1. 기존의 페이지 주소가 새롭게 변경되어서 하나의 페이지에 유도해야할 경우
    2. 불필요하거나 잘못된 서브 주소를 하나로 이동시키는 경우

- a(앵커)태그 사용시 의미있는 앵커 텍스트 활용`<a href="www.naver.com">앵커 텍스트</a>`

- onchange 옵션으로 html내에서 JS쓰지 말고 a태그 이용해서 페이지 이동하기 (검색엔진이 JS해석 불가능 or 어려움)

- 이미지 등을 이용할 때, alt옵션 사용하기 (이미지 로드 실패시, 정보 제공)

- 이미지 파일명도 관련된 파일명으로 설정

- 제목 태그 (h1~6)사용시 알맞은 의미 사용. (p태그 등의 스타일을 이용해 h처럼 사용하면 안되는 이유)

- https 사용 (구글 검색엔진에서 전체 점수의 약 1% 정도에 해당하는 랭킹 가산점 부여)

- #### PageRank 
  ![pagerank](https://user-images.githubusercontent.com/52786355/83699050-05942700-a63e-11ea-8199-f5f65d14682e.PNG)

  - C, D, E는 어디에도 링크가 걸려있지 않기 때문에 PageRank 순위가 낮다. (검색시 노출도↓)
  - A는 C, D, E에서 A 사이트를 링크로 걸어 놓고 있기 때문에, PageRank 순위가 높다 (검색시 노출도↑)
  - D는 A에서 링크를 걸고 있기 때문에 PageRank 순위가 높다 (검색시 노출도↑)
  - B는 링크가 걸려있진 않지만, 방문을 많이 했기 때문에 PageRank 순위가 높다 (검색시 노출도↑)

  웹 페이지에 스팸 링크가 많은 이유. (PageRank를 높이기 위해서)

  

참고자료 : 인프런 - 생활코딩 강의