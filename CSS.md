# CSS (Cascading Style Sheet)

프론트엔드의 구조, 표현, 행위 중 표현을 담당한다. 뜻 그대로 폭포수처럼 내려가면서 스타일을 적용한다. 기존의 HTML에선 디자인에 관련된 부분도 태그 내에서 같이 처리하다보니 문서가 구조화되지 않고, 가독성이 떨어지게 되어 관리가 힘들어지게 되면서 디자인에 관련된 부분만 따로 관리하기 위해 CSS가 나오게 되었다.  

![css구조](https://user-images.githubusercontent.com/52786355/83699173-586dde80-a63e-11ea-86c4-0e7601afa498.PNG)

​																				[ 기본적인 구조 ]

[HTML/CSS/JS 연습사이트](https://jsbin.com/?html,output)



## Index

- [선택자](#선택자)
- [명시도](#명시도)
- [BoxModel](#BoxModel)
- [Box-Sizing](#Box-Sizing)

- [Position](#Position)

- [Flex](#Flex)

- [Media Query](#Media-Query)

- [Float](#Float)

- [Column](#Column)

- [Filter](#Filter)

- [Transform](#Transform)

- [Transition](#Transition)

- [Minify](#Minify)

- [Preprocessor](#Preprocessor)

- [Fontello](#Fontello)

  

## 선택자

- `{`가 나오기 전의 모든 부분이 선택자이다.  (`@`제외)

- 자식 : 해당 요소의 바로 하위
- 자손 : 해당 요소의 자식을 포함한 **모든**하위

|              종류               | 내용                                                         | CSS Level |
| :-----------------------------: | ------------------------------------------------------------ | :-------: |
|           E[pattern]            | pattern에 따른 포함, 시작, 끝나는 등의 패턴을 따르는 요소 E를 선택 |    2~3    |
|               `,`               | or(\|\|)의 의미 `ul,ol{background-color:powderblue;}`        |           |
|        `*` (전체 선택자)        | HTML페이지 내부의 모든 태그를 선택한다. 모든 요소를 읽어내려야 하기 때문에 페이지 로딩 속도가 느려질 수 있다. |     2     |
|         E (태그 선택자)         | 태그명이 E인 특정 태그를 선택                                |     2     |
|            `.class`             | 클래스 속성값이 class으로 지정된 요소를 선택 (다수 특성)     |     1     |
|              `#id`              | 특성 속성에 대해 id값으로 요소 선택 (단일 특성) 특정 id속성값은 오직 하나만 있어야 함 |     1     |
|        `>` (자식 선택자)        | 자식(직계자손)을 의미 `#id>li {color:red}` (IE6에서 지원안됨) |     2     |
|        E F(하위 선택자)         | 자손을 의미 `section ul{color:blue}`                         |     1     |
|      E+F(인접 형제 선택자)      | E 요소를 뒤따르는 F 요소를 선택 (E와 F사이에 다른 요소가 존재하면 선택하지 않음) / IE6지원 안됨 |     2     |
|      E~F(일반 형제 선택자)      | E 요소가 앞에 존재하면 F를 선택한다. (E가 F보다 먼저 등장하지 않으면 선택하지 않음) / IE6지원 안됨 |     3     |
| E:[option] (가상 클래스 선택자) | link, visited, active, hover, focus 등이 있다. (방문여부, 클릭or엔터 눌린동안 요소선택, 호버, 포커스동안 E선택 등...) 워낙 많은 패턴이 있기 때문에 필요시마다 습득해 적용해야 할 것 같다. |           |

[생각보다 재미있는 선택자 학습 게임](http://flukeout.github.io/)





## 명시도

서로 교집합 관계에 있는 상황에서 어떤 규칙을 적용해야 하는지 일종의 가중치로 계산해서 적용한다. 3가지 종류의 가중치가 있다. 순차적으로 각각의 계층에서 명시도를 우선적으로 비교하고 같을시, 하위 계층으로 내려오는 방식이다. 겹치는 부분에 대해서 우선순위를 적용하고 겹치지 않는 부분은 그대로 상속된다.

먼저, style을 적용하는 방법은 3가지가 있다. 

- `<p style="color:red">`와 같은 inline style
- `<style>`태그 안에서 사용하는 internal style
- `<link>`태그 안에서 사용하는 (불러와서 사용하는 방식) external style

우선순위는 inline style > internal style = external style 이다. (그러나 호이스팅이 발생할 수 있기 때문에 internal style과 external style 사용시 확인을 해야한다.)

![specificity](https://user-images.githubusercontent.com/52786355/83699170-57d54800-a63e-11ea-8a41-c5a5b91ca6ae.PNG)



가장 위의 계층인 ID부터 우선적으로 비교하게 되며, 이 수치가 같을 시 하위 계층인 Class, Attribute, pseudo-classes의 수를 세어 비교하는 방식이다. 3계층의 명시도 가중치까지 같을 경우엔 가장 최근에 (마지막에) 선언된 규칙을 따른다. [명시도 계산기](https://specificity.keegan.st/)

```
!important > inline style > id [ 100 ] > class [ 10 ] > tag [ 1 ] > * [ 0 ]
```

`!important`의 경우 다른 선언들을 덮어버릴 수 있기 때문에 디버깅이 어려워진다. 안 쓰는게 가장 좋고, 반드시 필요한 부분만 사용해야한다.



## BoxModel

여백과 크기에 관한 정보로 총 4가지 요소가 있다.

1. 내용(content) : 텍스트나 이미지가 들어있는 박스의 실질적인 내용 부분이다.
2. 패딩(padding) : 내용과 테두리 사이의 간격입니다. 패딩은 눈에 보이지 않는다.
3. 테두리(border) : 내용와 패딩 주변을 감싸는 테두리이다.
4. 마진(margin) : 테두리와 이웃하는 요소 사이의 간격입니다. 마진은 눈에 보이지 않는다.
   - 다른 요소와 다르게 **마진은 서로 겹친다.** 
   - 부모와 자식이 서로 겹친다면, **자식은 둘 중 값이 큰 쪽의 마진을 따른다.**
   - 만약 요소에 **시각적인 정보가 없다면, top ,left, right, bottom 중에 가장 큰 마진값을 따른다.**
   - border가 겹칠 때 해당 굵기만큼 -,+ px을 주어 오버랩되는 현상을 막을 수 있다.

![boxmodel](https://user-images.githubusercontent.com/52786355/83842604-4d9a7300-a73e-11ea-8438-ae1a781f54aa.png)



#### [자료 출처 : TCPSchool](http://tcpschool.com/css/css_boxmodel_boxmodel)



## Box-sizing

- content기준이 아닌, border 기준으로 크기를 지정 (크기를 맞출 때 유용해서 자주 쓰인다.)

- default값은`box-sizing : content-box`
- `box-sizing : border-box` : border기준으로 크기를 지정

#### Why use `box-sizing:border-box`?

`box-sizing : border-box`를 많이 쓰는 이유는 기본적으로 border까지 박스사이즈에 들어가기 때문에, 예를들어 박스사이즈가 150px에 border가 1px 크기 일 경우 즉, 

```html
...
<style>
    .classname{
        width:150px;
        border:1px solid gray;
    }
</style>
...
```

와 같은 상황일 경우, 박스사이즈는 150px가 아닌 151px이다. 이럴경우 `box-sizing : border-box`옵션을 주어서 전체크기를 150px로 맞출 수 있기 때문에 자주 사용하는 옵션이다.



## Position

- `position: static` : 위치와 관련된 설정을 하지 않은 상태 (default)

- `position: relative` :  상대적인 위치를 설정 (부모기준)

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <style>
          html{border:1px solid gray;}
          div{
              border:5px solid tomato;
              margin:10px;
          }
          #me{
              position: relative;
              left:100px;
              top:100px;
          }
      </style>
    </head>
    <body>
      <div id="other">other</div>
      <div id="parent">
         parent
         <div id="me">me</div>
      </div>
    </body>
  </html>
  ```

- `position : absolute` : 절대적인 위치를 설정한다. default는 현재위치, 설정시 페이지 최상단 좌측기준으로 적용된다. 그러나 부모의 offset값이 `position: relative`라면 부모 기준으로 적용된다.

- `position : fixed` : 페이지가 길어져 스크롤이 생겨도 항상 절대적인 위치에 배치한다. (광고 등에 사용됨)



## Flex

그리드 레이아웃을 기본으로 해 플렉스 박스를 원하는 위치에 배치하는 것을 말한다. 화면 크기에 따라 레이아웃의 배치나 크기를 조절해야 할 때 편리하게 사용할 수 있다. `ul`과 `li`와 같이 자식과 부모간의 관계가 있어야 한다. 

```html
<!doctype>
<html>
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            /* 이 옵션 사용시 자식들은 모두 inline으로 바뀐다. */
            display:flex;
            flex-direction:row-reverse;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>
```

- `Flex- derection ` : 정렬된 배치를 원할 때 사용한다. default값은 row. `row-reverse`나 `column-reverse`가 있다. 
- `Flex-basis` : 기본 크기를 설정. ex) `Flex-basis : 100px;`

- `Flex-grow` : 여백을 모두 채우면서 분할 값을 준다. `Flex-grow:0`이 default값이며, 1이상 값을 주었을 때, 부모 컨테이너에 꽉 찬 형태로 채워지게 된다. 각각의 요소에 `Flex-grow`값을 준다면 모두 더한 값을 분모로, 각각의 값을 분자로 가지는 만큼 할당한다.

- `Flex-shrink` : **`Flex-basis`값을 가지고 있을 때**, 창의 크기를 줄인다면 해당 요소가 같이 줄어들지만 shrink 값을 설정하면 줄어들지 않거나, 일정 비율대로 줄어들게 할 수 있다. `Flex-grow`와 같이 모두 더한 값을 분모로, 각각의 값을 분자로 가지는 비율만큼 줄어든다. default값은 0이다. (이 말은 기본적으로 Flex를 사용시 크기에 따라 요소도 줄어든다는 의미이다.)

- holy grail layout : 성배라는 뜻으로 양옆의 요소는 줄어들지 않고, 중간의 메인 컨텐츠만 줄어드는 레이아웃을 의미한다. 많은 사람들이 이러한 레이아웃을 찾기 위해 노력했지만 성배를 찾는 것 만큼 찾기 힘들었다고 해서 성배 레이아웃이라고 한다. (그만큼 이상적인(?) 레이아웃인 것 같다.)

  ```html
  <!doctype>
  <html>
  <head>
      <meta charset="utf-8">
      <style>
          .container{
              display: flex;
              flex-direction: column;
          }
          header{
              border-bottom:1px solid gray;
              padding-left:20px;
          }
          footer{
              border-top:1px solid gray;
              padding:20px;
              text-align: center;
          }
          .content{
              display:flex;
          }
          .content nav{
              border-right:1px solid gray;
          }
          .content aside{
              border-left:1px solid gray;    
          }
          nav, aside{
              /* 기본크기가 있기 때문에 줄어들지 않는다. */
              flex-basis: 150px;
              flex-shrink: 0;
          }
          main{
              padding:10px;
          }
      </style>
  </head>
  <body>
      <div class="container">
          <header>
              <h1>생활코딩</h1>
          </header>
          <section class="content">
              <nav>
                  <ul>
                      <li>html</li>
                      <li>css</li>
                      <li>javascript</li>
                  </ul>
              </nav>
              <main>
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis veniam totam labore ipsum, nesciunt temporibus repudiandae facilis earum, sunt autem illum quam dolore, quae optio nemo vero quidem animi tempore aliquam voluptas assumenda ipsa voluptates.
              </main>
              <aside>
                  AD
              </aside>
          </section>
          <footer>
              <a href="https://opentutorials.org/course/1">홈페이지</a>
          </footer>
      </div>
  </body>
  </html>
  ```

- 이 밖에도 다양한 옵션을 [생활코딩 강의 사이트](https://opentutorials.org/module/2367/13526)에서 확인 할 수 있다.



## Media Query

사이트에 접근하는 기기의 해상도에 따라 서로 다른 스타일 시트를 적용해 주는 것을 미디어 쿼리라고 한다. 반응형 디자인의 핵심적인 요소이며, 반응형 웹 디자인은 미디어 쿼리를 기반으로 한다. (`@`기호 이용) 예제를 보는게 이해가 더 빠르다. 참고로 모바일 화면에서 적용하려면 반드시`<meta name="viewport" content="width=device-width, initial-scale=1.0">`옵션을 넣어주어야 한다.

```html
<!doctype html>
<html>
<head>
    /* meta 태그에 viewport를 설정해 주어야만 적용된다! */
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* 600px 이하일 경우(501~600px) */
        @media (max-width:600px){
            body{
                background-color: green;
            }
        }
        /* 500px 이하일 경우 */
        @media (max-width:500px){
            body{
                background-color: red;
            }
        }
        /* 601px 이상일 경우*/
        @media (min-width:601px){
            body{
                background-color: blue;
            }
        }
    </style>
</head>
<body>
   <ul>
       <li>~500px : red</li>
       <li>501~600px : green</li>
       <li>601px~ : blue</li>
   </ul>
</body>
</html>
```



```html
<!doctype>
<html>
<head>
    <meta charset="utf-8">
    <style>
        .container{
            /*container 하위요소들이 전부 inline으로 바뀜*/
            display: flex;
            flex-direction: column;
        }
        header{
            border-bottom:1px solid gray;
            padding-left:20px;
        }
        footer{
            border-top:1px solid gray;
            padding:20px;
            text-align: center;
        }
        .content{
            display:flex;
        }
        .content nav{
            border-right:1px solid gray;
        }
        .content aside{
            border-left:1px solid gray;    
        }
        @media(max-width:500px){
            .content{
                flex-direction: column;
            }
            .content nav, .content aside{
                border:none;
                flex-basis: auto;
            }
            main{
                /* 우선순위. main이 먼저 나옴 */
                order:0;
            }
            nav{
                /* main 뒤에 nav가 나옴 */
                order:1;
            }
            aside{
            	/* nav뒤에 aside가 나옴 */
                order:2;
                /* aside를 안 보이게 함 */
                display: none;
            }
        }
        nav, aside{
            flex-basis: 150px;
            flex-shrink: 0;
        }
        main{
            padding:10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>생활코딩</h1>
        </header>
        <section class="content">
            <nav>
                <ul>
                    <li>html</li>
                    <li>css</li>
                    <li>javascript</li>
                </ul>
            </nav>
            <main>
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis veniam totam labore ipsum, nesciunt temporibus repudiandae facilis earum, sunt autem illum quam dolore, quae optio nemo vero quidem animi tempore aliquam voluptas assumenda ipsa voluptates. Illum facere dolor eos, corporis nobis, accusamus velit, similique cum iste unde vero harum voluptatem molestias excepturi.
            </main>
            <aside>
                AD
            </aside>
        </section>
        <footer>
            <a href="https://opentutorials.org/course/1">홈페이지</a>
        </footer>
    </div>
</body>
</html>
```

[w3shcools의 래퍼런스](www.w3schools.com/cssref/css3_pr_mediaquery.asp)에 media query 관련 다양한 옵션이 있다.




## Float

요소들과 어울리도록 세팅하고 싶을 때 이용한다. 실제로 적용을 해보면서 이해하는 것이 더 빠르다. 

```html
<!doctype html>
<html>
<head>
  <style>
    img{
      width:300px;
      /* float: left 효과를 주어 이미지가 왼쪽에 배치되며, p태그와 어우러짐*/
      float:left;
      margin:20px;
    }
    p{
      border:1px solid gray;
    }
  </style>
</head>
<body>
  <img src="이미지 주소" alt="">
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate minus, obcaecati quia eaque perspiciatis! Vero cum libero architecto. Odit, et. Totam expedita
  </p>
  /* clear 효과를 주어 어울리지 않도록 세팅 */
  <p style="clear:both;">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate minus, obcaecati quia eaque perspiciatis! Vero cum libero architecto. Odit, et. Totam expedita Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate minus, obcaecati quia eaque perspiciatis! Vero cum libero architecto. Odit, et. Totam expedita Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptate minus, obcaecati quia eaque perspiciatis! Vero cum libero architecto. Odit, et. Totam expedita
  </p>
</body>
</html>
```



Float를 활용한 holy grail 레이아웃 실습

```html
<!doctype html>
<html>
<head>
  <style>
    *{
      box-sizing:border-box;
    }
    .container{
      width:540px;
      border:1px solid gray;
      margin:auto;
    }
    header{
      border-bottom: 1px solid gray;
    }
    nav{
      float:left;
      width:120px;
      border-right:1px solid gray;
    }
    article{
      float:left;
      width:300px;
      border-left:1px solid gray;
      border-right:1px solid gray;
      margin-left:-1px;
    }
    aside{
      float:left;
      width:120px;
      border-left:1px solid gray;
      margin-left:-1px;
    }
    footer{
      clear:both;
      border-top:1px solid gray;
      text-align: center;
      padding:20px;
    }
  </style>
</head>
<body>
 <div class="container">
    <header>
    <h1>
      CSS
    </h1>
    </header>
    <nav>
      <ul>
        <li>position</li>
        <li>float</li>
        <li>flex</li>
      </ul>  
    </nav>
    <article>
      <h2>float</h2>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sit quae earum enim ab distinctio corrupti eius reprehenderit non, rerum ut nisi autem cum sint perferendis eum id velit, molestias nesciunt. Ullam dignissimos consequuntur explicabo id voluptas vel deleniti nesciunt veritatis iusto commodi, laudantium cumque vero deserunt laboriosam. Ea, quia est?
    </article>
    <aside>
      ad  
    </aside>
    <footer>
      copyleft  
    </footer>
 </div>
</body>
</html>
```



## Column

신문처럼 컬럼을 나누어 다단형식으로 레이아웃을 지정할 수 있다. 

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="author" content="egoing">
    <style>
      .column{
        text-align: justify;
        column-count: 4;
/*        column-width: 200px;*/
        column-gap:30px;
        column-rule-style: solid;
        column-rule-width: 5px;
        column-rule-color: red;
      }
      h1{
        column-span: all;
      }
    </style>
</head>
<body>
   <div class="column">
     Lorem ipsum dolor sit amet, consectetur adipisicing elit. Molestiae blanditiis nostrum eum ipsam, 
      
     quam expedita distinctio aspernatur voluptas inventore in officia at, a repudiandae modi vel dicta exercitationem accusamus? Tenetur minima doloremque, sequi id, necessitatibus deleniti porro ex maxime perferendis quaerat rerum molestias dolor fugit ullam expedita? Earum velit eaque, esse aliquid labore, ex, corporis odit deserunt consectetur sit aspernatur
      <h1>Lorem ipsum dolor sit amet.</h1>
       ipsam quos cupiditate dolores voluptatem non nam voluptas ab animi quidem adipisci repellat id quod. Laboriosam, distinctio, ut. Quia deserunt, voluptates illum eos, qui, doloremque recusandae laudantium aliquam amet rerum nulla, eveniet. Libero quas iusto, suscipit esse beatae voluptas labore. Nobis facere architecto adipisci ipsa molestias, possimus tempore. Obcaecati, quae laborum atque perspiciatis natus dolore repellendus in officia, sit! Placeat, nesciunt cupiditate similique vitae minima iusto blanditiis perferendis obcaecati enim odio delectus. Quaerat quos deserunt, voluptas aperiam. Quo neque ducimus accusamus quibusdam minima incidunt, voluptatem saepe iusto sit numquam, expedita distinctio aliquid voluptatum alias voluptate sint est ab similique ipsam unde quas porro error? Illum unde consequuntur ab optio architecto, adipisci odit saepe dolor est perferendis error autem iusto a iste tempore nam enim quaerat dicta fugit vel eaque itaque, laborum? Dolores consequatur quo labore dolorem nemo in, tempora animi enim delectus ipsam amet possimus et deserunt recusandae eveniet provident cum quaerat dolorum esse, nam doloremque! Porro sapiente labore aliquam incidunt temporibus praesentium est tempora magnam placeat rem. Autem non provident eos perferendis nihil numquam quisquam suscipit aut, vero minima ex iure cum possimus eveniet veniam aliquam nulla a dignissimos, fugit tempora eaque totam temporibus! Magni minus expedita tempore deserunt necessitatibus, quibusdam, repellat sequi quos exercitationem aliquam sapiente libero eius vitae rem ea nihil deleniti nemo debitis tempora soluta a similique inventore. Sit vero dignissimos facere dolore dicta nulla iure magni quos officiis esse hic accusantium, praesentium adipisci laudantium impedit provident fuga suscipit, placeat porro itaque voluptatum dolorem ullam velit quasi. Laboriosam distinctio explicabo, ullam fugit nesciunt nam itaque repellendus nemo doloribus officia unde quaerat aspernatur odit. Porro quisquam at officia, ad totam minima minus aliquid aliquam rerum dicta, odio sint optio. Exercitationem similique, dignissimos sit nihil fuga ex dolores molestiae ratione impedit error, vitae aliquid reiciendis maxime id odit sed eveniet. Corporis in mollitia assumenda, exercitationem ullam explicabo dolorum tempore architecto cum. Possimus natus ipsam facilis porro magni deleniti nulla eveniet aliquam incidunt minima nihil alias voluptatem, odio molestiae quaerat suscipit, officiis temporibus itaque veritatis, placeat modi corporis saepe harum delectus officia. Libero rerum expedita dolorem porro architecto reprehenderit eligendi molestiae, amet minima quae assumenda neque nulla error, officiis suscipit placeat, illo eius. Aliquid dicta cupiditate culpa consequatur totam. Qui consequuntur eveniet eum dicta repellendus quam ea quisquam dolore, distinctio, quidem facilis minus ratione ullam perferendis. Ad ea, aliquid doloremque distinctio enim hic sunt illum dolore, commodi iusto nobis temporibus nesciunt, vero quae velit perferendis dicta. Quod necessitatibus sit, accusamus odit aspernatur! Sequi, nisi aut at totam perspiciatis fugit quos minus sapiente consequatur neque officiis quibusdam qui nemo, voluptatibus minima dolore laboriosam. Recusandae similique accusamus vel eaque tempore fugiat dolore adipisci, tempora, impedit harum facere aspernatur et nam sequi, facilis architecto voluptate sunt iusto soluta. Itaque laboriosam tempore ab harum fugit natus, eius laborum culpa, impedit autem magni totam. Et dicta animi molestiae, aliquam, sequi enim. Accusamus consectetur eum eligendi nemo sunt provident ut repudiandae, distinctio! Recusandae harum animi quia perferendis maiores! Ratione quis cupiditate odio dolore nulla minus iure veritatis hic temporibus neque beatae delectus doloribus repellat quisquam alias mollitia accusantium perferendis, quibusdam recusandae, iusto modi maiores excepturi corrupti voluptatibus! Facere, maiores ea natus culpa necessitatibus temporibus, eaque, vitae nihil animi repudiandae expedita aspernatur quo sequi, soluta. Minus eligendi tenetur ullam, doloremque, quod libero provident excepturi beatae cumque quo, voluptate. Quam deleniti minus officiis. Sit velit, debitis voluptatem modi consequatur doloremque aperiam assumenda expedita odio nesciunt quis ipsam, cumque impedit quia veritatis error quidem similique accusantium eos, qui sunt? Blanditiis facere tenetur eius minus dolorum, praesentium doloremque consequatur accusamus quis expedita, reiciendis odio optio illo voluptatibus ut asperiores quos officia totam distinctio eaque. Aspernatur eaque nihil porro illo laboriosam ex ea id fuga ipsa! Cum reprehenderit, cumque dolorum aliquam quidem aliquid soluta corrupti pariatur fugiat quae excepturi tempora, nostrum eveniet accusamus consectetur alias minus nulla unde. Rem expedita vitae labore culpa, id sit reiciendis quaerat, temporibus nemo eos modi error excepturi voluptatem. Non officia, accusantium inventore reiciendis cupiditate laboriosam ullam quaerat officiis facilis modi eum iste eius, soluta, iure nobis dolor. Similique deserunt beatae officia reprehenderit quo, aliquam facilis autem nihil in! Quisquam minima sunt corporis, ipsum maiores nam quia corrupti, odit id suscipit ratione voluptate nisi incidunt sequi eum facilis dicta deleniti aliquid ducimus maxime esse qui. Sunt eius, deserunt illo quod ducimus quasi, sed soluta ipsum inventore nisi! Optio modi omnis, ex, fugit nemo eveniet. Nostrum, incidunt porro, dolores non, dolor velit commodi eius recusandae eaque necessitatibus molestiae dolorem unde ipsa voluptatum. Ipsa ab minus atque non quis debitis delectus similique excepturi, ipsum suscipit perferendis doloribus deleniti nam blanditiis architecto quae fuga porro perspiciatis magnam ipsam pariatur. Quia, temporibus. Molestias quia nesciunt vitae quam, deserunt dolor adipisci architecto minus natus facere, molestiae, sint eum. Soluta magni totam ducimus, deserunt quam, nisi unde, asperiores iusto, repudiandae aperiam dolorem ab libero aliquam fugit ratione voluptatem sunt vel earum saepe debitis id nostrum minus ullam quaerat. Amet molestias deserunt quae assumenda ut odit corporis accusantium saepe labore ad. Distinctio in doloremque, deleniti provident ducimus quisquam at, temporibus odio eligendi, consequuntur sequi quibusdam facere aut enim vel similique eius asperiores aperiam ratione suscipit est eum dolore. In eius dignissimos, quod illum dolores! Molestiae possimus eius, illo incidunt optio deleniti, nihil odit nisi harum, quo ex. Corporis omnis accusantium consequuntur ratione laudantium magni tempora expedita. Earum ullam, aspernatur quisquam doloremque soluta quae eius tempora atque magni omnis ex vel iusto, similique eos provident! Autem ipsum aliquam quasi minima, incidunt perferendis facere, optio nobis rerum dolor ipsam quas. Quam consectetur recusandae voluptatem. Praesentium excepturi sunt ut neque eum labore ducimus repudiandae eveniet quibusdam explicabo, iure obcaecati nobis, veritatis quis et accusantium ipsa.
   </div>
</body>
</html>
```



## Filter

img 태그 뿐만아니라 여러 태그(h1, p 등의 문자열 태그도 가능)에서도 포토샵에서 적용하는 다양한 필터효과를 줄 수 있다. 포토셥과 다른 점은 예를 들어 문자태그에 블러처리를 해도 검색할 수 있는 등 정보를 그대로 담고 있다는 점이다. 그러나 IE 9버전은 지원하지만, 10과 11버젼에서는 [지원하지 않기 때문에](https://stackoverflow.com/questions/16407268/css-filter-grayscale-image-for-ie-10)(~~킹갓 크롬~~) 파일을 다운받는 등 따로 처리를 해주어야 한다.  [코드펜](https://codepen.io/search/pens?q=filter)을 통해 필터를 적용한 다양한 예제를 확인할 수 있다.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    img:hover,h1:hover{
        /* 간단한 애니메이션 효과 */
      transition : all 5s;
      filter: grayscale(100%) blur(3px);
    }
  </style>
</head>
<body>
  <img src="이미지 주소">
<h1>Context</h1>
</body>
</html>
```



## Transform

포토샵으로 사진을 왜곡하거나 변형하는 등의 처리를 CSS를 통해서도 할 수 있다. 매우 다양한 기능을 [코드펜](codepen.io/vineethtr/full/XKKEgM/)에서 확인 할 수 있다.



## Transition

애니메이션 기능으로 역시 설명보다는 직접 실습을 해보는게 이해가 빠르다. [능력자분의 사이트](https://matthewlein.com/tools/ceaser)와 [코드펜](https://codepen.io/search/pens?q=transition)에서 다양한 기능을 사용해볼 수 있다.



## Minify

보통 bootstrap에서 css파일명이 `bootstrap.css`가 아니라 `bootstrap.min.css`로 되어있는 경우가 많은데, 코드를 경량화(Minify) 했다는 뜻이다. CSS를 작성할 때, 가독성을 위해 개행을 하고 주석을 추가하는 등 실제 코드가 실행되는 부분이랑 상관없는 부분을 모두 삭제해 숏코드처럼 코드가 매우 짧아짐으로써 용량을 줄일 수 있다. 압축을 한다고 생각하면 된다. [웹 싸이트](https://adam.id.au/clean-css-online/)에서도 제공을 하고, node의 경우 npm을 이용해 설치할 수도 있다.



## Preprocessor

CSS작성시 선택자의 중첩이나 조건문, 반복분, 다양한 단위 연산 등 마치 프로그래밍 언어로 코딩을 하는 것 처럼 유용한 기능을 사용해 작성할 수 있도록 해주는 **전처리기**이다. Sass, Less, Stylus 등 다양한 전처리기가 있다. 해당 전처리기로 코딩을 하고 컴파일을 하면, CSS파일로 변환해주는 방식이다. compress옵션을 줘서 Minify할 수도 있는 등 다양한 기능을 포함하고 있다. 그러나 CSS뿐만 아니라 전처리기를 활용하기 위한 문법도 따로 공부해야하는 단점이 있다.



## Fontello

[Fontello](http://fontello.com/)에서 다양한 아이콘을 넣을 수 있다. Fontello에서 제공하는 아이콘 뿐만 아니라 다운로드 받은 아이콘을 Fontello에 업로드해 사용할 수도 있고, 그러한 사항을 저장할 수 있다. json파일에 모두 기록이 남기 때문이다.



참고자료 : 인프런 - 생활코딩 강의