# undefined 타입

undefined 타입의 값은 `undefined` 가 유일하다.

var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화된다. 따라서 변수를 선언한 이후 값을 할당하지 않은 변수를 참조하면 undefined가 반환된다.

```jsx
var a;
console.log(a); // undefined
```

이처럼 undefined는 **개발자가 의도적으로 할당하기 위한 값이 아니다**. 만약 변수에 값이 없다는 것을 명시하고 싶다면 undefined가 아니라 null을 할당하는 것이 좋다.
