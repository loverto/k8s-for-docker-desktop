# Docker Desktop for Mac/Windows 开启 Kubernetes

中文 | [English](README_en.md)


说明: 

 *  **注意** 请阅读并遵守 [docker subscription service agreement](https://www.docker.com/legal/docker-subscription-service-agreement/) , 如果不接受 Docker Desktop 的使用条款，建议使用 [Minikube](https://minikube.sigs.k8s.io/docs/) 等其他开源工具。
 


* 需安装 Docker Desktop 的 Mac 或者 Windows 版本
* 当前 master 分支已经在 Docker for Mac/Windows 4.37.0 (包含 Docker 27.4.0 和 Kubernetes v1.31.4) 版本测试通过
* 如果需要测试其他版本，请查看 Docker Desktop版本，Docker -> About Docker Desktop
  ![about](images/about.png)
  * 如Kubernetes版本为 v1.31.4, 请使用下面命令切换 [v1.31.4 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.31.4) ```git checkout v1.31.4```
  * 如Kubernetes版本为 v1.30.5, 请使用下面命令切换 [v1.30.5 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.30.5) ```git checkout v1.30.5```
  * 如Kubernetes版本为 v1.30.2, 请使用下面命令切换 [v1.30.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.30.2) ```git checkout v1.30.2```
  * 如Kubernetes版本为 v1.29.2, 请使用下面命令切换 [v1.29.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.29.2) ```git checkout v1.29.2```
  * 如Kubernetes版本为 v1.29.1, 请使用下面命令切换 [v1.29.1 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.29.1) ```git checkout v1.29.1```
  * 如Kubernetes版本为 v1.28.2, 请使用下面命令切换 [v1.28.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.28.2) ```git checkout v1.28.2```
  * 如Kubernetes版本为 v1.27.2, 请使用下面命令切换 [v1.27.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.27.2) ```git checkout v1.27.2```
  * 如Kubernetes版本为 v1.25.9, 请使用下面命令切换 [v1.25.9 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.25.9) ```git checkout v1.25.9```
  * 如Kubernetes版本为 v1.25.4, 请使用下面命令切换 [v1.25.4 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.25.4) ```git checkout v1.25.4```
  * 如Kubernetes版本为 v1.25.2, 请使用下面命令切换 [v1.25.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.25.2) ```git checkout v1.25.2```
  * 如Kubernetes版本为 v1.25.0, 请使用下面命令切换 [v1.25.0 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.25.0) ```git checkout v1.25.0```
  * 如Kubernetes版本为 v1.24.2, 请使用下面命令切换 [v1.24.2 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.24.2) ```git checkout v1.24.2```
  * 如Kubernetes版本为 v1.24.0, 请使用下面命令切换 [v1.24.0 分支](https://github.com/AliyunContainerService/k8s-for-docker-desktop/tree/v1.24.0) ```git checkout v1.24.0```
  

注：

* 如果发现K8s版本尚未提供，您可以修改```images.properties```文件指明所需镜像版本，并欢迎提交 Pull Request
  * 通过如下命令可以获取指定K8s版本所需镜像 ```kubeadm config images list --kubernetes-version v1.30.2```
  * 可以访问 Docker Hub 获取所需如下镜像版本 tag [docker/desktop-kubernetes](https://hub.docker.com/r/docker/desktop-kubernetes/tags), [docker/desktop-vpnkit-controller](https://hub.docker.com/r/docker/desktop-vpnkit-controller/tags), [docker/desktop-storage-provisioner](https://hub.docker.com/r/docker/desktop-storage-provisioner/tags) 。
* 欢迎体验阿里云容器服务 阿里云容器计算服务 ACS （Alibaba Cloud Container Compute Service，ACS）, 开启云上Kubernetes实践之旅。https://www.aliyun.com/product/acs


### 开启 Kubernetes

为 Kubernetes 配置 CPU 和 内存资源，建议分配 4GB 或更多内存。 

![resource](images/resource.png)

从阿里云镜像服务下载 Kubernetes 所需要的镜像

在 Mac 上执行如下脚本

```bash
./load_images.sh
```

在Windows上，使用 PowerShell

```powershell
 .\load_images.ps1
```

说明: 
* 如果因为安全策略无法执行 PowerShell 脚本，请在 “以管理员身份运行” 的 PowerShell 中执行 ```Set-ExecutionPolicy RemoteSigned``` 命令。 
* 如果需要，可以通过修改 ```images.properties``` 文件自行加载你自己需要的镜像


开启 Kubernetes，并等待 Kubernetes 开始运行
![k8s](images/k8s.png)

**TIPS**：

在Mac上:

如果在Kubernetes部署的过程中出现问题，可以通过docker desktop应用日志获得实时日志信息：

```bash
pred='process matches ".*(ocker|vpnkit).*"
  || (process in {"taskgated-helper", "launchservicesd", "kernel"} && eventMessage contains[c] "docker")'
/usr/bin/log stream --style syslog --level=debug --color=always --predicate "$pred"
```

在Windows上:

如果在Kubernetes部署的过程中出现问题，可以在 C:\ProgramData\DockerDesktop下的service.txt 查看Docker日志, 在 C:\Users\yourUserName\AppData\Local\Docker下的log.txt 查看Kubernetes日志 


**问题诊断**：

如果看到 Kubernetes一直在启动状态，请参考 

* [Issue 3769(comment)](https://github.com/docker/for-win/issues/3769#issuecomment-486046718) 或 [Issue 3649(comment)](https://github.com/docker/for-mac/issues/3649#issuecomment-497441158)
  * 在macOS上面，执行 ```rm -fr '~/Library/Group\ Containers/group.com.docker/pki'```
  * 在Windows上面删除 'C:\ProgramData\DockerDesktop\pki' 目录 和 'C:\Users\yourUserName\AppData\Local\Docker\pki' 目录
* [Issue 1962(comment)](https://github.com/docker/for-win/issues/1962#issuecomment-431091114)



**K8S进入容器方法**

K8s如何进入一个pod里有多个容器的方法

```
kubectl --namespace=kube-system exec -it kube-dns-1336009800-15b1h --container nginx -- sh
```

或

```
kubectl --namespace=kube-system exec -it kube-dns-1336009800-15b1h  -c  nginx -- sh
```

注释：--namespace 为命名空间kube-dns为pod的名字，-c或-container为Pod里其中的一个容器名字


### 配置 Kubernetes


可选操作: 切换Kubernetes运行上下文至 docker-desktop (之前版本的 context 为 docker-for-desktop)


```shell
kubectl config use-context docker-desktop
```

验证 Kubernetes 集群状态

```shell
kubectl cluster-info
kubectl get nodes
```

### 配置 Kubernetes 控制台

#### 部署 Kubernetes dashboard

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.1/aio/deploy/recommended.yaml
```

或

```shell
kubectl apply -f kubernetes-dashboard.yaml
```

检查 kubernetes-dashboard 应用状态

```shell
kubectl get pod -n kubernetes-dashboard
```

开启 API Server 访问代理

```shell
kubectl proxy
```

通过如下 URL 访问 Kubernetes dashboard

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

#### 配置控制台访问令牌

授权`kube-system`默认服务账号

```shell
kubectl apply -f kube-system-default.yaml
```

对于Mac环境

```shell
TOKEN=$(kubectl -n kube-system describe secret default| awk '$1=="token:"{print $2}')
kubectl config set-credentials docker-desktop --token="${TOKEN}"
echo $TOKEN
```

对于Windows环境

```shell
$TOKEN=((kubectl -n kube-system describe secret default | Select-String "token:") -split " +")[1]
kubectl config set-credentials docker-desktop --token="${TOKEN}"
echo $TOKEN
```

#### 登录dashboard的时候

![resource](images/k8s_credentials.png)

选择 **令牌** 

输入上文控制台输出的内容

或者选择 **Kubeconfig** 文件,路径如下：

```
Mac: $HOME/.kube/config
Win: %UserProfile%\.kube\config
```

点击登陆，进入Kubernetes Dashboard

### 配置 Ingress

说明：如果测试 Istio，不需要安装 Ingress

#### 安装 Ingress

[源地址安装说明](https://github.com/kubernetes/ingress-nginx/blob/master/docs/deploy/index.md)

验证

```shell
kubectl get pods --all-namespaces -l app.kubernetes.io/name=ingress-nginx
```

#### 测试示例应用


部署测试应用，详情参见[社区文章](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html)


```shell
kubectl create -f sample/apple.yaml
kubectl create -f sample/banana.yaml
kubectl create -f sample/ingress.yaml
```

测试示例应用

```bash
$ curl -kL http://localhost/apple
apple
$ curl -kL http://localhost/banana
banana
```

删除示例应用

```shell
kubectl delete -f sample/apple.yaml
kubectl delete -f sample/banana.yaml
kubectl delete -f sample/ingress.yaml
```

#### 删除 Ingress

```shell
kubectl delete -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml
```

或

```shell
kubectl delete -f ingress-nginx-controller.yaml
```

### 安装 Helm

可以根据文档安装 helm v3 https://helm.sh/docs/intro/install/
在国内由于helm的cdn节点使用的是谷歌云所以可能访问不到，可以参考已存在的官方issue： https://github.com/helm/helm/issues/7028

#### 在 Mac OS 上安装

##### 通过 brew 安装

```shell
# Use homebrew on Mac
brew install helm

# Add helm repo
helm repo add stable http://mirror.azure.cn/kubernetes/charts/

# Update charts repo
helm repo update
```

#### 在Windows上安装

如果在后续使用 helm 安装组件的过程中出现版本兼容问题，可以参考 `通过二进制包安装` 思路安装匹配的版本

```shell
# Use Chocolatey on Windows
# 注：安装的时候需要保证网络能够访问googleapis这个域名
choco install kubernetes-helm

# Change helm repo
helm repo add stable http://mirror.azure.cn/kubernetes/charts/

# Update charts repo
helm repo update
```

#### 测试 Helm (可选)

安装 Wordpress

```shell
helm install wordpress stable/wordpress
```

查看 wordpress 发布状态

```shell
helm status wordpress
```

卸载 wordpress 发布

```shell
helm uninstall wordpress
```

### 配置 Istio

说明：Istio Ingress Gateway和Ingress缺省的端口冲突，请移除Ingress并进行下面测试

可以根据文档安装 Istio https://istio.io/docs/setup/getting-started/

#### 下载 Istio

例如下载Istio版本1.22.1（其他更新版本可以自行替换）, 执行如下命令：

```bash
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.22.1 sh -
cd istio-1.22.1
export PATH=$PWD/bin:$PATH
```

注意： Windows环境未经严格测试。

在Windows上，您可以手工下载Istio安装包，或者把```getLatestIstio.ps1```拷贝到你希望下载 Istio 的目录，并执行 - 说明：根据社区提供的[安装脚本](https://gist.github.com/kameshsampath/796060a806da15b39aa9569c8f8e6bcf)修改而来

```powershell
.\getLatestIstio.ps1
```

#### 安装 Istio

```shell
istioctl install --set profile=demo -y
```

#### 检查 Istio 状态

```shell
kubectl get pods -n istio-system
```

#### 为 ```default``` 名空间开启自动 sidecar 注入

```shell
kubectl label namespace default istio-injection=enabled
kubectl get namespace -L istio-injection
```

#### 安装 Book Info 示例

请参考 https://istio.io/docs/examples/bookinfo/

```shell
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

查看示例应用资源

```shell
kubectl get svc,pod
```

确认示例应用在运行中

```shell
kubectl exec -it $(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}') -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"
```

创建 Ingress Gateway

```shell
kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
```

查看 Gateway 配置

```shell
kubectl get gateway
```

确认示例应用可以访问

```shell
export GATEWAY_URL=localhost:80
curl -s http://${GATEWAY_URL}/productpage | grep -o "<title>.*</title>"
```

可以通过浏览器访问

http://localhost/productpage

#### 删除实例应用

```shell
samples/bookinfo/platform/kube/cleanup.sh
```

### 卸载 Istio

```shell
istioctl manifest generate --set profile=demo | kubectl delete -f -
```


