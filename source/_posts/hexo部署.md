---
title: hexo部署
tags:
  - hexo
  - next
categories: hexo
abbrlink: 55230
date: 2021-01-04 15:48:49
---
## 部署
1. 注册github账号(有github账号的可跳过)
2. 登录后，新建一个代码仓库名为：github账号名.github.io,权限为public

3. 实现git和github的链接
    1. 鼠标右键打开git Bash Here
    2. 在git Bash Here中设置
    ```     
    git config --global user.name "Your Name"
    git config --global user.email "email@example.com"
    ```
    3.  然后再输入，获取密钥
   ```
   ssh-keygen -t rsa -C "your_email@example.com" 
   ```
   按照提示默认下一步，生成两个文件，按照所给出的路径，用记事本打开id_rsa.pub，并复制
   4. 打开github的settings/SSH and GPG keys
   点击SSH keys旁边的新建，在Title处给密钥起一个名字，并把密钥粘贴到Key处，
   5. 输入` ssh -T git@github.com`判断git和github是否连接成功
4. 添加提交设置：打开blog/_config.yml在最后添加
   ```
    deploy:
    type: git   
    repo: https://github.com/Romanticqq/romanticqq.github.io.git //提交的github仓库地址
    branch: master //分支名
   ```
5. 进行部署
    ```
    hexo clean //清理public的内容
    hexo g //生成静态内容
    hexo d  //部署上传
    可能在上传时会报错，此时需要执行下面一句命令行
    npm install hexo-deployer-git --save
    ```
6. 访问
在浏览器地址栏输入`https://仓库名.github.io`,即可访问




