# shOfCICD
脚本文件库

### 步骤
#### 1.initCentOS.sh

// 系统centos7
----- 下载docker/docker-compose 并更新源
----- 创建工作目录 /home/work

#### 2.k8s centos_conf <所有机器>
----- 配置k8s运行环境
----- // 关闭防火墙 - 关闭selinux -关闭swap

#### 3.k8s kubeadm kubelet 下载
----- 配置k8s源
----- 下载并启动adm/let

THEN命令
初始化k8s 以下这个命令开始安装k8s需要用到的docker镜像，可以使用docker images查看到
这里的--apiserver-advertise-address使用的是master和node间能互相ping通的ip
这条命令执行时会卡在[preflight] You can also perform this action in beforehand using ''kubeadm config images pull，大概需要2分钟，请耐心等待。

##### kubeadm init --image-repository registry.aliyuncs.com/google_containers --kubernetes-version v1.16.0 --apiserver-advertise-address 192.168.99.104 --pod-network-cidr=10.244.0.0/16 --token-ttl 0

#### 4.加入集群
记住node加入集群的命令 上面kubeadm init执行成功后会返回给你node节点加入集群的命令，等会要在node节点上执行，需要保存下来，如果忘记了，可以使用如下命令获取。
##### kubeadm token create --print-join-command

master 节点安装完毕 使用以下命令查看状态
##### kubectl get nodes

切换至node节点--继续步骤2、3
b 加入集群 -步骤4

#### 5.最后 安装flannel（master）

> 以上完成后可见，集群状态依旧为 notReady (kubectl get nodes)

下载官方fannel配置文件 使用wget命令

kubectl apply -f kube-flannel.yml
