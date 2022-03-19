---
title: Hello CC
---

###在vercel新建hexo博客项目并用git将其clone到本地后，我想要自定义博文内容并更新
###
在此过程中遇到了如下问题：
###

#####无法用hexo命令进行博文的快速创建/初始化
#####例如:
```bash 
$ hexo init
```

### 报错

```bash
无法加载文件xxx
因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170  所在位置
```


### 解决方案

```bash
$ set-ExecutionPolicy RemoteSigned
```


