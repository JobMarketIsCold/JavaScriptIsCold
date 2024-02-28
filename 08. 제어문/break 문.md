# break 문

`break` 문은 코드 블록을 탈출한다. 정확히는 레이블 문, 반복문, switch문의 코드 블록을 탈출한다. 이 외에 break문을 사용하면 SyntaxError가 발생한다.

```jsx
if (true) {
	break; // SyntaxError
}
```

레이블 문은 식별자가 붙은 문을 말한다.

```jsx
foo: console.log("foo");
```

레이블 문은 프로그램의 실행 순서를 제어하는 데 사용한다. switch문의 cas문과 default문도 레이블 문이다. 레이블 문을 탈출하려면 break문에 레이블 식별자를 지정한다.

```jsx
foo: {
  console.log(1);
  break foo;
  console.log(2);
}

console.log("done");
```

중첩된 for문 내부 for문에서 break문을 실행하면 내부 for문을 탈출하여 외부 for문으로 진입한다. 이때 내부 for문이 아닌 외부 for문을 탈출하려면 레이블 문을 사용한다.

```jsx
outer: for (var i = 0; i < 5; i++) {
  for (var j = 0; j < 5; j++) {
    if (i + j === 3) break outer;
    console.log(`[${i}, ${j}]`);
  }
}

console.log("done");
```

break문은 레이블 문 뿐만 아니라 반복문, switch문에서도 사용할 수 있다. 이 경우에는 break문에 레이블 식별자를 지정하지 않는다.

다음은 문자열에서 특정 문자의 인덱스를 검색하는 예다.

```jsx
var string = "Hello World.";
var search = "l";
var index;

// 문자열은 유사 배열이므로 for문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l' 이면
  if (string[i] === search) {
    index = i;
    break;
  }
}

console.log(index); // 2
```
