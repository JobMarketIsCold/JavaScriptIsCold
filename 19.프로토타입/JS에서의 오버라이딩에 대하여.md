# JS에서의 오버라이딩에 대하여

> ### 오버라이딩: 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의하여 사용하는 방식

### 대부분 사람들이 알고 있는 오버라이딩입니다. 그렇다면 자바스크립트 엔진은 어떻게 오버라이딩을 처리하고, 이 과정에서 무슨 개념이 필요할까요?

##

### 오버라이딩을 이해하기 위한 개념들부터 알아봅시다.

- 프로토타입이 소유하는 프로퍼티 : 프로토타입 프로퍼티
- 인스턴스가 소유하는 프로퍼티 : 인스턴스 프로퍼티

여기서 프로퍼티를 추가할 때, 프로토타입 프로퍼티와 같은 이름의 프로퍼티를 추가하면 프로토타입 프로퍼티를 검색하여 이를 덮어씌우는 게 아닌, **인스턴스 프로퍼티로 추가**합니다. 이 때, 인스턴스 메서드는 프로토타입 메서드를 오버라이딩하고 프로토타입 메서드는 가려집니다.

이와 같이 상속 관계에 의해서 프로퍼티가 가려지는 현상을 **프로퍼티 섀도잉** 이라고 합니다.

들으면 잘 이해가 되지 않을 수도 있습니다. 자바로 설명하면, 클래스를 상속 받을 때 메서드 오버라이딩을 통해 하위 클래스가 상위 클래스의 메서드를 재정의하여 가리는 것과 비슷하다고 볼 수 있습니다.**(명재 고마워!!!!!!!!!!!)**

또한, 프로퍼티를 삭제하는 경우에도 단순한 인스턴스 메서드는 delete키워드로 삭제할 수 있지만, 프로토타입 메서드는 delete와 같이 하위 객체를 통해 프로토타입의 프로퍼티/메서드를 삭제할 수 없습니다. 즉, get은 허용되지만 set은 허용되지 않습니다.

### 그렇다면, 프로토타입을 set, 교체하려면 어떻게 해야 할까요?

##

## 프로토타입의 교체

### 프로토타입은 생성자 함수, 인스턴스 위 두 가지 방법으로 교체할 수 있습니다.

```js
const Person = (function () {
  function Person(name) {
    this.name = name;
  }
  Person.prototype = {
    // 프로토타입 교체
    sayHello() {
      console.log(`${this.name}`);
    },
  };

  return Person;
})();

const me = new Person('me');
```

여기서 Person.prototype에 객체 리터럴을 할당했습니다. 이는 Person 생성자 함수가 생성할 객체의 프로토타입을 객체 리터럴로 교체한 것입니다.

프로토타입으로 교체한 객체 리터럴에는 당연하게도 constructor 프로퍼티가 없으므로, me 객체의 생성자 함수는 Person이 아닌 Object일 것입니다. 이렇게 교체하게 되면 constructor와 생성자 함수 간의 연결이 파괴된다는 것입니다.

```js
console.log(me.constructor === Person); //false
console.log(me.constructor === Object); //true
```

이렇게 파괴된 연결을 살리려면, 객체 리터럴에 constructor 프로퍼티를 추가하면 됩니다.

```js
const Person = (function () {
  function Person(name) {
    this.name = name;
  }
  Person.prototype = {
    constructor: Person, // constructor 추가
    sayHello() {
      console.log(`${this.name}`);
    },
  };

  return Person;
})();

const me = new Person('me');
```

### 인스턴스에 의한 프로토타입은, 앞서 배웠던 **proto**나 Object.setPrototypeOf 메서드를 통해 교체할 수 있습니다.

```js
function Person(name) {
  this.name = name;
}

const me = new Person('me');

const parent = {
  sayHello() {
    console.log(`hello, ${this.name}`);
  },
};

Object.setPrototypeOf(me, parent); // 교체
```
