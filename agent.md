# CashewTeam 博客写文 Agent 约定

本文件用于指导后续 agent 在本仓库中快速新增博客文章。

核心原则：

1. 不修改现有文件，除非用户明确要求。
2. 新文章放在 `_posts/`。
3. 文章资源优先沿用仓库现有风格，不擅自引入新的目录结构或新的引用习惯。
4. 优先遵循“仓库当前实际写法”，不要机械照搬上游 Chirpy 文档示例。

## 1. 仓库现有结构

- 文章目录：`_posts/`
- 页面目录：`_tabs/`
- 文章图片主要目录：`assets/image/posts/`
- 站点图标等资源目录：`assets/img/`、`assets/image/`

后续新增文章时：

- Markdown 文件新建到 `_posts/`
- 文章配图优先放到 `assets/image/posts/<专题或文章目录>/`
- 不要把文章图片放到 `assets/img/`，因为当前仓库文章正文主要使用的是 `assets/image/posts/...`

## 2. 文章文件命名

文件名格式：

```text
_posts/YYYY-MM-DD-slug.md
```

示例：

```text
_posts/2026-05-12-my-new-post.md
```

说明：

- `slug` 使用英文、小写、短横线连接。
- 日期必须与文章 Front Matter 中的发布日期保持一致。

## 3. Front Matter 规范

仓库现有文章的常用头部如下：

```yaml
---
title: 文章标题
date: 2026-05-12 20:00:00 +800
categories: [主分类, 子分类]
tags: [标签1, 标签2]
description: 一句话摘要
pin: false
image:
  path: /assets/image/posts/example/cover.jpg
  alt: 文章标题
---
```

约定说明：

- `title`：必填。
- `date`：必填，当前仓库实际大量使用 `+800`。
- `categories`：通常为 2 级，例如 `[网络, 建站]`、`[Blender, Blender文档]`。
- `tags`：按现有文章风格填写，不强制小写。虽然注释里写了 lowercase，但仓库实际存在 `AE`、`Blender`、`Minecraft`、`SMARTISAN` 等大写标签，因此应优先保持与现有内容一致。
- `description`：建议填写，较新的文章都在用。
- `pin`：默认 `false`，只有用户明确希望置顶时才设为 `true`。
- `image`：封面图可选，但仓库里很多较新的文章都使用了。

补充开关：

```yaml
render_with_liquid: false
math: true
mermaid: true
toc: false
comments: false
pin: true
```

使用时机：

- `render_with_liquid: false`：正文里要展示 Liquid 代码本身时使用。
- `math: true`：文章包含数学公式时使用。
- `mermaid: true`：文章包含 Mermaid 图表时使用。
- `toc: false`：关闭当前文章右侧 TOC。
- `comments: false`：关闭当前文章评论。
- `pin: true`：置顶文章。

## 4. TOC 相关规范

仓库配置中：

- `_config.yml` 已全局启用 `toc: true`
- 因此默认新文章会显示右侧目录

### 4.1 关闭当前文章 TOC

在 Front Matter 中加入：

```yaml
toc: false
```

### 4.2 只是不想让某个标题进入 TOC

可在标题后补属性：

```md
## 标题
{: data-toc-skip='' }
```

### 4.3 当前仓库里“TOC 折叠/展开”的特殊处理

仓库现有文章说明里出现过下面这段局部样式：

```html
<style>
.is-collapsed {
  max-height: 0 !important;
}
</style>
```

用途：

- 这是对当前页面 TOC 折叠行为的局部覆盖方式。
- 只在用户明确需要某篇文章恢复折叠效果时再加。
- 不要为了单篇文章去改全局样式文件。

## 5. 图片引用规范

优先使用站内绝对路径，从网站根开始写：

```md
![图片说明](/assets/image/posts/example/demo.jpg)
```

当前仓库正文图片主要遵循：

1. 路径以 `/assets/image/posts/...` 开头
2. 直接使用标准 Markdown 图片语法
3. 需要说明文字时，下一行写斜体说明

示例：

```md
![修改预览](/assets/image/posts/example/demo.jpg)
_修改前 / 修改后_
```

仓库里部分文章在图片后补 `<br />`，例如：

```md
![原图](/assets/image/posts/example/demo.jpg)<br />
_图片说明_
```

建议：

- 普通场景优先使用最简单的 Markdown 图片写法。
- 只有在需要和现有文章视觉风格保持一致时，再补 `<br />`。

### 5.1 封面图与正文图的区别

- 封面图写在 Front Matter 的 `image.path`
- 正文图写在 Markdown 正文中
- 两者都优先使用 `/assets/image/posts/...`

### 5.2 新图片目录建议

如需为新文章配图，优先新建：

```text
assets/image/posts/<slug>/
```

如果该文章属于已有专题，也可以复用专题目录，例如：

- `assets/image/posts/blender/`
- `assets/image/posts/aescripts/`
- `assets/image/posts/smartisan/`

原则是与现有仓库命名保持一致，不另起一套风格。

## 6. 视频引用规范

### 6.1 Bilibili 视频嵌入

仓库当前实际使用的规范是：

```liquid
{% include embed/bilibili.html id='BV1xN411q7sq' %}
```

要求：

- `id` 填 BV 号
- 优先使用这一写法嵌入 Bilibili 视频

### 6.2 直接贴视频链接

仓库里也存在直接放链接的写法，例如：

```md
<https://www.bilibili.com/video/BV1tBWkenE34/>
```

或：

```md
[介绍视频](https://www.bilibili.com/video/BV1gg4y1X7aU/)
```

选择建议：

- 需要直接在文章中播放时，优先用 `{% include embed/bilibili.html %}`
- 只是资料索引或参考链接时，直接放普通链接即可

### 6.3 本地视频文件嵌入

如用户明确提供本地视频资源，可使用 Chirpy 的视频嵌入：

```liquid
{% include embed/video.html src='/assets/video/example/demo.mp4' %}
```

当前仓库文章里暂无实际使用案例，只有说明文档示例，因此：

- 仅在用户明确要嵌入本地视频文件时使用
- 默认不要主动引入新的视频目录结构

## 7. 正文写法习惯

根据现有文章，建议优先遵循以下风格：

1. 中文为主。
2. 使用 `##`、`###` 组织层级。
3. 需要强制换行时使用 `<br />`。
4. 资源导航类文章可以大量使用列表、表格、外链。
5. 教程类文章可以搭配提示块。

提示块示例：

```md
> 这是提示信息
{: .prompt-tip }
```

也可使用：

- `.prompt-info`
- `.prompt-warning`
- `.prompt-danger`

## 8. 新文章推荐模板

```md
---
title: 文章标题
date: 2026-05-12 20:00:00 +800
categories: [主分类, 子分类]
tags: [标签1, 标签2]
description: 一句话摘要
pin: false
image:
  path: /assets/image/posts/example/cover.jpg
  alt: 文章标题
---

## 介绍

这里写正文简介。

## 正文小节

这里写正文内容。

![配图说明](/assets/image/posts/example/demo.jpg)
_配图注释_

## 视频

{% include embed/bilibili.html id='BV1xxxxxxxxxx' %}

## 结尾

这里写总结或补充说明。
```

## 9. Agent 执行要求

当用户要求“新增一篇文章”时，后续 agent 应按下面顺序执行：

1. 先查看 `_posts/` 中同主题文章，复用已有分类、标签、措辞风格。
2. 新建文章文件到 `_posts/YYYY-MM-DD-slug.md`。
3. 如果用户提供图片，再决定是否新建 `assets/image/posts/...` 目录。
4. 图片路径统一写成 `/assets/image/posts/...`。
5. Bilibili 视频优先用 `{% include embed/bilibili.html id='...' %}`。
6. 默认保留 TOC，不主动关闭；只有用户明确要求或文章确实不需要目录时才加 `toc: false`。
7. 不修改现有文章、不重排旧资源、不批量改标签大小写。

## 10. 简短判断准则

如果不确定怎么写，优先按下面规则决策：

1. 先模仿同主题现有文章。
2. 路径优先用 `/assets/image/posts/...`。
3. 视频优先用 Bilibili embed。
4. TOC 默认开着。
5. `pin` 默认 `false`。
6. 标签大小写跟仓库现有风格保持一致，不强制改成小写。

