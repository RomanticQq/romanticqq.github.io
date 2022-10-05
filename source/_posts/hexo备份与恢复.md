---
title: hexo备份与恢复
tags:
  - hexo
  - next
categories: hexo
abbrlink: 49250
date: 2021-01-04 18:43:43
---
## 备份
1. 在github的博客仓库创建新的分支**backup**
2. 打开git Bash Here，输入
    ```
    npm install hexo-git-backup --save
    ```

3. 添加提交设置：打开blog/_config.yml在最后添加
   ```
    backup:
    type: git
    repository:
    github: git@github.com:Romanticqq/romanticqq.github.io.git,backup(提交的github地址,分支名)
   ```
4. 当要对代码备份时，执行`hexo d`即备份成功

## 恢复
1. 把github的博客仓库**backup**分支的内容下载到本地
2. 依次执行下列命令
    ```
    npm install hexo
    npm install
    npm install hexo-deployer-git
    ```
3. 本地文件恢复，`hexo s`开启本地服务，在浏览器输入`http://localhost:4000`测试是否正常
## 当遇到提交失败时
```php
OpenSSL SSL_read: Connection was reset, errno 10054
//在hexo d之前执行命令
git config --global http.sslVerify "false"
```