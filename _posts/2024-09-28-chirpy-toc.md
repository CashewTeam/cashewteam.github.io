---
title: 如何让Jekyll Theme Chirpy右侧目录始终展开
date: 2024-09-28 11:11:00 +800
categories: [教程, 前端]
tags: [jekyll]     # TAG names should always be lowercase
description: 修改"\assets\css\jekyll-theme-chirpy.scss"中的内容
pin: false
---
## 起因
在根据[Marvin的教程](https://winxuan.github.io/posts/creat-blog/)部署好[Jekyll Theme Chirpy][jtc]后，我发现右侧目录不会像其他文档软件那样全部展开或有展开按钮，只会自动根据查看进度展开，会影响较长文章的信息检索效率，所以开始寻找修改方法，本人不会前端开发，本文只是简单的经验分享。
### 修改预览
![修改预览](/assets/image/posts/24-09-28/1toc.jpg)
_修改前 修改后_

## 经过
经过查看项目的目录结构，在"_config.yml"以及其他目录内并没有找到相关可以用于配置目录（TOC）的内容，几番寻找后查询到项目使用了[tocbot](https://tscanlin.github.io/tocbot/#)作为目录的解决方案，尽管找到了文档，还是没有找到修改方法，之后在[Jekyll Theme Chirpy][jtc]的Issues和Disussions中找到有人讨论目录（TOC）相关话题，并找到了解决方案。
## 解决方法
最终在[Huanyu Shi发的讨论](https://github.com/cotes2020/jekyll-theme-chirpy/discussions/1706)中找到了解决方法，感谢Huanyu Shi及其他探索过相关问题的同志。
在 "assets/css/jekyll-theme-chirpy.scss"中添加以下代码，使用[starter](https://github.com/cotes2020/chirpy-starter)生成的项目不会有这个文件需要自己新建，注释前面的内容也需要完整添加，一开始我没有复制两行"---"导致没有生效。
``` scss
---
---

@import 'main
{%- if jekyll.environment == 'production' -%}
  .bundle
{%- endif -%}
';

/* append your custom style below */

// 让目录不产生折叠效果
.is-collapsed {
  max-height: none !important;
}
```

## 其他[Jekyll Theme Chirpy][jtc]相关中文教程：
[Marvin的教程](https://winxuan.github.io/categories/build/): 建站、配置评论区、搜索引擎收录和一些错误的解决方案。<br />
[基于 Jekyll-Theme-Chirpy v7.0.0 的个性化方案](https://huanyushi.github.io/posts/chirpy-blog-customization/): MathJax 配置、侧边栏样式、页脚站点统计、背景动画、自定义新的 prompt 和 details 元素样式、LQIP 和反色图片的 Python 实现等内容。<br />
[jekyll-theme-chirpy主题常用基础配置及侧边导航栏联系方式修改](https://blog.csdn.net/qq_36816662/article/details/128314721)


[jtc]: https://github.com/cotes2020/jekyll-theme-chirpy