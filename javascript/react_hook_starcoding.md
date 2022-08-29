# useState 15분만에 마스터하기 | 리액트 훅스 시리즈
```
// 1
const [state, setState] = useState(초기값);

// 2
setState((prevState) => {
  // some works...
  return new State;
});

// 3
useState(() => {
  return heavyWorks();
});
```

# useEffect 깔끔하게 마스터하기 | 리액트 훅스 시리즈
- Mount : 화면에 첫 렌더링
- Update : 다시 렌더링
- Unmount: 화면에서 사라질때

- 렌더링 될때 마다 실행
```
// 1
useEffect( () => {
  //작업... 
});
```

- 화면에 첫 렌더링 될때 실행 / value 값이 바뀔때
```
// 2
useEffect( () => {
  //작업...
}, [value] );
```

- 화면에 첫 렌더링 될때만 
```
// 3
useEffect( () => {
  //작업...
}, [] );
```


- Clean up 정리
```
useEffect( () => {
  //구독...
  return () => {
    //구독 해지...
  }

}, []);
```

# useRef 완벽 정리 1# 변수 관리 | 리액트 훅스 시리즈
- useRef : 컴포넌트가 Mount >> Unmount 되기 전까지는 값을 유지 / 렌더링이 발생하지 않으므로 성능향상
  > 1. 저장공간으로 사용 : Ref의 변화 -> No 렌더링 -> 변수들의 값이 유지됨 / State의 변화 -> 렌더링 -> 컴포넌트 내부 변수들 초기화 (Ref의 값은 유지됨)
  > 2. DOM 요소에 접근
```
const ref = useRef(value)
// ref : { current: value}
ref.current = "hello"
ref.current = "nice"
```
# useRef 완벽 정리 2# DOM 요소 접근 | 리액트 훅스 시리즈
- ex) Input 요소에 포커스를 줄때
```
useEffect(() => {
    ref.current.focus();
},[]);

const ref = useRef(value)
<input ref = {ref} />
```

# useContext + Context API | 리액트 훅스 시리즈
- useContext는 context로 공유한 데이터를 받아올수 있는 기능
- 그럼 Props는? Context를 사용하면 컴포넌트를 재사용하기 어려워 질수 있다 / Props drilling 을 피하기 위한 목적이라면 Component Composistion을 먼저 고려
