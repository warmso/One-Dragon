# 面试问题一条龙

[TOC]

## iOS相关
#### AFNetworking源码分析

#### 自定义控件

#### 常用的设计模式
##### MVC
##### MVVM
##### 单例
##### 工厂
##### 代理

#### property的关键字

#### BAD_ACCESS的出现场景

#### 圆角

#### crash
###### crash收集
###### crash救活

#### CALayer

#### runtime

#### runloop

#### 三种多线程
###### NSThread
###### GCD
###### NSOperation


#### 各种多线程锁的对比

#### 内存管理

#### KVC（Key-value coding）键值编码

#### KVO

#### block相关

#### 离屏渲染

#### json解析

#### CoreData

#### CocoaPods

#### UITableView优化

#### 响应者链（+）
##### Hit-Test 机制

当用户触摸(Touch)屏幕进行交互时，系统首先要找到响应者（Responder）。系统检测到手指触摸(Touch)操作时，将Touch行为 以UIEvent的方式加入UIApplication事件队列中。UIApplication从事件队列中取出最早的触摸事件进行分发传递到UIWindow进行处理。UIWindow 会通过hitTest:withEvent:方法寻找触碰点所在的视图，这个过程称之为hit-test view。

hitTest 的顺序如下
UIApplication -> UIWindow -> Root View -> ··· -> subview

在顶级视图（Root View）上调用pointInside:withEvent:方法判断触摸点是否在当前视图内；
如果返回NO，那么hitTest:withEvent:返回nil；
** 如果返回YES，那么它会向当前视图的所有子视图发送hitTest:withEvent:消息 **

所有子视图的遍历顺序是从最父层视图一直到到最子层视图，直到有子视图返回非空对象或者全部子视图遍历完毕。
如果有subview的hitTest:withEvent:返回非空对象则A返回此对象，处理结束

注意这个过程，子视图也是根据pointInside:withEvent:的返回值来确定是返回空还是当前子视图对象的。并且这个过程中如果子视图的hidden=YES、userInteractionEnabled=NO或者alpha小于0.1都会被忽略（alpha的子视图也会继承alpha）

如果所有subview遍历结束仍然没有返回对象，则 UIWindow 的hitTest:withEvent:返回self；

系统就是这样通过hit test找到触碰到的视图(Initial View)进行响应。
##### 响应者链 （Responder Chain）
系统通过hit test 机制找到了触碰到的Initial View，但是有时候Initial view并没有或者无法正常处理此次Touch。这个时候，系统便会通过响应者链寻找下一个响应者，以对此次Touch 进行响应。

响应者链顺序如下：

Initial View（首要视图，也就是上一步找到的那个view）-> View Controller（如果存在） -> superview -> ···  -> rootView -> UIWindow -> UIApplication

如果一直到Root View都没有处理这个事件，事件会传递到UIWindow（iOS中有一个单例Window），此时Window如果也没有处理事件，便进入UIApplication，UIApplication是一个响应者链的终点，它的下一个响应者指向nil，以结束整个响应者链。





## 数据结构
#### 链表
###### 判断是否有环
###### 判断环周长
###### 判断环交点
###### O（1）时间复杂度删除节点
###### 链表排序
###### 链表的倒数第K个数

#### 红黑树
#### 平衡二叉树
#### 堆
#### 图
###### 克鲁斯卡尔
###### 迪杰斯特拉
###### 广度优先/深度优先遍历
###### 拓扑排序



## 算法




## 操作系统
#### 进程死锁/如何检测
#### 进程与线程的区别
#### 进程的内存分布
#### 进程间通信
#### 堆内存和栈内存
#### 堆区分配的算法
#### 信号量
#### 原子操作
#### 看门狗





## 计算机网络
#### 一次网络请求的完整过程
#### http和https的区别
#### http1.0、1.1、2.0版本对比
#### http的状态码
#### TCP的三次握手
#### TCP的四次挥手
#### TCP的拥塞控制
#### TCP和UDP的比较
#### GET和POST请求的对比
#### 端口监听
#### 对称/非对称加密

## 数据库
#### 范式
#### 索引
###### 索引的分类
###### 索引的实现原理
#### 视图
#### 数据库的优化
#### SQLite的线程安全
#### 