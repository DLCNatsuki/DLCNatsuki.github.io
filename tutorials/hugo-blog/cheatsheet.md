# 命令速查表

> 打印出来贴显示器旁边。

---

## 建站

```bash
hugo new site myblog          # 新建站点
hugo new theme mytheme        # 新建主题（一般不用）
hugo new content posts/a.md   # 新建文章
```

---

## 本地预览

```bash
hugo server                   # 默认 http://localhost:1313
hugo server -D                # 包含草稿
hugo server --port 8080       # 换端口
hugo server --bind 0.0.0.0    # 局域网可访问
hugo server --disableFastRender  # 关快速渲染（排查样式问题）
```

`Ctrl + C` 停止。

---

## 构建

```bash
hugo                          # 输出到 public/
hugo --minify                 # 压缩
hugo -d docs                  # 输出到指定目录
hugo --cleanDestinationDir    # 先清空再构建
```

---

## 内容管理

```bash
hugo list all                 # 列出所有文章
hugo list drafts              # 列出草稿
hugo list future              # 列出未来日期的文章
hugo list expired             # 列出过期的文章

hugo new content posts/x.md --kind post   # 用指定模板
```

---

## Git 日常

```bash
git status                    # 看状态
git add .                     # 暂存全部
git add 文件                  # 暂存单个
git commit -m "说明"          # 提交
git push                      # 推送
git pull --rebase origin main # 拉取并变基（推荐）
git log --oneline -10         # 最近 10 次提交
git diff                      # 看未暂存的改动
```

---

## Git 救急

```bash
git restore 文件              # 撤销工作区改动
git restore --staged 文件     # 取消暂存
git reset --hard HEAD         # 丢弃所有未提交改动（危险）
git reset --soft HEAD~1       # 撤销上次提交，保留改动
git checkout 提交哈希 -- 文件  # 恢复文件到某版本
git stash                     # 临时保存改动
git stash pop                 # 恢复
```

---

## 主题

```bash
# 安装（submodule）
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod

# 更新
git submodule update --remote --merge

# 克隆带 submodule 的仓库
git clone --recursive 仓库地址
git submodule update --init --recursive
```

---

## 配置片段

### 基础

```toml
baseURL = 'https://example.com/'
title = '站点名'
theme = 'PaperMod'
defaultContentLanguage = 'zh'
```

### 首页信息

```toml
[params.homeInfoParams]
  Title = '你好，我是 XXX'
  Content = '简介文字'
```

### 菜单

```toml
[[menu.main]]
  identifier = 'posts'
  name = '文章'
  url = '/posts/'
  weight = 10
```

### 社交图标

```toml
[[params.socialIcons]]
  name = 'github'
  url = 'https://github.com/用户名'

[[params.socialIcons]]
  name = 'mail'
  url = 'mailto:a@b.com'
```

### 搜索（必须）

```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]
```

---

## Front matter 模板

```toml
+++
title = '文章标题'
date = 2026-11-20T10:00:00+08:00
draft = false
tags = ['标签1', '标签2']
categories = ['分类']
summary = '一句话摘要'
ShowToc = true
slug = 'custom-url'

[cover]
  image = 'images/cover.jpg'
  alt = '封面说明'
+++
```

---

## 目录约定

| 路径 | 放什么 |
| --- | --- |
| `content/` | 文章 |
| `content/posts/` | 博客文章 |
| `static/` | 原样复制的文件（图片、favicon） |
| `static/images/` | 图片 |
| `assets/` | 需要 Hugo 处理的资源 |
| `assets/css/extended/` | **自定义 CSS**（自动加载） |
| `layouts/` | 覆盖主题的模板 |
| `themes/` | 主题 |
| `public/` | 构建产物（**不提交**） |
| `resources/` | 缓存（**不提交**） |

---

## 部署检查

```bash
# 推送前
git pull --rebase origin main
hugo --minify          # 本地构建一遍，确认无报错
git status             # 确认没有 public/ 等不该提交的
git add -A
git commit -m "更新"
git push
```

---

## 常用在线工具

| 工具 | 用途 |
| --- | --- |
| <https://giscus.app/zh-CN> | 生成评论配置 |
| <https://dnschecker.org> | 检查 DNS 全球生效 |
| <https://squoosh.app/> | 图片压缩 |
| <https://carbon.now.sh> | 代码截图美化 |
| <https://www.tablesgenerator.com/markdown_tables> | 生成 Markdown 表格 |
| <https://pandoc.org/try/> | 格式转换 |
