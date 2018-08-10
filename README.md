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

如果使用 ssh-key 登陆，将 pub 写入 `.env` 文件中的 `SSH_PUB` 变量中

```
cp  .env-example .env
```

启动 vagrant

```
vagrant up
```
