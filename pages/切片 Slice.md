- 切片是对数组的抽象。
-
- 定义切片
	- 声明一个未指定大小的数组来定义切片：
		- ```
		  var identifier []type
		  // 注意，切片是不需要设置长度的
		  ```
	- 或者使用 make() 来创建一个切片
		- make()
			- ```
			  make([]T, length, [capacity]) 
			  // length 即表示数组长度又表示切片初始长度
			  // capacity 表示容量，可选
			  ```
		- ```
		  var slice1 []type = make([]type, len)
		  // OR
		  slice1 := make([]type, len)
		  ```
	-
	- 与 array 定义的区别
		- ```
		  // 定义 array
		  var a [length]int
		  ```
-
- 切片初始化
  collapsed:: true
	- ```
	  s := [] int{1, 2, 3}
	  // 直接初始化切片，[] 表示是切片类型，{1,2,3} 初始化值依次是 1,2,3，其 cap=len=3。
	  
	  s := arr[:]
	  // 初始化切片 s，是数组 arr 的引用。
	  
	  s := arr[startIndex:endIndex] 
	  // 将 arr 中从下标 startIndex 到 endIndex-1 下的元素创建为一个新的切片。
	  
	  s := arr[startIndex:] 
	  // 默认 endIndex 时将表示一直到arr的最后一个元素。
	  
	  s1 := s[startIndex:endIndex] 
	  // 通过切片 s 初始化切片 s1。
	  
	  s :=make([]int,len,cap) 
	  // 通过内置函数 make() 初始化切片s，[]int 标识为其元素类型为 int 的切片。
	  ```
-
- len() & cap()
	- len()：计算切片的长度
	- cap()：计算切片的容量
- append() & copy()
	- 如果想增加切片的容量，我们必须创建一个新的更大的切片并把原分片的内容都拷贝过来。
		- 下面的实例中好像直接 append 也能够自动增加 capacity？ #problem
	- append(s, param1, param2, ....)：向切片中添加新的元素
	- copy(s2, s1)：将 s1 的内容拷贝到 s2 中
	- 实例
	  collapsed:: true
		- ```
		  package main
		  
		  import "fmt"
		  
		  func main() {
		     var numbers []int
		     printSlice(numbers)
		  
		     /* 允许追加空切片 */
		     numbers = append(numbers, 0)
		     printSlice(numbers)
		  
		     /* 向切片添加一个元素 */
		     numbers = append(numbers, 1)
		     printSlice(numbers)
		  
		     /* 同时添加多个元素 */
		     numbers = append(numbers, 2,3,4)
		     printSlice(numbers)
		  
		     /* 创建切片 numbers1 是之前切片的两倍容量*/
		     numbers1 := make([]int, len(numbers), (cap(numbers))*2)
		  
		     /* 拷贝 numbers 的内容到 numbers1 */
		     copy(numbers1,numbers)
		     printSlice(numbers1)  
		  }
		  
		  func printSlice(x []int){
		     fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
		  }
		  
		  // output:
		  // len=0 cap=0 slice=[]
		  // len=1 cap=1 slice=[0]
		  // len=2 cap=2 slice=[0 1]
		  // len=5 cap=6 slice=[0 1 2 3 4]
		  // len=5 cap=12 slice=[0 1 2 3 4]
		  ```
-
-
- 空切片（nil）：初始化默认为 nil，长度为 0
- 切片截取：
	- ```
	  s1 := s[startIndex:endIndex] 
	  ```
-
-
- slice 容量变化
	- cap < 1024, cap = 2 * cap
	- cap >= 1024, cap = 1.25 * cap
- 预先分配内存可提升性能
- 直接使用 index 赋值，而非 append 可以提升性能
-
- slice 作为函数传递传递
	- 【注意】go 中的函数参数传递是值传递
		- 但是我们可能会发现，当我传递一个数组/slice 的时候，我直接修改某个值，发现原函数中的值也发生了对应的变化，这是因为我们传递的是一个指针，当我们修改里面的值时时会发生变化的。而如果我们将被调函数中的参数的 len 或者 cap 改变了，那么此时原函数中的 len 和 cap 是不会被改变的。因为他俩的数据结构就不同了。
	- 如果在函数中没有对 slice 进行扩容，那么修改在原来的函数中
	- 如果在函数中对 slice 进行了扩容，那么修改在新的函数中
	- 例子
		- ```
		  func main (){
		  	var s []int
		      for i := 0; i < 3; i++ {
		      	s = append(s, i)
		      }
		      modifySlice(s)
		      fmt.Println(s)
		  }
		  
		  func modifySlice(s []int) {
		  	s = append(s, 2048)
		      s = append(s, 4096)
		      s[0] = 1024
		  }
		  
		  // output [0,1,2]
		  ```