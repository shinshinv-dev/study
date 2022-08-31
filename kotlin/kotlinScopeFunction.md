> https://www.youtube.com/watch?v=-X8uUOqjeSg

# 스코프함수 run, let, apply, also, with
- run : 변수를 통째로 넘김 > 코드의 반복을 줄임
```
val list = mutableListOf(1,2,3,4,5)

// list.add(6)
// list.add(7)

list.run { //this: list
  add(6)
}
```
- list : 변수명을 지정해서 사용할수 있음 (alias)
```
// 1
list.let {
  it.add(6)
  it.add(7)
}

// 2 (alias)
list.let { item ->
  item.add(6)
  item.add(7)
}
```
