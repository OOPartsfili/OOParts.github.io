# 个人主页项目使用说明书 (精简版)

欢迎来到你的个人主页项目！本主页基于 Jekyll 框架构建，并托管在 GitHub Pages 上。
为了让项目体积更轻量、逻辑更清晰，目前我们已经删除了所有不需要的原生模板页面（如 Publications、Talks 等），仅保留了你所需要的**核心三页：基本信息 (Home)、成果 (Achievements)、资源分享 (Resources)**。

为了方便日后的维护与更新，本说明书将整个项目拆分为几个核心模块，并用最通俗易懂的语言告诉你：**每个模块的原理是什么？如果想要修改或添加内容，你应该去哪里找对应的文件？**

---

## 💡 进阶知识 1：顶部按钮点击跳转的原理是什么？

在学习如何修改网站之前，我们先来解答一个疑惑：**为什么点击网页顶部的“成果”按钮，就能跳转到正确的成果页面？**

1. **菜单是怎样被定义的？ (`_data/navigation.yml`)**
   在这个文件里，你定义了所有的顶部按钮以及它们的相对路径。
   ```yaml
   main:
     - title: "成果 (Achievements)"
       url: /achievements/
   ```
   这里的 `url: /achievements/` 告诉网站：“成果”按钮对应的后缀路径是 `/achievements/`。

2. **网址前缀是怎样拼接的？ (`_config.yml`)**
   因为你的 GitHub 账号名是 `oopartsfili`，而仓库名是 `OOParts.github.io`。在 GitHub Pages 的规则中，这种名字不一致的仓库会被分配到一个“子目录”网址下。因此在 `_config.yml` 中，我们定义了绝对的主域和子目录：
   ```yaml
   url     : "https://oopartsfili.github.io"
   baseurl : "/OOParts.github.io"
   ```
   系统会在后台将这两个变量组合成一个 `base_path` (即前缀：`https://oopartsfili.github.io/OOParts.github.io`)。

3. **最终的按钮链接是如何生成的？ (`_includes/masthead.html`)**
   在网页顶部导航栏的代码组件中，有一段自动拼接链接的逻辑：
   ```html
   <!-- 核心代码原理演示 -->
   <a href="{{ base_path }}{{ link.url }}">{{ link.title }}</a>
   ```
   当程序运行到这一行时，它会把前面的 `base_path` 和你在菜单里写的 `/achievements/` 缝合在一起，生成最终的完美跳转链接：`<a href="https://oopartsfili.github.io/OOParts.github.io/achievements/">成果 (Achievements)</a>`。

了解了这个原理，你就能毫无阻碍地在这个系统中添加任何新页面了！

---

## 💡 进阶知识 2：文件名与 `permalink` (永久链接) 有什么关联？

当你打开 `_resources/` 里的 `.md` 文件时，会发现开头写了 `permalink: /resources/ai-links`。这跟文件名（比如 `2026-04-25-ai-links.md`）是什么关系？

- **`permalink` 是“绝对的最高指令”**：只要你在文件开头写了 `permalink: /abc/def/`，不管这个文件叫什么名字，不管它放在哪个文件夹，Jekyll 最终都会把这个页面的网址强制生成为 `你的主页/abc/def/`。
- **如果不写 `permalink` 会怎样？**：Jekyll 就会按照 `_config.yml` 里定义的规则 `/:collection/:path/` 来“按图索骥”。它会提取所在的文件夹名（`resources`）和文件名本身。如果文件名是 `2026-04-25-note.md`，它就会自动生成一个有点冗长的网址：`/resources/2026-04-25-note/`。

**结论与建议**：
文件名和 `permalink` **没有绑定关系**。你可以把文件名取名叫 `1.md`，把 permalink 写成 `/resources/ai-links`。
但在实际维护中，**强烈建议在开头手动写上简短、英文的 `permalink`**（比如 `/resources/my-first-note/`），这样别人在浏览器中看到的网址会非常优雅干净，而不是带着一长串日期和奇怪的拼音文件名！

---

## 1. 核心配置模块 (全局设置与导航栏)

这个模块决定了网站的“骨架”，比如你的名字、头像、联系方式以及网页顶部的菜单栏。

### 全局配置文件：`_config.yml`
这是整个网站的“总控台”。诸如网站标题、作者个人信息（左侧边栏）、社交媒体链接等都在这里修改。

```yaml
# 在 _config.yml 文件中（约第 11 行开始）：
title                    : "黄烨鑫 (Huang Yexin) - 个人主页"
author:
  name             : "黄烨鑫"
  bio              : "同济大学 交通数据科学与工程 硕士在读"
  email            : "1074249938@qq.com" 
```
**📜 作用与修改指南**：
当你的邮箱改变了，或者你想给左侧边栏换一句话简介时，直接打开 `_config.yml`，找到对应字段修改即可。注意冒号后面要保留一个空格。

### 顶部导航菜单：`_data/navigation.yml`
这个文件专门用来控制网页最顶端的那一排点击按钮（菜单栏）。

```yaml
# 在 _data/navigation.yml 文件中：
main:
  - title: "基本信息 (Home)"
    url: /
  - title: "成果 (Achievements)"
    url: /achievements/
```
**📜 作用与修改指南**：
按照上面的**“跳转原理”**，如果你未来想在网页顶部新增一个叫做“我的博客”的入口，只需要在这里按格式加上 `title: "我的博客"` 和对应的相对路径 `url: /blog/` 即可。

---

## 2. 固定页面模块 (主页与各个分栏主界面)

这个模块决定了用户点击导航栏后，第一眼看到的静态内容。

### 主页基本信息页：`_pages/about.md`
当别人输入你的网址进入网站时，首先看到的就是这个文件渲染出来的页面。我们在顶部菜单配置的 `url: /` 就是指向它。

```markdown
# 在 _pages/about.md 文件中：
---
permalink: /
title: "基本信息 (Basic Information)"
---
## 教育经历 (Education)
**同济大学 (Tongji University)** | *2024.09 – 2027.06*
...
```
**📜 作用与修改指南**：
你想修改简历中的“实习经历”、“主要项目经历”，或者更新教育背景时，直接修改这个 Markdown 文件里的文字即可，语法非常简单，就像在使用基础的记事本打字。

### 动态列表页外壳：`_pages/achievements.html` & `_pages/resources.html`
这是“成果”和“资源分享”这俩子页面的外壳，它们会自动把对应文件夹里的一篇篇文章汇总并罗列出来。

```html
<!-- 在 _pages/achievements.html 中： -->
{% for post in site.achievements reversed %}
  {% include archive-single.html %}
{% endfor %}
```
**📜 作用与修改指南**：
这段代码包含了一个 Jekyll 的 Liquid 语法循环 (`for post in site.achievements`)，它的作用是：**自动去拉取 `_achievements` 文件夹下的所有文章记录，并按照时间倒序排列成一个整齐的列表**。通常情况下你**不需要**修改这两个 HTML 文件。要添加新成果，请直接看下一个“动态内容扩展模块”。

---

## 3. 动态内容扩展模块 (如何添加新成果/新笔记)

这部分是你未来使用最频繁的模块！当你发了新论文、得了新奖项，或者写了新的学习笔记，都在这里操作。得益于刚刚提到的“动态列表页外壳”，你完全不需要去手写 HTML 代码排版。

### 成果文件夹：`_achievements/`
里面存放了你所有的荣誉、论文和竞赛记录。每添加一个 `.md` 文件，网页上的“成果”列表里就会多出一条记录。

```markdown
# 在 _achievements/ 文件夹新建一个文件，例如 2027-01-01-new-paper.md：
---
title: "新论文发表 (CVPR 2027)"
collection: achievements
permalink: /achievements/cvpr2027
date: 2027-01-01
---
这里是关于这篇新论文的详细介绍...可以随意书写正文。
```
**📜 作用与修改指南**：
无需改动任何复杂的网页代码！只需要在这个文件夹里**新建一个文本文件**，按照上面的格式填好标题 (`title`)、所属集合 (`collection: achievements`)、和日期 (`date`)，然后写上正文。网站的循环机制就会自动把它抓取并作为一条新成果展示出来。

### 资源分享文件夹：`_resources/`
同理，里面存放了你推荐的 AI 资源链接和学习笔记预告。

```markdown
# 在 _resources/ 文件夹新建一个文件，例如 2026-05-01-note.md：
---
title: "我的第一篇大模型微调笔记"
collection: resources
permalink: /resources/llm-note-1
date: 2026-05-01
---
今天学习了 QLoRA 的微调方法，踩了如下几个坑...
```
**📜 作用与修改指南**：
未来你要发布新的学习笔记时，直接在这个文件夹里添加带有同样头部信息的 `.md` 文件即可，非常便捷。

---

## 📝 日常更新工作流总结 (一图流)

记住这个傻瓜式更新流程：

1. **想改简历了** 👉 去 `_pages/about.md` 敲字。
2. **得奖发论文了** 👉 去 `_achievements/` 文件夹下“照猫画虎”新建一个 `.md` 文件。
3. **想发学习笔记** 👉 去 `_resources/` 文件夹下“照猫画虎”新建一个 `.md` 文件。
4. **保存推送到网上** 👉 在电脑终端里依次运行以下三条命令：
   ```bash
   git add .
   git commit -m "更新了我的个人主页"
   git push
   ```
   等待 1~2 分钟，刷新你的个人主页网页，大功告成！
