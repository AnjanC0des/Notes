---
title: "Hi"
output: pdf_document
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">

<style>
div {
    font-family: 'Work Sans', sans-serif;font-size: 16px;
}
</style>
<div>

```go

```  
---  

# Title
## Introduction
**Why Go?**
* Made by Google to address needs unable to be met by other languages.
* Made by the same team of people that made other programming languages like B, C and laid the foundation of programming.
* Go was made to take advantage to multiple cores in computers.
* Made to fast compilation, concurrency, fastish execution and fun developer experience.

**Some beginner go codes**
```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
	fmt.Println("This is line")
}
```

```cmd
This is a line
```

* Printf allows for formatted printing.

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
    const a,b="Name",100
	fmt.Printf("This is a formatted string %s %d",a,b)
}
```

```cmd
This is a formatted string Name 100
```

* %T in the formatted string prints the datatype of the referenced thing.

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
    const a,b="Name",100
	fmt.Printf("Data type of %s = %T and %d = %T",a,a,b,b)
}
```

```cmd
Data type of Name = string and 100 = int
```

* backticks can be used to print raw string literals

```go
package main

import "fmt"

func main() {
	const a, b = "Name", 100
	fmt.Printf(`This is an
example of 
raw string literal`)
}
```

```cmd
This is an
example of 
raw string literal
```

**declarations and assignments**

* Statically type
* variables are decalred by *var* keyword
* short declaration operator :=
* tuple unpacking type decalration
* _ empty declaration
* declaration like var x int which assigns 0 value 
* declaring unused variables not allowed.
* %b and %x to print short declared variables in binary and hexadecimal

**Values,types,conversion,scope and housekeeping**

* conversion: to store a value of type x in a variable with type y assigned to it, we need to convert it and that can be done simply by using syntax y(x) when the conversion can occur.
* there is no concept of type casting 
* the scope of variables assigned from short decalration operator is only limited to the functions they are assigned in.

**Values,types,conversion,scope and housekeeping**

* conversion: to store a value of type x in a variable with type y assigned to it, we need to convert it and that can be done simply by using syntax y(x) when the conversion can occur.
* there is no concept of type casting 
* the scope of variables assigned from short decalration operator is only limited to the functions they are assigned in.
* combining different types in a bigger Struct is called composition
* math/rand-> Intn(n) -> returns a pseudo random number in interval [0,n) math.Pi returns the constant pi 

```go package main 
import (
	"fmt" 
	"math" 
	"math/rand" 
) 
func main() { 
	fmt.Printf("Random number between 0 and 100 = %d \n", rand.Intn(100)) 
	fmt.Printf("Pi= %f", math.Pi) } 
```
```cmd 
Random number between 0 and 100 = 51 Pi= 3.141593 
``` 
* There is no public or private in golang. There is exported and unexported. 
* functions can be defined and their return type and the type of parameters is written after the parameters or function name themselves. 
```go 
package main 
import ( 
	"fmt" 
) 
func main() { 
	fmt.Printf("10+20 = %d", add(10, 20)) 
} 
func add(x int, y int) int { return x + y } 
``` 
```cmd
10+20 = 30 
``` 
* Also when consecutive function parameters share a type you can omit the type of all but the last. 
```go 
func add(x int, y int){ 
// 
} 
``` 
same as 
```go 
func add(x, y int){ 
// 
} 
``` 
* functions can return any number of results like so 
```go 
package main 
import ( 
	"fmt" 
	"math" 
) 
func main() { 
	x, y := twoSqNos(1, 2) 
	fmt.Printf("1 and 2 squared is %f and %f", x, y) 
} 
func twoSqNos(x, y float64) (float64, float64) { 
	return math.Pow(x, 2), math.Pow(y, 2) 
} 
``` 
```cmd 
1 and 2 squared is 1.000000 and 4.000000 
``` 
* functions can also do named returns 
```go 
package main 
import ( 
	"fmt" 
	"math" 
) 
func main() { 
	x, y := twoSqNos(1, 2) 
	fmt.Printf("1 and 2 squared is %f and %f", x, y) 
}
func twoSqNos(x, y float64) (x1, y1 float64) { 
	x1, y1 = math.Pow(x, 2), math.Pow(y, 2) 
	return 
} 
``` 
```cmd 
1 and 2 squared is 1.000000 and 4.000000 
``` 
* variables can be reassigned in the same scope(look up redeclaration and reassignment for go) 
* We can use the var keyword to declare list of variables at package level. We mention the type after variable name. Implicit assignment is also possible if the type is not mentioned. 
```go 
package main 
var x int= 69 
var y= 96 
func main(){ 
	// do 
} 
``` 
* ":=" short assignment operator can be used to assign variables with implicit type. But this can only be used in function and not be used in package level. 
```go 
package main 
func main(){ 
	x:=69 
} 
``` 
* var declarations can also be factored into blocks like the imports 
```go 
import ( 
	"fmt" 
	"math" 
) 
var ( 
	x int =69 
	y int =96 
) 
``` 
* constants can also be declared like using the var keyword but cnnot be decalred using := 
* incrementing values can be decalred using iota 
```go 
package main 
import( "fmt" ) 
const( 
	x int = iota 
	y 
	z 
) 
func main(){ 
	fmt.Println(x,y,z) 
} 
``` 
```cmd 
0 1 2 
``` 
* iota can be used in conjunction with operations to generate a series of values 
```go 
package main
import( "fmt" ) 
const( 
	_ int = 1<<(10*iota) 
	kb 
	mb 
	gb 
) 
func main(){ 
	fmt.Println(kb,mb,gb) 
} 
``` 
```cmd 
1024 1048576 1073741824
``` 
* init struct and define methods like 
```go 
import( "fmt" ) 
type person struct{ 
	FirstName string 
} 
func (p person) sayHello(){ 
	fmt.Println("Hello, my name is ",p.FirstName) 
} 
``` 
* go has something called "comma okay idiom" 
```go 
import "fmt" 
func main(){ 
	if var z=69; z>50{ 
		fmt.Println("Okay") 
	} 
} 
``` 
```cmd 
Hello 
``` 
* if, else if, else example 
```go 
if x < 4 && y < 4 { 
	fmt.Println("both < 4") 
} else if x > 6 && y > 6 { 
	fmt.Println("both > 6") 
} else if x >= 4 && x <= 6 { 
	fmt.Println("4<=x<=6") 
} else if y != 5 { 
	fmt.Println("Y Not 5") 
} else { 
	fmt.Println("None of the previous cases were met.") 
	} 
``` 
* switch case example
```go 
switch{ 
	case x < 4 && y < 4 : 
		fmt.Println("both < 4") 
	case x > 6 && y > 6 : 
		fmt.Println("both > 6") 
	case x >= 4 && x <= 6 : 
		fmt.Println("4<=x<=6") 
	case y != 5 : 
		fmt.Println("Y Not 5") 
	case default : 
		fmt.Println("None of the previous cases were met.") 
	} 
``` 
* "fallthrough" keyword is used inside a switch case to continue evaluating remaining conditions in the switch block. * A select statement is used to run code based on data from channels.(more on that later) 
* A channel is a way you can send and recieve values and doesnt require locks and concunrrency solutions. You can make chnnels like so: 

```go 
  c:=make(chan int) 
``` 
* init() function runs before the main function and is useful to make the necessary initialisations. 
```go 
import "fmt" 
func init(){ 
	fmt.Println("I run before the main function") 
} 
func main(){ 
	//do 
} 
``` 
```cmd 
I run before the main function 
``` 
* There are three common ways to write loops in go 
```go 
for init;condition;increment{ 
	//do 
} 

for condition{ 
	//do 
	increment 
} 

for{ 
	//do 
	conditon 
	increment 
} 
``` 
for loop example: 
```go 
package main 
import ( 
	"fmt" 
	"math/rand"
	) 
func main() { 
	for i := 0; i < 100; i++ { 
		fmt.Println(i) 
	} 
	for i := 0; i <= 100; i++ { 
		x, y := rand.Intn(10), rand.Intn(10) 
		fmt.Println(x, y) 
	} 
} 
``` 
* you can also use "continue" and "break" keywords in loops * You can also iterate through an array or map using range function 
```go
import "fmt" 
func main(){ 
	x:=[]int {1,2,3} 
	for i,v:= range x{ 
		fmt.Println(i, v) 
	} 
} 
``` 
```cmd 
0 1 1 2 2 3 
``` 
```go 
import "fmt" 
func main(){ 
	x:=map[string]int 
		{"Name": 0, 
		"Age": 0} 
	for k,v:= range x{ 
		fmt.Println(i, v) 
	} 
} 
``` 
```cmd 
Name 0 Age 0 
``` 
* small statement;statement idion example 
```go 
func main(){ 
	xx := map[string]int{ 
		"Name": 0, 
		"Age": 0} 
	for k, v := range xx { 
		fmt.Println(k, v) 
	} 
	if xxx,ok := xx["Name"]; ok {
		fmt.Println(xxx, "Condition satisfied") 
	} 
	if xxx, ok := xx["James"]; ok {
		fmt.Println(xxx) 
	} 
} 
``` 
```cmd 
0 Conditon satisfied 
//No output 
``` 
* different types of grouping :
Array, slices, map, struct

* arrays can be defined as so

```go
a:= [2]string{"Hey","Hello"}
b:= [...]string{"Hello","How are you"}
```

* arrays cant reassigned to each other unless they have same type and length
* len(array) gives the name of the array
* we can define slices just like arrays but without defines the size
* slices are arrays without their length defined

```go
x:=[]int{2,3,4}
```
* for range is most commonly used to access values from arrays and slices
```go
import "fmt"
func main(){
	x:=[]int{2,3,4}
	for _,v:= range x{
		fmt.Println(v)
	}
}
```
```cmd
2,3,4
```

* items can be accessed from arrays and slices by indexing similar to java and python

```go
x:=[]int{2,3,4}
fmt.Println(x[0])
```
```cmd
2
```
* Things can be appended to slices using the append function that takes a slice and all the elements to be appened. It returns another slice with all the elements appended.

```go
x:=[]int{2,3,4}
x= append(x,5)
fmt.Printf("#v",x)
```

```cmd
[]int{2, 3, 4, 5}
```
* Slicing the slice is similar to slicing in python
```go
x:=[]int{2,3,4}
fmt.Printf("%#v",x[:1])
fmt.Printf("%#v",x[1:])
```
```cmd
[]int{2}
[]int{3,4}
```

* 

</div>