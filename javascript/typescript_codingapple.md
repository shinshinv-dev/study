# Typescript 필수문법 10분 정리와 설치 셋팅 (Vue, React 포함)
- 자유도가 높은 Javascript의 타입을 엄격히 검사
- 에러메세지가 정확함
```
let name: string = 'shin';
let name: { name?: string } = { };
let name: string | number = 123;

// type alias
type MyType = string | number;

function multiply(x : number) : number {
  return x * 2
}

// tuple type
type Member = [number, boolean];
let john: Member = [123, true]

// object key
// type Member = { name: string }
type Member = {
  [key: string]: string
}
```

- Type 종류
>- string
>- number
>- boolean
>- null
>- undefined
>- bigint
>- []
>- {}
>- ...
