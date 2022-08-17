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
