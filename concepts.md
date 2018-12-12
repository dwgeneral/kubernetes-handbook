## Service

- Service 是应用服务的抽象，通过labels为饮用提供负载均衡和服务发现。
- 匹配labels的Pod IP和Port 列表组成 endpoints，由kube-proxy负责将服务IP负载均衡到这些 endpoints上

- 每个Service都会自动分配一个cluster IP（仅在集群内部可访问的虚拟地址）和DNS名
- 其他容器可以通过该地址或DNS来访问服务,而不需要了解后端容器的运行

## Label

- 用来识别对象的标签
- Label Selector支持以下方式
  - 等式, (app=nginx), (env!=production)
  - 集合, env in (production, qa)
  - 与关系，(app=nginx,env=test)
