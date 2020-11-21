---
title: hexo YAMLException
tags:
  - hexo
abbrlink: 20645
date: 2020-10-30 12:45:07
categories:
- hexo_false
---

## hexo YAMLException: cannot read a block mapping entry; a multi line key may not be an implicit key a



安装 heox时报错：



YAMLException: cannot read a block mapping entry; a multi line key may not be an implicit key at line 5, column 1: # Site



YAMLException: cannot read a block mapping entry; a multi line key may not be an implicit key at line 13, column 1: # URL



启动hexo 时包上面的错误时，你们都是配置文件：_config.yml  中 # Site #URL 属性设置后面的：需要有空格再填写内容！！！



如果按照流程步骤 执行hexo server 没有反应，说明你少了npm install  这部，没有安装hexo server 模块