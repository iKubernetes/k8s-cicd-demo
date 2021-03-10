# k8s-cicd-demo
在Kubernetes上基于GitLab和Jenkins的CICD测试环境~

## 部署步骤
Jenkins和GitLab之间没有依赖关系，可分别按需部署。

### 部署GitLab
- redis、postgresql和gitlab都使用了hostPath类型的存储卷，该方式并不适用于生产环境，应用于生产环境之前，请按需要修改为可用的PVC资源后再进行部署；
- GitLab目录下的配置清单文件名被依次编制了序号，建议按序号依次进行部署，且应该在redis和postgresql服务均就绪后再部署GitLab；
- 它们默认均部署于gitlab名称空间下；
- GitLab Service默认通过NodePort向外暴露，它固定使用31080的端口；SSH Service默认通过NodePort向外暴露，它固定使用31022的端口；

### 部署Jenkins
- Jenkins使用了hostPath类型的存储卷，该方式并不适用于生产环境，应用于生产环境之前，建议按需要修改为可用的PVC资源后再进行部署；
- Jenkins目录下的配置清单文件名被依次编制了序号，建议按序号依次进行部署；
- 它默认均部署于jenkins名称空间下；
- Jenkins Service默认通过NodePort向外暴露，它固定使用32080的端口；
- 部署完成后，可使用类似如下命令获取Jenkins的解锁密钥；
```bash
kubectl logs $(kubectl get pods -n jenkins | awk '{print $1}' | grep jenkins) -n jenkins
```

## 课程视频
[马哥教育](www.magedu.com)录制了基于Jenkins和GitLab的CICD视频，请有需要的朋友至马哥教育网站上找课程顾问了解相关的信息。

## iKubernetes公众号

![ikubernetes公众号二维码](https://github.com/iKubernetes/Kubernetes_Advanced_Practical_2rd/raw/main/imgs/iKubernetes%E5%85%AC%E4%BC%97%E5%8F%B7%E4%BA%8C%E7%BB%B4%E7%A0%81.jpg)
