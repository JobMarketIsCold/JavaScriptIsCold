# typeof 연산자

typeof 연산자는 피연산자의 데이터 타입을 문자열로 반환한다. typeof 연산자는 7가지 문자열 “string”, “number”, “boolean”, “undefined”, “symbol”, “object”, “function” 중 하나를 반환한다. 그러나 typeof 연산자가 반환하는 문자열이 7개의 데이터 타입과 정확히 일치하지는 않는다.

```jsx
typeof ""; // "string"
typeof 1; // "number"
typeof NaN; // "number"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof Symbol(); // "symbol"
typeof null; // "object"
typeof []; // "object"
typeof {}; // "object"
typeof new Date(); // "object"
typeof /test/gi; // "object"
typeof function () {}; // "function
```

typeof 연산자로 null 값을 연산해 보면 “null” 이 아닌 “object” 를 반환하는 점을 주의하자 .이는 자바스크립트 첫 번째 버전의 버그이다. 따라서 null 타입을 확인할 때에는 일치 연산자(===)를 사용하자.

```jsx
var foo = null;

typeof foo === null; // false
foo === null; // true
```

또 주의해야 할 점은 선언하지 않은 식별자를 typeof 연산자로 연산하면 오류가 발생하는것이 아닌 undefined를 반환한다는 점이다.

```jsx
// undeclared 식별자를 선언한 적이 없다.
typeof undeclared; // undefined
```
