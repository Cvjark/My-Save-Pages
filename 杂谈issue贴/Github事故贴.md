该贴记录自己以往使用 git 遇到的一些问题

### 问题描述

```Bash
$ git push
fatal: unable to access 'https://github.com/xxx/xxx/': OpenSSL SSL_read: Connection was reset, errno 10054
```
Google 了以下，发现解决方案是关闭 ssl 校验，命令如下：
```bash
$ git config http.sslVerify false
```

随后出现新问题：
```Bash
$ git push
fatal: unable to access 'https://github.com/xxx/xxx/': Failed to connect to github.com port 443 after 21045 ms: Timed out
```
可以看到，是个超时错误，由于 Github 国内会被 Anti-Magic Shield 挡住，怀疑是 DNS 的问题，因为我的机器能访问 Github，就是 git push 出错。
查看当前 GitHub.com 的可用 ip，可以使用如下网站：[Link](https://ipaddress.com/website/github.com)

<img  src="https://user-images.githubusercontent.com/89090949/191400987-0302afa8-6e20-4413-9ec9-3a79ba0cfc66.png" />

修改 host 文件
![image](https://user-images.githubusercontent.com/89090949/191401099-0d823e78-4b1b-4d3e-a408-cff6d02a0d89.png)

问题解决：
![image](https://user-images.githubusercontent.com/89090949/191401342-0faa0d6d-6a5b-4e4e-9e16-8370da8b49fa.png)
