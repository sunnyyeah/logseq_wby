- defer 的思想类似于C++中的析构函数，不过Go语言中“析构”的不是对象，**而是函数**，defer就是**用来添加函数结束时执行的语句**。
- defer 代码块**会在函数调用链表中增加一个函数调用**。这个函数调用不是普通的函数调用，而是会在函数正常返回，也就是 **return 之后添加一个函数调用**。因此，defer通常用来释放函数内部变量。
- 如果有多个 defer 代码块，那么采用 **先定义后调用** 的原则
- 例子🌰
	- ```
	  package main
	  
	  import (
	      "fmt"
	  )
	  
	  func main() {
	      fmt.Println("Step 1")
	      fmt.Println("Step 2")
	      defer fmt.Println("Step Final")   // 添加 defer 代码块
	      fmt.Println("Step 3")
	      fmt.Println("Step 4")
	  }
	  
	  // output
	  // Step 1
	  // Step 2
	  // Step 3
	  // Step 4
	  // Step Final
	  ```
	- 无论上面的 defer 代码块在 main 中的哪个位置，输出的结果都是一样的。也就是手它只会在 return 的时候执行