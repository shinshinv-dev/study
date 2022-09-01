> https://www.youtube.com/watch?v=-X8uUOqjeSg

# 스코프함수 run, let, apply, also, with
- run : 변수를 통째로 넘김 > 코드의 반복을 줄임
```
val list = mutableListOf(1,2,3,4,5)

// list.add(6)
// list.add(7)

val result = list.run { //this: list
  add(6)
}
```
- list : 변수명을 지정해서 사용할수 있음 (alias)
```
// 1
val result = list.let {
  it.add(6)
  it.add(7)
}

// 2 (alias)
val result = list.let { item ->
  item.add(6)
  item.add(7)
}
```
- apply : run 과 사용법이 같음 > 마지막 줄과 상관없이 원래 변수에 변경된 값(객체 자체를 리턴), run 은 마지막줄의 값을 리턴

- also : let 과 사용법이 같음 > 마지막 줄과 상관없이 원래 변수에 변경된 값(객체 자체를 리턴), let 은 마지막줄의 값을 리턴

- with : 
```
binding.button.setOnClick()
binding.imageView.setImage()
binding.textView.text = " "

with(binding) {
  button.setOnClick()
  ...

}
```
