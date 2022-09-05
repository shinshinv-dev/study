# 리액트 Hooks 10분만에 사용법 배우기 | Learn How to use React Hooks in 10 min
- functional component 에서 state을 가질 수 있게 해줌
- 앱을 래액트 훅으로 만든다면, class component, did mount, render.. 이런 것들을 안해도 된다는 뜻, 모든것은 하나의 function 이 되는 것
```
import React , {useState } from "react";
const [conunt, setCount] = useState(0);
```
```
const [email, setEmail] = useState("");
const updateEmail = e => {
  const {
    target: {value}
  } = e;
  setEmail(value);
};

return (
  <>
    <input placeholder="Email" value={email} onChange={updateEmail}
  </>
)
```

