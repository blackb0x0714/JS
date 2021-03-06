# 상세내용은 [Velog](https://velog.io/@blackb0x)에 정리하고 있습니다.

# 📝 Table of Contents

# JS

- [CSS](#CSS)

- JavaScript
  - [JS-OOP](#OOP)
  - [JS-Immutability](#Immutability)
  - [Ajax](#Ajax)

  - [REACT](#REACT)
    - [React class와 function style coding](#React-class-function-style-coding)
    - [React Router](#React-Router)
    - [React Redux](#React-Redux)
    - [React Ajax](#React-Ajax)

- [Redux](#Redux)

- [Node.js](#Nodejs)
  - [Express](#Express)

- [DATABASE1](#DATABASE1)
  - [DATABASE2 - MySQL](#MySQL)

- [AWS1](#AWS1)

- [Git1](#Git1)

- [POSIX](#)
  - [NPM1](#NPM)
- [궁금했던 것들](#Question-Mark)

---
# ⭐
# CSS

- [생활코딩 CSS 수업](https://www.youtube.com/watch?v=ONcmkf07EuI&list=PLuHgQVnccGMDaVaBmkX0qfB45R_bYrV62)

[Top](#JS)

---

## 레이아웃 - 인라인 vs 블랙레벨
- html 엘리먼트들은 크게 두가지로 구분된다.
  - `block element` : 화면 전체를 사용하는 태그
  - `inline level element` : 화면의 일부를 차지하는 태그
- `display` 속성

[Top](#JS)

---
# ⭐
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
  
- **prototype ojbect 상속 2가지 방법**
  - `__proto__`
  - `Object.create()`

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

- **`_proto__`보다는 더 좋은 방법**

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

- **`__proto__` 사용**

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
👉lee.__proto__ = kim
console.log(lee.sum()) // 20
console.log(lee.avg()) // 10
```

- **`Object.create()` 사용**

```javascript
let kim = {
  name: 'kim',
  first: 10,
  second: 20,
  sum: function () {
    return this.first + this.second
  },
}
👉let lee = Object.create(kim)
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
console.log(👉sum.call(kim, 'Kim : ')) // Kim : 30
console.log(👉sum.call(lee, 'Lee : ')) // Lee : 20
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

![1](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-1.PNG)

- **Person 함수를 생성할 때**

- **`Person`객체와 `Person's prototype`객체가 생긴다.**

  - **`Person`객체가 생성된다.**

    - `Person.prototype === Person's prototype`
    - 내부적으로 `prototype 프로퍼티`가 생성되고 `Person's prototype`객체를 가르킨다.

  - **`Person's prototype`객체가 생긴다.**
    - 내부적으로 `constructor`프로퍼티가 생성되고 `Person`객체를 가르킨다.
<br><br>
![2](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-2.PNG)

- **Person.prototype.sum = function(){}`이 생성될 때**

  - **`Person's prototype`객체 내부에 `sum`함수가 정의된다.**

<br><br>
![3](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-3.PNG)

- **생성자를 통해 객체를 만들 때-1**
  - `var kim = new Person('kim', 10, 20)
  - `kim`객체 안에 `__proto__`, `name`, `first`, `second` 프로퍼티가 생성된다.
  - `__proto__`는 자신을 생성한 `Person's prototype`객체를 가리킨다.

<br><br>
![4](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-4.PNG)

- **생성자를 통해 객체를 만들 때-2**
  - `var lee = new Person('kim', 10, 10)
  - `lee`객체 안에 `__proto__`, `name`, `first`, `second` 프로퍼티가 생성된다.
  - `__proto__`는 자신을 생성한 `Person's prototype`객체를 가리킨다.

<br><br>
![5](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-5.PNG)

- **출력할 때**
  - `console.log(kim.name)`
  - `kim` 객체에서 `name` 프로퍼티를 찾는다.
  - 만약에 없다면 `__proto`가 가리키고 있는 `Person's prototype`에서 `name`을 찾는다.

<br><br>
![6](https://github.com/blackb0x0714/JS/blob/master/img/OOP-15-6.PNG)

- **함수를 호출할 때**
  - `kim.sum()`
  - `kim`객체에서 `sum`함수를 찾는다.
  - 만약에 없다면 `__proto`가 가리키고 있는 `Person's prototype`에서 `sum`을 찾는다.

[Top](#JS)

---

## 16.1 생성자 함수를 통한 상속 : 소개

- **목표**
  - prototype 통한 상속(`__proto__`, `Object.create()`)
  - 그러나 class를 통한 상속이 더 편하다.

[Top](#JS)

---

## 16.2 생성자 함수를 통한 상속 : 부모 생성자 실행

- **this에 집중**

- **`Person.call(this, name, first, second)`은 부모를 호출했을 뿐 연결은 되지 않았다.**
  - 아래 코드는 실행되지 않는다.

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}
Person.prototype.sum = function () {
  return this.first + this.second
}

function PersonPlus(name, first, second, third) {
  👉Person.call(this, name, first, second)
  this.third = third
}
PersonPlus.prototype.avg = function () {
  return (this.first + this.second + this.third) / 3
}

let kim = new PersonPlus('kim', 10, 20, 30)
console.log(kim.sum())
console.log(kim.avg())
```

[Top](#JS)

---

## 16.3 생성자 함수를 통한 상속 : 부모와 연결하기

![1](https://github.com/blackb0x0714/JS/blob/master/img/OOP-16.3.PNG)

- **현재 상황**

  - `kim.sum()`를 호출했을 때 `PersonPlus's prototype`객체에 없기 때문에<br>`Person's prototype`객체의 `sum`에 연결해줘야 한다.
  - 객체가 생성될때는 항상 `__proto__`가 생성이 되며 그 객체의 prototype을 가르킨다.

- **2가지 방법**
- **prototype을 이용한 연결방법 2가지**
  - `__proto__`는 비표준이다.
  - `Object.create()`를 이용한 연결 : 다음 강의에서 다룬다

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}
Person.prototype.sum = function () {
  return this.first + this.second
}

function PersonPlus(name, first, second, third) {
  Person.call(this, name, first, second)
  this.third = third
}
👉PersonPlus.prototype.__proto__ = Person.prototype

PersonPlus.prototype.avg = function () {
  return (this.first + this.second + this.third) / 3
}

let kim = new PersonPlus('kim', 10, 20, 30)
console.log(kim.sum()) // 60
console.log(kim.avg()) // 20
```

[Top](#JS)

---

## 16.4 생성자 함수를 통한 상속 : constructor 속성은 무엇인가?

![1](https://github.com/blackb0x0714/JS/blob/master/img/OOP-16.4.PNG)

- **constructor의 기능**

  - 어떠한 객체가 누구로부터 만들어졌는지
  - 새로운 객체를 생성

- **Object.create를 이용한 연결**
  - 그러나 아래코드에는 에러가 있다.
  - 👉이해를 더 해봐야겠다.

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}
Person.prototype.sum = function () {
  return this.first + this.second
}

function PersonPlus(name, first, second, third) {
  Person.call(this, name, first, second)
  this.third = third
}
👉PersonPlus.prototype = Object.create(Person.prototype)

PersonPlus.prototype.avg = function () {
  return (this.first + this.second + this.third) / 3
}

let kim = new PersonPlus('kim', 10, 20, 30)
console.log(kim.sum()) // 60
console.log(kim.avg()) // 20
console.log(kim.constructor) 👉/* ƒ Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
} */
```

- **이해해보기**

```javascript
var d = new Date()
Date.prototype.constructor === Date // true
d.constructor // f Date() { [navtive code] }
```

[Top](#JS)

---

## 16.5 생성자 함수를 통한 상속 : constructor 속성 바로잡기

- 👉**코드를 추가해 에러를 해결하는데 좀더 이해를 해봐야겠다.**

- **결론**
  - `__proto__`는 비표준이다.
  - class 상속을 추천

```javascript
function Person(name, first, second) {
  this.name = name
  this.first = first
  this.second = second
}
Person.prototype.sum = function () {
  return this.first + this.second
}

function PersonPlus(name, first, second, third) {
  Person.call(this, name, first, second)
  this.third = third
}
PersonPlus.prototype = Object.create(Person.prototype)
👉PersonPlus.prototype.constructor = PersonPlus

PersonPlus.prototype.avg = function () {
  return (this.first + this.second + this.third) / 3
}

let kim = new PersonPlus('kim', 10, 20, 30)
console.log(kim.sum()) // 60
console.log(kim.avg()) // 20
console.log(kim.constructor) // 👉/* ƒ PersonPlus(name, first, second, third) {
  Person.call(this, name, first, second)
  this.third = third
} */
```

[Top](#JS)

---
# ⭐
# Immutability

- [생활코딩 Immutability 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMBxNK38TqfBWk-QpEI7UkY8)

[Top](#JS)

---

## 1. 수업소개

- **immutability**

  - 데이터의 원본이 훼손되는 것을 막는 것

- **4개의 기본적인 작업**
  - CRUD(Create, Read, Update, Delete)
  - Create, Read이 더 중요하다.

[Top](#JS)

---

## 2. 이름에 대한 불변함 : const vs var

- **목표**

  - 이름(변수)을 불변하게

- **const(상수) 이름을 변경하려고 할 때**
  - `TypeError : Assignment to constant variable.`

[Top](#JS)

---

## 3.0. 변수 할당 방식 비교

- **목표**

  - 값(value)을 불변하게

[Top](#JS)

---

## 3.0. 변수 할당 방식 비교
- **목표**
  - 값(value)을 불변하게

- **`원시데이터 타입`과 `객체 타입`에 따라 동작 방법이 달라진다.**

- **원시데이터 타입(Primitive)**
  - 더 이상 쪼갤 수 없는 최소한의 정보들
  - `Number`, `String`, `Boolean`, `Null`, `Undefined`, `Symbol`

- **객체(Object)**
  - 연관되어 있는 정보를 정리정돈 하는데 사용된다.
  - `Object`, `Array`, `Function`

[Top](#JS)

---

## 3.1. 초기 값의 비교
![1](https://github.com/blackb0x0714/JS/blob/master/img/immutability-3.1.PNG)
- **원시데이터 타입과 객체의 동작 비교**
  - 원시데이터 타입은 불변
  - 객체는 값이 변할 수가 있다.

[Top](#JS)

---

## 3.2. 객체의 가변성
![2](https://github.com/blackb0x0714/JS/blob/master/img/immutability-3.2.PNG)
- **원시데이터 타입**
  - `var p3 = p1`일 때, p3는 1을 가르키다가<br>`var p3 = 2`일 때, 2를 가르킨다.
  
- **객체**
  - `var o3 = o1`일 때, o3는 `{name:'kim'}을 가리키다가<br>`o3.name='lee'`일 때, 값이 `{name:'lee'}`로 바뀐다.
  - 문제점 : o1은 원래 `{name:'kim'}을 가리키고 있었는데, 값이 `{name:'lee'}`로 바뀌었다.

[Top](#JS)

---

## 3.3. 객체의 복사
![3](https://github.com/blackb0x0714/JS/blob/master/img/immutability-3.3.PNG)
- **목표**
  - 객체의 원본을 건드리지 않고 자신만의 데이터를 가리키고 싶다.
  - 객체의 불변

- **객체의 복사**
  - `Object.assign({}, o1)`
    - {} : 리턴이 될 객체
    - o1이 가지고 있는 값을 복사

[Top](#JS)

---

## 3.4. 중첩된 객체의 복사
- **문제점**
  - 객체를 복제할 때 프로퍼티의 값이 객체인 경우 그 값을 복제하는게 아니라 그 주소를 복제한다.
![4-1](https://github.com/blackb0x0714/JS/blob/master/img/immutability-3.4.1.PNG)

- **해결**
  - `concat()` 사용한다.
![4-2](https://github.com/blackb0x0714/JS/blob/master/img/immutability-3.4.2.PNG)

[Top](#JS)

---

## 4. 불변의 함수 만들기
- **목표**

  - 아래의 코드의 함수가 변하지 않게 만들기
  - `function fn(person){person.name = 'lee'}` == `var person =o1` `person.name = 'lee'`

```javascript
function fn(person) {
  person.name = 'lee'
}
👉var o1 = { name: 'kim' } // 원본
fn(o1)
console.log(o1) // 👉{ name: 'lee' } // 바뀌어버림
```
- **방법-1**

  - 원본 `person`을 복제해서 그 복제본 `person`을 리턴
```javascript
function fn(person) {
  👉person = Object.assign({}, person)
  person.name = 'lee'
  👉return person
}
var o1 = { name: 'kim' }
var o2 = fn(o1)
console.log(o1, o2) // { name: 'kim' } { name: 'lee' }
```
- **방법-2**

  - `o2`에 복제본을 생성
```javasscript
function fn(person) {
  person.name = 'lee'
}
var o1 = { name: 'kim' }
👉var o2 = Object.assign({}, o1)
👉fn(o2)
console.log(o1, o2) //  { name: 'kim' } { name: 'lee' }
```

[Top](#JS)

---

## 5. 가변과 불변 API 비교
- **원본의 가변과 불변**

- **가변**

  - 복제과정이 없기 때문에 성능이 빠르다.
```javascript
let score = [1, 2, 3]
👉score.push(4)
console.log(score) // [ 1, 2, 3, 4 ]
```
- **불변**

  - 복제과정 때문에 성능이 느리다.
```javascript
let score = [1, 2, 3]
let score2 = 👉score.concat(4)
console.log(score, score2) // [ 1, 2, 3 ] [ 1, 2, 3, 4 ]
```

[Top](#JS)

---

## 6. Object freeze로 객체를 불변하게 만들기
- **`Object.freeze`**

  - 객체 자체를 변경하지 못하게 만든다.
  - 그 객체를 사용하고 싶으면 복제해서 사용해야 한다.
  - 프로퍼티의 객체를 규제할 순 없다.
  - 프로퍼티의 객체도 얼려버리면 된다.
```javascript
let o1 = { name: 'kim', score: [1, 2] }
👉Object.freeze(o1)
👉Object.freeze(o1.score)
o1.name = 'lee'
o1.city = 'seoul'
o1.score.push(3)
console.log(o1) // Error
```

[Top](#JS)

---

## 7. const vs object freeze
![7](https://github.com/blackb0x0714/JS/blob/master/img/Immutability-7.PNG)
- **차이점**

  - `const`는 `이름`이 가리키는 값을 다른 것으로 바꾸지 못하게 한다.
  - `Object.freeze`는 `값` 자체를 바꾸지 못하게 한다.
```javascript
// const : 이름을 규제
👉const o1 = { name: 'kim' }
Object.freeze(o1)
const o2 = { name: 'lee' }
o1 = o2
console.log(o1) // 👉Error

👉let o1 = { name: 'kim' }
Object.freeze(o1)
const o2 = { name: 'lee' }
o1 = o2
console.log(o1) // 👉{ name: 'lee' }

// freeze : 값을 규제
let o1 = { name: 'kim' }
Object.freeze(o1)
const o2 = { name: 'lee' }
o1.name = 'park'
console.log(o1) // 👉{ name: 'kim' }
```

## 8. 수업을 마치며
- **살펴봐야  것**

  - `functional programing` : pure function
  - `Library` : immer, mori
  - `React` : 이전 데이터와 현재 데이터를 비교해서 렌더링

[Top](#JS)

---
# ⭐
# Ajax

- [생활코딩 Ajax 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMA9-1PvblBehoGg7Pu1lg6q)
- [생활코딩 Ajax 소스코드](https://github.com/web-n/web3-ajax)
[Top](#JS)

---

## 1. 수업소개
- **웹페이지의 정보를 부분적으로 변경**

[Top](#JS)

---

## 2. 수업의 목적
- **고정되는 부분과 바뀔 수 있는 부분을 구분**

[Top](#JS)

---

## 3. 실습환경
- **서버통신**

  - NodeJS Express 사용
```node
const express = require('express')
const path = require('path')
const app = express()
app.use(express.static(path.join(__dirname)))

app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'index.html'))
})

app.get('/1', (req, res) => {
  res.sendFile(path.join(__dirname, '1.html'))
})

app.get('/2', (req, res) => {
  res.sendFile(path.join(__dirname, '2.html'))
})

app.get('/3', (req, res) => {
  res.sendFile(path.join(__dirname, '3.html'))
})

app.listen(3000, () => {
  console.log('Express App on port 3000!')
})
```

[Top](#JS)

---

## 4. 동적으로 컨텐츠 변경하기
- **목표**
  - list의 Anchor 태그를 클릭했을 때 그에 맞는 본문을 보여주고 싶다.

- **타게팅 방법**
  - 부분적으로 바꾸고 싶은 부분에 태그 설정 `<article>`
  - 이벤트 설정 `onclick`
  - 태그를 찾은 후 `innerHTML = '내용'`

- **문제**
  - 모든 내용이 하나의 html에 문서 안에 있다.

- **바뀔 부분의 html을 별도로 관리하고 싶다**

```html
// index.html 변경전
<li><a href="1.html">HTML</a></li>
  <h2>WEB</h2>The World Wide Web...

// index.html 변경후
<li>
  <a 👉onclick="document.querySelector('article').innerHTML = '<h2>WEB</h2>The World Wide Web'">
    HTML</a>
</li>
<ariticle>👉</ariticle>
```

[Top](#JS)

---

## 5.0. fetch API-사용법
- **코드를 이해하자**
  - `fetch`를 통해 `html`파일을 서버에게 요청한다.
  - 서버 응답이 끝나면 데이터는 변수 `text`에 들어가 있다.
  - 호출되도록 약속이 된 `document.querySelector('article').innerHTML = text`가 실행된다.
  - `<article>` 태그 안에 `text`의 내용이 보여지게 된다.
```html
<article></article>
    <input
      type="button"
      value="fetch"
      onclick="
        👉fetch('html').then(function(response){
            response.text().then(function(text){document.querySelector('article').innerHTML = text})
        })
    "/>
```

[Top](#JS)

---

## 5.1. fetch API-요청과 응답
- **코드를 나눠서 보자**
  - `fetch('html')` : `client`가 `server`에게 `html`파일을 요청
  - `.then(callbackme)` : `server`의 응답이 끝나면 `callackme` 함수가 실행된다.
  - fetch API는 Asynchronous(비동기)로 작동되기 때문에 출력순서는 `>> 1 2 response end`이다.
```html
function callbackme(){
  👉console.log('response end')
}
fetch('html').then(callbackme)
👉console.log(1)
👉console.log(2)
```

[Top](#JS)

---

## 5.2. fetch API-response 객체
- **response(서버응답) 객체**
```html
function(response){
  if(response.status == '404){
    alert('Not found')
  }
}
```

[Top](#JS)

---

## 6.1. ajax의 적용
```javascript

<a onclick="
  👉fetch('html')
    .then(function(response){
      response.text()
    .then(function(text){
      document.querySelector('article').innerHTML = text
    })
  })
">HTML</a>

```

[Top](#JS)

---

## 6.2. 리팩토링 함수화
- **중복 제거**
```html
<ol>
  <li>
    👉<a onclick="fetchPage('html')">HTML</a>
  </li>
  <li>
    👉<a onclick="fetchPage('css')">CSS</a>
  </li>
  <li>
    👉<a onclick="fetchPage('javasciprt')">JS</a>
  </li>
</ol>
<article></article>
<script>
  👉function fetchPage(name) {
    fetch(name).then(function (response) {
      response.text().then(function (text) {
        document.querySelector('article').innerHTML = text
      })
    })
  }
</script>
```

[Top](#JS)

---

## 7.1. 초기 페이지 (1/2)
- **Ajax를 적용했을 때 여러가지 문제점들**
  - 링크의 순수한 모양으로 만들고 싶다.
  - 클릭했을 때 해당 페이지의 url이 나오게 하고 싶다.

- **해결**
  - 해시(Hash) : 페이지의 특정 부분을 사용자에게 접근하게 하고 싶을 때 사용<br>ex) 북마크 `#three`
  - 크롤링 때문에 현재는 많이 사용되지 않는다.
  - `location.hash == #three`
  - `location.hash.substr(1) == three`

```html
<!-- url : localhost:3000/hash.html#three -->

<!DOCTYPE html>
<html>
  <body>
    <a href="👉#three">three</a>
    <p>One</p>
    <p>Two</p>
    <p id="three">Three</p>
  </body>
</html>

<script>
  if (location.hash) {
    console.log(👉location.hash.substr(1))
  } else {
  }
</script>
```

[Top](#JS)

---

## 7.2 초기 페이지 (2/2)
```html
<body>
  <ol>
    <li>
      <a href="👉#!html" onclick="fetchPage('html')">HTML</a>
    </li>
  </ol>
  <article></article>
  <script>
    👉if (location.has) {
      fetchPage(location.hash.substr(2))
    } else {
      fetchPage('welcome')
    }
  </script>
</body>
```

[Top](#JS)

---

## 8.1. 글목록 (1/2)

- **데이터와 로직을 분리하는 이유**
  - 사용자들이 이용할 때 사고를 방지
  - 컨텐츠를 어디에 어떻게 입력을 해야 하는가
```html
// list
<li>
        <a href="#!html" onclick="fetchPage('html')">HTML</a>
      </li>
      <li>
        <a href="#!css" onclick="fetchPage('css')">CSS</a>
      </li>
      <li>
        <a href="#!javascript" onclick="fetchPage('javasciprt')">JS</a>
      </li>
```

```html
// index.html
<ol 👉id="nav"></ol>

<script>
  fetch(list).then(function (response) {
    response.text().then(function (text) {
      document.querySelector('👉#nav').innerHTML = text
    })
  })
</script>
```

[Top](#JS)

---

## 8.1. 글목록 (2/2)
- **list파일에 html, css, javascript를 배열로 읽어올수 있게 하기**
```html
<!-- list 파일 -->

👉html,css,javascript
```

```html
<script>
  var items = text.split(',')
  var i = 0
  var tags = ''
  while (i < items.length) {
    var item = items[i]
    item = item.trim()
    var tag =
      '<li><a href="#!' +
      item +
      '" onclick="fetchPage(\'' +
      item +
      '\')">' +
      item +
      '</a></li>'
    tags = tags + tag
    i = i + 1
  }
  document.querySelector('#nav').innerHTML = tags
</script>
```

[Top](#JS)

---

## 9. fetch API polyfill
- **호환성의 문제**
  - [호환성 확인 사이트](https://caniuse.com)

- **`fetch API polyfill`**
  - 익스플로어 10 이상에서 `fetch`를 사용할 수 있다.
  - 호환성의 확보

[Top](#JS)

---

## 10. 수업을 마치며
- **공부할만한 주제**
  - XML
  - JSON
  - SPA(Single Page Application)
  - `PJAX(pushState + ajax)` : 검색엔진에 반영이 되면서 ajax가 가능
  - Progressive Web Apps : online + offline

[Top](#JS)

---
# ⭐
# REACT

- [생활코딩 리액트 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCRv6f8H9K5Xwsdyg4sFSdi)
- [생활코딩 리액트 소스코드](https://github.com/egoing/react-tutorial-example)

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

  - `App` 컴포넌트는 `TOC` 컴포넌트의 부모이다.
  - `contents`는 `props`

```javascript
// App.js
class App extends Component {
    return (
      <div className="App">
        <TOC 👉data={this.state.contens}></TOC>
      </div>
    )
}
```

```javascript
//TOC.js
class TOC extends Component {
  render() {
        <li 👉key={data[i].id}>
          <a href={'/content/' + data[i].id}>{data[i].title}</a>
        </li>
  }
}

```

[Top](#JS)

---

## 16.1 이벤트 state props 그리고 render 함수

- **목표**

  - `Content` 컴포넌트의 `mode`가 `'welcome'`이면 ~ 출력, `'read'`이면 ~ 출력
  - 그 외는 아무것도 출력이 안된다.
   - `Content` 컴포넌트의 `attribute`인 `title`에 값이 없기 때문

- **`props`나 `state`의 값이 바뀔 때 `render` 함수 하위에 있는 컴포넌트들도 다시 그려진다.**

  - App -> Subject -> TOC -> Content

- **State 설정**

```javascript
// App.js

class App extends Component {
  👉constructor(props) {
    super(props)
    this.state = {
      👉mode: 'read',
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
    return (
      <div className="App">
        <Content title=👉{_title} desc=👉{_desc}></Content>
      </div>
    )
  }
}
```
```javascript
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

  - `Subject` 컴포넌트의 `anchor` 태그를 클릭했을 때<br>
  어떤 자바스크립트가 실행될 수 있게 하기

- **문제**

  - 이벤트(onClick)가 발생할 때 새로고침이 되버린다.
  
- **해결**
- 이벤트(onClick 함수)의 매개변수로 객체 e를 넣고 `e.preventDefault()`를 실행하면 된다.  

- **디버거 사용**

  - `debugger` 코드를 만나면 실행이 정지
  - 개발자 도구의 `Sources` 탭에서 다양한 정보를 볼 수 있다.

```javascript
// App.js

class App extends Component {
    return (
      <div className="App">
        👉<header>
          <h1>
            <a
              href="/"
              onClick={function (e) {
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

  - `header` 태그의 `anchor` 태그를 클릭했을 때<br>
  `App` 컴포넌트 `State`의 `mode` 값을 `'welcome'`으로 변경하기

- **`this.state.mode = 'welcome'` 코드의 2가지의 문제**

  - 이벤트가 실행되는 함수안의 `this`는 아무값도 가리키고 있지 않다.
  - 리액트는 `state`의 값이 바뀐지 모른다.

- **해결**

  - 이벤트함수가 끝나는 지점에 `.bind(this)`를 붙여주면<br>
  `this`는 자신의 컴포넌트를 가리키게 된다.
  - 바뀐 `state`값을 알도록 `this.setState({mode: 'welcome'})`으로 바꾸어준다.

- **자세한 설명**
  - 강의 16.4 이벤트 bind 함수 이해하기
  - 강의 16.5 이벤트 setState 함수 이해하기

```javascript
// App.js

class App extends Component {
    return (
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
  - `render` 함수안의 `this`는 `render` 함수가 속해있는 컴포넌트를 가르킨다.
  - 함수 안의 `this`는 아무것도 가리키고 있지 않다. == `undefined`

- **그래서**
  - `this`의 값을 강제로 주입하고 싶다.

- **목표**
  - `bindTest` 함수의 `this`가 `obj` 객체를 가리키게 하고 싶다.

```javascript
var obj = {name: 'egoing'};
function bindTest(){
    console.log(this.name);
}
👉bindTest() // undefined

var bindTest2 = 👉bindTest.bind(obj);
bindTest2(); // 'egoing'이 출력되며 새로운 함수가 만들어 진다.
```

[Top](#JS)

---

## 16.5 이벤트 setState 함수 이해하기

- **생성자 `constructor` 함수에서는 `state`값을 다음과 같이 변경해도 되지만**

```javascript
constructor(props) {
  super(props);
  this.state = {
    mode: 'read'
   }
```

- **컴포넌트 생성이 끝난 후 동적으로 state값을 변경하고 싶을 때는<br>
`this.state.mode = 'welcome` 이 아닌 `this.setState({mode: 'welcome'})`로 변경해야 한다.**

- **이유**
  - 리액트가 state 값의 변화를 인지못하여 렌더링을 하지 못한다.

[Top](#JS)

---

## 17.1 컴포넌트 이벤트 만들기

- **목표**

  - 이벤트를 만드는 생산자가 되어보기
  - `Subject` 컴포넌트안에 이벤트 생성
  - `App` 컴포넌트의 `mode`가 `'welcome'`으로 바뀌게

- **순서**
  - `Subject` 컴포넌트 안에 우리가 `onChangePage`라는 이벤트를 만들고 함수를 설치
  - 그 이벤트가 발생되었을 때 `props`로 전달된 `onChangePage` 함수가 실행된다.

```javascript
// App.js

class App extends Component {
    return (
      <div className="App">
        <Subject
            👉onChangePage={function () {
            👉this.setState({ mode: 'welcome' })
          👉}.bind(this)}
        ></Subject>
      </div>
    )
}
```

```javascript
// Subject.js

class Subject extends Component {
  render() {
    return (
      <header>
        <h1>
          <a
            href="/"
            👉onClick={function (e) {
             👉e.preventDefault()
             👉this.props.onChangePage()
            }.bind(this)}
          >
            {this.props.title}
          </a>
        </h1>
        {this.props.sub}
      </header>
    )
  }
}
```

[Top](#JS)

---

## 17.2 컴포넌트 이벤트 만들기
- **목표**

  - `<TOC>`의 `anchor` 태그를 클릭했을 때 `mode`를 `read`로 바꿔주기
  
```javascript
// App.js

return (
    <div className="App">
      <TOC
        onChangePage={function () {
          this.setState({
            👉mode: 'read'
          })
        }.bind(this)}
        data={this.state.contents}
      ></TOC>
    </div>
  )
```

```javascript
// TOC.js

lists.push(
    <li key={data[i].id}>
      <a
        href={'/content/' + data[i].id}
        onClick={function (e) {
          e.preventDefault()
          👉this.props.onChangePage()
        }.bind(this)}
      >{data[i].title}
      </a>
      
    </li>
  )
```

[Top](#JS)

---

## 17.3.
- **목표**
  - `list`를 클릭하면 본문이 보일 수 있게
  - `state`의 `selected_id`에 맞는 내용을 표시

- **이벤트 함수는 `target`속성을 가지는데<br>
그 이벤트가 발생한 태그를 가리킨다.**
  - ex) `<a onClick={function(){}}></a>
  - 디버깅을 통해 개발자 도구에서 확인 가능

- **`data-id={data[i].id}`의 값은 `id: "2"`이고<br>
개발자도구 `Sources`의 `dataset`에서 볼 수 있다.**

- **정리**

- **공통코드 App.js**
```javascript
constructor(props) {
    super(props)
    this.state = {
      👉selected_content_id: 2
    }
  }
  render() {
      👉var i = 0
      while (i < this.state.contents.length) {
        var data = this.state.contents[i]
        if (data.id === this.state.selected_content_id) {
          _title = data.title
          _desc = data.desc
          break
        }
        i = i + 1
      }
    }
    return (
      <div className="App">
        <TOC
          👉onChangePage={function (id) {
            this.setState({
              mode: 'read',
              👉selected_content_id: Number(id),
            })
          }.bind(this)}
          data={this.state.contents}
        ></TOC>
      </div>
    )
  }
}
```

- **1. 속성을 이용하는 방법(현재사용코드)**

  - `TOP` 컴포넌트의 `onClick`의 속성을 이벤트를 실행시킬 때<br>
  `e.target.dataset.id`을 통해서 값을 추출했기 때문에<br>
  `data-id` 값이 바뀌면 `e.target.dataset.id` 값도 바뀐다.<br>
  ex) `data-AA` -> `e.target.dataset.AA`
  
```javascript
// TOC.js

<li key={data[i].id}>
  <a 
    href={"/content/"+data[i].id}
    👉data-id={data[i].id}
    onClick={function(e){
      e.preventDefault();
      this.props.onChangePage();
      👉this.props.onChangePage(e.target.dataset.id);
    }.bind(this)}
  >{data[i].title}</a>
</li>)
```

- **2. 속성을 이용하지 않는 방법**

  - `bind`의 두 번째 인자로 `data[i].id` 값을 주면<br>
  `bind`는 `onClick` 함수의 두번째 인자로 들어온 인자를<br>
  그 함수의 첫번째 매개변수의 값으로 넣어준다.<br>
  기존에 있던 값은 뒤로 밀린다. ex) `function(-, e){}
  
```javascript
<li key={data[i].id}>
  <a
    href={'/content/' + data[i].id}
    onClick={function (e👉) {
      e.preventDefault()
      this.props.onChangePage(👉id)
    }.bind(this👉)}
  >{data[i].title}
  </a>
</li>
```

[Top](#JS)

---

## 18. 베이스 캠프
- **개념정리**
  - props are **read-only**
    - 컴포넌트 안에서 props  변경할 수 없다.
  - props **can not be modified**
  - state changes **can be asynchronous**
  - state **can be modified** using `this.setState`
  - 상위 컴포넌트가 하위 컴포넌트로 값을 전달 할 때는 `props`, 그 반대는 `이벤트`를 사용

[Top](#JS)

---

## 19.1 create 구현 : 소개
- **목표**

  - `create`버튼을 누르면 `App` 컴포넌트의 `mode`가 `create`로 바뀐다.
  - 읽기로 사용되는 `Content` 컴포넌트가 글을 추가할 때 사용되는 컴포넌트로 바뀐다.
  - 폼형태로 제공되며 저장을 하면 `App` 컴포넌트 State `contetns` 목록에<br>
  새로운 정보(`desc`, `id`, `title`)가 객체로 담겨서 추가된다.
  - 그에 따라 `TOC`에 표시될 내용이 늘어난다.

[Top](#JS)

---

## 19.2 create 구현 : mode 변경 기능
- **목표**
  - `<TOC>`, `<Content>` 사이에<br>`create`, `update`, `delete` 모드로 진입하는 버튼을 만든다.

- **`Control` 컴포넌트 생성**
- `Control` 컴포넌트의 `onChangeMode` 함수의 인자 `create`, `update`, `delete`는<br>
`App` 컴포넌트 함수의 매개변수 `_mode`로 전달이 된다.

```javascript
// App.js

<Control
  onChangeMode={function (👉_mode) {
    this.setState({ mode: _mode })
  }.bind(this)}
></Control>
```
```javascript
// Control.js
<a
  onClick={function (e) {
    e.preventDefault()
    this.props.onChangeMode(👉'update')
  }.bind(this)}
  href="/update">
  Update
</a>
```

[Top](#JS)

---

## 19.3 create 구현 : mode 전환 기능
- **목표**
  - `state.mode`의 값에 따라서 `content` 영역이 교체되는 기능 구현
  - `create`을 클릭했을 때<br>
`<Content>`를 읽기(read)에서 사용될 `<ReadContent>` 컴포넌트와<br>
쓰기(create)에서 사용될 `<CreateContent>` 컴포넌트로 변경

- **`ReadContent`, `CreateContent` 컴포넌트 생성**
  - 기존 `Content`는 `ReadContent`로 변경

```javascript
// App.js

import ReadContent from './components/ReadContent'
import CreateContent from 

class App extends Component {
  render() {
    var _title,
      _desc,
      👉_article = null
   
    } 👉else if (this.state.mode === 'create') {
      _article = <CreateContent></CreateContent>
    }
    return (
      <div className="App">
        👉{_article}
      </div>
    )
}
```
```javascript
// CreateContent.js

import React, { Component } from 'react';

class CreateContent extends Component{
    render(){
      return (
        <article>
            <h2>Create</h2>
            <form>

            </form>
        </article>
      );
    }
  }

export default CreateContent; 
```

[Top](#JS)

---

## 19.4. create 구현 : form
- **목표**
  - 글을 추가하는 기능인 `form`을 완성

- **`onSubmit`은 `form`태그의 고유 기능**

```javascript
// App.js

class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      👉mode:'create',
      ]
    }
  }
```
```javascript
// CreateContent.js

render(){
    console.log('Content render');
    return (
      <article>
          <h2>Create</h2>
          👉<form action="/create_process" method="post"
            onSubmit={function(e){
              e.preventDefault();
              alert('Submit!!!!!');
            }.bind(this)}
          >
            <p><input type="text" name="title" placeholder="title"></input></p>
            <p>
              <textarea name="desc" placeholder="description"></textarea>
            </p>
            <p>
              <input type="submit"></input>
            </p>
          👉</form>
      </article>
    );
  }
```

[Top](#JS)

---

## 19.5 create 구현 : onSubmit 이벤트
- **목표**

  - `onSubmit` 이벤트 생성
  - 생성된  `_title` 과 `_desc`는 어떻게 가져올 것인가
  - `CreateContent`에 이벤트로 설치된 함수를 실행
  - `e.target.title.value` == `"React"(Create의 타이틀에서 입력한 값)`<br>
  - 찾는 방법은 개발자 도구에서<br>
`e -> target(form) -> title(input) -> value("React")`

```javascript
// App.js

render() {
      👉_article = <CreateContent onSubmit={function(_title, _desc){
        // add content to this.state.contents
      }.bind(this)}></CreateContent>
    }
```
```javascript
<form
  action="/create_process"
  method="post"
  onSubmit={function (e) {
    e.preventDefault()
    👉this.props.onSubmit(e.target.title.value, e.target.desc.value)
    alert('Submit!!!!!')
  }.bind(this)}
></form>
```

[Top](#JS)

---

## 19.6 create 구현 : contents 변경
- **목표**
  - `App` 컴포넌트의 `state`의 `contents` 끝에다가 사용자가 입력한 정보를 추가
  - 그에 따라 글 목록도 자동 추가

- **`this.max_content_id =3`**
  - 데이터를 추가할때 아이디값을 알려주는 사용하는 정보일 뿐<br>
  UI에 영향을 주지 않기 때문에 `state` 값에 넣지 않는다.

- **`setState`**
  - `State` 값을 변경할 때 주의

- **`push` vs `concat`**
  - `state`에는 원본을 보존하고 복제한 데이터를 사용하는게 성능에 좋다.

```javascript
// App.js
class App extends Component {
    constructor(props){
      super(props);
      👉this.max_content_id = 3;
      this.state = {

      }
    }
    render() {
      } else  if(this.state.mode === 'create'){
        _article = <CreateContent onSubmit={function(_title, _desc){
          // add content to this.state.contents
          👉this.max_content_id = this.max_content_id+1;
          // this.state.contents.push(
          //   {id:this.max_content_id, title:_title, desc:_desc}
          // );
          👉var _contents = this.state.contents.concat(
            {id:this.max_content_id, title:_title, desc:_desc}
          )
          👉this.setState({
            contents:_contents
          });
      }
```

[Top](#JS)

---

## 19.7. create 구현 : shouldComponentUpdate
- **목표**
  - `push`, `concat`을 사용했을 때의 차이점
  - `newProps`, `newState` 를 통해서 비교

- **`TOC` 컴포넌트에서 `shouldComponentUpdate` 함수를 통해 알수 있는 점**
  - `render` 함수 이전에 `shouldComponentUpdate` 이 실행된다.
  
  - `shouldComponentUpdate`의 `return` 값이
    - `true` : `render` 함수 실행 o
    - `false` : `render` 함수 실행 x

  - `shouldComponentUpdate`의 매개변수 : `newProps`, `newState`
    - `newProps` : 새로운데이터, 바뀐 값
    - `newSate` : 현재 값

- **`push` 의 문제점**
  - 기존의 `this.state.contents`의 원본을 바꿔버린다.
  - 이전값과 이후값이 완전히 같아지게 된다.

- **수정**
  - `TOC` 컴포넌트로 들어오는 `props data` 값이 바뀌었을 때<br>
render가 실행, 아니면 실행이 되지 않는다.
  - 글을 썼을 때 이전 값과 현재 값이 다르기 때문에<br>
  `true`가 리턴이 되면서 `return` 함수가 실행이 된다.

```javascript
// TOC.js

class TOC extends Component {
  👉shouldComponentUpdate(newProps, newState)
  👉if(this.props.data === newProps.data){
    👉return false;
  }
  👉return true;
  render() {
  }
}
```

[Top](#JS)

--- 
 
## 19.8. create 구현 : immutable
- **목표**
  - 원본을 바꾸지 않고 `setState`에 값을 세팅

- **`Array.from`**
   - 배열 복제

- **`Object.assign`**
  - 객체 복제

```javascript
_ariticle = (
  <CreateContent
    onSubmit={function (_title, _desc) {
      this.max_content_id = this.max_content_id + 1
      var newContents = 👉Array.from(this.state.contents)
      newContents.push({ id: this.max_content_id, title: _title, desc: _desc })
      this.setState({
        contents: newContents,
      })
    }.bind(this)}
  ></CreateContent>
)
```

[Top](#JS)

---

## 20.1. update 구현
- **`read` + `create`**
- **`UpdateContent` 생성**
- **`mode`, `title`  분리**

```javascript

```
```javascript

```

[Top](#JS)

---

## 20.2. form 구현
- [리액트 공식문서](https://reactjs.org/docs/forms.html)

input 값이 바뀌었을 때 state의 값이ㅣ 바뀌게

[Top](#JS)

---

## 20.3. update 구현 : state 변경
- 업데이트의 식별자
onSubmit
mode를 read로

[Top](#JS)

---

## 21. delete 구현
- window.confirm() 확인 true, 캔슬 false

[Top](#JS)

---

## 22. 수업을 마치며
- **공부할 것**
  - immutable
    - immutableJS
  - router
    - React Router(url)
  - create-react-app
    - npm run eject(더 많은 도구들)
  - redux
    - 컴포넌트를 한 곳에 모은다.
  - react server side rendering
    - 서버에서 웹페이지를 완성해서 클라이언트로 완성된 html을 전달
  - react native

[Top](#JS)

---
# ⭐
# React class function style coding

- [생활코딩 React class & function style coding 수업](https://www.youtube.com/watch?v=iY_vmP-Q3Ak&list=PLuHgQVnccGMCEfBwnNGsJCQDiqSWI-edj)
- [생활코딩 React class & function style coding 소스코드](https://github.com/egoing/react-function-vs-class-style)

[Top](#JS)

---

## 1. 수업소개
- **리액트에서 컴포넌트를 만드는 2가지 방법**
  - Class 문법
  - Function 문법
    - `state`와 `life cycle API`를 사용할 수 없다.
    - 'hook'을 이용해서 보완이 가능하다.

[Top](#JS)

---

## 2. 수업의 목표
- **목표**
  - `Class`와 `Function`으로 비슷한 기능을 가진<br>컴포넌트의 내부를 비교

- **개발환경 세팅**
  - 리액트 설치
  - `FuncComp`, `ClassComp` 컴포넌트 생성

- **기본 비교**
  - `function`은 자기 자신이 렌더(바로 리턴)
  - `class`는 render 메소드 안에서 리턴

```javascript
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="container">
      <FuncComp></FuncComp>
      <ClassComp></ClassComp>
    </div> 
  )
}

function FuncComp(){
  return (
    <div className="container">
      <h2>function style component</h2>
    </div>
  )
}

class ClassComp extends React.Component{
  render(){
    return (
      <div className="container">
        <h2>class style component</h2>
      </div>
    )
  }
}

export default App;
```

[Top](#JS)

---

## 3.1 클래스에서 state 사용법
- **목표**
  - 클래스에서 내부 상태의 변화를 관리하기 위해서 사용하는 데이터 형태가 state입니다. state를 클래스에서 다루는 방법을 소개합니다. 

- **`props`를 사용할 때**
  - 컴포넌트에서
  - 함수형 : 매개변수로 `props`를 받은 후 `props.~`
  - 클래스형 : `this.props.변수`

- **`state`를 사용할 때**
  - 컴포넌트에서
  - 함수형 : `state` 와 `라이프사이클` 을 사용할 수 없다.
  - 클래스형 : `state = {number:this.proprs.~}` , `{this.state.~}`

- [소스코드](https://github.com/egoing/react-function-vs-class-style/commit/9864edae07cbc9d57b8fd488132f32efa18a9192)

[Top](#JS)

---

## 3.2. 함수에서 state사용법 (hook)
- **목표**
  - 리액트 16.8 버전에서는 hook이라는 기능이 추가 되었습니다. hook은 기존에 클래스 스타일 코딩에서만 가능했던 여러작업을 함수 스타일 코딩에서도 가능하게 해주는 기능입니다. 이 기능을 이용해서 함수 내에서 state를 사용하는 방법을 살펴봅시다. 

- [리액트 훅](https://ko.reactjs.org/docs/hooks-intro.html)
  - 내장된 훅(`use` 로 시작), 사용자가 만들어서 사용가능
  - `import React, {useSate} from 'react';`
  - `var numberState = useState();` : 2개의 배열이 리턴 된다.
  - `numberState[0]` == `state` 값
  - `numberState[1]` == `setState` 의 역할  
  - `{props.init}` == `{number}`
  - `initNumber` 를 사용할 때는<br>`useState()` 의 인자로 넣어서 사용<br>== `useState(props.initNumber)`

- **중요**
```javascript
// var dateSate = useState((new Date()).toString())
// var _date = dateState[0] // state
// var setDate = dateSate[1] // setState

var [_date, setDate] = useState((new Date()).toString())
```  
- [소스코드](https://github.com/egoing/react-function-vs-class-style/commit/a7da7b8230e49eff41e3b5c875846963e152e4de)

[Top](#JS)

---

## 4.1. 클래스에서 라이프 사이클 이용하기
- **목표**
  - 콤포넌트의 생성과 변화 그리고 소멸에 따라서 해야 할 일을 구현할 수 있는 기능인 라이프 사이클 API를 클래스 방식으로 구현하는 방법을 소개합니다. 

- **검색 : `react lifecycle`**
  - `componentWillMount` -> `render` -> `componentDidMount` -> `(shouldComponentUpdate)`

- 이미지 추가

- [소스코드](https://github.com/egoing/react-function-vs-class-style/commit/c1095d94e1961ba9f4605ab7c8bc93b841d58517)

[Top](#JS)

---

## 4.2. 함수에서 라이프 사이클 이용하기
- **목표**
  - hook 이전까지는 함수에서 라이프 사이클을 이용할 수 없었습니다. hook이 등장하면서 useEffect를 이용해서 라이프 사이클을 이용할 수 있는 방법이 생겼습니다. 이에 대한 수업입니다. 

- **`componentDidMount`**
  - 컴포넌트가 `등장` 할 때

- **`componentWillunmount`**
  - 컴포넌트가 `퇴장` 할 때

- **`componentDidUpdate`**
  - `state` 가 바뀔 때마다 실행

- [실습준비 소스코드](https://github.com/egoing/react-function-vs-class-style/commit/46493d6731945f66ccc6c933cd80a4b3cd5bec49)

- **`useEffect` == `componentDidMount & `componentDidUpdate``**
  - `render` 후에 필요한 작업 == `render` 가 메인작업
  - 첫번째 인자는 `함수`
  - `render` 가 실행될 때마다 실행

- [useEffect 소스코드](https://github.com/egoing/react-function-vs-class- style/commit/44ba328d83fd8ef325afb1d941a6a3bb70013f00)

- **`useEffect의 return 값 == `componentWillUnmount`**
  - `render` 생성 후 , `useEffect` 가 실행되기 전에 `clean up` 작업
  - 컴포넌트가 사라질때 해야 되는 작업
  
- [clean up 소스코드](https://github.com/egoing/react-function-vs-class-style/commit/98ea5ca66e02b3bf7ecd94e4edb8ad012cd424c7)

- **필요성**
  - `componentDidUpdate` 를 할때, 변한 값만을 비교한다면 불필요한 처리를 줄일 수 있다.

- **2번째 인자가 있을 경우**
```javascript
useEffect(function(){
  // #2 실행
  document.title = number
  return function(){
    // #1 실행 : clean up 하기 위해
  }
}, [number])
```
- **2번째 인자가 없을 경우**
```javascript
useEffect(function(){
  // #1 실행 : 1회만 실행
  document.title = number
  return function(){
    // #2 실행 : clean up 하기 위해
  }
}, [])
```
- [skipping effect 소스코드](https://github.com/egoing/react-function-vs-class-style/commit/608a67dfc0259f3f8d6f8828e3417f6e52327513)

[Top](#JS)

---

# React Router
- [생활코딩 React Router 수업](https://www.youtube.com/watch?v=WLdbsl9UwDc&feature=youtu.be)
- [생활코딩 React Router 소스코드](https://github.com/egoing/react-router-dom-example)

[Top](#JS)

---

# React Redux
- [생활코딩 React Redux 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMDuVdsGtH1_452MtRxALb_7)
- [생활코딩 React Redux 소스코드](https://github.com/egoing/react-redux-tutorial-example)

[Top](#JS)

---

# React Ajax
- [생활코딩 React Ajax 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMDVTrQYa2HRj1OBbT-4HU_v)
- [생활코딩 React Ajax 소스코드](https://github.com/egoing/react-ajax)

[Top](#JS)

---

# Redux
- [생활코딩 Redux 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMB-iGMgONoRPArZfjRuRNVc)
- [생활코딩 Redux 소스코드](https://github.com/egoing/redux-tutorial-example)

[Top](#JS)

---

# ⭐
# NodeJS
- [생활코딩 Node.js 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMA9QQX5wqj6ThK7t2tsGxjm)
- [생활코딩 Node.js 소스코드](https://github.com/web-n/Nodejs)

[Top](#JS)

---

## 1. 수업소개
- **HTML의 생성을 Web Application에게 맡김**

- **V8 엔진 기반** : 컴퓨터 자체를 제어

[Top](#JS)

---

## 2. 수업의 목적
- **생산성**
  - 1억개의 웹페이지를 한번에 수정

- **사용자의 참여가 가능**

[Top](#JS)

---

## 3. 설치
- **구조**
  - `WEB Browser`, `HTML`, `WEB Application`

  - `Node.js runtime`, JavaScript`, Node.js Application`

- **`Node.js runtime` 설치**
  - [nodejs](https://nodejs.org/en/)
  - 설치확인 : 터미널 `node -v`

[Top](#JS)

---

## 4. 공부방법
- **공부순서**
  - `JavaScript` 문법
  - `Node.js runtime` 기능
  - `Node.js Application` 만들기

[Top](#JS)

---

## 5. Node.js로 웹서버 만들기
- **Web Server**
  - Node.js는 서버가 내장
  - 사용자에게 전송할 데이터를 생성

```node
var http = require('http');
var fs = require('fs');
var app = http.createServer(function(request,response){
    var url = request.url;
    if(request.url == '/'){
      url = '/index.html';
    }
    if(request.url == '/favicon.ico'){
      response.writeHead(404);
      response.end();
      return;
    }
    response.writeHead(200);
    response.end(fs.readFileSync(__dirname + url));
 
});
app.listen(3000);
```

[Top](#JS)

---

## 9. URL의 이해
- **목표**
  - 자바스크립트를 이용해서 node.js의 기능을 호출

- **`http://opentutorials.org:3000/main?id=HTML&page=12`**
  - `http` : `protocol` : 통신규칙 : 사용자가 서버에 통신할때 어떤 규칙을 이용할지
  - `opentutorials.org` : `host(domain)` : 인터넷에 접속되있는 각각의 컴퓨터 : 특정한 인터넷에 연결되어 있는 컴퓨터를 가리키는 주소
  - `3000` : `port` : 한 대의 컴퓨터 안에 여러 대의 서버 중에 3000번 포트와 연결
  - `main` : `path` : 컴퓨터 안에 있는 파일의 경로
  - `id=HTML&page=12` : `query string` : 웹서버에게 데이터를 전달 가능 : `?`로 시작, 값과 값은 `&`, 값의 이름과 값은 `=`로 구분

[Top](#JS)

---

## 10. URL을 통해서 입력된 값 사용하기
- **목표**
  - `Query String` 에 따라 다른 정보를 보여준다.

- **`url` 값을 추출해 원하는 값을 얻어낼 수 있다.**
  - `localhost:3000/?id=HTML` : `id=HTML`의 `HTML` 값을 알아내고 싶다.
  - 검색 : `nodejs url parse query string`
  - `queryData` = `{ id : HTML }`
  - `queryData.id` = `HTML`

```node
var url = require('url');
var _url = request.url;
    var queryData = url.parse(_url, true).query;
 response.end(queryData.id);
```

[Top](#JS)

---

## 11. App 제작-동적인 웹페이지 만들기
- **타이틀을 정적으로 바꾸기**
  
  - 본문의 `${title}`
  - `root`로 접속시 제목 `Welcome`

```node
 var title = queryData.id;
if(_url == '/'){
      title = 'Welcome';
var template =`
 <title>WEB1 - ${title}</title>
response.end(template)
```

[Top](#JS)

---

## 12 .Node.js의 파일 읽기 기능
- **CRUD**
  - `Create`, `Read`, `Update`, `Delete`

- **READ**
  - 검색 : `nodejs file read`

```node
// nodejs/readfile.js

var fs = require('fs');
fs.readFile('sample.txt', 'utf8', function(err, data){
  console.log(data);
});
```

[Top](#JS)

---

## 13. App 제작- 파일을 이용해 본문 구현
- **목표**
  - `Query string` 에 따라서 `본문`이 변경되는 App

- **본문에 넣을 폴더 생성**

- **`fs`를 이용해 폴더안의 파일을 읽는다**

```node
fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
  var template =`
    <title>WEB1 - ${title}</title>
    <p>${description}</p>
  response.end(template)
}
```

[Top](#JS)

---

## 18. NodeJS - 콘솔에서의 입력값
- **INPUT**
  - `Parameter`, `Argument`
  - 검색 : `nodejs console input parameters`

- **OUTPUT**

- **배열의 3번째(인덱스2) 부터 값이 들어간다**

```node
// conditional.js
var args = process.argv;
if(args[2] === '1'){
  console.log('C1');
} else {
  console.log('C2');
}
console.log('D');

// 출력 : node conditional.js 1 -> C1 D
// 출력 : node conditional.js 2 -> C2 D
```

[Top](#JS)

---

## 19.1. App 제작-Not found 구현
- **목표**
  - 존재하지 않는 정보에 대한 요청이 들어왔을 때 Not found 오류 메시지를 전송하는 방법

- **`url.parse(_url, true)`**
  - `url` 에 대한 정보가 객체로 담겨있다.
  - `pathname` : `/`
  - `path` : `/?id=CSS` : `Query string` 을 포함한 정보

```node
var pathname = url.parse(_url, true).pathname;

if(pathname === '/'){

} else {
      response.writeHead(404);
      response.end('Not found'); 
```

[Top](#JS)

---

## 19.2. App 제작-홈페이지 구현
- **목표**
  - 조건문을 활용해서 홈페이지를 표현하는 방법

- **`queryData.id === undefined`**
  - `root` 경로

```node
if(queryData.id === undefined){
  // root 경로일 때 정보를 보여준다.  
} else {
  // url에 맞는 정보를 보여준다.
}
```

[Top](#JS)

---

## 23. Node.js에서 파일목록 알아내기
- **목표**
  - 특정 디렉토리 하위에 있는 파일과 디렉토리의 목록을 알아내는 방법

- **검색 : `nodejs file list in directory`**

- **배열로 출력**

```node
var testFolder = './data';
var fs = require('fs');
 
fs.readdir(testFolder, function(error, filelist){
  console.log(filelist);
})
```

[Top](#JS)

---

## 24. App 제작 - 글목록 출력하기
- **목표**
  - data 디렉토리에 있는 파일들의 이름을 이용해서 글 목록을 생성하는 기능을 구현

```node
if(pathname === '/'){
  if(queryData.id === undefined){
    fs.readdir('./data', function(error, filelist){
var list = '<ul>';
      var i = 0;
      while(i < filelist.length){
        list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
        i = i + 1;
      }
      list = list+'</ul>';
        ${list}
  })
} else {

}
```

[Top](#JS)

---

## 26. App 제작-함수를 이용해서 정리 정돈하기
- **목표**
  - 함수를 이용해서 코드를 정리 정돈하는 모습을 경험

```node
function templateHTML(title, list, body){
  // 중복내용
}

function templateList(filelist){
  // 중복내용
}
```

[Top](#JS)

---

## 28.1. Nodejs에서 동기와 비동기 1
- **목표**
  - Node.js 실행순서를 파악하는 것

- **asynchronous**
  - 병렬적 처리

[Top](#JS)

---

## 28.2. Nodejs에서 동기와 비동기 2
- **차이**

  - `readFileSync` : 동기 
  - `readFile` : 비동기

```node
// result == B
var fs = require('fs');
 
console.log('A');
var result = fs.readFileSync('syntax/sample.txt', 'utf8');
console.log(result);
console.log('C');
// 출력 : A B C
 
console.log('A');
fs.readFile('syntax/sample.txt', 'utf8', function(err, result){
    console.log(result);
});
console.log('C');
// 출력 : A C B
```

[Top](#JS)

---

## 28.3. JavaScript-callback
```node
var a = function(){
  console.log('A');
}
 
function slowfunc(callback){
  callback();
}
 
slowfunc(a); // A
```

[Top](#JS)

---

## 29. Node.js의 패키지 매니저와 PM2
- **NPM**

  - `pm2` 설치 : `npm install pm2 -g`
  - 실행 : `pm2 start app.js`

[Top](#JS)

---

## 30. HTML-form
- **목표**
  - 컨텐츠를 사용자가 웹을 통해 생성하고 수정하고 삭제하는 방법

- **post**
  - 편지봉투에는 받는 주소만, 편지지에는 내용을 적는다.
  - 편지지가 허용하는 만큼 데이터 전달 용량이 상대적으로 크다.
  - 내용 노출도 안된다.

- **get**
  - 편지봉투 겉면 주소란에 모든 내용을 다 적었다.
  - 노출이 되고, 편지봉투에 뭐 열심히 적을래도 공간 부족하니 용량 제한이 있다.

```html
<form action="http://localhost:3000/process_create" method="post">
  <p><input type="text" name="title"></p>
  <p>
    <textarea name="description"></textarea>
  </p>
  <p>
    <input type="submit">
  </p>
</form>
```

[Top](#JS)

---

## 31. App - 글생성 UI 만들기
- **목표**
  - 글 작성을 할 수 있는 UI를 구현해봅시다.

- [소스코드](https://github.com/web-n/Nodejs/commit/ead2c8f716588d3950d596a57934386dd398891a)

[Top](#JS)

---

## 32. App - POST 방식으로 전송된 데이터 받기
- **목표**
  - POST 방식으로 전송된 데이터를 받아서 파일로 저장하는 방법에 대해서 알아보겠습니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/ab13376e1ebae972f8216626dc5981adfdab5ecb)

[Top](#JS)

---

## 33. App - 파일생성과 리다이렉션
- **목표**
  - 전송된 POST 데이터를 받아서 파일에 저장하고, 그 결과 페이지로 리다이렉션하는 방법에 대해서 알아보겠습니다.

- [소스코드](https://github.com/web-n/Nodejs/commit/8996a047c3d07d01752be17751969ebd47e52ced)

[Top](#JS)

---

## 34. App - 글수정 - 수정 링크 생성
- **목표**
  - 글 수정 기능을 구현하기 위해서 수정 링크를 추가하는 법을 살펴봅니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/70bd0cb49a37692dbb0a8488b95bcba8d7d9690f?diff=unified)

[Top](#JS)

---

## 35. App - 글수정 - 수정할 정보 전송
- **목표**
  - 수정할 내용을 서버로 전송하는 법을 살펴봅니다.

- [소스코드](https://github.com/web-n/Nodejs/commit/5c62d421d9d0dd1fb958f7e6438b97e0cbf58d4f)

[Top](#JS)

---

## 36. App - 글수정 - 수정된 내용 저장
- **목표**
  - 전송된 수정 내용을 받아서 파일명을 변경하고, 내용을 저장하는 방법을 알아봅니다.

- [소스코드](https://github.com/web-n/Nodejs/commit/ecbb65278ebe726463ab829a7e8ccaffa787e70f)

[Top](#JS)

---

## 37. App - 글삭제 - 삭제버튼 구현 
- **목표**
  - 삭제 작업을 하기 위해서는 삭제 버튼이 있어야 합니다. 이 때 링크를 사용하는 안됩니다. 링크 대신 form을 이용해서 삭제 버튼을 만드는 방법을 살펴보겠습니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/a96085948f84fbf9d48941ad159e3fcb493e3286)

[Top](#JS)

---

## 38. App - 글삭제 기능 완성 
- **목표**
  - 글삭제 기능을 완성해봅시다!

- [소스코드](https://github.com/web-n/Nodejs/commit/c6207ad04a9aafdb333b5d9e0d8f06699b53b23f)

[Top](#JS)

---

## 39. App -객체를 이용해서 템플릿 기능 정리 정돈하기 
- **목표**
  - 객체를 이용해서 탬플릿 기능을 정리 정돈하는 법을 소개합니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/b62600c227c01b22e35916f485730d2eb29040bb)

[Top](#JS)

---

## 40. Node.js - 모듈의 형식
- **목표**
  - 많아진 코드를 정리 정돈하는 가장 큰 도구인 모듈의 형식을 살펴보겠습니다. 

```node
// nodejs/mpart.js

var M = {
  v:'v',
  f:function(){
    console.log(this.v);
  }
}
 
module.exports = M;
```
```node
// muse.js

var part = require('./mpart.js');
part.f(); // v
```

[Top](#JS)

---

## 41. App 제작 - 모듈의 활용
- **목표**
  - 모듈을 활용해서 템플릿 기능을 모듈화 해보겠습니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/de4cb8b38062284c89d1ed5cb2dc8559accee303)

[Top](#JS)

---

## 42. App - 입력 정보에 대한 보안
- **목표**
  - 입력정보와 관련해서 보안적으로 처리해야 할 이슈를 살펴보겠습니다. 

- 검색 : `node path parse`

- [소스코드](https://github.com/web-n/Nodejs/commit/f3af5af5e404ffe33fe5e4a4f9ebb74b60f60829)

[Top](#JS)

---

## 43. App - 출력정보에 대한 보안
- **목표**
  
  - 출력정보에서 발생할 수 있는 보안적인 이슈를 살펴보겠습니다. 

- [소스코드](https://github.com/web-n/Nodejs/commit/4c072c98d55527b4ffc804d524ddd11bbc57210a)

[Top](#JS)

---

## 44. API
- **목표**
  
  - API라는 중요한 개념의 의미를 알아보고, 지금까지 베일에 쌓여있었던 createServer API의 의미를 살펴보겠습니다. 

[Top](#JS)

---

## 45. 수업을 마치며
- **목표**
  
  - 공부해볼만한 주제

[Top](#JS)

---

# ⭐
# Express
- [생활코딩 Express 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMAGOQu8CBDO9hn-FXFmm4Wp)
- [생활코딩 Express 소스코드](https://github.com/web-n/express)

[Top](#JS)

---

## 1. 수업소개
- **Node.js 위에서 동작하는 Web Framework**
  
  - 반복되는 일을 자동화

[Top](#JS)

---

## 2. 실습준비
- [프로젝트 다운로드](https://github.com/web-n/Nodejs)

[Top](#JS)

---

## 3. Hello Word
- **목표**
  - 가장 기본적인 골격 만들기

- [Express 홈페이지](https://expressjs.com/)
  - 설치 : `npm install express --save`
  - [API reference](https://expressjs.com/en/4x/api.html)

```node
var express = require('express')
var app = express()
 
//route, routing
//app.get('/', (req, res) => res.send('Hello World!'))
app.get('/', function(req, res) { 
  return res.send('/');
});
 
app.get('/page', function(req, res) { 
  return res.send('/page');
});
 
app.listen(3000, function() {
  console.log('Example app listening on port 3000!')
});
```

[Top](#JS)

---

## 4. 홈페이지 구현
- **목표**

  - `Route` 기능을 중심으로 홈페이지 기능을 구현

- [소스코드](https://github.com/web-n/express/commit/5094046499287f1fb6296518e615c05b3a51418c)

## 5. 상세페이지구현
- **목표**
  - 상세보기 페이지를 `Express` 버전으로 변환<br>
  이 과정에서 `query string`을 사용하지 않는<br>
  `pretty url-path parameter(clean url, semantic url..)`로 라우트 기능을 구현하는 방법 

- **`Clean URL` 로 `Route` 를 구현하는 방법을 소개
  - [Routing-Route Parameters](https://expressjs.com/en/guide/routing.html)
  - [소스코드](https://github.com/web-n/express/commit/30b0d4a8e328103a5c3c8273c8f079798e78ae0b)

- **상세보기 페이지를 완성**
  - [소스코드](https://github.com/web-n/express/commit/549db5253bfe4d3d1833aa515546abd9c431d724)

[Top](#JS)

---

## 6. 페이지 생성 구현
- **목표**

  - 페이지 생성 기능을 Express 버전으로 전환하는 방법

- [소스코드](https://github.com/web-n/express/commit/338464ede30730a8b7e8ea2a602f129a878c2cc3)

[Top](#JS)

---

## 7. 페이지 수정 기능 구현
- **목표**

  - 페이지 수정 기능을 Express 버전으로 전환해봅시다.

- [소스코드](https://github.com/web-n/express/commit/5e448076a46c7550bc2833cfb296e3541dc98a67)

[Top](#JS)

---

## 8. 삭제 기능 구현 
- **목표**
  - 삭제 기능을 구현하는 방법을 살펴봅니다

- **리다이렉트**
  - 검색 : `nodejs express redirect`

- [소스코드](https://github.com/web-n/express/commit/3680648c5b8de523a1056709b716a13f907174bd)

[Top](#JS)

---

## 9. Express 미들웨어의 사용
- **목표**
  - 여기서는 미들웨어의 개념을 소개하고, 타인이 만든 미들웨어를 사용하는 방법을 알아봅니다.

[Top](#JS)

---

## 10. Express 미들웨어 만들기
- **목표**
  - Express의 미들웨어를 만드는 방법을 살펴봅니다. 

[Top](#JS)

---

## 11. Express 미들웨어의 실행순서
- **목표**
  - Express의 미들웨어가 실행되는 순서를 살펴보겠습니다. 

[Top](#JS)

---

## 12. 정적인 파일의 서비스
- **목표**
  - 이미지, 자바스크립트, CSS와 같은 파일을 서비스하는 방법을 살펴보겠습니다. 

[Top](#JS)

---

## 13. 에러처리 
- **목표**
  - 에러가 발생했을 때 처리하는 방법을 소개합니다. 

[Top](#JS)

---

## 14. 라우터
- **목표**
  - 관리하는 페이지가 많아짐에 따라서 코드의 복잡도가 급격히 높아지게 됩니다. 복잡도를 낮추는 방법이 라우터입니다. 라우터를 알아봅시다.

[Top](#JS)

---

## 15. 보안
- **목표**
  - Express 애플리케이션을 구현할 때 주의해야 할 보안적인 이슈를 살펴봅시다. 

[Top](#JS)

---

## 16. express generator
- **목표**
  - Express 기반의 프로젝트를 할 때 기본적으로 필요한 파일과 코드를 자동으로 만들어주는 앱인 Express generator를 소개합니다. 

[Top](#JS)

---

# ⭐
# DATABASE1
- [생활코딩 DATABASE1 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMBe0848t2_ZUgFNJdanOA_I)

[Top](#JS)

---

## 1. 수업소개
- **대규모의 데이터를 관리**

  - file -> database

[Top](#JS)

---

## 2. 데이터베이스의 본질
- **input**
  - Create, Upate, Delete

- ** output**
  - Read

[Top](#JS)

---

## 3. file vs database
- **1억개의 파일을 읽거나 수정하고 싶을 때**

  - `File` -> `Spreadsheet` -> `Database`
  - 구조적으로 데이터를 저장할 때 효용성이 가장 큼

[Top](#JS)

---

## 4. 수업을 마치며
- **데이터베이스의 선택**

  - 통계를 기반으로
  - 관계형 데이터베이스를 먼저 배워보기
  - Oracle은 비싸다 ㅠㅠ
  - MySQL은 오픈 소스

[Top](#JS)

---
# ⭐
## MySQL
- [생활코딩 DATABASE2 - MySQL 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCgrP_9HL3dAcvdt8qOZxjW)

[Top](#JS)

---

## 1. 수업소개
- **file의 한계**

- **Relational Database**

[Top](#JS)

---

## 2. 데이터베이스의 목적
- **데이터를 표의 형태로 나타낸다.**

- **컴퓨터 언어를 통해서 데이터베이스를 제어**

[Top](#JS)

---

## 3. MySQL 설치
- **mysql community edition download**
  - [MySQL Community Downloads](https://www.mysql.com/products/community/) 

- **bitnami wamp**
  - `Apache`, `mySQL`, `PHP` 를 동시에 설치해주는 프로그램
  - `Manage Servers` 탭에서 실행 혹은 중지
  - 실행 : 터미널에서 `C:\Bitnami\wampstack-7.4.9-0\mysql\bin` 로 이동 후 `mysql -uroot -p`.

[Top](#JS)

---

## 4. MySQL의 구조
- **구성요소**

  - `표(table)`
  - `데이터베이스(database, schema)` : 일종의 폴더로 표들을 그룹핑한 것
  - `데이터베이스 서버(database server)` : 데이터베이스, 스키마를 그룹핑한 것

[Top](#JS)

---

## 5. 서버접속
- **데이터베이스 서버로 접속**

- **bitnami wamp**
  - `Apache`, `mySQL`, `PHP` 를 동시에 설치해주는 프로그램
  - `Manage Servers` 탭에서 실행 혹은 중지
  - 실행 : 터미널에서 `C:\Bitnami\wampstack-7.4.9-0\mysql\bin` 로 이동 후 `mysql -uroot -p`

- **효용**
  - 보안, 권한 부여

- **`-u` : User**

- **`-p` : Password**

[Top](#JS)

---

## 6. 스키마의 사용
- **데이터베이스 사용**

- **검색**
  - `mysql create database`
  - `mysql delete database`
  - `how to show database list in mysql`

- **생성**
  - `CREATE DATABASE 스키마이름;`

- **삭제**
  - `DROP DATABASE 스키마이름;`

- **확인**
  - `SHOW DATABASES;`

- **사용**
  - `USE 스키마이름;`

[Top](#JS)

---

## 7. SQL과 테이블의 구조
- **SQL*
  - Structured Query Language
  - `SQL`을 통해 `MySQL Server`와 대화

- **table, 표**
  - x축 : `row`, `record`, `행`
  - y축 : `column`, `열`

[Top](#JS)

---

## 8. 테이블의 생성
- **테이블 생성**
  - 검색 : `create table in mysql cheat sheet`

- **`id column` 생성**
  - 검색 : `mysql datatype number`
  - `NOT NULL` : 값을 반드시 입력
  - `AUTO_INCREMENT` : 자동으로 1씩 증가
  - `PRIMARY KEY (id)` : 식별자로 사용하고 있기 때문에 중복방지

- **`title column` 생성**
  - 검색 : `mysql datatype string`
  - `VARCHAR` : 정한 글자수만 입력

- **`description column` 생성**
  - 검색 : `mysql datatype string`
  - `TEXT` : 65,535자 까지 가능

- **`created column` 생성**
  - 검색 : `mysql datatype date/time`

- `ERROR 1820 (HY000): You must reset your password using ALTER USER statement before excuting this statement.`
  - 기본 세팅된 비밀번호를 바꿔야 한다.
  - `SET PASSWORD = PASSWORD(`'새로운 비밀번호');`

```sql
CREATE TABLE topic (
  id INT(11) NOT NULL AUTO_INCREMENT,
  title VARCHAR(100) NOT NULL,
  description TEXT NULL,
  created DATETIME NOT NULL,
  author VARCHAR(30) NULL,
  profile VARCHAR(100) NULL,
  PRIMARY KEY (id)
);
```

[Top](#JS)

---

## 9. CRUD
- **CRUD**

  - `Create`
  - `Read`
  - `Update`
  - `Delete`

[Top](#JS)

---

## 10. INSERT
- **쓰기**

- **`row` 생성
  - 검색 : `mysql create row`
  - `INSERT INTO table_name (column1, ...) VALUES (value1...);`
  - `DESC 테이블명;` : 구조를 보여준다.

- **실습**
  - `INSERT INTO topic (title,description,created,author,profile) VALUES('MySQL','MySQL is ...',NOW(),'egoing','developer');`
  - 검색 : `how to read row in mysql`

[Top](#JS)

---

## 11. SELECT
- **읽기**
  - 검색 : `mysql select syntax`

- **`SELECT * FROM topic;`**
  - 모든 `column` 보기
  
- **`SELECT '표시하고 싶은 column' FROM topic WHERE '조건';`**
  - `SELECT id, title,created,author FROM topic WHERE author='egoing' ORDER BY id DESC LIMIT 2;`
  - `WHERE` : 조건에 맞는 행만을 출력
  - `ORDER BY` 원하는 행의 오름차순, 내림차순 정렬
  - `LIMIT` : 데이터를 가져오는 수
  
[Top](#JS)

---
  
## 12. UPDATE
- **수정**
  - 검색 : `sql update mysql`

- **`UPDATE 'table이름' SET 'column이름 = '값'' WHERE '원하는 행';`**
  - `WHERE` 을 사용하지 않으면 모든 데이터가 바뀐다.
  - `UPDATE topic SET description='ORACLE is', title='Oracle' WHERE id=2;`

[Top](#JS)

---

## 13. DELETE
- **삭제**
  - 검색 : `sql delete in mysql` 

- **`DELETE FROM '테이블이름' WHERE '원하는 행';`**
  - `WHERE` 을 사용하지 않으면 모든 데이터가 삭제된다.
  - `DELETE FROM topic WHERE id =5;`

[Top](#JS)

---

## 14. 수업의 정상
- **혁신과 본질**
  
  - `Relational` = `혁신` = `innovation`
  - `Database` = `본질` = `essence` = `CRUD`

[Top](#JS)

---

## 15. 관계형데이터베이스의 필요성
- **필요성**
  
  - 중복 개선을 위해 테이블을 분리
  - 저장할땐 분리, 보여줄 땐 병합
  
[Top](#JS)

---  
  
## 16. 테이블 분리하기
- **흐름을 이해해보자**

  - `topic` 테이블 이름을 `topic_backup` 으로 변경
  - `topic` 테이블의 `author_id` 가 `author` 테이블 참조

```sql
--
-- Table structure for table `author`
--
 
 
CREATE TABLE `author` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `profile` varchar(200) DEFAULT NULL,
  PRIMARY KEY (`id`)
);
 
--
-- Dumping data for table `author`
--
 
INSERT INTO `author` VALUES (1,'egoing','developer');
INSERT INTO `author` VALUES (2,'duru','database administrator');
INSERT INTO `author` VALUES (3,'taeho','data scientist, developer');
 
--
-- Table structure for table `topic`
--
 
CREATE TABLE `topic` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(30) NOT NULL,
  `description` text,
  `created` datetime NOT NULL,
  `author_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
);
 
--
-- Dumping data for table `topic`
--
 
INSERT INTO `topic` VALUES (1,'MySQL','MySQL is...','2018-01-01 12:10:11',1);
INSERT INTO `topic` VALUES (2,'Oracle','Oracle is ...','2018-01-03 13:01:10',1);
INSERT INTO `topic` VALUES (3,'SQL Server','SQL Server is ...','2018-01-20 11:01:10',2);
INSERT INTO `topic` VALUES (4,'PostgreSQL','PostgreSQL is ...','2018-01-23 01:03:03',3);
INSERT INTO `topic` VALUES (5,'MongoDB','MongoDB is ...','2018-01-30 12:31:03',1);
```

[Top](#JS)

---

## 17. JOIN
- **`topic` 테이블의 `author_id` 값과 `author` 테이블의 `id` 값을 연결**

- **`SELECT * FROM topic LEFT JOIN author ON topic.author_id=author.id;`**
  - `topic` 테이블과 `join` 테이블을 합친다
  - `ON` 조건 만족시키는 경우

- **`SELECT id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;`**
  - 오류

- **`SELECT topic.id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;`**
  - 정상 출력

- **`SELECT topic.id AS topic_id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;`** 
  - 열에 `id` 란 값이 2개 중복되므로 `id` 를 `topic.id` 로 열 구분을 해줘야 함
  - `topic.id AS topic_id`에서 `AS` 를 이용해 이름 변경하여 출력 가능

- **테이블을 분리한다는 것은, 모든 테이블이 식별자 값만 행에 포함하고 있다면<br>
**`JOIN` 을 통해 얼마든지 관계를 맺을 수 있다.**

[Top](#JS)

---

## 18. 인터넷과 데이터베이스
- **`client` → `Internet` → `server`**

- **`client` ← `Internet` ← `server`**

- **`mysql` 은 `서버` 와 `클라이언트` 둘다 설치
  - `mysql monitor(client)` 를 통해 명령어로 `server` 를 제어
  - `database server` 를 직접 제어할 수 없다.

[Top](#JS)

---

## 19. MySQL Client
- **MySQL monitor**
 
  - 어디서나 사용가능
  - `CLI` 기반
 
- **MySQL client**
  - 검색 : `mysql client`

[Top](#JS)

---

## 20. MySQL Workbench 

- **Workbench GUI 환경**

  - `SQL` 을 `MySQL 서버`에 전송함으로써 데이터베이스 서버를 제어
  - `./mysql -uroot -p -hlocalhost`

[Top](#JS)

---

## 21. 수업을 마치며 
- **공부할 것들**

  - `index` (색인) : 사용자들이 검색을 자주 하는 컬럼에 색인을 걸어둠
  - `modeling` : 성능, 설계
  - `backup` : 내 컴퓨터와 별도의 컴퓨터에 복제해서 보관 ex) `mysqldump`, `binary log`
  - `cloud` : 내 컴퓨터가 아닌 큰 회사들의 인프라를 임대해서 원격 제어.<br>`backup`도 알아서 해준다.<br>ex) `AWS RDS`, `Google Cloud SQL for MySQL`, `AZURE Database for MySQL`
  - `programming` : DB 서버 핸들링<br>ex) `python mysql api`, `php mysql api`, `java mysql api`

[Top](#JS)

---
# ⭐
# AWS1

- [생활코딩 AWS 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMDNWIEgnXjaZ3jgbIo5zQGi)

[Top](#JS)

---

## 1. Amazon Web Services 수업소개
- **Cloud Computing**
  - 남의 컴퓨터를 빌려원격 제어를 통해서 사용하는 것

- **Hosting**
  - 컴퓨터를 빌려주는 임대사업

- **EC2**
  - Elastic Compute Cloud

- **RDS**
  - Relational Database Service
    - MySQL, SQL Server, ORACLE

[Top](#JS)

---

## 2. 수업의 목적
 - **상상**

  - 맥북을 사용하고 있지만 윈도우가 필요하다!

[Top](#JS)

---

## 3. 나에게 필요한 서비스를 찾기
- [AWS](https://aws.amazon.com/ko/)

  - 제품 : 스토리지, 데이터베이스, 기계 학습, 사물 인터넷, AWS 비용 관리, 관리 도구
  - 컴퓨팅 : Amazon EC2

[Top](#JS)

---

## 4. 요금 따져보기
- **온디맨드**
  - 쓰는만큼 요금 지불
  - 운영체제, 리전(Resion)

- **예약 인스턴스**
  - 할인쿠폰

- **스팟 인스턴스**

- **전용 호스팅**

[Top](#JS)

---

##  5. 프리티어
- [AWS 프리 티어](https://aws.amazon.com/ko/free)

  - 1년동안 무료로 사용

[Top](#JS)

---

## 6. 회원가입
- [AWS](https://aws.amazon.com/ko/)
  - `가입 완료`
  - `AWS 계정 새로 만들기`
  - `기본 플랜`
  - `콘솔에 로그인`, `AWS management Console`

[Top](#JS)

---

## 7. 서비스 켜기 EC2
- **EC2 대시보드**
  - `인스턴스` : 컴퓨터 한 대
    - 새 키 페어 생성
    - 키 페어 다운로드

[Top](#JS)

---

## 8. 원격제어
- **EC2 대시보드**
  - `인스턴스`
    - 원격 데스크롭 파일 다운로드
    - 암호 가져오기에 키페어 업로드

[Top](#JS)

---

## 9. 서비스끄기 EC2
- **인스턴스 상태**
  - `중지`
    - 컴퓨터의 전원을 끈다.
    - 데이터는 남는다.
    - 아이피가 변경된다.

  - `종료`
    - 컴퓨터를 버리는 것
    - 데이터도 사라진다.

[Top](#JS)

---

## 10. 돈 관리
- **내 결제 대시보드**
  - `Month-to-Date`

- **Budget**
  - 예산 설정이 가능

[Top](#JS)

---

## 11. 보안 (OTP)
- **IAM**
  - `루트 계정에서 MFA 활성화`
  - `MFA 활성화`
  - `가상 MFA 디바이스`

[Top](#JS)

---

## 12. 계정종료
- **`내 계정`**
  - `Close Account`

[Top](#JS)

---

## 13. 수업을 마치며
- **공부할만한 주제들**

  - `S3` : 컴퓨터의 부분 기능 서비스 ex) 파일 저장
    - `CLI` 을 통해 제어 가능

[Top](#JS)

---
# ⭐
# Git1
- [생활코딩 Git1 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCNJESahrVV-uYGMNYK_vMf)

[Top](#JS)

---

## 1. 수업소개
- **소스코드 지옥**

[Top](#JS)

---

## 2. git을 구경합시다!
- **Git의 3대 목적**

  - `version`
  - `backup`
  - `collaborate`

[Top](#JS)

---

## 3. git의 목적 1 - 버전관리
- **변화가 될 때마다 설명**

[Top](#JS)

---

## 4. git의 목적 2 - 백업
- **소중한 정보를 다룰때**

[Top](#JS)

---

## 5. git의 목적 3 - 협업
- **로컬 저장소, 원격 저장소**

  - `push`, `pull`

[Top](#JS)

---

## 6. git의 종류
- **git**

[Top](#JS)

---

## 7. 수업을 마치며
- **이후 학습 순서**

  - Version
  - Backup
  - Collaborate

[Top](#JS)

---
# ⭐
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
# ⭐
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
