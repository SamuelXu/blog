---
layout: post
title:  "jekyll 安装记录"
date:   2019-03-23 22:30:54 +0800
categories: jekyll 
tags: jekyll
---

## 1. 安装ruby

使用rvm安装ruby和进行版本管理，rvm相关命令有：

```shell
##安装rvm
#gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
#curl -sSL  https://get.rvm.io | bash -s stable
#rvm reload //重新加载rvm
#rvm -v  //查看版本
#rvm list known //list 已知的ruby版本
#rvm install 2.6 //安装ruby 2.6
#rvm remove 2.4 //删除2.4版本
#rvm 2.6.0 --default //设置2.6为默认版本

#ruby -v //查看ruby版本
#gem -v //查看gem版本
```

## 2. 安装jekyll

RubyGems是一个方便而强大的Ruby程序包管理器（ package manager），类似RedHat的RPM.它将一个Ruby应用程序打包到一个gem里，作为一个安装单元。

Bundle相当于多个RubyGems批处理运行。在配置文件gemfile里说明你的应用依赖哪些第三方包，他自动帮你下载安装多个包，并且会下载这些包依赖的包

```shell
#gem source -r https://rubygems.org/   //删除镜像源
#gem source -a https://gems.ruby-china.com/  //增加镜像源
#gem sources -l //查看镜像源
#gem install jekyll bundler
#jekyll -v  //查看版本
#bundle config mirror.https://rubygems.org https://gems.ruby-china.com //对source https://rubygems.org/ 会转向 http://ruby.taobao.com，是全局设置,修改的是~/.bundle/config 文件中内容
#bundle config  --delete 'mirror.https://rubygems.org/' //删除映射
#gem update  //更新gem管理的软件
```

## 3.添加jekyll模版

*一、添加本地已有项目：*

在已存在项目(GitHub pages项目)中，创建Gemfile如下:

```
source 'https://gems.ruby-china.com'
gem "minimal-mistakes-jekyll"
```

```shell
#bundle //根据Gemfile,获取minimal-mistakes-jekyll工程
```

更改 _config.yml文件，替换下面一行后，执行 bundle update 即可。

```
theme: minimal-mistakes-jekyll
```

```shell
jekyll s --host 0.0.0.0  //执行后，就可以在通过ip:4000端口进行访问
```

*二、添加github项目*

1. 在github创建 username.github.io的repo

2. git clone `username.github.io` 到本地

3. 在项目中执行 `jekyll new .` ，创建博客

4. 更改Gemfile 如下:

   ```
   #source "https://rubygems.org"
   source 'https://gems.ruby-china.com'
   
   # If you want to use GitHub Pages, remove the "gem "jekyll"" above and
   # uncomment the line below. To upgrade, run `bundle update github-pages`.
    gem "github-pages", group: :jekyll_plugins
   
   # If you have any plugins, put them here!
   group :jekyll_plugins do
     gem "jekyll-include-cache"
   end
   ```

5. 编辑 _config.yml， 使用配置：

   ```
   remote_theme           : "mmistakes/minimal-mistakes@4.15.2"  //并且删除其他theme配置
   
   paginate: 5 # 增加这两行配置
   paginate_path: /page:num/
   ```

6. 删除index.md，替换为：[index.html](https://github.com/mmistakes/minimal-mistakes/blob/master/index.html)

7. 编辑更改 0000-00-00-welcome-to-jekyll.markdown 和about.md: `layout: post` 

8. 执行 `jekyll s --host 0.0.0.0` 即可通过ip:4000 访问本地

9. git commit && git push，即可通过 username.github.io 访问

10. 根据实际情况配置 _config.yml
