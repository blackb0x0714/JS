# 📝 Table of Contents

# JS

- [JS-OOP](#OOP)
- [JS-Immutability](#Immutability)
- [Ajax](#Ajax)
- [REACT](#REACT)
- [NPM](#NPM)
- [궁금했던 것들](#Question-Mark)

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

# Ajax

- [생활코딩 Ajax 수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMA9-1PvblBehoGg7Pu1lg6q)

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
      👉mode: 'mode',
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

- **컴포넌트 생성이 끝난 후 동적으로 state값을 변경하고 싶을 때는<br>`this.state.mode = 'welcome` 이 아닌 `this.setState({mode: 'welcome'})`로 변경해야 한다.**

- **이유**
  - 리액트가 state 값의 변화를 인지못하여 렌더링을 하지 못한다.

[Top](#JS)

---

## 17.1 컴포넌트 이벤트 만들기

- **목표**

  - 이벤트를 만드는 생산자가 되어보기
  - `Subject` 컴포넌트안에 이벤트 생성
  - App 컴포넌트의 mode가 'welcome'으로 바뀌게

- **순서**
  - `Subject` 컴포넌트안에 우리가 `onChangePage`라는 이벤트를 만들고 함수를 설치
  - 그 이벤트가 발생되었을 때 `props`로 전달된 `onChangePage` 함수가 실행된다.

```javascript
// App.js
class App extends Component {
  constructor(props) {
    super(props)
    this.state = {
      {/*생략*/}
    }
  }
  render() {
      {/*생략*/}
    }
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

  - `<TOC>`의 anchor 태그를 클릭했을 때 `mode`를 `read`로 바꿔주기
  
```javascript
// App.js
return (
      <div className="App">
        <TOC
          👉onChangePage={function () {
            this.setState({
              mode: 'read',
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
            👉onClick={function (e) {
              e.preventDefault()
              this.props.onChangePage()
            }.bind(this)}
          >
            {data[i].title}
          </a>
        </li>
      )
```

[Top](#JS)

---

## 17.3.
- **목표**
  - `List`를 클릭하면 본문이 보일 수 있게
  - `State`의 `selected_id`에 맞는 내용을 표시

- **이벤트 함수는 `target`속성을 가지는데 그 이벤트가 발생한 태그를 가리킨다.**
  - ex) `<a onClick={function(){}}></a>
  - 디버깅을 통해 개발자 도구에서 확인 가능

- **`data-id={data[i].id}`의 값은 `id: "2"`이고, 개발자도구 `Sources`의 `dataset`에서 볼 수 있다.**

- **정리**

- **공통코드 App.js**
```javascript
constructor(props) {
    super(props)
    this.state = {
      mode: 'read',
      👉selected_content_id: 2,
      subject: { title: 'WEB', sub: 'World Wide Web!' },
      welcome: { title: 'Welcome', desc: 'Hello, React!!' },
      contents: [
        { id: 1, title: 'HTML', desc: 'HTML is for information' },
        { id: 2, title: 'CSS', desc: 'CSS is for design' },
        { id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive' },
      ],
    }
  }
  render() {
    console.log('App render')
    var _title,
      _desc = null
    if (this.state.mode === 'welcome') {
      _title = this.state.welcome.title
      _desc = this.state.welcome.desc
    } else if (this.state.mode === 'read') {
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
        <Subject
          title={this.state.subject.title}
          sub={this.state.subject.sub}
          onChangePage={function () {
            this.setState({ mode: 'welcome' })
          }.bind(this)}
        ></Subject>
        <TOC
          👉onChangePage={function (id) {
            this.setState({
              mode: 'read',
              👉selected_content_id: Number(id),
            })
          }.bind(this)}
          data={this.state.contents}
        ></TOC>
        <Content title={_title} desc={_desc}></Content>
      </div>
    )
  }
}
```

- **1. 속성을 이용하는 방법(현재사용코드)**

  - TOP.js의 onClick의 속성을 이벤트를 실행시킬 때<br>
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
</li>);
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
    onClick={function (👉e) {
      e.preventDefault()
      this.props.onChangePage(👉id)
    }.bind(👉this)}
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
