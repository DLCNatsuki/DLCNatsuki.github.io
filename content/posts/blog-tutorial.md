---
title: "个人博客网页开发教程"
date: 2026-11-20T14:00:00+08:00
draft: false
tags: ["Hugo", "教程", "博客", "GitHub Pages"]
categories: ["教程"]
summary: "从零搭一个个人博客的完整步骤：装环境、建站、装主题、写文章、改样式、自动部署、绑域名。全部代码和配置开源在 GitHub 上。"
---

搭这个站花了我不少时间，中间踩的坑比想象中多——主题装不上、部署后 404、域名解析不生效、推送被拒。

所以我把整个过程整理成了一套教程，放在 GitHub 上，**照着做就能搭出一样的站**。

仓库地址：

**<https://github.com/DLCNatsuki/DLCNatsuki.github.io/tree/main/tutorials/hugo-blog>**

## 这套教程能做出什么

一个跑在 `https://你的用户名.github.io` 的博客：

- Markdown 写文章，支持标签、分类、搜索、深色模式
- 推送到 GitHub 自动构建，30 秒上线
- 可以绑自己的域名，免费 HTTPS
- 全程零成本，不需要服务器和数据库

## 章节安排

| 章节 | 内容 |
| --- | --- |
| 01 环境准备 | 装 Hugo Extended 和 Git，三平台命令 |
| 02 创建站点 | `hugo new site`，目录结构，开发命令 |
| 03 配置与主题 | 装 PaperMod，菜单、社交图标、归档页 |
| 04 写第一篇文章 | front matter 每个字段，图片两种放法 |
| 05 自定义样式 | 改配色、中文字体、覆盖模板 |
| 06 部署到 GitHub Pages | 仓库命名、Actions 工作流、Pages 设置 |
| 07 绑定域名与 HTTPS | 4 条 A 记录、CNAME、证书 |
| 08 日常维护与排错 | 报错对照表、Git 冲突处理 |
| 09 进阶玩法 | 评论、统计、404、Mermaid |

另外还有一份 `cheatsheet.md`，把常用命令压缩成一页，可以打印出来贴旁边。

## 三个最容易卡住的地方

写教程时我特意把这三个单独拎出来讲，因为我自己都在上面卡过。

### ① Pages 的 Source 必须选 GitHub Actions

不设置的话，GitHub 会用默认的 Jekyll 构建，结果是**部署成功但访问 404**。

```
仓库 → Settings → Pages → Build and deployment → Source → GitHub Actions
```

这一步不看教程真的想不到。

### ② 文章的日期不能写成未来

Hugo 默认**不构建未来日期的文章**。我把 `date` 写成 16:00，而当时才 15:55，结果 `public/posts/xxx/` 目录是空的，折腾了十几分钟。

症状：本地 `hugo server -D` 能看到，但 `hugo` 构建后没有这个页面。

### ③ PAT 必须勾 `workflow` 权限

用 HTTPS + Personal Access Token 推送时，如果仓库里有 `.github/workflows/`，token 没勾 `workflow` 会被直接拒绝：

```
refusing to allow a Personal Access Token to create or update workflow
```

我的解决办法是改用 SSH，一次配好再也不用管。

## 除了文档，还有能直接用的文件

`examples/` 目录里是真实在跑的配置，不是伪代码：

| 文件 | 用途 |
| --- | --- |
| `hugo.toml` | 完整配置，改掉域名就能用 |
| `custom.css` | 中文排版、配色变量、头像样式 |
| `hugo.yaml` | 部署工作流，实测可用 |
| `default.md` | 文章模板，新建自动带 front matter |
| `hello-world.md` | Markdown 语法示例 |

## 关于技术选型

我用的是 **Hugo + PaperMod**，选它的原因：

| 方案 | 构建速度 | 依赖 |
| --- | --- | --- |
| **Hugo** | 几百毫秒 | 单文件，无依赖 |
| Hexo | 几秒到几十秒 | Node 环境 |
| Jekyll | 十几秒 | Ruby 环境 |
| WordPress | 依赖数据库 | 需要服务器 |

文章多了以后差距会很明显。Hugo 编译 1000 篇也就是一次眨眼。

## 怎么用

**方式一：照着教程自己做**

从 [01 环境准备](https://github.com/DLCNatsuki/DLCNatsuki.github.io/tree/main/tutorials/hugo-blog) 开始，按顺序做完，大约 3 小时。

**方式二：直接抄配置**

把 `examples/` 里的文件复制进你的项目，改掉 `baseURL`、`title`、社交链接，能省掉大半天调试。

**方式三：clone 这个站当模板**

```bash
git clone https://github.com/DLCNatsuki/DLCNatsuki.github.io.git myblog
cd myblog
rm -rf .git
git init
```

然后把自己的内容替换进去。

## 最后

教程是持续更新的——后面每加一个新功能，我都会顺手把步骤补进去。

如果照着做的时候卡在某一步，欢迎在 GitHub 上开 issue，或者直接在文章下面留言。

> 下一篇大概会写「怎么给博客加评论系统」，用 Giscus 那套，不用后端。
