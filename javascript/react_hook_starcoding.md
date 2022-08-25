# useState 15분만에 마스터하기 | 리액트 훅스 시리즈
```
# 1
const [state, setState] = useState(초기값);

# 2
setState((prevState) => {
  // some works...
  return new State;
});

# 3
useState(() => {
  return heavyWorks();
});
```

# useEffect 깔끔하게 마스터하기 | 리액트 훅스 시리즈
- Mount : 화면에 첫 렌더링
- Update : 다시 렌더링
- Unmount: 화면에서 사라질때

```
useEffect( () => { //작업... } )
```

