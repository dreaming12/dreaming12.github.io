---
title: setup
date: 2022-03-04
tags:
---

# 搭建说明

> [Hexo](https://hexo.io/zh-cn/) ~ [Docs](https://hexo.io/docs/)

注意修改网址永久链接格式为 `:title/`，方便使用

安装 `hexo-server`。服务器启动后，它就能根据文件变动自动更新，不需要重启服务器

```shell
$ npm install hexo-server --save
```

## GitHub Pages

安装 `hexo-deployer-git`

```shell
$ npm install hexo-deployer-git --save
```

在 `_config.yml` 中添加配置：

```yml
deploy:
    type: git
    repo: https://github.com/<username>/<project-name>
    branch: gh-pages
```

GitHub Pages 默认从 `mian` 分支构建，需要在 `Settings` 中修改为 `gh-pages` 分支

```shell
$ hexo clean
$ hexo deploy
```
