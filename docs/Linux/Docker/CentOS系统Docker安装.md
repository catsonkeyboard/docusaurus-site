---
slug: CentOS系统Docker安装
title: CentOS系统Docker安装
authors: liming
tags: [linux, docker, centos]
---
官网安装地址：

[Install Docker Engine on CentOS](https://docs.docker.com/engine/install/centos/)

<!-- truncate -->

第一步

```Bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

第二步

##官网地址

```Bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

##阿里云地址

```Bash
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

查看所有版本

```Bash
yum list docker-ce --showduplicates | sort -r
```

安装docker

```Bash
sudo yum install docker-ce
```

```Bash
sudo yum install docker-ce docker-ce-cli containerd.io
```

如果containerd.io版本过低

```Bash
yum install -y docker-ce --nobest
```

启动docker及测试

```Bash
systemctl enable docker systemctl start docker docker run hello-world
```

卸载docker

```Bash
yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux docker-engine-selinux docker-engine
```

centos8安装报错：

```Bash
sudo dnf install https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm
```

安装命令:

```Bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

```Bash
sudo yum-config-manage -add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

```Bash
sudo dnf install https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm
```

```ada
sudo yum install docker-ce docker-ce-cli
```

```ada
sudo systemctl start docker && sudo systemctl enable docker.service
```

```Bash
sudo gpasswd -a $(whoami) docker
```