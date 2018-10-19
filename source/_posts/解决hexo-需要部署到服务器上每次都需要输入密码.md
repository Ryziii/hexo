---
title: 解决hexo 需要部署到服务器上每次都需要输入密码
date: 2018-10-19 14:28:38
tags:
    - hexo
---
  
  最近经常用hexo写总结经验和学习笔记，但是每次hexo clean && hexo d -g的时候都需要输入密码。因为我不是部署到github page是部署到个人的服务器上（按照类似这两个教程[教程1](https://segmentfault.com/a/1190000009363890)、[教程2](https://segmentfault.com/a/1190000010680022)部署的），所以网上很多经验教程不适用。
  
  网上很多人说的方法如下，在_config.yml中设置deploy把http改成git，此方法不适用我。
  
  ```yml
　deploy:
　type:git
　repository:git@xxx:xxx.git
　branch:master
　```

  我使用的是ssh免密登陆，一开始一直找不到问题在哪里，后来看到[这个帖子](https://www.jianshu.com/p/59eeb1493a45)终于发现问题。因为给服务器创建了一个git用户，所以需要切换用户到git然后设置ssh key，之前一直在root用户下设置的，巨坑。。。
  
  设置ssh key过程：
   1. 在本地端生成ssh公钥`ssh-keygen `
   2. 在服务器端切换至git用户`su git `
   3. 在服务器端`vi ~/.ssh/authorized_keys`，将本地端生成的id_rsa.pub粘贴至此
   4. `ssh -T git@xxx`测试是否成功（无需输入密码则成功）
  
  
  
  