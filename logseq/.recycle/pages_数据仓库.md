- > **tags:**  #数仓 #数据库
-
- ## 数仓是什么？
- **定义：**Data Warehouse，也成为企业数据仓库。数据仓库是一个大型的数据存储系统，主要用于储存、查询和分析企业的历史数据。数据仓库是商业智能应用的重要组成部分，它可以帮助公司了解业务过去的行为，并促进更好的决策。
-
-
- ## 数仓和数据库的区别是什么？
-
-
- ## 数仓分类
- ### 按建模类型划分
- ### 按数据量划分
-
-
-
- 确认关注点：
  background-color:: green
	- background-color:: gray
	  > 对于 query 分析而言，主要需要关心数据的哪些属性，通过分析当前业界与公司的相关数仓，匹配我们所需满足的条件，找出最适合的数仓进行数据存储和分析
	- 是否需要可视化
	  logseq.order-list-type:: number
	- 数据量
	  logseq.order-list-type:: number
	- 并发：目前线上并发低于 1 QPS。中期来看，目标是支持 100 QPS 的并发度。
	  logseq.order-list-type:: number
	- 事务：数据来自业务系统（可能会经过一层处理转换），Nice to have
	  logseq.order-list-type:: number
	- 响应时间：秒级、毫秒级
	  logseq.order-list-type:: number
	- 数据模型：维度不固定；条件复杂（Join、层级递归查询）
	  logseq.order-list-type:: number
-
- 调研方向：
  background-color:: green
	- 数仓的类型
	  logseq.order-list-type:: number
	- 各个类型的数仓有哪些（归纳总结）
	  logseq.order-list-type:: number
	- 各个数仓的优缺点
	  logseq.order-list-type:: number
	- 数仓的接入方式
	  logseq.order-list-type:: number
	- 适用场景和非适用场景
	  logseq.order-list-type:: number
-
- 可参考文档：
	- [数仓选型](https://bytedance.larkoffice.com/wiki/wikcn6muD4n0s8S7fH3xfpyyjpb)
-
- ## 名词解释
	- |术语|解释|
	  |--|--|
	  |TP（Transaction Processing，事务处理）|TP 系统用来处理、管理和监控执行日常业务操作的事务。它们强调快速、可靠地处理类似创建、读取、更新、删除的操作。其中 OLTP（OnLine Transaction Processing，联机事务处理）是最常见类型，能高效处理大量短期在线事务。|
	  |AP（Analytical Processing，分析处理）|AP 系统用来分析和支持决策过程。它们通常用于多维分析查询，如趋势分析、聚合、分组等复杂查询。其中 OLAP（OnLine Analytical Processing，联机分析处理）是 AP 的一种类型，强调在大规模、复杂数据上支持复杂分析查询。|
	  |HTAP（Hybrid Transactional/Analytical Processing，混合事务/分析处理）|HTAP 系统和解决方案旨在同时处理 TP 和 AP 工作负载，结合了事务处理的操作和分析查询的处理。HTAP 核心价值在于减少数据复制和移动，处理实时或近实时的业务情况，并且能够在同一系统中支持 OLTP 和 OLAP。|