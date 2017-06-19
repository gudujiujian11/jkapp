# jkapp
	第一天 国际物流 杰信商贸 + 搭建环境
1.	项目背景
杰信项目物流行业的项目，
信商贸是国际物流行业一家专门从事进出口玻璃器皿贸易的公司。公司总部位于十一个朝代的帝王之都西安，业务遍及欧美。随着公司不断发展壮大，旧的信息系统已无法满足公司的快速发展需求，妨碍公司成长，在此背景下，公司领导决定研发《杰信商贸综合管理平台》。
《杰信商贸综合管理平台》分三期完成。一期完成仓储管理（包括：采购单、仓库、货物、条形码、入库、出库、退货、盘点、库存、库存上限报警、统计查询）和展会管理（包括：展会管理、出单管理），形成货物统一数字化管理。二期完成货运全流程管理，包括购销合同、出货表统计、出口报运单、HOME装箱单、装箱单、委托书、发票、财务统计等。三期完成决策分析（包括：成本分析图、销售情况统计、重点客户、经营情况同期比对统计、工作绩效），为公司经营决策提供数据支持。

2.	【面试】拿到新框架，如何下手
当到一家新的软件公司，公司给你一个新框架，让你完成一个简单模块的CRUD操作，你怎样完成？
	步骤：
1）	大概浏览一下说明的文档，了解软件解决什么问题，解决用户的什么需求
2）	找jar，浏览它的核心框架，核心技术freemake（看到不了解的，百度，了解它的作用即可）
3）	画图，画系统架构的草图
4）	系统都是分层体系，都从后往前画。
a)	看数据库配置文件，了解系统所连接的数据库，账号，密码
b)	持久层
c)	Dao 数据库访问层
d)	Service 业务层
e)	Controller/action 控制层
f)	Jsp 视图层
找权限管理部门表，一般都是一个单表的CRUD操作。
找到模板，仿造模板，根据草图一步一步实现
遇到新的不了解的技术，应该怎么处理？百度，了解其作用即可。然后仿写。


了解业务，UML 用例图
业界画用例图 Rational rose UML 非常强大的工具（大公司）用例图、类图、序列图、状态图（复杂状态流转时才画）
用PowerDesigner 画数据库建模
PD,ROSE都可以生产伪代码，但在实际业务中无人问津。

 

3.	用例图
1）	角色：代表系统中的一类用户
2）	用例：代表业务功能
3）	连线关系：哪个角色操作哪些用例

画图的目的：为了开发人员了解整个系统的概貌，当画很多细节时，就会干扰我们对图的了解。


 

4.	系统功能结构图
1）	功能点（分层，主次）演化成主菜单，左侧菜单，功能点
2）	了解系统的所有功能
3）	按功能点分配工作
4）	用户报价的依据（按模块报价）
 

5.	系统的架构

 

6.	数据库
异构数据库技术：当前的系统直接支持主流的数据库，需要少量的编码
OracleXEUniv简版 （推荐）
11g正式版安装包，2个文件，3G

之前的10g的简版，不能创建一个本地服务，没有导入数据命令和导出数据的命令。
sqlPlus它可以直接用账号，可以远程访问。（权限大）
PL/SQL oracle客户端工具不能直接远程访问oracle。必须创建通道（本地服务）


 

一般安装完oracle数据库，默认服务都是自动启动；日常不用时，可以停掉服务，加速系统启动，不占内存。

安装ORACLE创建SID，创建数据库（账号），默认system/sys系统账号。一定要记住密码。

a)	创建一个账号
 
b)	授权

 

c)	使用自己创建的账号登陆
 
d)	选择MyObjects只看到自己的内容
 



7.	业务需求：
a)	《需求说明书》
1）	描述业务功能
生产厂家模块
功能：为在购销合同模块中的货物信息和附件信息它们都有所属的生产厂家。

b)	《概要设计》
1）	细化描述业务功能
2）	以表格形式数据库表（表+字段+描述）

c)	生产厂家信息维护基础表FACTORY_C
功能：为在购销合同模块中的货物信息和附件信息它们都有所属的生产厂家。
序号	中文名称	英文名称	类型（长度）	备注
1.		编号	FACTORY_ID	VARCHAR2(40)	UUID
2.		全称	FULL_NAME	VARCHAR2(200)	根据客户所说的最大长度，比较模糊的长度，在他的基础上，翻2到4倍
3.		简称	FACTORY_NAME	VARCHAR2(50)	
4.		联系人	CONTACTS	VARCHAR2(30)	20/30
5.		电话	PHONE	VARCHAR2(20)	
6.		手机	MOBILE	VARCHAR2(20)	
7.		传真	FAX	VARCHAR2(20)	
8.		备注	CNOTE	VARCHAR2(2000)	当感觉它可能和关键字相冲突时，就加一个C前缀
9.		验货员	INSPECTOR	VARCHAR2(30)	
10.		排序号	ORDER_NO	INT	
11.		创建人	CREATE_BY	VARCHAR2(40)	当前登录人的ID
12.		创建部门	CREATE_DEPT	VARCHAR2(40)	当前登录人所在部门
13.		创建时间	CREATE_TIME	TIMESTAMP	

d)	主键策略
1）	自增类型INT/LONG 速度快
2）	UUID字符串 速度慢 （推荐使用UUID）

8.	开发步骤
a)	PD数据库建模，执行建表SQL语句
 

 

b)	创建PO对象



创建MAVEN工程
Myeclipse10~10.7  
1）	测试类，无法运行测试类
2）	Maven构建环境仓库
Maven命令实际是通过jar中的类执行的
3）	maven不同的myeclipse插件有BUG
当本地利用现有MYECLIPSE创建不了maven工程
解决办法
1）	升级2013/2014
2）	使用web工程，拷贝libs放到web工程中

Maven工程如何增加依赖，依赖原则：
1）	主要核心框架springmvc、spring、mybatis
2）	数据库 c3p0、 oracle/mysql驱动
3）	第三方核心jar 
4）	日常其他jar log4j、junit、poi
5）	排除冲突的jar servlet.jar TOMCAT实现，

坐标怎么来？
1）	search.maven.org 搜索坐标
2）	myeclipse maven插件，增加依赖，必须构建索引

 
 


9.	PD基础配置
1）	改直角线为直线
 
再设置 ，保存修改的样式
2）	取消name和code的联动
 
3）	直接显示备注字段
 

