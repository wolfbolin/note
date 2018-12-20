# Docker 相关操作

## CentOS7安装docker

包含yum安装过程与更换加速源的过程

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker-ce
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://yb0igknh.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
systemctl enable docker
```

