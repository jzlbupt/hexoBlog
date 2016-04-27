title: Hexo常见问题解决
date: 2016-02-13 18:44:10
tags: Hexo
categories: 技术
---
本文主要介绍在搭建博客的过程中遇到的问题和相应解决方案

<!--more-->
### Hexo 无用标签的删除
- 执行以下命令涌来删除无用的标签和分类
```
hexo clean
hexo d -g
```
使用hexo博客系统时，因为他是静态的，当删除一些页面后，页面的标签和分类还存在。我们可以使用以下命令来清空缓存并重新生成标签和分类
如果文章太多，分类和标签关系复杂，建议每次生成静态页面都执行以上命令，避免没必要的垃圾标签和分类

### 生成摘要
为博文生成摘要，即如何在主页显示博文时显示**阅读全文**
在用markdown编辑博文时，插入代码`<!--more-->`，之前的文字即为摘要，后面的内容在首页不显示

### 添加评论系统
采用**多说**统，其实非常傻瓜，在多说官网注册一个账号，再在站点配置文件`_config.yml`里添加`duoshuo_shortname`字段即可
另外，如果不想在`分类`和`标签`页显示评论系统，修改响应的`index.md`头部代码，加入`comments: false` 即可

### 添加来访统计
采用`busuanzi`,具体参考[该博文](http://zhiho.github.io/2015/09/29/hexo-next/)

### 添加图片
*背景：在本地使用资源文件夹添加图片，本地用例如haroopad这种编辑器预览没有问题，但是只要`hexo g`，打开服务器一看就是不显示图片的，也参考了[官网对于插入图片的说明](https://hexo.io/zh-cn/docs/asset-folders.html),但是根本没用，来回折腾了半天，终于通过一行插件搞定了问题*
安装插件：[CodeFalling-hexo-asset-image](https://github.com/CodeFalling/hexo-asset-image)
安装办法：`npm install https://github.com/CodeFalling/hexo-asset-image --save`
在插入图片时，将`image.png`放入博文对应的资源文件夹中，然后在博文中插入`![image-test](blog-test-file/image.png)`即可。
这时再看生成的代码，就从原来的

```html
<img src="blog-test-file/image.png" alt="image-test">

```
变成了
```html
<img src="/2016/04/26/blog-test-file/image.png" alt="image-test">

```

