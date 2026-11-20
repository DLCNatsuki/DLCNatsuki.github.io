# 06 部署到 GitHub Pages

> 目标：`git push` 之后，网站自动上线到 `https://你的用户名.github.io`。

---

## 一、创建仓库

1. 打开 <https://github.com/new>
2. **Repository name 必须是**：

   ```
   你的用户名.github.io
   ```

   例如用户名是 `alice`，仓库就叫 `alice.github.io`。

   > 只有这个特殊名字，GitHub 才会把它当个人主页，地址才是 `https://alice.github.io`。
   > 叫别的名字也能用，但地址会变成 `https://alice.github.io/仓库名/`。

3. 选 **Public**（Private 也能用 Pages，但需要付费账号）
4. **不要**勾选 README / .gitignore / license（本地已经有仓库了）
5. 创建

---

## 二、添加部署工作流

在项目里创建 `.github/workflows/hugo.yaml`：

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.169.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
        run: |
          hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

> **`HUGO_VERSION` 要和本地一致**，否则可能出现"本地正常、线上报错"。

---

## 三、开启 Pages（关键一步）

**很多人卡在这里**：不设置的话，GitHub 会用旧的 Jekyll 构建，结果是 404。

1. 仓库 → **Settings** → 左侧 **Pages**
2. **Build and deployment** → **Source** 选 **GitHub Actions**
   （不要选 "Deploy from a branch"）
3. 保存

---

## 四、推送代码

```bash
git add .
git commit -m "初始化博客"
git branch -M main
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
git push -u origin main
```

### 认证方式

| 方式 | 说明 |
| --- | --- |
| **HTTPS + PAT** | 密码位置填 Personal Access Token（不是登录密码） |
| SSH | 配置密钥后 `git@github.com:用户名/仓库.git` |

**生成 PAT**：GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token，勾选 `repo` 和 `workflow`。

> ⚠️ **`workflow` 权限必须勾**，否则推送含 `.github/workflows/` 的提交会被拒绝。

---

## 五、看部署状态

1. 仓库 → **Actions** 标签
2. 能看到 `Deploy Hugo site to Pages` 正在跑
3. 绿勾 = 成功，红叉 = 失败（点进去看日志）

成功后访问：

```
https://你的用户名.github.io
```

---

## 六、后续更新流程

```bash
# 改了文章或配置后
git add .
git commit -m "新增文章：xxx"
git push

# 30 秒后自动重新部署
```

**建议习惯**：push 前先 `git pull --rebase origin main`，避免冲突（尤其你在网页上也改过文件时）。

---

## 七、验证

```
□ 仓库 Settings → Pages → Source 是 GitHub Actions
□ Actions 里最新一次运行是绿色
□ 打开 https://用户名.github.io 能看到首页
□ 点进一篇文章，样式正常
□ 再 push 一次，能自动重新部署
```

---

## 常见错误

| 现象 | 原因 | 解决 |
| --- | --- | --- |
| 访问 404 | Pages Source 没设成 Actions | 见第三节 |
| Actions 红叉：`workflow` 权限 | PAT 缺 scope | 重新生成勾 `workflow` |
| `! [rejected] main -> main` | 远端有你本地没有的提交 | `git pull --rebase origin main` |
| 样式丢失 | `baseURL` 不对 | 用 `--baseURL` 参数或改配置 |
| 图片 404 | 图片没提交 | 确认 `static/` 进了 git |
| 部署成功但页面很旧 | 浏览器缓存 | `Ctrl+F5` |
| Actions 报 `hugo: not found` | 版本号写错 | 检查 `HUGO_VERSION` |

---

## 下一步

绑域名：👉 [07 绑定域名与 HTTPS](07-绑定域名与HTTPS.md)
