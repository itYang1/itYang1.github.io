---
title: 创建hexo播客(二)
abbrlink: 1f529b85
---

```
npm install hexo-generator-search --save

```

在_config.yml文件中查找并输入:
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
在所在的主题配置文件中（_config.xxx.yml）查找到并修改为：
local_search:
  enable: true
  preload: false
  CDN: