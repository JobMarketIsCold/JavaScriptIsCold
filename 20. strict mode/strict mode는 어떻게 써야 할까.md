# strict mode는 어떻게 써야 할까?

### 깃허브에 있는 코드를 둘러 보다 보면 가끔 최상단에 이런 선언이 있습니다.

```js
'use strict';

...
```

### 유즈 스트릭트? 어디에 쓰는걸까?

### 항상 궁금했지만 별로 알아보고 싶진 않았습니다. 그런데 모던 자바스크립트 Deep Dive에 use strict에 관련한 내용이 있어 배우게 되었습니다.

##

# use strict === 하드코어 모드

### 말 그대로입니다. 상당히 유한 자바스크립트의 문법을 좀 더 엄격하게 보도록 하는 것이 strict mode라고 할 수 있습니다.

적용되는 예시를 보면,

```js
function foo() {
  x = 10;
}
foo();
console.log(x);
```

이렇게 사용하면 console.log에는 무엇이 출력될까요?

js를 공부하거나 사용하는 사람이라면 저 x는 전역으로 선언되지 않았기 때문에 ReferenceError가 발생할 것이라고 생각할 것입니다.

그러나, 10이 출력됩니다. 이는 **암묵적 전역(implicit global)** 때문입니다.

저 코드의 동작방식을 자바스크립트 엔진의 관점에서 설명해 보겠습니다.

- x를 출력해야 하므로, 스코프를 따라서 x 변수를 검색한다.
- foo함수에서 x를 검색한다. foo함수에는 x변수가 없으므로, 상위 스코프인 전역 스코프로 올라가서 검색한다.
- 전역 스코프에도 없으므로 **암묵적으로 전역 객체에 x 프로퍼티를 동적으로 생성한다.** 이 때 x 프로퍼티는 전역 변수처럼 사용이 가능하다(암묵적 전역)

물론 좋다고 생각할 수도 있지만 개발자의 의도와 다르게 암묵적 전역이 발생한 경우는 여러 오류를 일으킬 수도 있기 때문에, 지양해야 합니다.

이와 같은 상황을 위해서 **strict mode**가 존재하는 것입니다.

그러나 저희는 strict mode와 유사한 기능을 이미 사용하고 있습니다.

바로 eslint입니다.

vscode를 사용하신다면 다들 깔아서 쓰실텐데, eslint와 같은 린트 도구는 소스 코드 실행 전에 문법적 오류와 더불어 잠재적 오류까지 잡아줍니다. 따라서 strict mode보다는 린트 도구가 좋다고 봅니다.

다시 돌아가, strict mode를 사용할 때 유의할 점을 살펴 보고 마치겠습니다.

## strict mode 사용 시 유의점

### 최상단에 배치할 것

사용 시에는 솔직히 이것뿐입니다.<br>
js는 순차적으로 코드를 실행하기 때문에 코드 뒤에 있으면 당연히 strict 앞에 있는 코드에는 strict mode가 적용되지 않을 것입니다.

함수 단위로 적용하게 되면, 어떤 함수는 적용하고 어떤 함수는 적용하지 않는 것은 일관적이지 못해 혼란이 올 수 있습니다.

##

### strict mode에 대한 궁금증을 해결하였습니다. 정말 좋은 기능을 가지고 있었던 strict mode였지만 저희는 이미 eslint라는 더 좋은 린트 도구를 사용하고 있었네요!
