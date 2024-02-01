# 프로토타입과 \_\_proto\_\_

## "자바스크립트는 객체지향 언어인데 다른 객체지향 언어와는 꽤 다르구나"

### 제가 모던 자바스크립트 Deep Dive를 공부하며 생각하게 된 문장입니다. 분명 자바스크립트는 객체지향 언어이지만 다른 언어들과 달리 class 기반 언어가 아닙니다. 자바스크립트는 prototype 기반 언어라고 할 수 있습니다.

### 그렇다면, prototype는 무엇이고, 상속과 같은 객체지향의 핵심 기능을 어떻게 구현할까요?

##

> 모든 JavaScript 객체는 프로토타입을 가지며, 프로토타입은 해당 객체의 기본 프로퍼티와 메서드를 정의한다.

위 문장을 보면, 객체지향을 공부한 사람들이라면 프로토타입은 **객체 간 상속** 을 구현하기 위해 사용된다는 것을 알 수 있을 것 같습니다.

프로토타입은 어느 객체의 부모 역할을 하는 객체로서, 다른 객체에 공유 프로퍼티(메서드도)를 제공합니다. 그러므로 프로토타입을 상속받은 자식 객체는 부모의 프로퍼티를 자신의 것처럼 사용할 수 있게 됩니다.

객체와 프로토타입은 서로 연결되어 있지만, 책에서는 객체는 프로토타입에 접근하려면 \_\_proto\_\_ 접근자 프로퍼티를 통해 접근해야 한다고 합니다.

그 이유는 직접 접근이 가능하게 되면 서로가 서로의 프로토타입이 되어 무한으로 체인이 돌게 되기 때문입니다. 따라서 **단방향 체인**을 지키기 위함이라고 할 수 있습니다.

크롬 브라우저에서 테스트해 봤습니다.

```js
const person = { name: 'hun' };
```

을 선언하고 person을 부르면,

```js
[[Prototype]]: Object // 책에는 __proto__: 로 되어있다.
constructor: ƒ Object()
hasOwnProperty: ƒ hasOwnProperty()
isPrototypeOf: ƒ isPrototypeOf()
propertyIsEnumerable: ƒ propertyIsEnumerable()
toLocaleString: ƒ toLocaleString()
toString: ƒ toString()
valueOf: ƒ valueOf()
.....등등
```

가 나옵니다. 그런데 책에는 \_\_proto\_\_로 상단이 출력되는데 제가 출력한 코드에는 [[Prototype]]가 출력되어 이상해서 검색을 해 보았습니다.

그랬더니 대부분 **proto보다는 Object.getPrototypeOf를 사용하자** 라는 말을 하고 있었습니다. 실제로 제가 console.log를 찍어 보았는데도 둘 다 별 차이가 없었습니다. 그래서 proto가 정말 안 쓰이는지, 검색을 해 보았습니다.

##

### \_\_proto\_\_는 deprecated 되었다.

현재 \_\_proto\_\_는 deprecated, 즉 **더 이상 권장되지 않는 기능**이라고 합니다.

\_\_proto\_\_는 호환성을 위해 ES6에서 표준으로 채택했다곤 하지만, 아래와 같이 모든 객체가 proto를 사용할 수 있는 게 아니라서 코드 내에서 proto를 사용하는 것은 권장되지 않는다고 합니다.

```js
const obj = Object.create(null);

console.log(obj.__proto__); // undefined
```

obj는 프로토타입의 종점, 즉 null 프로토타입을 가지므로 proto를 가질 수 없습니다.

이 때문에 \_\_proto\_\_대신 [[prototype]]의 값을 참조하고 싶은 경우 Object.getPrototypeOf 메서드를 사용하고, 값을 바꾸고 싶을 땐 Object.setPrototypeOf 메서드를 사용하라고 하는 것 같습니다.

##

### 물론 우리가 개발하면서 proto와 같은 프로토타입을 조정하는 기능을 구현하리라곤 생각되지 않습니다. 특히 proto는 표준인지 비표준인지 사람에 따라 말이 달라, 검색이 정말 어려웠습니다.

### 아직 프로토타입은 배울 게 많습니다..ㅜ 그래서 다음에는 프로토타입의 생성 시점과 객체 리터럴, 클래스와 같이 여러 객체 생성 방식에 따른 프로토타입의 결정에 대해 알아보겠습니다.
