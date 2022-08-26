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
