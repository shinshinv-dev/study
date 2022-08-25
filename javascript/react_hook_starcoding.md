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

