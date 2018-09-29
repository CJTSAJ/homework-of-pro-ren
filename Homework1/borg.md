# borg
## 简介
Borg是一个比较顶层的集成管理系统。在这上面运行着大量的job，这些job来自许多不同的应用，比如Gmail、Google Docs、Web Search等等，并且跨越多个集群，每个集群由大量机器组成。borg通过准入控制、高效的任务打包，超额的资源分配和进程隔离的机器共享，来__提高资源利用率__。几乎所有的google应用程序都要通过borg来管理底层的物理机。
![](http://dockone.io/uploads/article/20151031/bdafee63be9f2e11be87aae3ffe2972c.png)

## 特性

#### ● 集群和cell
一个cell中的机器通常属于单个集群，并且由数据中心规模的高性能网络结构连接起来。一个集群通常存在于单个数据中心里，而多个数据中心的集合构成了一个site。一个集群通常包含一个大的cell，也许其中还有一些小规模用于测试或者其他特殊目的的cell。
集群Cluster包含若干个单元Cell，单元Cell又包含大量的机器Machine。三者关系示意图如下图所示。
![](http://s3.51cto.com/wyfs02/M00/74/B2/wKiom1Ym7N3DkPdpAAGhC9Q7NIA298.jpg)

#### ● borg架构
在cell运行着一个逻辑的中央控制器叫做Borgmaster，cell中的每台机器上则运行着一个代理进程Borglet。
![](http://s1.51cto.com/wyfs02/M01/74/65/wKioL1YcdfCBfJxVAAKGlr_rfgk174.jpg-wh_651x-s_898612228.jpg)

#### ● job和task
一个Borg作业Job具有属性，包括name、owner、task数量等。Job具有约束来强制其任务运行在具有特定属性的机器上，例如处理器架构、OS版本、IP地址等。约束可以分为硬约束和软约束，前者是需求，必须满足；后者是偏好，尽量满足。
下图展示了job和task运行走完它们整个生命周期的过程。
![](http://img.blog.csdn.net/20170219200042842?)
上图描述的是具体每一个task的生命周期。用户主要可以做的事情是
1.递交一个工作（submit）
2.销毁一个工作（kill）
3.更新一个工作（update）


#### ● allocs
一个Borg alloc是一台machine上预留资源的集合，可以用于一个或多个任务运行。每个工作可以告知系统需要给我预留多少资源，这样系统可以确保不会太过激进的去叠加

#### ● 优先级和配额
当超出了处理能力的负载时，会根据优先级、配额、准入控制等来进行资源的分配调度。
每个作业都有一个优先级。Borg不允许一个生产型作业区抢占另一个，只允许生产型作业抢占非生产型作业。
资源配额Quota是一组资源量化表达式（CPU、RAM、Disk等），它与一个优先级和一个时间段对应。如果Quota不足，作业提交会被拒绝。

#### ● 调度
调度算法主要有两个部分：可行性检查（feasibility checking）跟打分选机器（scoring）
下图为调度算法过程
![](https://pic2.zhimg.com/v2-a7ee0cab772f04bcc4cb3ba5226cd3bd_b.jpg)

#### ● 监控
每个task都有一个内置的HTTP server用于发布task的健康状况以及其他性能指标。Borg会记录所有的job提交情况，task事件，以及Infrastore中详细的task执行前的资源使用情况。
## 优点
* 隐藏了资源管理和错误处理，因此程序员能专注于开发应用；

* 失败在大规模系统中非常常见，而borg具有很高的可靠性和可用性，能够支持高可靠性的应用；

* 能让我们跨越大量不同配置的机器有效地处理任务。

## 不足
* job是borg最基础的单位，没有办法在job下面做更复杂的分配。

* Borg为了大用户做了很多优化，所有API非常复杂，很多api根本用不到。

* 机器上的所有任务都使用其主机的单个IP地址，这样导致Borg会把port当成一个资源来分配。

## 评价
borg在谷歌已经应用十多年了，而且规模非常巨大，其一个集群就拥有数万台机器，borg用C++编写，并且在集群调度方面做了很多优化，非常专业和高大上。可能borg并不适合一般的中小型公司，中小型公司更适合用简化但又设计优良的Kubernetes，但对于google这样的大公司，borg能非常好的利用资源，节省资金。

## 参考资料
[Borg和Kubernetes有什么不同以及未来的云需要什么？](http://dockone.io/article/784)

[深度译文｜Google的大规模集群管理系统Borg](https://blog.csdn.net/karamos/article/details/80128781)

[Google大规模集群管理系统Borg的解读](http://blog.51cto.com/speakingbaicai/1704735)
