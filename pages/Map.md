- Map 实际上的值是一个指针，传的参数也是一个指针
- Map 是一种无序的键值对的集合，通过 key 来快速检索数据，key 类似于索引，指向数据的值。
- 我们可以像迭代数组和切片那样迭代它。不过，Map 是无序的，我们无法决定它的返回顺序，这是因为 Map 是使用 hash 表来实现的。
-
- 定义
	- ```
	  /* 声明变量，默认 map 是 nil */
	  var map_variable map[key_data_type]value_data_type
	  
	  /* 使用 make 函数 */
	  map_variable := make(map[key_data_type]value_data_type)
	  ```
	- 【注】如果不初始化 map，那么就会创建一个 nil map。nil map 不能用来存放键值对
-
- delete(map, key)
  collapsed:: true
	- ```
	  package main
	  
	  import "fmt"
	  
	  func main() {
	          /* 创建map */
	          countryCapitalMap := map[string]string{"France": "Paris", "Italy": "Rome", "Japan": "Tokyo", "India": "New delhi"}
	  
	          fmt.Println("原始地图")
	  
	          /* 打印地图 */
	          for country := range countryCapitalMap {
	                  fmt.Println(country, "首都是", countryCapitalMap [ country ])
	          }
	  
	          /*删除元素*/ delete(countryCapitalMap, "France")
	          fmt.Println("法国条目被删除")
	  
	          fmt.Println("删除元素后地图")
	  
	          /*打印地图*/
	          for country := range countryCapitalMap {
	                  fmt.Println(country, "首都是", countryCapitalMap [ country ])
	          }
	  }
	  ```
	-
- map 删除key 不会自动缩容
-
- map 作为函数参数传递
	- map 作为参数传递给某给函数时，该函数接收这个引用的一份拷贝，被调用函数对 map 底层数据结构的任何修改，调用者函数都可以通过持有的 map 引用看到。如下面的例子，counts 是通过 make 创建的 map 的引用，将 counts 作为参数传入函数 countLines 时，countLines 和 main 指向同一个 map。（可以理解这里做的是浅拷贝操作）
	- 例子
	  collapsed:: true
		- ```
		  package main
		  
		  import (
		      "bufio"
		      "fmt"
		      "os"
		  )
		  
		  func main() {
		  	// map是一个由make函数创建的数据结构的引用
		      counts := make(map[string]int)
		      files := os.Args[1:]
		      if len(files) == 0 {
		          countLines(os.Stdin, counts)
		      } else {
		          for _, arg := range files {
		              f, err := os.Open(arg)
		              if err != nil {
		                  fmt.Fprintf(os.Stderr, "dup2: %v\n", err)
		                  continue
		              }
		              countLines(f, counts)
		              f.Close()
		          }
		      }
		      for line, n := range counts {
		          if n > 1 {
		              fmt.Printf("%d\t%s\n", n, line)
		          }
		      }
		  }
		  
		  func countLines(f *os.File, counts map[string]int) {
		      input := bufio.NewScanner(f)
		      for input.Scan() {
		          counts[input.Text()]++
		      }
		      // NOTE: ignoring potential errors from input.Err()
		  }
		  ```
-
-