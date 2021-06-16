# SSH配置

## Windows

```shell
Host github.com
  User git
  Hostname ssh.github.com
  PreferredAuthentications publickey
  ProxyCommand connect -S 127.0.0.1:10808 %h %p
  IdentityFile C:\Users\拾荒老冰棍\.ssh\id_rsa
  Port 443
```

