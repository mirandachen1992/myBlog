---
layout: post
title:  "github pages 创建个人博客"
date:   2015-08-21 15:14:54
categories: githubPages
---
## 序


从实习之后，一直想建立一个个人博客，然而由于个人的拖延症，一直到今天。嘛~ 所以开始还是说一说怎么使用github pages 建立个人博客吧。（ps：吐槽一下，用了两个月Mac之后发现Windows好难用~~）


---

## 为什么要用[github pages](https://pages.github.com)

1. 搭建简单而且免费；

2. 支持静态脚本；

3. 可以绑定你的域名；

4. DIY自由发挥，动手实践一些有意思的东西git,markdown,bootstrap,jekyll；

5. 理想写博环境，git+github+markdown+jekyll；

---

## github pages 两种模式

###User/Organization Pages 个人或公司站点

1. 己的用户名，每个用户名下面只能建立一个；

2. 命名必须符合这样的规则username/username.github.com；

3. 主干上内容被用来构建和发布页面

###Project Pages 项目站点

1. gh-pages分支用于构建和发布；

2. 如果user/org pages使用了独立域名，那么托管在账户下的所有project pages将使用相同的域名进行重定向，除非project pages使用了自己的独立域名；

3. 如果没有使用独立域名，project pages将通过子路径的形式提供服务username.github.com/projectname；

4. 自定义404页面只能在独立域名下使用，否则会使用User Pages 404；<br>

>第一种模式相当简单，按照[github pages](https://pages.github.com)步骤做就可以了，还可以选择默认的模板，瞬间blingbling。接下来看一下第二种模式的步骤。

---

## Project Pages搭建过程

1. 安装Ruby

	前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)

	在 “RubyInstallers” 部分，选择某个版本点击下载。
例如， Ruby 2.0.0-p451 (x64) 是适于64位 Windows 机器上的 Ruby 2.0.0 x64 安装包。安装后配置环境变量你懂得……

2. 安装 DevKit

	再次前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)

	下载同系统及 Ruby 版本相对应的 DevKit 安装包。

	运行安装包并解压缩至某文件夹，如 C:\DevKit

	通过初始化来创建 `config.yml` 文件。在命令行窗口内，输入下列命令：

	<pre><code class="markdown">
	cd “C:\DevKit”
    ruby dk.rb init
    notepad config.yml
	</code></pre>

	在打开的记事本窗口中，于末尾添加新的一行 - `C:\Ruby200-x64`，保存文件并退出。

	回到命令行窗口内，审查（非必须）并安装。

	<pre><code class="markdown">
	ruby dk.rb review
	ruby dk.rb install
	</code></pre>

3. 安装gem

	Ruby里面自带gem，由于国内的网络，gem官方的源基本上是没法用了,参考[taobao镜像](http://ruby.taobao.org/)。

4. 安装jekyll

	<pre><code class="markdown">gem install jekyll</code></pre>

5. 搭建网络目录

	在github上新建一个项目比如叫`myBlog`，本地pull下来之后新建`gh-pages`分支，然后按照下面的目录在myBlog文件夹下搭建网络目录。
	<pre><code class="markdown">
	|—— _config.yml
	|—— _includes
	|—— _layouts
	|   |—— default.html
	|   |—— post.html
	|—— _posts
	|   |—— 20011-10-25-open-source-is-good.html
	|   |—— 20011-04-26-hello-world.html
	|—— _site
	|—— index.html
	|—— assets
	|   |—— css
	|      |—— style.css
	|   |—— javascripts
	</code></pre>

	具体文件内容和样例可以参考[http://www.pchou.info/web-build/2013/01/07/build-github-blog-page-05.html](http://www.pchou.info/web-build/2013/01/07/build-github-blog-page-05.html)

	搭建完之后在该目录下运行
	<pre><code class="markdown">jekyll server</code></pre>
	成功后就可以在[http://localhost:4000/](http://localhost:4000/)中查看效果了

6. 发布
	
	博客写好之后，直接push到myBlog远程gh-pages分支就可以了，随后查看[https://mirandachen1992.github.io/myBlog/](https://mirandachen1992.github.io/myBlog/)(这里要替换成自己的用户名和项目名称哦~)，完成bingo!

	当然你也可以下载别人的模板进行使用，如果有空的话自己写一个模板也是很有意思的事情呢~~~
