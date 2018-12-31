# 在Kubernetes集群中体验下应用

## 先创建一个 Deployment 资源(replicas=1)，再由与 Deployment 关联的 ReplicaSet 来创建Pod，镜像使用Nginx
- $ kubectl create --image=nginx:alpine nginx-app --port=80

## 查看
- $ kubectl get pods
- $ kubectl exec nginx-app-4028413181-cnt1i ps aux
- $ kubectl describe pod nginx-app-4028413181-cnt1i
- $ kubectl logs nginx-app-4028413181-cnt1i

## 为nginx-app创建一个Service
- kubectl expose deployment nginx-app --port=80 --target-port=80 --type=NodePort
- kubectl describe service nginx-app
> 这样，在cluster内部就可以通过 http://IP 和 http://nodeIP:NodePort 来访问nginx-app,
> 而在cluster外部，只能通过 http://nodeIP:NodePort 访问

## 动态扩展应用
- kubectl scale --replicas=3 deployment/nginx-app
- kubectl get deploy

## 滚动升级
- kubectl rolling-update frontend-v1 frontend-v2 --image=image:v2

## 滚动回滚
- kubectl rolling-update frontend-v1 frontend-v2 --rollback

> 需要注意的是，kubectl rolling-update 只针对 ReplicationController。
> 对于更新策略是 RollingUpdate 的 Deployment（Deployment 可以在 spec 中设置更新策略为 RollingUpdate，默认就是 RollingUpdate），更新应用后会自动滚动升级
> 而更新应用的话，可以直接用 kubectl set 命令

- kubectl set image deployment/nginx-app nginx-app=nginx:1.9.1

## 查看滚动更新过程
- kubectl rollout status deployment/nginx-app

## 回滚Deployment
- kubectl rollout history deployment/nginx-app
- kubectl rollout undo deployment/nginx-app
