# DLCNatsuki 的博客源码

这是 [dlcnatsuki.top](https://dlcnatsuki.top) 的完整源码，用 **Hugo + PaperMod** 构建，托管在 **GitHub Pages**上。

## 想自己搭一个？

我把整个搭建过程整理成了教程，放在 [`tutorials/hugo-blog/`](tutorials/hugo-blog/README.md)：

| 章节 | 内容 |
| --- | --- |
| [01 环境准备](tutorials/hugo-blog/01-环境准备.md) | 装 Hugo、Git |
| [02 创建站点](tutorials/hugo-blog/02-创建站点.md) | `hugo new site`，本地预览 |
| [03 配置与主题](tutorials/hugo-blog/03-配置与主题.md) | PaperMod、菜单、社交图标 |
| [04 写第一篇文章](tutorials/hugo-blog/04-写第一篇文章.md) | front matter、Markdown、图片 |
| [05 自定义样式](tutorials/hugo-blog/05-自定义样式.md) | CSS 覆盖、模板覆盖 |
| [06 部署到 GitHub Pages](tutorials/hugo-blog/06-部署到GitHub-Pages.md) | Actions 自动部署 |
| [07 绑定域名与 HTTPS](tutorials/hugo-blog/07-绑定域名与HTTPS.md) | DNS、证书 |
| [08 日常维护与排错](tutorials/hugo-blog/08-日常维护与排错.md) | 命令、报错对照表 |
| [09 进阶玩法](tutorials/hugo-blog/09-进阶玩法.md) | 评论、统计、搜索 |
| [速查表](tutorials/hugo-blog/cheatsheet.md) | 命令速查 |

[`tutorials/hugo-blog/examples/`](tutorials/hugo-blog/examples/) 里是可直接复制的配置文件：
`hugo.toml`、`custom.css`、部署工作流、文章模板等。

## 本站技术栈

| 部分 | 用了什么 |
| --- | --- |
| 静态生成 | Hugo 0.169.0 extended |
| 主题 | PaperMod（vendored，非 submodule） |
| 部署 | GitHub Actions + `actions/deploy-pages` |
| 域名 | `dlcnatsuki.top`（自定义 A 记录） |
| 自定义 | 抽屉式导航、标题头像、自定义 CSS |

## 本地预览

```bash
git clone https://github.com/DLCNatsuki/DLCNatsuki.github.io.git
cd DLCNatsuki.github.io
hugo server -D
```

打开 <http://localhost:1313>。

## 目录

```
content/      文章（posts/、games.md 等）
layouts/      覆盖主题的模板
assets/       CSS、图片源文件
static/       原样发布的文件（图片、游戏）
themes/       PaperMod
tutorials/    ★ 教程（不影响站点构建）
.github/      自动部署工作流
```

## 更新与发布

```bash
git add .
git commit -m "更新内容"
git pull --rebase origin main
git push
```

推送后 GitHub Actions 自动构建，约 30 秒后线上生效。

## 许可

- 博客文章：CC BY-NC-SA 4.0
- 代码与教程：MIT
