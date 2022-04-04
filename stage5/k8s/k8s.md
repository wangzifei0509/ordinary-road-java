[k8s从入门到精通](https://www.bilibili.com/video/BV1cK4y1L7Am)
# K8S入门
k8s使用go语言编写
### kubectl命令
`apply`命令包含create/patch两个命令，定义资源的最终态，如果没有就是创建，如果有就是更新。
`kubectl run nginx --images=`这个命令是创建了一个名为nginx的deployment
`kubectl explain deployment.status` 解释yml文件中每个字段的含义和可选值
`kubectl edit deployment my-deployment -n argo ` 编辑某个资源
### namespace
namespace是一个逻辑概念，为了实现资源隔离。
### 存储
pv是针对cluster的
pvc是属于某个namespace的


创建/更新资源 使用声明式对象配置 kubectl apply -f XXX.yaml

删除资源 使用命令式对象配置 kubectl delete -f XXX.yaml

查询资源 使用命令式对象管理 kubectl get(describe) 资源名称


查看k8s中资源的常用命令
```
kubectl get podName -o wide|yaml|json
kubectl describe podName -n argo 
kubectl get pod nginx-pod  -n dev --show-labels
```
pod的状态
- Pending 有资源条件不满足挂起
- Running  
- Succeeded
- Failed













