#ribbon负载均衡
1.ribon 客户端实现负载均衡效果
2.IRule中的七种默认访问策略
    RoundRobinRule:轮询获取服务(轮询,默认)
    RandomRule：随机选择一个UP的服务（随机）。
    AvailabilityFilteringRule：会先过滤掉由于多次访问故障而处于断路由跳闸状态的服务，还有并发的连接数量超过阈值的服务，然后对剩余的服务列表按照轮询策略进行访问
    WeightedResponseTimeRule：。权重的方式挑选服务服务实例响应时间越小的服务，则更容易被选中如果服务实例响应的时间相差不大的，排在前面的服务实例更容易被选中（加权）
    RetryRule：先按照RoundRobinRule的策略获取服务，如果获取服务失败，则再指定时间内会进行重试，获取可用的服务，不可用的服务就不再轮询范文内，既活着的服务安装轮询，有问题的服务会跳过
    BestAvailableRule：。跳过熔断的服务，获取请求数最少的服务通常与ServerListSubsetFilter一起使用（选择并发亮最少）
    ZoneAvoidanceRule：使用ZoneAvoidancePredicate和AvailabilityPredicate来判断是否选择某个服务器，前一个判断判定一个区的运行性能是否可用，剔除不可用的区域（的所有服务器），AvailabilityPredicate用于过滤掉连接数过多的服务器。
3.自定义IRule


配置：
	windows中配置host文件中的域名解析，在C:\Windows\System32\drivers\etc\HOSTS中添加如下配置
	127.0.0.1 eureka7001.com
	127.0.0.1 eureka7002.com
	127.0.0.1 eureka7003.com
	
启动顺序：
	1.首先启动eureka集群：microservicecloud-eureka-7001、microservicecloud-eureka-7002、microservicecloud-eureka-7003
	2.然后启动服务提供者提供的微服务，这里是一个微服务的三个集群：microservicecloud-provider-dept-8001、microservicecloud-provider-dept-8002、microservicecloud-provider-dept-8003
	3.最后启动服务消费者：microservicecloud-consumer-dept-80
	其中microservicecloud为所有服模块的父工程，microservicecloud-api是公共模块
	
	
结果呈现：访问http://localhost/comsumer/dept/list
eureka服务注册中心：http://eureka7001.com:7001、http://eureka7002.com:7002、http://eureka7003.com:7003
