---
title: Hello Hexo
---
博客搭建好了，那就记录一下安装过程吧～～

1. 安装[hexo](https://hexo.io/zh-cn/)
  ```
  npm install hexo-cli -g
  ```

2. 初始化
  ```
  hexo init blog #会自动在当前目录创建一个blog文件夹，并初始化（文件夹的名字可以任意）
  cd blog
  npm install #安装相关的依赖包（执行init的时候默认会执行）
  hexo server #启动本地server，（启动后直接访问http://localhost:4000）
  ```
  执行完以上操作后，一个本地的博客网站就搭建好了，那怎么让别人能访问到我的博客呢？

3. 关联github page
  github page 分为两种类型： User or organization site 和 Project site。
  我选择的是User site，具体区别可以看[Github Pages](https://pages.github.com/)
  - 新建一个repository,如下图（项目名字格式为：[你的用户名].github.io）
    ![](/images/githubpage.png)
  - 进入到步骤2的blog目录,修改`_config.yml`配置文件
      ```
      ...
      ...
      # URL
      ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
      url: https://[你的用户名].github.io #关联成功后的访问地址
      root: /
      ...
      ...
      # Deployment
      ## Docs: https://hexo.io/docs/deployment.html
      deploy:
        type: git
        repo:
          github: https://github.com/sweetolive/sweetolive.github.io.git #repository url（https or ssh）
          branch: master #把生成的blog部署到master分支
      ```
  - 对该目录进行git初始化，然后，创建一个没有父节点的分支`blog`（博客的工作分支）
    ```
    git init
    git checkout --orphan blog
    ```
  - 安装 hexo-deployer-git（hexo3.0后需要这个库的支持）
    ```
    npm install hexo-deployer-git --save
    ```
  - 把本地blog分支推送到远程github
    ```
    git remote add origin https://github.com/sweetolive/sweetolive.github.io.git #repository url（https or ssh）
    git push -u origin blog
    ```
  - 生成网站，把生成的网站内容部署到master分支
    ```
    hexo clean #清除缓存文件 (db.json) 和已生成的静态文件 (public)
    hexo generate #生成静态文件
    hexo deploy #部署网站
    ```
  - 大功告成，访问https://[你的用户名].github.io～～
4. Reference
  - [如何搭建一个独立博客](http://www.jianshu.com/p/05289a4bc8b2)
  - [搭建一个免费的，无限流量的Blog----github Pages](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
  - [YAML 语言教程](http://www.ruanyifeng.com/blog/2016/07/yaml.html)
  - [hexo官网](https://hexo.io/zh-cn/)
  - [hexo 部署](https://hexo.io/zh-cn/docs/deployment.html)
  - [hexo wiki](https://github.com/hexojs/hexo/wiki/Breaking-Changes-in-Hexo-3.0#slimmer-core-module)
