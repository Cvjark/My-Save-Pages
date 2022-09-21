该贴记录自己以往使用 git 遇到的一些问题


<details><summary>问题一：OpenSSL SSL_read: Connection was reset, errno 10054</summary>
  
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

</details>

  
  
<details><summary>问题一的补充</summary>
  <br>
  实际应用过程中，发现问题一的解决方式不能全局应用，因为问题一的方案是对当个已 clone 下来的项目有效。随后笔者在 clone 其他项目仓库也发现了同样的问题
  
  ![image](https://user-images.githubusercontent.com/89090949/191408515-8152478d-9004-4978-88f6-bbace42e85ff.png)
  
  因此，猜想是否 git 本身就存在配置文件，随后找到 git 的安装目录，找到了一个配置文件：
  
  ![image](https://user-images.githubusercontent.com/89090949/191408608-f790e8d8-9298-4e51-bf19-453a32fa9f4c.png)
  
管理员打开，加入如下内容：
  
  ![image](https://user-images.githubusercontent.com/89090949/191408689-4c929ad5-8380-4294-a9e6-6b82df24a2e3.png)
  
解决问题
  
</details>
  
