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
