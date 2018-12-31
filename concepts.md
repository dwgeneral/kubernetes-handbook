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

## Volume

- 与Docker不同的是，K8S的存储卷的生命周期和作用范围是一个Pod,每个Pod中声明的存储卷由Pod中的所有容器共享

## Persistent Volume(PV) 和 Persistent Volume Claim(PVC)

- PV 资源的提供者（类似Node）
- PVC 资源的使用者（类似Pod）

## UserAccount 和 ServiceAccount

- 用户账户为人提供账户标识，与服务的namespace无关, 是跨namespace的
- 服务账户为计算机进程和K8s集群中运行的Pod提供账户标识, 与特定的namespace是相关的

## (Role-based Access Control)RBAC访问授权

- RBAC主要引入了角色（Role）和角色绑定（RoleBinding）的抽象概念
- 在RBAC中，访问策略可以跟某个角色有关，用户再跟一个或多个角色关联

## Ingress

- Service 的 Service 对象
- K8S 对反向代理的一种抽象
