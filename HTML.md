# HTML (Hyper Text Mark-up Language)

- 문서의 내용 이외에도 문서의 구조나 서식 등을 포함한다.
- DOM(Document Object Model) 구조
  - html을 루트로 head, body등 트리구조로 이루어짐
- 서버에서 보내오는 정적인 정보를 그대로 그려내는 것에 강하지만, 동적인 화면구성에 약함. 따라서 동적인 입력에 반응하는 것은 JS(AJAX 등)가 처리



## 태그

|  태그명   | 내용                                                         |
| :-------: | ------------------------------------------------------------ |
|   html    | HTML DOM 구조의 루트격 태그. 보통 head와 body로 나뉨         |
|   head    | HTML 문서의 속성을 지정하기 위한 태그. title, meta(utf8..)등을 사용 |
|   body    | HTML 문서의 본 모양(내용)을 나타내기 위한 태그               |
| H[number] | 제목, 부제 등에 사용되는 태그                                |
|     p     | 일반 text                                                    |
|    img    | 이미지 `<img src="주소 or 파일위치" alt="산 이미지"(값 못불러왔을때)> ` |
|  iframe   | 동영상 `<iframe width="너비" height="높이" src="주소">`      |
|     b     | 굵게(Bold)                                                   |
|     i     | 기울임꼴(italic)                                             |
|  strong   | 강한강조                                                     |
|    em     | 약한강조                                                     |
|  ins, s   | 밑줄(insert)                                                 |
|  del, u   | 취소선(delete)                                               |
|    sup    | 위첨자                                                       |
|    sub    | 아래첨자                                                     |
|   small   | 작게                                                         |
|    br     | 줄바꿈                                                       |
|    hr     | 가로줄                                                       |
|    ul     | 순서 없는 목록(unordered list) li로 하위요소 표기            |
|    ol     | 순서 있는 목록(ordered list) li로 하위요소 표기              |
|     a     | 링크 `<a href="https://www.naver.com" target="_black"(새창) title="네이버"(툴팁표기)>` 형태로 작성 |
|   table   | 테이블의 시작태그                                            |
|    tr     | 행의 시작                                                    |
|    th     | 행의 요소중 제목을 위한 태그(굵은 글씨)                      |
|    td     | 행의 요소                                                    |
|  rowspan  | 행병합 td또는 th에 `<td rowspan="2">`형태로 사용             |
|  colspan  | 열병합 td또는 th에 `<td colspan="3">` 형태로 사용            |



## 폼

|     태그명     | 내용                                                         |
| :------------: | ------------------------------------------------------------ |
|      form      | 폼의 시작태그 `<form action="www.naver.com" method="post">` 형태로 사용 |
|     input      | 입력값 요소를 지정                                           |
|      text      | 한 줄 짜리 문자열 값 `<input type="text(형식)" name="key값" id="id값" value="defalut값">`의 형태로 사용 |
|     number     | 숫자                                                         |
|     email      | 이메일                                                       |
|      tel       | 전화번호                                                     |
|      url       | url                                                          |
|    checkbox    | 체크박스                                                     |
|     radio      | 라디오 버튼                                                  |
|     submit     | 제출 버튼                                                    |
|     reset      | 리셋 버튼                                                    |
|      file      | 파일 업로드                                                  |
|     hidden     | 입력값을 수정하지 않고 곧바로 보낼 때 쓰임.                  |
|     image      | 제출버튼 이미지 입히기 `<input type="image" src="주소 또는 파일명" alt="이미지 로드 실패시 문구" title="툴팁">`형태로 사용 |
|    textarea    | 텍스트 여러 줄 입력시 사용`<textarea cols="열 사이즈" rows="행 사이즈" placeholder="미입력시 희미하게 예시 텍스트기재"></textarea>`형태로 사용 |
|     button     | `<button>버튼 이름</button>` 또는 `<input type="button" value="버튼이름">` |
|     select     | `<select name="key"> <option value="value값" selected="selected(초기선택)">텍스트 표기</option>`형태로 사용 |
| optgroup label | select안에서 `<optgroup label="내부 카테고리명">..여러 option.. </optgroup>` |
|    fieldset    | 폼 요소를 그룹으로 묶어줌 (네모난 선으로 둘러줌)             |
|     legend     | 그룹에 제목 부여 (fieldset에 제목 표기)                      |



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



## 검색 엔진

- 페이지마다 title 태그에 제목 선정 (제목 그대로 검색결과가 반영됨)
- meta 태그의 description 표기
- URL구조 개선
  - 단어사용
  - 단순구조

- 다수의 페이지, 같은 컨텐츠의 경우 301리다이렉션 또는 head태그 안에 rel="canonical" 옵션 설정
  - 301리다이렉션 : 서버사이드나 클라이언트 단에서 어떤 코드도 수행하지 않고 바로 리다이렉션함. 다음과 같은 2가지 경우에 사용. 301은 요청한 정보가 새로운 주소로 영구적으로 옮겨갔다는 의미, 302는 일시적으로 옮겨갔다는 의미. 육안으로 구별할 수 없으나, 검색엔진 크롤러에서 차이를 파악해 검색엔진 최적화에 영향을 미침.
    1.  기존의 페이지 주소가 새롭게 변경되어서 하나의 페이지에 유도해야할 경우
    2. 불필요하거나 잘못된 서브 주소를 하나로 이동시키는 경우

- 위의 시맨틱 태그 사용 (시맨틱 태그를 해석하여 검색시 해당 부분을 노출)