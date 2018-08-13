# ubuntu-vagrant

vagrant 安装插件

```
vagrant plugin install vagrant-hostmanager vagrant-env --plugin-clean-sources --plugin-source https://gems.ruby-china.org/
```

vagrant 添加本地文件

```
vagrant box add ubuntu-metadata.json
```

如果使用 windows , path 按以下调整

```
file:///d:/path/to/file.box
```

设置 env 文件

如果使用 ssh-key 登陆，将 pub 写入 `.env` 文件中的 `SSH_PUB` 变量中

```
cp  .env-example .env

$ cat .env-example
SSH_PUB="xxxxx"
NODE_COUNT=1
OS=ubuntu/trusty64
```

虚拟机数量，在 Vagrantfile 中调整变量 n 的值对应虚拟机数量

```
N = 2
```

启动 vagrant

```
vagrant up
```
