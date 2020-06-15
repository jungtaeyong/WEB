# JavaScript

프론트엔드의 구조, 표현, 행위 중 행위를 담당해 실질적인 데이터를 다룬다. 프로그래밍 언어로써, 타 언어에 비해 가장 큰 특징은 **비동기 프로그래밍 언어**라는 점이다. 프론트엔드 뿐만 아니라 백엔드도 JS(Node.js)를 이용해 구축할 수 있다.  JS는 ES6 기준으로 다양한 기능이 추가되었다. 언어를 처음부터 배우는 것이 아니기 때문에 조건문, 반복문의 기초적인 개념보다는 **ES6**를 통해 활용할 수 있는 유용한 기능과 개념만 알고 사용법은 몰랐던 **정규식**에 대해 정리한다.



## Index

- [정규식](#정규식)
- [ES6](#ES6-(ECMAScript6))
- [==, ===의 차이](#==와-===의 차이)



## 정규식

정규 표현식은 문자열에 나타나는 특정 문자 조합과 대응시키기 위해 사용되는 패턴이다. JavaScript에서 정규 표현식 또한 객체이다. 이 패턴들은 [`RegExp`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp)의 [`exec`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) 메소드와 [`test`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) 메소드 ,그리고 [`String`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)의 [`match`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/match)메소드 , [`replace`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/replace)메소드 , [`search`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/search)메소드 , [`split`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split) 메소드와 함께 쓰입니다 . 자바스크립트의 정규식에 대해 알아보자.

[MND 정규 표현식]([https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/정규식)), [ZVON.org](http://zvon.org/comp/r/tut-Regexp.html#Pages~Contents)를 참고하자

| 태그 | 내용                                                         |
| :--: | ------------------------------------------------------------ |
| `^`  | 시작에 포함. ex) ^who -> `who` is who `\A`와 다른 점은 `^`은 멀티라인 지원, `\A`는 모든 문단에서 한 번만 적용. 또한 포함하는 문자를 의미하는 `[]`안에 들어갈 경우 부정의 의미 |
| `$`  | 끝에 포함. ex) who$ -> who is `who` `\Z`와 다른 점은 멀티라인의 지원여부. |
| `\`  | 이스케이프 라고 부른다. $, ^처럼 정규식 의미가 아닌 그 자체의 기호로 사용하고 싶을 경우 `\$`와 같이 표현할 수 있다. |
| `.`  | 와일드 카드 역할(리눅스 등에서 `*`로 사용 하는 역할). 모든 문자를 지칭한다. |
| `[]` | 포함되는 문자 **하나**와 대응된다. ex) `[dh]`-> `h`ow `d`o you `d`o ? |
| `-`  | 범위를 지정한다. ex) `[A-D]` = `[ABCD]`                      |
| `()` | 포함되는 문자 **모두**와 대응된다. ex)`..(id|esd|nd)ay`-> `Monday` `Tuesday` `Friday` |
| `|`  | or의 역할                                                    |
| `*`  | 수량자로 0개~ 여러 개를 대응한다. ex) `a*b`-> `aab`c `ab`c `b`c |
| `+`  | 수량자로 1개~ 여러 개를 대응한다. ex) `a+b`-> `aab`c `ab`c bc |
| `?`  | 수량자로 0개~ 1개를 대응한다. ex) `a?b`-> a`ab`c `ab`c `b`c / `?`도 수량자이지만, 수량자 뒤에 붙었을 경우, **해당 수량자의 최소 조건**으로 의미가 달라진다. ex) `r.??`-> ?은 0개~ 1개를 의미하는데, 뒤에 ?가 더 붙었기 때문에, 최소 조건인 0개라는 뜻이므로, r만 대응되는 것을 찾는다. |
| `{}` | 수량을 나타낸다. ex) `.{5}`-> 5배수로 짜른다. `1234567890`123 , `{3,}`-> 3개 이상, `{1,}`->1개 이상 (=`+`), `{0,1}`-> 0개~ 1개 (=`?`) |
| `\w` | 단어로 구분한다. 공백, `-`, `:` 등의 기호를 빼고 모두 선택한다. `\W`(대문자)의 경우 반대로 단어 빼고 모두 선택한다. |
| `\d` | 숫자(digit)만 선택한다. `\D`(대문자)의 경우 반대로 숫자 빼고 모두 선택한다. |
| `\b` | 바운더리를 주어 선택한다.                                    |
| `\A` | 시작점을 의미한다. `^`와 차이점은 멀티라인이 아닌 문단에서 처음에만 적용한다는 점이다. |
| `\Z` | 끝점을 의미한다. `$`와 차이점은 멀티라인이 아닌 문단에서 처음에만 적용한다는 점이다. |

- 연습
  - `.*` : 모든 텍스트
  - `-A*-` : 앞뒤로 -가 붙고 A가 0개~ 여러 개
  - `[-@]*` : -또는 @에 대응되는 것이 0개~ 여러 개
  - `\*+` : `*`기호가 반드시 하나 이상
  - `[^ ]` : 공백이 아닌 것 하나 이상 존재
  - `-X?XX?X` : -로 시작하고, X가 0개~ 1개, X , X가 0개~ 1개, X
  - `-@?@?@?-` : -로 시작하고, @가 0개~ 1개, @가 0개~ 1개, @가 0개~ 1개, -
  - `[els]{1,3}` : e, l, s 중 매치되는 것 1개~ 3개 



## ES6 (ECMAScript6)



 

## ==와 ===의 차이

`==`는 Equal Operator라고 하고, `===`는 Strict Equal Operator라고 한다. 뜻 그대로 `===`는 더 엄격한 판별을 한다.  예를 들어, `1=="1"`은 `true`지만, `1==="1"`은 `false`이다. 이처럼 `===`는 **타입과 형식이 정확하게 같은지** 까지 판단한다. 또 하나의 예시로, `null`과 `undefined`는 값이 없다는 의미의 데이터 형이다. `null`은 값이 없음을 명시적으로 표시한 것이고, `undefined`는 그냥 값이 없는 상태이기 때문에, `==`는 `true`값을 반환하지만, `===`는 `false`가 리턴된다. 실무에선 코딩을 할 때 `==`보다는 `===`를 추천한다. 의미 그대로 엄격한 비교를 통해 에러를 줄이려는 의도가 아닐까 하는 추측을 해본다.









