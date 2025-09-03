- https://sanyuesha.com/2018/05/07/go-json/
- 将 json 转为 go 的结构体的 [工具](https://oktools.net/json2go)
-
- JSON 是 js 的严格子集，利用 JS 中的几种模式来表示结构化数据。JSON 被作为替代 XML 的一个方案提出，因为 JSON 可以直接传给 eval() 而不需要创建 DOM
- 【注】理解 JSON 最关键的一点是要把它当成一种**数据格式**，而不是编程语言
-
- 语法：
	- JSON 支持 3 种类型的值
		- 简单值：字符串、数值、布尔值和 null（注意，特殊值 undefined 是不可以出现在 JSON 中的）
		- 对象：有序键值对
		- 数组
	- JSON 字符串必须使用双引号
-
- JS 中的 JSON 的方法
	- stringfy()：将 js 序列化为 JSON 字符串
		- stringfy 还可以接受两个参数：1. 过滤器，可以是数组或函数；2. 用于缩进结果 JSON 字符串的选项
		- 例子
		  collapsed:: true
			- ```
			  const book = {
			  	title: "hello world",
			  	authors: [
			  		"Tom",
			  		"Jerry"
			  	],
			  	edition: 4,
			  	year: 2017
			  };
			  
			  const jsonText1 = JSON.stringify(book)
			  console.log("无任何处理：",jsonText1)
			  
			  const jsonText2 = JSON.stringify(book, null, 4);
			  console.log("缩进为4:",jsonText2)
			  
			  const jsonText3 = JSON.stringify(book, ["title", "edition"]);
			  console.log("过滤title和edition:",jsonText3);
			  
			  const jsonText4 = JSON.stringify(book, (key, value) => {
			  	switch(key) {
			  		case "authors":
			  			return value.join(",")	// 将value转为字符串
			  		case "year":
			  			return 4000;
			  		case "edition":
			  			return undefined;		// 忽略 edition
			  		default:
			  			return value;
			  	}
			  })
			  console.log("使用函数过滤:",jsonText4);
			  ```
		- toJSON()：该方法可以在要序列化的对象中添加 toJSON() 方法，序列化时会基于这个方法返回适当的 JSON 表示
		- toJSON() 可以和过滤函数一起使用，因此理解不同序列化流程的顺序非常重要。在把对象传给 JSON.stringify() 时会执行如下步骤：
			- 1. 如果可以获取实际的值，则调用toJSON() 方法获取实际的值，否则使用默认的序列化
			  2. 如果提供了第二个参数，则应用过滤。传入过滤函数的值就是第 1 步返回的值
			  3. 第 2 步返回的每个值都会相应第进行序列化
			  4. 如果提供了第三个参数，则相应地进行缩进
	- parse()：将 jSON 字符串解析为 js
		- 该方法也可以接收一个额外的参数，这个函数会针对每个键值对都调用一次。为区别于传给 JSON.stringify()  的起过滤作用的替代函数，这个函数被称为**还原函数**
		-