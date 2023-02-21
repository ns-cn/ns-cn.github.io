---
title: "基于本站快速搭建自己的网站-New from this."
date: 2023-02-08T09:56:29+08:00
draft: false
tags: [DoItYourself]
categories: [ThinRedLine]
url: /posts/thinreadline/new-from-this/
---

> 本文介绍基于仓库[ns-cn/ns-cn.github.io](https://github.com/ns-cn/ns-cn.github.io)使用`Hugo`和`Github Pages`搭建个人博客

## 一、依赖组件

|组件|说明|
|:---:|:---:|
|Github|Github账号密码|
|git|本地需安装git|
|hugo|如需本地调时需安装hugo([官网](https://gohugo.io/)、[安装手册](https://gohugo.io/installation/))|



## 二、Get Started

### 核心步骤

{{< mermaid >}}
flowchart LR
    s1[克隆仓库]-->s2[初始化]
    s2-->s3[新建文章]
    s3-->s4[本地调试]
    s4-->s5[远程推送]
    s5-->s6[配置GithubPages]
    s6-->s7[访问测试]
{{</mermaid>}}

## 三、流程

### 1、克隆仓库

#### 1.1、fork仓库

登录github并fork仓库[ns-cn/ns-cn.github.io](https://github.com/ns-cn/ns-cn.github.io)、修改仓库名称为`{user-name}.github.io`，例如github用户名为`tom`，则克隆仓库名称为`tom.github.io`

> 注：如果仓库名不为`{user-name}.github.io`，则最后生成的网站访问链接为`{user-name}.github.io/{repo-name}`，例如tom的博客仓库为blog，则则最后的访问链接为`tom.github.io/blog`

#### 1.2、克隆到本地

克隆网站源码到本地并初始化主题仓库

```shell
git clone {your-repo}
cd {your-repo}
git submodule init
git submodule update
```

例如

```shell
git clone https://github.com/ns-cn/ns-cn.github.io.git
cd ns-cn.github.io
git submodule init
git submodule update
```



### 2、初始化

> 初始化主要是根据自己的情况删除不必要的原始文章，并根据个人修改配置网站配置

#### 2.1、初始文章

原始文章在目录content中，需删除原始内容并自行新增，针对content内容做简单说明

|目录|说明|
|:---:|:---:|
|about|关于页面，可根据自行需要删除|
|best|收藏页面，可根据自行需要删除|
|opensource|开源页面，可根据自行需要删除|
|posts|文章原始目录，写的markdown文章就放在这里面|
|start|导航页面，可根据自行需要删除|
|tags|标签页面，按标签索引，不建议删除|

#### 2.2、网站配置

修改hugo的全局配置文件`config.toml`，可手动搜索`ns-cn`搜索个人相关配置，进行修改

#### 2.3、网站菜单

通过配置`languages.zh-cn.menu.main`进行全局菜单栏配置

#### 2.4、配置域名

如果需要个性化定制域名，可修改CNAME文件为自己的域名，例如`tangyujun.com`，并参考附录文章[^1]进行Github配置和域名解析。

### 3、新建文章

> 全局文章均保存在content/posts目录，可新建目录自行分类

在仓库根目录使用命令`hugo new content/posts/***.md`或新建markdown文件，文件大致内容

```markdown
---
title: "基于本站快速搭建自己的网站-New from this."
date: 2023-02-08T09:56:29+08:00
draft: true
tags: [TAG]
categories: [ThinRedLine]
url: /posts/thinreadline/new-from-this/
---

## markdown正文
```

|标签内容|说明|
|:---:|:---:|
|title|文章标题|
|date|文章时刻|
|draf|是否是草稿，发布改为false|
|tags|文章标签|
|categories|文章分类|
|url|指定文章url，可选默认文件名称|

### 4、本地调试

在仓库根目录使用命令`hugo server`在本地启动服务器，访问[localhost:1313](http://localhost:1313/)预览

> 预览为实时预览，修改markdown文件即可实时在网页显示渲染效果

如果想使用docker部署hugo，可参考在仓库文件路径下执行如下命令

```shell
docker pull klakegg/hugo:0.107.0-ext-ubuntu-onbuild
docker run --rm -it -v $(pwd):/src -p 1313:1313 klakegg/hugo:0.107.0-ext-ubuntu-onbuild server -DEF
```

### 5、远程推送

正常提交仓库中的文章文件和配置文件等内容

```shell
git commit -a -m "新文章"
git push
```

### 6、部署GithubPages

仓库已包含自动部署hugo的Github Action，可在提交时自动部署到GithubPages。

## 四、主题定制

可参考官方收录的主题：[Hugo Themes](https://themes.gohugo.io/)，主题使用可参考对应仓库的说明，本站使用主题：[dillonzq/LoveIt](https://github.com/dillonzq/LoveIt)

## 五、高级使用

[MarkDown进阶之Mermaid绘图](/posts/thinreadline/graph-with-markdown/)

[^1]: [github怎么绑定自己的域名？](https://www.zhihu.com/question/31377141)
