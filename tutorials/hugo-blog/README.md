# 从零搭建个人博客（Hugo + PaperMod + GitHub Pages）

> 一套完整、可复现的静态博客搭建指南。
> 全部免费：域名可选，其余零成本。
> 适合：会一点命令行、想有自己的网站但不想学后端的人。

---

## 这套教程能做出什么

- 一个跑在 `https://你的用户名.github.io` 的博客
- 支持 Markdown 写文章、标签分类、搜索、深色模式
- 改一行配置换主题样式，改 CSS 换配色
- 推送到 GitHub 自动构建部署，30 秒上线
- 可选：绑定自己的域名 + 免费 HTTPS

**不需要**：服务器、数据库、后端语言、付费托管。

---

## 学习路线

| 章节 | 内容 | 预计耗时 |
| --- | --- | --- |
| [01 环境准备](01-环境准备.md) | 装 Hugo、Git，验证能跑 | 20 分钟 |
| [02 创建站点](02-创建站点.md) | `hugo new site`，跑起本地预览 | 10 分钟 |
| [03 配置与主题](03-配置与主题.md) | 装 PaperMod，改标题、菜单、社交链接 | 30 分钟 |
| [04 写第一篇文章](04-写第一篇文章.md) | front matter、Markdown、图片、草稿 | 20 分钟 |
| [05 自定义样式](05-自定义样式.md) | 覆盖 CSS、改模板、加组件 | 40 分钟 |
| [06 部署到 GitHub Pages](06-部署到GitHub-Pages.md) | 仓库、Actions、Pages 设置 | 30 分钟 |
| [07 绑定域名与 HTTPS](07-绑定域名与HTTPS.md) | DNS 解析、CNAME、强制 HTTPS | 20 分钟 |
| [08 日常维护与排错](08-日常维护与排错.md) | 常用命令、报错对照表 | 随时查 |
| [09 进阶玩法](09-进阶玩法.md) | 评论、搜索、统计、图片处理 | 选做 |

**总计约 3 小时**，可以分几次做完。

---

## 快速开始（已经会 Hugo 的人）

```bash
# 1. 建站
hugo new site myblog && cd myblog
git init

# 2. 装主题
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod

# 3. 配置
echo "theme = 'PaperMod'" >> hugo.toml

# 4. 写文章
hugo new content posts/hello.md

# 5. 预览
hugo server -D
```

部署见 [06 章](06-部署到GitHub-Pages.md)。

---

## 目录说明

```
hugo-blog/
├── README.md                本文件：总览与路线
├── 01-环境准备.md
├── 02-创建站点.md
├── 03-配置与主题.md
├── 04-写第一篇文章.md
├── 05-自定义样式.md
├── 06-部署到GitHub-Pages.md
├── 07-绑定域名与HTTPS.md
├── 08-日常维护与排错.md
├── 09-进阶玩法.md
├── cheatsheet.md            命令速查（打印出来贴旁边）
└── examples/                可直接复制的文件
    ├── hugo.toml            完整的配置示例
    ├── .gitignore
    ├── archetypes/
    │   └── default.md       新建文章的模板
    ├── content/
    │   └── posts/
    │       └── hello-world.md
    ├── assets/
    │   └── css/extended/
    │       └── custom.css   自定义样式示例
    └── .github/workflows/
        └── hugo.yaml        自动部署工作流
```

---

## 为什么选这套技术栈

| 方案 | 优点 | 缺点 |
| --- | --- | --- |
| **Hugo**（本教程） | 构建毫秒级、单二进制、无依赖 | Go 模板语法要学一点 |
| Hexo | 中文资料多、插件丰富 | Node 依赖重、构建慢 |
| Jekyll | GitHub 原生支持 | Ruby 环境麻烦、构建慢 |
| WordPress | 功能全、可视化 | 要服务器和数据库、有安全风险 |
| 直接写 HTML | 完全可控 | 每篇文章都要复制粘贴 |

**Hugo 的核心优势**：一个 exe 就能跑，构建 1000 篇文章只要几百毫秒，写完 push 就自动上线。

---

## 前置知识

不需要会编程，但需要：

- 会用命令行（`cd`、`ls`/`dir`、执行程序）
- 知道什么是文件路径
- 有 GitHub 账号（免费）
- 会基本的 Markdown（10 分钟能学完）

如果这些都不会，先做 [01 章](01-环境准备.md) 的检查清单。

---

## 关于本教程

- 命令同时给了 macOS/Linux 和 Windows 版本
- 每一步都有「验证」小节，做完能确认成功
- 遇到的坑都写在「常见错误」里，包括我自己踩过的
- `examples/` 里的文件可以直接复制进你的项目

---

## 开始

👉 [01 环境准备](01-环境准备.md)
