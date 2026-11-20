+++
title = 'Hello World：我的第一篇文章'
date = 2026-11-20T10:00:00+08:00
draft = false
tags = ['随笔', 'Hugo']
categories = ['记录']
summary = '记录一下博客搭起来的过程。'
ShowToc = true

[cover]
  image = 'images/hello.jpg'
  alt = 'Hello World'
+++

这是一篇示例文章，用来演示各种 Markdown 语法。

## 文字格式

**加粗**、*斜体*、~~删除线~~、`行内代码`。

## 列表

- 第一项
- 第二项
  - 嵌套项

1. 有序第一
2. 有序第二

## 引用

> 引用一段话。
> 可以换行。

## 代码

```python
def hello(name: str) -> str:
    return f"Hello, {name}"

print(hello("World"))
```

```bash
hugo server -D
```

## 表格

| 项目 | 说明 |
| --- | --- |
| Hugo | 静态网站生成器 |
| PaperMod | 主题 |
| GitHub Pages | 免费托管 |

## 图片

![示例图片](/images/hello.jpg)

## 链接

[Hugo 官网](https://gohugo.io/)

---

以上就是全部常用语法。
