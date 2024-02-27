# continue 문

`continue` 문은 반복문의 코드 블록을 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.

다음은 문자열에서 특정 문자의 개수를 세는 예다.

```jsx
var string = "Hello World.";
var search = "l";
var count = 0;

// 문자열은 유사 배열이므로 for문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l' 이면
  if (string[i] !== search) continue;
  count++;
}

console.log(count); // 3
```
