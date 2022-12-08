# SSH 公钥

使用SSH公钥可以让你在你的电脑和 Gitee/Github 通讯的时候使用安全连接（Git的Remote要使用SSH地址），可以解决将代码推送到Github时连接失败问题。

## 创建 SSH 公钥

Gitee/Github 提供了基于SSH协议的Git服务，在使用SSH协议访问仓库之前，需要先配置好账户/仓库的SSH公钥。

```bash
ssh-keygen -t rsa -C "xxxxxx@xxxx.com"
# Generating public/private rsa key pair...
```

> 注意：这里的 `xxxxxx@xxxx.com` 只是生成的 sshkey 的名称，并不    约束或要求具体命名为某个邮箱。  
> 现网的大部分教程均讲解的使用邮箱生成，其一开始的初衷仅仅是为了便于辨识所以使用了邮箱。

安装提示完成三次回车，即可生成 ssh key。通过查看 `~/.ssh/id_rsa.pub` 文件内容，获取你的 public key。

```bash
cat ~/.ssh/id_rsa.pub
```

## 在远程仓库中使用 SSH

在 gitee 或 github 的设置中，添加 SSH 公钥，即可使用。

## 在本地查看 SSH 是否添加成功

**gitee**

```bash
ssh -T git@gitee.com
```

若返回 `Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access.` 内容，则证明添加成功。

**github**

```bash
ssh -T git@github.com
```

若返回 `Hi XXX! You've successfully authenticated, but Github does not provide shell access.` 内容，则证明添加成功。

## 配置多个 SSH 公钥

1. 生成一个公司用的SSH-Key

```bash
ssh-keygen -t rsa -C 'xxxxx@company.com' -f ~/.ssh/gitee_id_rsa
```

2. 生成一个github用的SSH-Key

```bash
ssh-keygen -t rsa -C 'xxxxx@qq.com' -f ~/.ssh/github_id_rsa
```

3. 在 ~/.ssh 目录下新建一个config文件，添加如下内容（其中Host和HostName填写git服务器的域名，IdentityFile指定私钥的路径）

```bash
# gitee
Host gitee.com
HostName gitee.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitee_id_rsa

# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_id_rsa
```
