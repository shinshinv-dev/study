# React 기초 1강 : 리액트 설치와 셋팅법 (2021+ 스타일)
- [설치] cmd> npx create-react-app blog
- 샘플에는 index.js 에서 app.js 에 있는 내용을 index.html 넣어줌
- public 폴더는 static 파일 저장

# React 기초 2강 : 리액트에선 HTML대신 JSX 써야함 (JSX 사용법)
- 기본문법
 ```
 <div className="클래스명">
 </div>
 ```
 - 리액트는 데이터 바인딩이 쉬움
 ```
 <div> {변수명} </div>
 <div> {함수명()} </div>
 -----
 import logo form '.logo.svg'
 <img src={logo} />
 ```
 - 상상하는 모든곳에 {} 로 변수 집어 넣기 가능
 ```
 <div className={클래스명} />
 ```
 - 스타일은 직접 넣으면 안되고 오브젝트 형식으로 넣어야 함, 대쉬를 사용할수 없고 CamelCase 로 사용해야함
 ```
 <div style={ {color : 'blue', fontSize : '30px'} }> blog </div>
 
 let post = {color : 'blue', fontSize : '30px'} // 변수로도 가능
 ```
 
 # React 기초 3강 : 리액트에선 변수말고 state 만들어 쓰랬죠 (useState)
 - state 사용법 / destruecturing
 - state에 데이터 저장해놓는 이유 : 웹이 App 처럼 동학하게 만들고 싶어서 / state가 변경되면 HTML이 자동으로 재렌더링이 된다
 ```
 import {useState } from 'react';
 let [a ,b] = useState('Test');
 ```
 
# React 기초 4강 : 리액트에서 버튼에 이벤트 리스너 (핸들러) 장착하는 법
- onClick={클릭될때 실행할 함수}
- 두번째변수(ex.setLike) 로 state 변경
```
let [like, setLike] = useState(0);
<h3> {content[0]} <span onClick={ ()=> { setLike(like+1) } }> 🤌 </span> {like} </h3>
```

# React 기초 5강 : state 맘대로 변경하는 법 (setState는 넘 옛날이고염)
- state 는 원본수정 불가 > 복사본을 만들어서 수정해야함 > 수정시에는 deep copy (...var) 사용
- react 대원칙 : immutable data
```
let [content, setContent] = useState(['content1', 'content2', 'content3']);

function changeName() {
  var newArray = [...content];
  newArray[0] = 'content2-1'
  setContent(newArray);
}

<button onClick={ changeName }> ClicK! </button>
```

# 6강 : Component로 HTML 깔끔하게 줄이는 법
- return() 안에는 하나의 html tag 만 가능
- HTML을 한단어로 줄여서 쓸수 있는 방법 : React의 Component 문법
```
return (
  <div>
    <Modal />
  </div>
)
 
function Modal() {
  return (
    <div className="modal">
      <h2>title</h2>
      <p>date</p>
      <p>content</p>
    </div>
  )
}
```
- Component 만드는 법
>- 1. 함수 만들고 이름짓고 (Pascal Case)
>- 2. 축약을 원하는 HTML 넣고
>- 3. 원하는 곳에서 <함수명 />
- fregment 문법 - return() 내부를 묶을때 의미없는 <div> 쓰기 싫으면 <> </>
```
function Modal() {
  return (
    <>
    <div className="modal">
      <h2>title</h2>
      <p>date</p>
      <p>content</p>
    </div>
    </>
  )
}

```
- Component 를 많이 만들면 단점
>- state 쓸 때 복잡해짐 - 상위 component에서 만든 state를 쓰려면 props 문법을 이용해야함
