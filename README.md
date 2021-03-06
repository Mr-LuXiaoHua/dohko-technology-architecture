dohko-technology-architecture
---
针对中小公司后端服务开发，探讨一下通用的技术架构方案

> 方案 

![方案](https://github.com/Mr-LuXiaoHua/dohko-technology-architecture/blob/master/technology-architecture.png)

---


  
关键部分说明：
#### CDN
用于图片、文件、js、css等静态资源存放

#### SLB
用于外部接入,统一入口。  

#### 聚合服务
负责业务服务的数据聚合，组装后返回给调用方  

##### 分布式锁服务
独立的分布式锁服务，提供获取锁、释放锁接口给业务服务调用

#### 缓存服务
独立的分布式缓存服务，提供缓存的增删改查操作接口给业务服务调用

#### MQ服务
独立的MQ服务，提供消费发布接口给业务服务调用

#### 搜索服务
独立的搜索服务，提供搜索、索引更新等接口给业务服务调用

#### 分布式调度服务
定时任务处理

#### 业务服务
如：商品服务、订单服务等，有自己独立的数据库，专注于自己的业务逻辑。
业务服务不直连Redis、MQ、ES等，需通过对应用的服务接口操作

#### 业务服务消费者
如：商品服务消费者、订单服务消费者，负责MQ消息消费，调用接口更新索引、缓存等。

#### ELFK 日志组合
Elasticsearch + Logstash + Filebeat + Kibana

   