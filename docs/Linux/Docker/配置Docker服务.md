
# 配置Docker服务

为了避免在使用非root用户下，每次使用Docker命令都需要sudo，可以将当前用户加入安装中自动创建的docker用户组
``` shell
sudo usermod -aG docker [用户]
```