# 講義で学んだ知識を問うGoに関するクイズを作成せよ
- クイズの回答とそのクイズで問われる知識について解説せよ
- 間違える可能性のある回答はなにか？
  - 何を理解していないと間違ってしまうのか？
- 他の人とかぶらないように工夫をすること
- 例：https://tenn.in/quiz
  - 4択でなくても良い

## 第 1 問
```go
package main

func main() {
	var num int
}
```
1. compile error
2. panic
3. 正常終了

<details>
<summary>答え</summary>

1. compile error

理由:  
go 言語では、定義した変数を必ず使用しなければならない。
</details>

## 第 2 問
```go
package main

func main() {
	num := 1
	println(num)
}
```
1. compile error
2. panic
3. 0
4. 1

<details>
<summary>答え</summary>

4. 1

理由:  
go 言語では、`:=` を使用して代入することで、変数宣言を書かなくても変数を作成することができる。
</details>

## 第 3 問
```go
package main

func main() {
	num := 1
	if (num == 1) println(num)
	else println(num + 1)
}
```
1. compile error
2. panic
3. 1
4. 2

<details>
<summary>答え</summary>

1. compile error

理由:  
go 言語では、`if` 文を使用する時、
```go
if num == 1 {
} else {
}
```
の様に記述しなければコンパイルエラーを起こすようになっている。
</details>

## 第 4 問
```go
package main

func main() {
    numbers := []int{10, 20, 30, 40, 50}
    nums := numbers[0:3]
    println(len(nums))
}
```
1. compile error
2. panic
3. 5
4. 3

<details>
<summary>答え</summary>

4. 3

理由:  
go 言語では、スライスを使うことで、配列の指定範囲をコピーすることができる。  
```go
variable := array[first:last]
```
の様に記述すると、配列 `array` の 範囲 `first` から `last` までの範囲をコピーし、`variable` に代入される。
</details>

## 第 5 問
```go
package main

func main() {
    num := 1_000
    result := num / 100
    println(result)
}
```
1. compile error
2. panic
3. 10
4. 1

<details>
<summary>答え</summary>

3. 10

理由:  
go 言語では、可読性向上のため、数字を `_` で区切ることができる。
</details>

## 第 6 問
```go
package main

func main() {
    var numCount map[int]int
    numCount[1]++
	println(numCount[1])
}
```
1. compile error
2. panic
3. 1
4. 10

<details>
<summary>答え</summary>

2. panic

理由:  
`numCount` は、`nil` で初期化されているため、`panic` になってしまう。
```go
numCount := make(map[int]int)
または、
numCount := map[int]int{}
```
このように書き換えると、指定の型で初期化することができるので、`panic` にならない。
</details>

## 第 7 問
`main.go`
```go
package main

import sub "インポート先"

func main() {
	sub.subMethod()
}
```
`sub.go`
```go
package sub

func subMethod() {
    println("sub")
}
```
1. compile error
2. panic
3. sub

<details>
<summary>答え</summary>

1. compile error

理由:  
`subMethod` は、パッケージ外にエクスポート (公開) されていないため、見つからずに `compile error` となる。
```diff_go
+ func SubMethod() {
- func subMethod() {
    println("sub")
}
```
このように、関数名の先頭文字を大文字にすることで、パッケージ外にエクスポートすることができる。
</details>