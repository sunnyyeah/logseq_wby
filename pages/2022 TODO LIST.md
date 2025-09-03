- ## M7 & M8 {{renderer :todomaster}}
	- 工作区开箱即用能力持续提升
		- DONE 【p0】支持 dashboard 场景的单点预创建能力
		- TODO 【p0】Android 全局索引接入索引服务，流程自动化
		- TODO 【p1】支持 bitsmr 场景更细粒度的预创建能力
	- 工作区管控策略优化
		- TODO 【p0】物料预热支持 AKE 架构的细分 vm flavor，降低资源浪费
		- TODO 【p0】支持预创建工作区数量根据 tcc 配置动态缩容
	- 前端
		- DONE 【p0】完成工作区修改名等业务迭代
	- 上线内容
		- 秒开
		- fix：v2 工作区的 theia 允许升级
		- fix：管理端工作区状态
-
-
- ##  M5 & M6 {{renderer :todomaster}}
	- 前端
		- TODO 接入线上日志监控
		  :LOGBOOK:
		  CLOCK: [2022-05-09 Mon 11:38:18]--[2022-05-09 Mon 11:38:19] =>  00:00:01
		  CLOCK: [2022-05-09 Mon 11:38:19]--[2022-05-09 Mon 11:38:19] =>  00:00:00
		  CLOCK: [2022-05-09 Mon 11:38:40]--[2022-05-09 Mon 11:38:41] =>  00:00:01
		  CLOCK: [2022-05-09 Mon 11:38:41]--[2022-05-09 Mon 11:38:43] =>  00:00:02
		  CLOCK: [2022-05-09 Mon 11:38:45]
		  :END:
		- DONE sleeping 玻璃拟态效果
		- TODO 支持用户修改工作区名称 & 支持可描述信息
		- DONE 前端状态页信息优化
		- TODO 前端支持统一创建入口
		- 批量删除 ide
			- DONE 批量删除卡片
			- DONE 批量删除过量的 ide
		- 管理端重构
	- 后端
		- 完成Aircode服务清理收尾工作，降低开发运维成本 {{renderer :todomaster-MjAyMiBUT0RPIExJU1Q=}}
			- TODO 完成gitserver服务与aircode_workspace服务合并
			- TODO 废弃wsmgr服务，与backend彻底解耦
		- 完成动态休眠 & 预热 & 预创建 逻辑优化，提升用户体验  {{renderer :todomaster-MjAyMiBUT0RPIExJU1Q=}}
			- DONE 支持 256G磁盘支持
			- TODO 支持根据集群资源实时情况 动态调整休眠间隔
			- DONE 支持用户theia settings配置持久化存储
			- TODO 预热支持AKE架构的细分vm flavor，降低资源浪费
			- DONE 预热 & 预创建 工作区支持动态升级theia & workspace服务
			- TODO 支持预创建工作区数量根据tcc配置动态缩容
			- TODO 支持根据集群资源实时情况 动态调整预创建工作区数量
			- DONE 单个工作区 theia 升级
			  :LOGBOOK:
			  CLOCK: [2022-05-27 Fri 10:44:09]--[2022-05-27 Fri 10:44:09] =>  00:00:00
			  CLOCK: [2022-05-27 Fri 10:44:10]--[2022-05-27 Fri 10:44:10] =>  00:00:00
			  CLOCK: [2022-05-27 Fri 10:44:12]--[2022-05-27 Fri 10:44:13] =>  00:00:01
			  CLOCK: [2022-05-27 Fri 10:44:13]--[2022-05-27 Fri 10:44:13] =>  00:00:00
			  CLOCK: [2022-05-27 Fri 10:44:14]
			  :END:
			-
			-
	-
	-
-
-
- 4.8 周会 todo
	- DONE 讨论一下 tag / commitID 创建工作区的时候，是否需要自动帮用户拉一个分支？
		- 暂时不支持
-
- ## 目前存在的问题
	- 登陆是自动的，如果没有成功就一直登录，这里需要调整为让用户手动输入
		- 这个需要平衡一下，如果是设置为让用户自己登录，那么可能存在用户在某次使用的时候 token 失效了，那么用户需要自行登录
			- 如果轮询的话，出现问题就会不停的尝试登录，就会产生页面抽搐的效果
		- TODO 不要自动登录了
	- 疑惑：
		- 我们在重试的时候应该从 launch 开始，还是直接从 get status 开始？
	- **sso 授权不稳定**
	- 管理端升级 theia 镜像鉴权改一下
-
- ## study {{renderer :todomaster}}
  collapsed:: true
	- backend
		- LATER go
		  :LOGBOOK:
		  CLOCK: [2022-04-01 Fri 12:11:43]--[2022-05-05 Thu 10:05:18] =>  813:53:35
		  :END:
		- DOING backend code
		  :LOGBOOK:
		  CLOCK: [2022-04-01 Fri 12:11:45]
		  :END:
		- TODO Kubernetes
		- TODO API
	- frontend
		- TODO CSS - flex
		- TODO .d.ts
		- TODO webpack
	- network
		- TODO CORS
		- TODO rpc
		-
-
-
- ## M3&M4 {{renderer :todomaster}}
	- 一阶段（待上线） {{renderer :todomaster}}
		- DONE debug 信息同步
		- DONE 数据指标设计
		- DONE 删除 theia 中的 header
		- DONE loading 页面超时统计
	- 二阶段（测试分支 feature/V2-2） {{renderer :todomaster}}
		- TODO 第三方详细信息 @飞跃
		- TODO 细化 loading status @润豪
		- DONE 创建 ide 错误优化
		- DONE 前端启动优化 （目前已开发完成，待提 MR）
			- 待确认：request-access 是否需要在工作区 ready 的情况下才能并行发送
		- 错误信息指引
			- DONE 服务端错误页面重定向（在一阶段中做完了，待上线）
			  :LOGBOOK:
			  CLOCK: [2022-04-01 Fri 11:48:26]--[2022-04-01 Fri 11:48:27] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 11:48:28]--[2022-04-01 Fri 11:48:29] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 11:48:29]--[2022-04-01 Fri 11:48:30] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 11:48:35]--[2022-04-01 Fri 11:48:36] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 11:48:44]--[2022-04-01 Fri 11:48:44] =>  00:00:00
			  :END:
			- DONE unknown 错误处理（重试，跟一阶段一块上线）
			- DONE failed 状态重试（后端 reset 数据库）
			  :LOGBOOK:
			  CLOCK: [2022-04-01 Fri 16:46:41]--[2022-04-01 Fri 16:46:42] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 16:46:43]--[2022-04-01 Fri 16:46:44] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 16:46:52]--[2022-04-01 Fri 16:46:54] =>  00:00:02
			  CLOCK: [2022-04-01 Fri 16:46:57]--[2022-04-01 Fri 16:46:58] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 16:46:58]--[2022-04-01 Fri 16:46:59] =>  00:00:01
			  CLOCK: [2022-04-01 Fri 16:47:00]
			  :END:
		- DONE 创建支持 tag 搜索、commitID 创建工作区
			- DONE 前端：设置可选搜索方式
			- 后端：
				- DONE 添加 tags 搜索接口
				- DONE 修改 check-repo 接口
				- DONE create 接口检查 commit_id
		- DONE 更新工作区（clone 失败时）
		- TODO sleeping / sleeped 状态 UI 调整
	- 三阶段 {{renderer :todomaster}}
		- TODO 管理端 UI
		- TODO 管理端 前端
		- TODO 管理端 后端
			- 整理当前后端所有的服务
			- 问卷：收集管理端所需要的内容
	-
-
	- #+BEGIN_TIP
	  待明确：
	  1. request-access 在工作区还没有 ready 的状态下是否有用？ **没有硬性规定**
	  2. 这个需要在大家不用 boe 的时候测试一下，如果没用的话需要调整一下 success page 的逻辑
	  #+END_TIP
-
-
- **3.28 - 4.2** {{renderer :todomaster}}
	- DONE 创建 ide 失败优化
	- DONE 创建 ide 超时优化
	- DONE 修复用户体验问题 1 个
	- DONE ide 启动优化（待提MR）
	  SCHEDULED: <2022-04-07 Thu>
	  :LOGBOOK:
	  CLOCK: [2022-04-01 Fri 11:44:50]--[2022-04-01 Fri 11:45:26] =>  00:00:36
	  CLOCK: [2022-04-01 Fri 11:45:32]--[2022-04-07 Thu 14:54:45] =>  147:09:13
	  :END:
-
-
- 绩效考核要准备的内容
	- 21年度绩效周期做的好的与不足
		- 做的好的：
			- 在维护图片库期间，能够快速响应业务和产品需求，并且针对问题做了文档总结，提供给技术支持的同学有效开展 oncall 工作，提升 oncall 效率。同时输出了较为详尽的快速上手图片库的文档，让新接手的同学能够快速对接
			- 在 tob 工作中，输出了竞品比较文档，凸显我们的优势，让我们在对外推广的时候更有竞争力
			- 在 Aircode 前端开发中，较快上手新的业务，
		- 做的不好的：
			- 没有形成闭环，很多事情做了并没有关注后续结果
			- 在做事之前没有很好的明确需求，存在模糊点就开始开发，所以存在遗漏
	- 下一步发展计划
		- 暂时想将重点放在前端上面，然后学习一点后端的知识，再做定夺
		- 能自己主导前端工作
	- 部门改进
		- 人手不够