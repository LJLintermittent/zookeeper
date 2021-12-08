## Zookeeper工作机制

zookeeper从设计模式角度来理解：是一个基于观察者模式设计的分布式服务管理框架，它负责存储和管理大家都关心的数据，然后接收观察者的注册，一旦这些数据的状态发生变化，zookeeper就将负责通知在zookeeper上注册的那些观察者做出相应的回应。

### zookeeper的特点

1.一个领导者（leader），多个随从（follower）组成的集群

2.集群中只要有半数以上的节点存活，zookeeper集群就能正常服务，所以zookeeper适合安装奇数台服务器

3.全局数据一致性：每个server保存一份相同的数据副本，client无论连接到哪一台server，数据都是一致的

4.更新请求顺序执行，来自同一个client的更新请求将按照其发送的顺序依次执行

5.数据更新原子性，一次数据更新要么成功，要么失败

6.实时性，在一定时间范围内，client都能读取到最新的数据

### 数据结构

zookeeper的数据结构与linux文件系统类似，整体上可以看做是一棵树，每个节点称作一个znode，每一个znode默认能够存储1MB的数据，每个znode都可以通过其路径唯一标识

### zookeeper的应用场景

统一命名服务，统一配置管理，统一集群管理，服务器节点动态上下线，软负载均衡

### zookeeper配置参数（zoo.cfg）

1.tickTime = 2000：通信心跳时间，zookeeper服务器与客户端心跳时间，单位毫秒

2.initTime = 10：LF初始通信时限（leader-follower）

leader和follower初始连接时能容忍的最多心跳数（tickTime的数量）

3.syncLimit = 5，LF同步通信时限

leader和follower之间通信时间如果超过syncLimit * tickTime，leader认为Follower死亡

4.dataDir：保存zookeeper中的数据

默认是tmp目录，这个目录下存放的都是Linux中的临时文件，会定期删除，所以不能使用这个目录

5.clientPort = 2181：客户端连接端口



