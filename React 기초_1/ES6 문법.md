# 가변변수 vs 불변변수

ES6란 자바스크립트를 표준화하기 위해 만들어진 스크립트 프로그래밍 언어를 말합니다.

ES6에서는 기존 자바스크립트에서 사용하던 문법 외에 다양한 것을 제공합니다.
```
let x = 2;
const x = 2;
```
여기서 let은 가변변수로 재선언이 가능하지만 재정의가 불가능합니다. 반면 const는 불변변수로 재선언과 재정의가 불가능합니다.

자바스크립트에서 배웠던 var와 함께 비교하면 아래와 같습니다.

| 선언 방식 | 재선언 | 재정의 |
|:---:|:---:|:---:|
| var | 가능 | 가능 |
| let | 불가능 | 가능 |
| const | 불가능 | 불가능 |

- 재선언: 똑같은 이름의 변수를 다시 만드는 것
- 재정의: 값이 지정된 변수에 값을 바꾸려는 행위

가변변수와 불변변수의 차이를 비교해보는 실습을 해봅시다.

```
var z = 2;
let x = 2;
const y = 2;

z = 4;
x = 4;
// let x = 2; 오류남
// const y = 4; 오류남

document.write(z);
document.write(x);
document.write(y);
```

# 화살표 함수

화살표 함수는 ES6에 추가된 표현식으로 화살표 기호 =>를 사용하여 함수를 선언합니다.

아래 예시를 살펴보겠습니다. 두 수를 입력 받아 곱을 반환하는 함수를 만들려고 합니다. 기존 자바스크립트에서는 아래처럼 선언을 해야 했습니다.
```
var x = function(x, y) {
   return x * y;
}
```

하지만 ES6의 화살표 함수를 이용하면 위의 코드를 한 줄로 표현할 수 있습니다. 

function 키워드를 생략하고 인자 블록(( ))과 본문 블록({ }) 사이에 =>를 표기해서 화살표 함수를 만듭니다.
```
const x = (x, y) => x * y;
```
만든 함수를 호출해서 값이 잘 나오는지도 확인해보세요.
```
document.write(x(5, 5));
```

```
// const x = (x, y) => x * y;

// document.write(x(5, 5));

const plus = (x, y, z) => x + y + z;

document.write(plus(10, 20, 30));
```

# 클래스

기존 자바스크립트 문법은 클래스 표현식이 없었지만 ES6는 클래스를 정의하여 사용할 수 있습니다.

class 키워드로 클래스를 정의할 수 있습니다. 클래스 내에 생성자**(constructor())**도 항상 포함되어 있어야 합니다. 

클래스에 대한 자세한 내용은 링크<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes>에서 확인해보세요!
```
class ClassName {
  constructor() { ... }
}
```
아래는 자동차의 이름과 연도에 대한 정보를 담는 클래스입니다.
```
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
}
```
클래스 객체 생성은 아래처럼 할 수 있습니다.
```
let myCar1 = new Car("Ford", 2014);
let myCar2 = new Car("Audi", 2019);
```
생성한 객체의 요소들에 접근하여 출력할 수도 있습니다.
```
document.write(myCar1.name)
document.write(myCar1.year)
```

```
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
}

let myCar1 = new Car("Ford", 2014);
let myCar2 = new Car("Audi", 2019);

document.write(myCar1.name)
document.write(myCar1.year)
document.write(myCar2.name)
document.write(myCar2.year)
```

# forEach() 함수

자바스크립트에서는 for문을 사용하여 반복문을 나타냈습니다.

하지만 forEach() 함수를 사용하면 반복문의 순번과 배열의 크기를 따로 변수에 저장하는 과정을 생략할 수 있습니다.

forEach()는 키를 넣어주면 키값을 반환해주는 구조 분해 할당 방식입니다. 

리스트의 요소가 키이고 forEach(함수)의 매개변수에 입력된 함수에 키를 넣고 값을 받는 것이라고 이해하면 됩니다. 

이것을 이용하면 반복문 코드를 더 간결하게 바꿀 수 있습니다.

예시와 함께 살펴봅시다. 아래에 과일이 담긴 배열이 있습니다.
```
var fruits = ["apple", "orange", "cherry"];
```
배열의 각 요소를 반복문 forEach()를 이용해 접근할 수 있습니다.
```
fruits.forEach(myFunction);
```
myFunction은 인덱스와 아이템을 출력하는 함수입니다.
```
function myFunction(item, index) {
    document.write(index + ":" + item + "<br>"); 
}
```

```
var fruits = ["apple", "orange", "cherry"];

function myFunction(item, index) {
  document.write(index + ":" + item + "<br>"); 
}

fruits.forEach(myFunction);

// for (i = 0; i < 3; i++) {
//     document.write(i);
//     document.write(":" + fruits[i] + "<br>");
// }
```

# map() 함수

map() 함수는 각 배열 요소를 정의된 함수를 통해 변환한 결괏값들로 새 배열을 반환합니다. 

쉽게 말해 배열을 가공하여 새 배열을 만드는 함수입니다.

예를 들어 아래와 같이 딕셔너리 배열이 주어졌습니다. 딕셔너리 요소인 firstname과 lastname을 합한 전체 이름을 출력하려고 합니다.
```
var persons = [
  {firstname : "Malcom", lastname: "Reynolds"},
  {firstname : "Kaylee", lastname: "Frye"},
  {firstname : "Jayne", lastname: "Cobb"}
];
```
먼저 getFullName() 함수에 대해 살펴봅시다. 해당 함수는 item의 firstname과 lastname을 더해서 반환하고 있습니다.
```
function getFullName(item) {
  var fullname = item.firstname + " " +item.lastname;
  return fullname;
}
```
그리고 persons 리스트에 대해 getFullName 함수에 map()을 이용한 결과를 확인해봅시다. map()은 아래와 같은 형태로 사용됩니다.
```
document.write(persons.map(getFullName));
```

또한 map() 함수와 자바스크립트의 내장함수를 이용해 결과를 얻을 수도 있습니다. 

자바스크립트 내장 함수 중 ```Math.sqrt()```는 제곱근을 반환합니다. 즉, 특정 숫자의 루트를 씌운 값을 반환합니다.
```
document.write(Math.sqrt(4));
```
해당 함수를 이용해 각 요소에 루트 연산을 한 새로운 배열을 얻고 싶다면 아래처럼 map() 함수를 이용하면 됩니다.
```
var numbers = [4, 9, 16, 25];
var x = numbers.map(Math.sqrt)
document.write(x);
```

```
var persons = [
  {firstname : "Malcom", lastname: "Reynolds"},
  {firstname : "Kaylee", lastname: "Frye"},
  {firstname : "Jayne", lastname: "Cobb"}
];

function getFullName(item) {
  var fullname = item.firstname + " " +item.lastname;
  return fullname;
}

document.write(persons.map(getFullName));


document.write("<br>");
var numbers = [4, 9, 16, 25];
var x = numbers.map(Math.sqrt);
document.write(x);
```

# reduce() 함수

덧셈 함수라고 많은 분들이 알고 계시는 reduce()는, 사실 매우 강력한 함수입니다.

reduce()는 배열의 각 요소에 대해 주어진 함수를 실행한 후, 하나의 결과값을 반환합니다.

앞에서 학습한 map이 배열의 각 요소를 변형한다면, reduce는 배열 자체를 변형합니다.

예를 들어, 배열에 들어있는 숫자를 더하거나 평균을 구하는 것은 배열을 값 하나로 줄이는 동작입니다.
```
배열.reduce((누적값, 현재값, 인덱스, 요소) => { return 결과 }, 초기값);
```
위 문법에서 이전 값이 아니라 누적 값이라는 점을 유의해주셔야 합니다.

```
var numbers = [175, 50, 25];

document.write(numbers.reduce(myFunc));

function myFunc(total, num) { //누적값
  return total - num;
}
```
