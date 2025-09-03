- 网络框架 —— Gin
	- Gin 是用 Go 编写的一个 Web 应用框架，对比其它主流的同类框架，他有更好的性能和更快的路由。由于其本身只是在官方 net/http 包的基础上做的完善，所以理解和上手很平滑。
	- 安装
		- ```
		  $ go get -u github.com/gin-gonic/gin
		  
		  // 但是使用上面的方法安装会有问题，报错找不到 import 文件，可以通过下面两个命令修复
		  $ go mod init gin
		  $ go mod edit -require github.com/gin-gonic/gin@latest
		  ```
	- 导入
		- ```
		  import "github.com/gin-gonic/gin"
		  ```
	- 使用实例
		- ```
		  package main
		  
		  import "github.com/gin-gonic/gin"
		  
		  func main() {
		  	r := gin.Default()
		      // 通常在使用过程中，我们会将 func 单独封装，然后所有的 GET/POST/DELETE 操作放一块
		  	r.GET("/ping", func(c *gin.Context) {
		  		c.JSON(200, gin.H{
		  			"code": 10000,
		  			"msg":  "success",
		  		})
		  	})
		  
		  	r.Run()
		  }
		  ```
-
- 常用方法说明
	- ```
	  router := gin.Default()	// 使用默认的中间件创建 gin router 
	  
	  router.GET("/someGet", getting)
	  router.POST("/somePost", posting)
	  router.PUT("/somePut", putting)
	  router.DELETE("/someDelete", deleting)
	  router.PATCH("/somePatch", patching)
	  router.HEAD("/someHead", head)
	  router.OPTIONS("/someOptions", options)
	  
	  ```
	- Grouping routes
		- ```
		  func main() {
		  	router := gin.Default()
		  
		  	// Simple group: v1
		  	v1 := router.Group("/v1")
		  	{
		  		v1.POST("/login", loginEndpoint)
		  		v1.POST("/submit", submitEndpoint)
		  		v1.POST("/read", readEndpoint)
		  	}
		  
		  	// Simple group: v2
		  	v2 := router.Group("/v2")
		  	{
		  		v2.POST("/login", loginEndpoint)
		  		v2.POST("/submit", submitEndpoint)
		  		v2.POST("/read", readEndpoint)
		  	}
		  
		  	router.Run(":8080")
		  }
		  ```
-
- 开发过程中使用的方式
	- api/backend/v2 目录下定义 response data 的类型
	- internal/handler 目录下写接口逻辑
		- ```
		  import (
		  	v2 "code.byted.org/tce/aircode_backend/api/backend/v2"
		      "code.byted.org/tce/aircode_backend/util/ginutil"
		  )
		  func (g *GitHandler) name(c *gin.Context) {
		  	// 写逻辑
		      // 返回数据
		      var res v2.xxx
		  	for _, branch := range branches {
		  		var b v2.yyy
		  		b.Name = branch.Name
		  		res.Branches = append(res.Branches, b)
		  	}
		  
		  	ginutil.JSON(c, res, nil)
		  }
		  
		  ```
	- 旧的要废弃的接口在后面加上 Deprecated