---
title: HexoBlog初体验
---

###在vercel新建hexo博客项目并用git将其clone到本地后，我想要自定义博文内容并更新
###在此过程中遇到了如下问题：


####无法用hexo命令进行博文的快速创建/初始化
####例如:
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

####同时,hexo-renderer-marked渲染引擎似乎也不太理想，将###等语法直接渲染成文字

###解决方案

```bash
$ npm uninstall hexo-renderer-marked
$ npn install hexo-renderer-kramed --save
```

###再次使用hexo server运行，则能看到正常的博文效果


