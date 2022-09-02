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

# Typescript 컴파일시 세부설정 (tsconfig.json)
- 타입스크립트 ts 파일들을 .js 파일로 변환할 때 어떻게 변환할 것인지 세부설정이 가능
```
{
 "compilerOptions": {

  "target": "es5", // 'es3', 'es5', 'es2015', 'es2016', 'es2017','es2018', 'esnext' 가능
  "module": "commonjs", //무슨 import 문법 쓸건지 'commonjs', 'amd', 'es2015', 'esnext'
  "allowJs": true, // js 파일들 ts에서 import해서 쓸 수 있는지 
  "checkJs": true, // 일반 js 파일에서도 에러체크 여부 
  "jsx": "preserve", // tsx 파일을 jsx로 어떻게 컴파일할 것인지 'preserve', 'react-native', 'react'
  "declaration": true, //컴파일시 .d.ts 파일도 자동으로 함께생성 (현재쓰는 모든 타입이 정의된 파일)
  "outFile": "./", //모든 ts파일을 js파일 하나로 컴파일해줌 (module이 none, amd, system일 때만 가능)
  "outDir": "./", //js파일 아웃풋 경로바꾸기
  "rootDir": "./", //루트경로 바꾸기 (js 파일 아웃풋 경로에 영향줌)
  "removeComments": true, //컴파일시 주석제거 

  "strict": true, //strict 관련, noimplicit 어쩌구 관련 모드 전부 켜기
  "noImplicitAny": true, //any타입 금지 여부
  "strictNullChecks": true, //null, undefined 타입에 이상한 짓 할시 에러내기 
  "strictFunctionTypes": true, //함수파라미터 타입체크 강하게 
  "strictPropertyInitialization": true, //class constructor 작성시 타입체크 강하게
  "noImplicitThis": true, //this 키워드가 any 타입일 경우 에러내기
  "alwaysStrict": true, //자바스크립트 "use strict" 모드 켜기

  "noUnusedLocals": true, //쓰지않는 지역변수 있으면 에러내기
  "noUnusedParameters": true, //쓰지않는 파라미터 있으면 에러내기
  "noImplicitReturns": true, //함수에서 return 빼먹으면 에러내기 
  "noFallthroughCasesInSwitch": true, //switch문 이상하면 에러내기 
 }
}
```

# 타입스크립트 기본 타입 정리 (primitive types)
```
let name: string = shin;
let age: number = 23;
let married: boolean = true;
let members: string[] = ['shin', 'noh'];
let membersobj: {member1: string, member2: string}= { member1: 'shin', member2: 'noh'}

```
- beginer : 온갖타입을 다 지정함 / pro : 타입지정이 원래 자동으로 됨(생략가능)

# 타입을 미리 정하기 애매할 때 (union type, any, unknown)
- union type - 할당을 해버리면 타입이 확정됨
```
let member :number | string = 'shin'
let member :(number | string) = 'shin'
let members :(number|string)[] = [1, '2', 3];
```
- any : 모든 자료형 허용 > typescript 를 쓰는 의미가 없음
```
let name :any;
```
- unknown : 모든 자료형 허용 > any보다는 안전 (타입이 있는 다른변수에 할당이 안됨) >> any보다는 그나마 나음
```
let names :unknown;
names = 123;
names = {};
let var1 :string = names; // 오류 스트링만 가능
```

# 함수에 타입 지정하는 법 & void 타입

```
// 기존
function fun(x) {
    return x * 2
}
fun(30)

// TS
function fun(x :number) :number {
    return x * 2
}
fun(30)

// TS void
function fun() :void{
    1 + 1
}

// TS parameter option 
function fun(x? :number) :void { // == function fun(x :number|undefined) :void { 
    1 + 1
}
fun()
```

