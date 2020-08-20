# 📝 Table of Contents

# JS

- [JS-OOP](#OOP)
- [JS-Immutability](#Immutability)
- [REACT](#REACT)

* [NPM](#NPM)

* [궁금했던 것들](#Question-Mark)

---

# OOP

- [생활코딩 OOP 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMAMctarDlPyv6upFUUnpSO3)

[Top](#JS)

---

## 1. 수업소개

- **객체(Object)**

  - 서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것

[Top](#JS)

---

## 2. 실습준비

- **NodeJS 사용**

  - 터미널에 값을 쉽게 확인하기 위해

[Top](#JS)

---

## 3.1 객체의 기본

- **배열 [ ]**

```javascript
let arr = ['A', 'B', 'C']
console.log(arr[1]) // B
```

- **객체 { }**

  - 키와 값으로 이루어져 이름이 있는 값을 다룬다

```javascript
let obj = {
  A: '1',
  B: '2',
  C: '3',
  D: '4',
}
👉obj.C = '4' // 변경
👉delete obj.D // 삭제
console.log(obj.A) // 1
👉console.log(obj['B']) // 2
console.log(obj['C']) // 4
👉console.log(obj.D) // undefiend
```

[Top](#JS)

---

## 3.2 객체와 반복문

- **배열 반복문**

```javascript
let arr = ['A', 'B', 'C', 'D']

let i = 0
while (i < arr.length) {
  console.log(arr[i])
  i++
} // A B C D
```

- **객체 반복문**

```javascript
let obj = {
  A: '1',
  B: '2',
  C: '3',
  D: '4',
}

for (let name 👉in obj) {
  console.log(name) // A B C D
  👉console.log(obj.name) // undefined
  👉console.log(obj[name]) // 1 2 3 4
}
```

- **팁 : console.log의 값을 보기 편하게**

```javascript
console.group('값')
// 원하는 출력
console.groupEnd('값')
```

[Top](#JS)

---

## 4.1 객체는 언제 쓰나요?

- **이미 내장된 객체 사용해보기**

  - `Math.PI` , `Math.random()` : 2가지 형태

[Top](#JS)

---

## 4.2 객체 만들어 보기

- **나만의 객체 만들기**

```javascript
let MyMath = {
  PI: Math.PI,
  random: function () {
    return Math.random()
  },
}
```

- **function(함수)**

- **method(메소드) = 객체 안에 있는 function(함수)**

[Top](#JS)

---

## 5. this

- **this는 메소드가 자신이 속해있는 객체를 가리킨다.**

```javascript
👉// 3. 객체(kim)을 가리킨다
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  👉// 2. 메소드(sum)가 자식이 속해있는
  sum: function () {
    👉// 1. this는
    return this.first + this.second
  }
}
```

[Top](#JS)

---

## 6.1 constructor의 필요성

- **목표**

  - 객체를 찍어낼 수 있다.

[Top](#JS)

---

## 6.2 constructor의 사례

- **두 객체의 차이점**

  - 설계도가 노출이 되지 않는다.
  - 코드가 깔끔하다.
  - 많은 객체를 자동으로 다르게 생산할 수 있다.

```javascript
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  sum: function () {
    return this.first + this.second
  },
}
```

`var d1 = new Date('2019-04-10');`

[Top](#JS)

---

## 6.3 constructor 만들기

- **constructor의 장점**

  - 내용이 변경될때마다 객체를 다시 정의할 필요가 없다.

- **기존 코드**

```javascript
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  sum: function () {
    return this.first + this.second
  },
}
```

- **생성**
  - 단순히 함수 호출은 리턴값이 없기 때문에 `undefined`
  - new를 붙여주면 새로운 객체가 생성되는 생성자가 된다.
  - this는 호출된 객체를 가리킨다.

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
  this.sum = function () {
    return this.first + this.second
  }
}
👉console.log(Person()) // undefined
👉console.log(new Person()) // Person {
  name: undefined,
  first: undefined,
  second: undefined,
  sum: [Function]
}
let lee = new Person('lee', 10, 20)
console.log(lee.sum()) // 30
```

[Top](#JS)

---

## 7.1 prototype이 필요한 이유

- **이유**

  - 객체가 생성될 때마다 객체의 함수를 생성해서 메모리 낭비
  - 객체를 사용하는 모든 함수를 바꾸고 싶을때

- **그래서**
  - 생성자를 이용해서 만든 객체가 **공통적으로 사용**하는 함수나 속성을 만들고 싶다!

[Top](#JS)

---

## 7.2 prototype을 이용해서 재사용성을 높이기

- **장점**

  - 한번만 실행이 되어 메모리, 성능 절약
  - 모든 객체가 공통적으로 사용하고 있어 변경이 용이하다.
  - 객체의 함수를 재정의 할 수 있다.

- **객체호출 우선순위**
  - 자신의 객체(kim) > 객체를 만든 생성자(Person) > 프로토타입

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}

👉Person.prototype.sum = function () {
  return this.first + this.second
}

let kim = new Person('kim', 20, 10)
kim.sum = function () {
  return this.first - this.second
}
let lee = new Person('lee', 10, 30)
console.log(kim.sum()) // 10
console.log(lee.sum()) // 40
```

[Top](#JS)

---

## 8.1 Classes

- **객체를 만드는 공장**

- **ES6부터 지원**

  - [문법 지원 사이트](https://caniuse.com)

- **ES6 이전 버전은?**
  - [바벨](https://babeljs.io) 사용

[Top](#JS)

---

## 8.2 Classes의 생성

- **객체를 생성한다.**

```javascript
class Person{

}
let kim = new Person()
console.log(kim) 👉// Person {}
```

[Top](#JS)

---

## 9. class의 constructor function

- **constructor 함수**
  - 객체를 생성하기 전에 초기화하는 역할
  - class 내부가 초기화 된후 객체가 생성된다.

```javascript
class Person {
  constructor() {
    console.log('constructor') 👉// 1.constructor
  }
}
let kim = new Person()
console.log(kim) 👉// 2. Person {}
```

- **constructor 값 넣기**

```javascript
class Person {
  constructor(name, first, second) {
    this.name = name
    this.first = first
    this.second = second
  }
}

let kim = new Person('kim', 20, 10)
console.log(kim) 👉// Person { name: 'kim', first: 20, second: 10 }
```

[Top](#JS)

---

## 10. 메소드 구현

- **아래 2개의 코드는 같다.**

- **constructor 이용**

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}

Person.prototype.sum = function () {
  return this.first + this.second
}

let kim = new Person('kim', 20, 10)
kim.sum = function () {
  return this.first - this.second
}
let lee = new Person('lee', 10, 30)
console.log(kim.sum()) // 10
console.log(lee.sum()) // 40
```

- **class 이용**

```javascript
class Person {
  constructor(name, first, second) {
    this.name = name
    this.first = first
    this.second = second
  }
  sum = function () {
    return this.first + this.second
  }
}

let kim = new Person('kim', 20, 10)
kim.sum = function () {
  return this.first - this.second
}
let lee = new Person('lee', 10, 30)
console.log(kim.sum()) // 10
console.log(lee.sum()) // 40
```

[Top](#JS)

---

## 11. 상속

- **목표**

  - 정의된 객체를 변경하지 않고 새로운 함수를 추가하고 싶다.

- **사용 이유**

  - 정의된 객체를 변경해서 사용할 수 없는 경우
  - 중복을 제거하기 위해서

- **avg()를 추가하고 싶을 때**

```javascript
class Person {
  constructor(name, first, second) {
    this.name = name
    this.first = first
    this.second = second
  }
  sum = function () {
    return this.first + this.second
  }
}

👉class PersonPlus extends Person {
  avg() {
    return (this.first + this.second) / 2
  }
}

let kim = new 👉PersonPlus('kim', 20, 10)
console.log(kim.avg()) // 15
```

[Top](#JS)

---

## 12. super

- **상속의 문제점**

  - 부모클래스와 자식클래스와의 관계

- **해결**

  - super로 부모클래스의 기능을 실현할 수 있다.

- **super의 2가지 기능**

  - `super(부모클래스의 생성자)`
  - `super.sum()`은 `부모클래스.sum()`

- **sum()의 파라마터 thrid를 추가하고 싶을 때**

```javascript
class Person {
  constructor(name, first, second) {
    this.name = name
    this.first = first
    this.second = second
  }
  👉// Person class의 sum()은 소속된 객체의 소속이 아니고 prototype객체에 소속이 되어 공유가 된다.
  sum = function () {
    return this.first + this.second
  }
}

class PersonPlus extends Person {
  constructor(name, first, second, 👉third) {
    👉super(name, first, second) // 부모의 constructor를 실행
    👉this.third = third
  }
  sum() {
    return super.sum() + this.thrid 👉// super.sum() == this.first+this.second
  }
  avg() {
    return (this.first + this.second) / 2
  }
}

let kim = new PersonPlus('kim', 20, 10, 30)
console.log(kim.sum()) // 30
```

[Top](#JS)

---

## 13.1 object inheritance

- **객체지향 프로그래밍 2가지 요소**

  - Class : 공장
  - Object(instance) : 결과

- **주류 객체지향 언어의 상속**

  - super class(부모) -> sub class(자식) -> object
  - object의 기능은 class에서 결정

- **자바스크립트의 상속**
  - 자바스크립트는 프로토타입을 베이스로 한다.
  - suepr object -> sub object
  - prototype link를 통해 어떤 object든 상속 받을 수 있다.
  - prototype link를 통해 연결된 `super object`는 `prototype object`라고 부른다.

[Top](#JS)

---

## 13.2 **proto**

- **목표**

  - prototype object로 상속 구현(수작업)

- **상속구현**

  - 원형(부모)이 무엇인지 알려주는 prototype link 지정 방법 `subObj.__proto__ = superObj`

  - `superObj`는 부모, `subObj`는 자식

  - 순서 : 자신객체 > 부모객체

  - 자식이 부모객체를 바꿀순 없다.

```javascript
let superObj = { superVal: 'super' }
let subObj = { subVal: 'sub' }
👉subObj.__proto__ = superObj
console.log(subObj.superVal) // super

👉subObj.superVal = 'sub'
console.log(superObj.superVal) // super
```

[Top](#JS)

---

## 13.3 Object.create()

- \***\*proto**보다 더 좋은 방법이지만 수작업\*\*

- **새로운 객체를 생성**

- **결론**
  - `subObj.__proto__ === superObj // true`

```javascript
let superObj = { superVal: 'super' }
👉let = subObj = Object.create(superObj)
subObj.subVal = 'sub'
👉debugger
console.log(subObj.superVal) // super

subObj.superVal = 'sub'
console.log(superObj.superVal) // super

```

- **디버깅 방법**
  - HTML과 Javascript를 연결
  - JavaScript의 보고싶은 코드 하단에 `debugger`
  - 웹에서 HTML을 열고 개발자 도구를 열고 리로드
  - `Souces` 탭에서 결과 확인
  - `Watch`는 찾기 기능

[Top](#JS)

---

## 13.4 객체상속의 사용

- \***\*proto\*\*** 사용

```javascript
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  sum: function () {
    return this.first + this.second
  },
}
var lee = {
  name: 'lee',
  first: 10,
  second: 10,
  avg: function () {
    return (this.first + this.second) / 2
  },
}
lee.__proto__ = kim
console.log(lee.sum()) // 20
console.log(lee.avg()) // 10
```

- **Object.create()** 사용

```javascript
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  sum: function () {
    return this.first + this.second
  },
}
let lee = Object.create(kim)
lee.name = 'lee'
lee.first = 10
lee.second = 10
lee.avg = function () {
  return (this.first + this.second) / 2
}
console.log(lee.sum()) // 20
console.log(lee.avg()) // 10
```

[Top](#JS)

---

## 14.1 객체와 함수

- **함수도 객체다.**

[Top](#JS)

---

## 14.2 call

- **호출할 때 this값의 컨텍스트를 바꾼다.**

  - apply와 유사

- **NaN의 이유**
  - 값이 없기 때문에

```javascript
let kim = { name: 'kim', first: 10, second: 20 }
let lee = { name: 'lee', first: 10, second: 10 }
function sum(str) {
  return str + (this.first + this.second)
}
console.log(sum('Kim : ')) // Kim : NaN
console.log(sum.call('Kim : ')) // NaN
👉console.log(sum.call(kim, 'Kim : ')) // Kim : 30
👉console.log(sum.call(lee, 'Lee : ')) // Lee : 20
```

[Top](#JS)

---

## 14.3 bind

- **this의 값을 영구적으로 바꾸는 새로운 함수를 만들어 낸다.**
  - 기존의 함수는 영향을 받지 않는다.

```javascript
let kim = { name: 'kim', first: 10, second: 20 }
function sum(str) {
  return str + (this.first + this.second)
}
👉let kimSum = sum.bind(kim, 'kimSum : ')
console.log(kimSum()) // kimSum : 30
```

[Top](#JS)

---

## 15. prototype vs proto

- **함수는 객체다!**

  - `function Person(){}` === `var Person = new Function();`

- **Person 함수를 생성할 때**
  - `Person`객체와 `Person's prototype`객체가 생긴다.

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}
```

- \*\* **`Person`객체가 생성된다.**

  - `Person.prototype === Person's prototype`
  - 내부적으로 `prototype 프로퍼티`가 생성되고 `Person's prototype`객체를 가르킨다.

- **`Person's prototype`객체가 생긴다.**

  - 내부적으로 `constructor`프로퍼티가 생성되고 `Person`객체를 가르킨다.

- **`Person.prototype.sum = function(){}`이 생성될 때**

  - `Person's prototype`객체 내부에 `sum`함수가 정의된다.

- **생성자를 통해 객체를 만들 때**

  - `var kim = new Person('kim', 10, 20)
  - `kim`객체 안에 `__proto__`, `name`, `first`, `second` 프로퍼티가 생성된다.
  - `__proto__`는 자신을 생성한 `Person's prototype`객체를 가리킨다.

- **출력할 때** -`console.log(kim.name)`

  - `kim` 객체에서 `name` 프로퍼티를 찾는다.
  - 만약에 없다면 `__proto`가 가리키고 있는 `Person's prototype`에서 `name`을 찾는다.

- **함수를 호출할 때**
  - `kim.sum()`
  - `kim`객체에서 `sum`함수를 찾는다.
  - 만약에 없다면 `__proto`가 가리키고 있는 `Person's prototype`에서 `sum`을 찾는다.

[Top](#JS)

---

# Immutability

- [생활코딩 Immutability 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMBxNK38TqfBWk-QpEI7UkY8)

[Top](#JS)

---

# REACT

- [생활코딩 리액트 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCRv6f8H9K5Xwsdyg4sFSdi)

[Top](#JS)

---

## 1. 수업소개

- **Component**

  - 정리해 놓은 박스 (일종의 클래스)

- **특징**
  - 가독성
  - 재사용성
  - 유지보수

[Top](#JS)

---

## 2. 공부전략

- **CODING - RUN - DEPLOY**

[Top](#JS)

---

## 3. 개발환경의 종류

- **Online Playgrounds**

  - ex) CodeSandbox

- **Add React to a Website**

  - 웹사이트에 부분적으로 사용할때

- **Create a New React App**

  - Toolchain
  - ex) Create React App, Next.js, Gastby

- [리액트 공식문서](https://reactjs.org/docs/getting-started.html)

[Top](#JS)

---

## 4. npm을 이용해서 create react app 설치

- **npm**

  - 플레이스토어와 같은 앱을 쉽게 설치할 수 있게 해주는 공간
  - nodeJS를 통해 설치

- **npm 설치확인**
  - `npm -v`

[Top](#JS)

---

## 5. create react app을 이용해서 개발환경구축

- **리액트 설치**

  - `npx create-react-app .`

- **리액트 설치 확인**
  `create-react-app -v`

[Top](#JS)

---

## 6. 샘플 웹앱 실행

- **리액트 실행**

  - `npm run start`

[Top](#JS)

---

## 7. JS 코딩하는 법

- **public**

  - 첫 화면을 담당하며 `index.html` 이 있는 곳
  - 구조 : `<div id="root">`, `<div class="App">`, 실제구현은 App.js에서 한다.

- **src**

  - 실제 구현을 하는 곳
  - `index.js` : `index.html`과 App Component(App.js에서 구현, 사용자 정의태그)의 진입파일

- **Component Type**
  - Class Type

```javascript
// class type(App.js)
import React, 👉{ Component } from 'react'
import './App.css'

👉class App extends Component {
  render() {
    return (
      <div className="App">

      </div>
    );
  }
}

export default App
```

- **Function Type**

```javascript
// function type(App.js)
import React from 'react'
import './App.css'

👉function App() {
  return (
    <div className="App">

    </div>
  );
}

export default App
```

[Top](#JS)

---

## 8. CSS 코딩하는 법

- **`import './index.css';` : 가져오고 싶은 루트**

- **`App.css`와 `index.css` 코드 모두 제거**

[Top](#JS)

---

## 9. 배포하는 법

- **`npm run build`**

  - 실제 서비스를 할 때 build 폴더안에 있는 것을 사용하면 됨

- **`npx serve -s build`**

  - build를 root로 하여 실제 서비스를 배포
  - 용량비교 : 개발환경(1.7MB), 배포(125KB)

[Top](#JS)

---

## 10. 리액트가 없다면

- **상상**

  - pure.html의 header, nav, ariticle이 각각 1억줄씩이라면..
  - 1억줄의 태그를 하나의 의미있는 태그로 나타낼수 있다면..
  - 여기서 탄생한것이 컴포넌트

[Top](#JS)

---

## 11. 컴포넌트 만들기

- **`pure.html`의 `<header>`, `<nav>`, `<ariticle>`를 `App.js`의 `<Subject>`, `<TOC>`, `<Content>`로**

  - 반드시 **하나의 최상위 태그**로 감싸져야 됨

  - **JSX 문법**을 사용하며 Javascript로 컨버팅 된다.

```javascript
// pure.html
<html>
  <body>
    👉
    <header>
      <h1>WEB</h1>
      world wide web!
    </header>
  </body>
</html>
```

```javascript
// App.js
import React, { Component } from 'react'
import './App.css'

👉class Subject extends Component {
  render() {
    return (
      <header>
        <h1>WEB</h1>
        world wide web!
      </header>
    )
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        👉<Subject></Subject>
      </div>
    )
  }
}

export default App
```

[Top](#JS)

---

## 12. props

- **정적인 사용자 태그의 내용을 부분적으로 바꾸고 싶을때**
- **Component의 속성(Attribute)을 표현**

- [리액트 공식문서](https://reactjs.org/docs/components-and-props.html)
  <br>

- **적용전**

```javascript
// App.js
class Subject extends Component {
  render() {
    return (
      <header>
        <h1>👉WEB</h1>
        👉world wide web!
      </header>
    )
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject></Subject>
      </div>
    )
  }
}
```

- **적용 후**

```javascript
// App.js

class Subject extends Component {
  render() {
    return (
      <header>
        👉// title props 사용
        <h1>👉{this.props.title}</h1>
        👉{this.props.sub}
      </header>
    )
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject 👉title="WEB" 👉sub="world wide web!"></Subject>
      </div>
    )
  }
}
```

[Top](#JS)

---

## 13. React Developer Tools

- **스스로 무언가를 할 수 있기 위하여**

  - 설명서를 볼줄 아는 것
  - 현재의 상태를 측정하고 분석할 줄 아는 것

- **설치**

  - [크롬 웹 스토어 - React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko)

- **왜?**

  - 개발자 도구에서 리액트의 컴포넌트를 보고 싶을 경우

- **사용**
  - 개발자 도구의 Components 탭

[Top](#JS)

---

## 14. Component 파일로 분리하기

- **컴포넌트들을 `src/components` 폴더에 분리**
  - Subject.js
  - TOC.js
  - Content.js

```javascript
// App.js

import React, { Component } from 'react'
👉// Subject는 클래스 이름을 나타냄
import 👉Subject from './components/Subject'
import './App.css'

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject title="WEB" sub="world wide web!"></Subject>
        <TOC></TOC>
        <Content
          title="HTML"
          desc="HTML is HyperText Markup Language."
        ></Content>
      </div>
    )
  }
}

export default App
```

```javascript
👉// components/Subject.js

👉// { Component } : extends에서 사용되고 있는 Component 클래스를 로딩하는 코드
import React, 👉{ Component } from 'react'

class Subject extends Component {
  render() {
    return (
      <header>
        <h1>{this.props.title}</h1>
        {this.props.sub}
      </header>
    )
  }
}

// 👉해당 클래스(SUbject)를 외부에서 가져다가 사용할 수 있게 하기 위해서
export default Subject
```

[Top](#JS)

---

## 15.1 State 소개

- **State의 목적**

  - 사용자와 구현자를 완벽히 분리해 서로의 편의성을 도모

- **Props**

  - 사용자가 Component를 사용할 때 중요

- **State**
  - props에 값에 따라 내부에 구현에 필요한 데이터들

[Top](#JS)

---

## 15.2 State 사용

- render 함수보다 먼저 실행이 되면서 그 컴포넌트를 **초기화**시키고 싶은 코드는 `super()` 밑에 넣으면 된다.
- `index.js`에서는 사용하고 있는 App.js Component의 state값을 알 수 없다.
- props인 subject를 state 화

```javascript
class App extends Component {
    // render 함수보다 먼저 실행이 되면서 그 컴포넌트를 초기화시키고 싶은 코드는 super 밑에 넣으면 된다.
    👉constructor(props) {
    👉super(props)
    👉this.state = {
      subject: { title: 'WEB', sub: 'world wide web!' },
    }
  }
  render() {
    return (
      <div className="App">
        <Subject
          // this는 클래스의 App를 가리키고 있음
          👉title={this.state.subject.title}
          👉sub={this.state.subject.sub}
        ></Subject>
      </div>
    )
  }
}
```

[Top](#JS)

---

## 15.3 key

- **props의 여러개의 값을 다룰때 사용**

  - 참고 : contents는 props

```javascript
// App.js
class App extends Component {
  👉// 부모 : App
  constructor(props) {
    super(props)
    this.state = {
      👉// contens는 props
      contens: [
        { id: 1, title: 'HTML', desc: 'HTML is for information' },
        { id: 2, title: 'CSS', desc: 'CSS is for design' },
        { id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive' },
      ],
    }
  }
  render() {
    return (
      <div className="App">
        👉// 위에 정의한 state의 contents를 사용
        👉// TOC는 data를 사용
        <TOC 👉data={this.state.contens}></TOC>
      </div>
    )
  }
}


//TOC.js
class TOC extends Component {
  👉// 자식 : TOC
  render() {
    var lists = []
    👉// App Component의 data를 사용
    var data = this.props.data
    var i = 0
    while (i < data.length) {
      lists.push(
        <li key={data[i].id}>
          <a href={'/content/' + data[i].id}>{data[i].title}</a>
        </li>
      )
      i = i + 1
    }
    return (
      // 중요하지 않아서 생략
  }
}

```

[Top](#JS)

---

## 16.1 이벤트 state props 그리고 render 함수

- **목표**

  - Content의 mode가 'welcome'이면 ~ 출력
  - 'read'이면 ~출력
  - 그 외는 아무것도 출력이 안된다. Content의 attribute인 title에 아무값도 들어있지 않기 때문

- **props나 state의 값이 바뀔 때 render 함수 하위에 있는 컴포넌트들도 다시 그려진다.**

  - App -> Subject -> TOC -> Content

- **State 설정**

```javascript
// App.js

class App extends Component {
  👉constructor(props) {
    super(props)
    this.state = {
      👉mode: 'welcome',
      👉welcome: { title: 'Welcome', desc: 'Hello, React!!' },
      contents: [
        { id: 1, title: 'HTML', desc: 'HTML is for information' },
        { id: 2, title: 'CSS', desc: 'CSS is for design' },
        { id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive' },
      ],
    }
  }
  👉render() {
    var _title,
      _desc = null
    if (this.state.mode === 'welcome') {
      _title = this.state.welcome.title
      _desc = this.state.welcome.desc
    } else if (this.state.mode === 'read') {
      _title = this.state.contents[0].title
      _desc = this.state.contents[0].desc
    }
    👉return (
      <div className="App">
        <Content title=👉{_title} desc=👉{_desc}></Content>
      </div>
    )
  }
}

// Content.js
class Content extends Component {
  render() {
    return (
      <article>
        <h2>👉{this.props.title}</h2>
        👉{this.props.desc}
      </article>
    )
  }
}
```

[Top](#JS)

---

## 16.2 이벤트 설치

- **목표**

  - Subject의 anchor 태그를 클릭했을 때 어떤 자바스크립트가 실행될 수 있게 하기

- **문제**

  - 이벤트(onClick)가 발생할 때 새로고침이 되버린다.

- **디버거 사용**

  - debugger 코드를 만나면 실행이 정지
  - 개발자 도구의 Sources에서 다양한 정보를 볼 수 있다.

- **해결**
- 이벤트(onClick 함수)의 파라미터로 객체 e를 넣고 `e.preventDefault()`를 실행하면 된다.

```javascript
// App.js

class App extends Component {
  // 생략
  }
  render() {
    // 생략
    }
    return (
      <div className="App">
        {/* <Subject
          title={this.state.subject.title}
          sub={this.state.subject.sub}
        ></Subject> */}
        <header>
          <h1>
            <a
              href="/"
              👉onClick={function (e) {
                e.preventDefault()
              }}
            >
              {this.state.subject.title}
            </a>
          </h1>
          {this.state.subject.sub}
        </header>
      </div>
    )
  }
}
```

[Top](#JS)

---

## 16.3 이벤트에서 state 변경하기

- **목표**

  - header의 anchor태그를 클릭했을 때 App 컴포넌트 State의 mode 값을 'welcome'으로 변경하기

- **`this.state.mode = 'welcome'` 코드의 2가지의 문제**

  - 이벤트가 실행되는 함수안의 this는 아무값도 가리키고 있지 않다.
  - 리액트는 state의 값이 바뀐지 모른다.

- **해결**

  - 이벤트함수가 끝나는 지점에 .bind(this)를 붙여주면 this는 자신의 컴포넌트를 가리키게 된다.
  - 바뀐 state값을 알도록 `this.setState({mode: 'welcome'})`으로 바꾸어준다.

- **자세한 설명**
  - 강의 16.4 이벤트 bind 함수 이해하기
  - 강의 16.5 이벤트 setState 함수 이해하기

```javascript
// App.js

class App extends Component {
  // 생략
  }
  render() {
    // 생략
    }
    return (
      <div className="App">
        {/* <Subject
          title={this.state.subject.title}
          sub={this.state.subject.sub}
        ></Subject> */}
        <header>
          <h1>
            <a
              href="/"
              onClick={function (e) {
                e.preventDefault()
                👉this.setState({
                  mode: 'welcome',
                })
              }👉.bind(this)}
            >
              {this.state.subject.title}
            </a>
          </h1>
          {this.state.subject.sub}
        </header>
      </div>
    )
  }
}
```

[Top](#JS)

## 16.4 이벤트 bind 함수 이해하기

- **문제**

  - render 함수안의 this는 render 함수가 속해있는 컴포넌트를 가르킨다.
  - 함수 안의 this는 아무것도 가리키고 있지 않다 = undefined

- **그래서**
- this의 값을 강제로 주입하고 싶다.

- **목표**
  - bindTest 함수의 this가 obj 객체를 가리키게 하고 싶다.

```javascript
var obj = {name: 'egoing'};
function bindTest(){
    console.log(this.name);
}
👉bindTest() // undefined

var bindTest2 = 👉bindTest.bind(obj);
bindTest2(); // 'egoing'이 출력되며 새로운 함수가 만들어 진다.
```

---

## 16.5 이벤트 setState 함수 이해하기

- **생성자 constructor 함수에서는 state값을 다음과 같이 변경해도 되지만**

```javascript
constructor(props) {
  super(props);
  this.state = {
    mode: 'read'
   }
```

- **컴포넌트 생성이 끝난 후 동적으로 state값을 변경하고 싶을 때는<br>`this.state.mode = 'welcome' 이 아닌 'this.setState({mode: 'welcome'})로 변경해야 한다.**

- **이유**
  - 리액트가 state 값의 변화를 인지못하여 렌더링을 하지 못한다.

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

[Top](#JS)

---

# NPM

- [생활코딩 NPM1 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCwEXgZ-dep4SJlGEuYip-6)

[Top](#JS)

---

## 1. 수업 소개

- **NPM (Node Package Manager)**
  - CLI를 기반으로 동작
  - 앱스토어와 유사
  - 다른 소프트웨어에 부품으로 사용

[Top](#JS)

---

## 2. npm 설치

- **NodeJS를 설치하면 npm도 설치가 된다.**

  - LTS : 안정적인 버전
  - Current : 최신 버전

- **설치확인**
  - `node -v` , `npm -v`

[Top](#JS)

---

## 3. 패키지 검색과 설치 그리고 실행

- [npm 검색 사이트](https://www.npmjs.com)

- **검색**

  - 원하는 패키지 검색 ex) web server
  - 인기도 확인 (p)
  - CLI이 지원하는지 찾기(Ctrl+F)를 통해 확인

- **설치**

  - install 부분의 설치방법 확인
  - 커맨드라인을 이용하여 설치

- **실행**

  - 커맨드라인에서 ex) `ws`

- **종료**
  - Ctrl+C

[Top](#JS)

---

## 4. 패키지의 목록 보기와 업데이트 그리고 삭제

- **패키지 목록 보기**

  - `npm`
  - `npm list`, `npm list -g`
  - 직접 설치한 패키지만 보기 `npm list -g --depth=0`

- **업데이트**

  - `npm update -g 패키지명`

- **삭제**
  - `npm uninstall -g 패키지명`

[Top](#JS)

---

# Question Mark

[Top](#JS)

---

## 라이브러리 vs 프레임워크

- **생산자로서의 소비자**

  - 소프트웨어의 사회성

- **공통점**

  - 남의 도움을 받아 소프트웨어를 개발

- **라이브러리**

  - 잘 정리정돈 된 부품

- **프레임워크**
  - 공통적인 부분을 가진 프레임워크 외에 개발
  - 반제품

[Top](#JS)

---

## UI vs API

- **UI (User Interface)**

  - **사용자**가 시스템을 제어하기 위해서 사용하는 조작장치
  - ex) 버튼을 누르면 경고창이 뜬다.

- **API (Application Programming Interface)**
  - 앱을 만들기 위해서 프로그래밍을 할 때 사용되는 조작장치
  - ex) alert 함수
  - 순서와 API의 관계

[Top](#JS)

---

## 검색 팁

- **document 객체**

  - 태그 삭제나 자식태그 삽입하고 싶을 때

- **DOM 객체**

  - document에서 찾을 수 없을 때

- **window 객체**

  - 웹브라우저 자체를 제어하고 싶을 때

- **ajax**

  - 웹페이지를 리로드하지 않고 변경하고 싶을 때

- **cookie**

  - 웹페이지가 리로드 되어도 현재 상태를 유지하고 싶을 때

- **offline web application**

  - 인터넷이 끊겨도 서비스가 되는 웹페이지를 만들고 싶을 때

- **webRTC**

  - 화상통신 앱을 만들고 싶을 때

- **speech API**

  - 음성으로 정보를 전달하고 싶을 때

- **webGL**

  - 3차원 그래픽으로 게임을 만들고 싶을 때

- **webVR**
  - 가상현실
