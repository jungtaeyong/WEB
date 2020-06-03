# CSS (Cascading Style Sheet)

뜻 그대로 폭포수처럼 내려가면서 스타일을 적용한다. 기존의 HTML에선 디자인에 관련된 부분도 태그 내에서 같이 처리하다보니 문서가 구조화되지 않고, 가독성이 떨어지게 되어 관리가 힘들어지게 되면서 디자인에 관련된 부분만 따로 관리하기 위해 CSS가 나오게 되었다.  

![css구조](C:\Users\User\Desktop\이미지\css구조.PNG)

​																				[ 기본적인 구조 ]



## Index

- [명시도](#명시도)



## 선택자

| 종류 | 내용                                                  |
| :--: | ----------------------------------------------------- |
| `>`  | 직계자손을 의미 `#id>li {coloe:red}`                  |
| `,`  | or(\|\|)의 의미 `ul,ol{background-color:powderblue;}` |
|      |                                                       |
|      |                                                       |
|      |                                                       |
|      |                                                       |
|      |                                                       |



## 명시도

css에서 매우 중요한 개념이다. 서로 교집합 관계에 있는 상황에서 어떤 규칙을 적용해야 하는지 일종의 가중치로, 계산을 해서 적용한다. 3가지 종류의 가중치가 있다. 순차적으로 각각의 계층에서 명시도를 우선적으로 비교하고 같을시, 하위 계층으로 내려오는 방식이다.

![specificity](C:\Users\User\Desktop\이미지\specificity.PNG)

가장 위의 계층인 ID부터 우선적으로 비교하게 되며, 이 수치가 같을 시 하위 계층인 Class, Attribute, pseudo-classes의 수를 세어 비교하는 방식이다. 3계층의 명시도 가중치까지 같을 경우엔 가장 최근에 (마지막에) 선언된 규칙을 따른다. [명시도 계산기](https://specificity.keegan.st/)

 이 밖에도 style을 적용하는 방법은 3가지가 있다. 

- `<p style="color:red">`와 같은 inline style
- `<style>`태그 안에서 사용하는 internal style
- `<link>`태그 안에서 사용하는 (불러와서 사용하는 방식) external style

우선순위는 inline style > internal style = external style 이다. (그러나 호이스팅이 발생할 수 있기 때문에 internal style과 external style 사용시 확인을 해야한다.)



