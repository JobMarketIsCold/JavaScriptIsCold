# null 타입

null 타입의 값은 `null` 이 유일하다.

프로그래밍 언어에서 null은 변수에 값이 없다는 것을 의도적으로 명시할 때 사용한다. 변수에 null을 할당하는 것은 **변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미**이다.

```jsx
var a = "asdf";

// 이전 참조를 제거한다.
a = null;
```

함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환하기도 한다.

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      var element = document.querySelector(".class");

      // HTML 문서에 class 클래스를 갖는 요소가 없다면 null 반환
      console.log(element); // null
    </script>
  </body>
</html>
```
