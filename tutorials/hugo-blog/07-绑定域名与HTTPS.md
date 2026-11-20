# 07 绑定自定义域名与 HTTPS

> 目标：用 `https://你的域名.com` 访问博客，而不是 `xxx.github.io`。

---

## 一、先买域名

| 平台 | 特点 |
| --- | --- |
| 阿里云 / 腾讯云 | 国内备案方便，`.top`/`.cn` 便宜 |
| Cloudflare | 便宜、DNS 好用、免备案（境外） |
| Namecheap / Porkbun | 境外，价格透明 |

**`.com` 约 60~80 元/年，`.top` 首年常 10 元以内。**

⚠️ 用国内服务器/备案的话，域名需要实名认证；GitHub Pages 在境外，**不需要备案**。

---

## 二、配置 DNS 解析

在域名服务商的 DNS 管理里添加：

### A 记录（4 条，指向 GitHub Pages）

| 类型 | 主机记录 | 记录值 |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

> 4 条都要加，这是 GitHub 的官方 IP，提供冗余。

### CNAME 记录（可选，让 `www` 也能访问）

| 类型 | 主机记录 | 记录值 |
| --- | --- | --- |
| CNAME | `www` | `你的用户名.github.io` |

---

## 三、仓库里配置域名

1. 仓库 → **Settings** → **Pages**
2. **Custom domain** 填：`你的域名.com`
3. 点 **Save**

保存后，GitHub 会自动在仓库根目录生成一个 `CNAME` 文件，内容是域名。

> **别手动删这个文件**，删了自定义域名就失效。

---

## 四、等待 DNS 生效

| 时间 | 说明 |
| --- | --- |
| 几分钟~几小时 | 正常 |
| 最长 24~48 小时 | 换了 DNS 服务商时 |

查询进度：

```bash
nslookup 你的域名.com
```

期望看到 `185.199.108.153` 等地址。

在线工具：<https://dnschecker.org>（全球节点查询）。

---

## 五、开启 HTTPS

DNS 生效、Pages 显示 "DNS check successful" 后：

1. Settings → Pages → 勾选 **Enforce HTTPS**
2. 等几分钟（GitHub 自动签发 Let's Encrypt 证书）

> 如果复选框是灰的，说明证书还在签发或 DNS 没完全生效，等一会儿刷新。

---

## 六、常见问题

| 问题 | 原因 | 解决 |
| --- | --- | --- |
| **DNS check unsuccessful** | 记录没加对，或还没生效 | 检查 A 记录，等 TTL |
| **证书一直不签发** | 有 CNAME 冲突，或域名解析到别处 | 删掉多余的 A/CNAME |
| **www 打不开** | 没加 CNAME | 加 `www` → `用户名.github.io` |
| **HTTPS 报证书错误** | 还在签发中 | 等 15 分钟，别急 |
| **改完域名旧地址 404** | 正常 | `github.io` 地址仍可用 |
| **国内访问慢** | GitHub Pages 在境外 | 正常现象，可用 CDN 加速（见 09 章） |

---

## 七、验证清单

```
□ nslookup 能解析到 185.199.x.153
□ Settings → Pages 显示 DNS check successful
□ https://你的域名.com 能打开
□ 证书有效（浏览器没有警告）
□ Enforce HTTPS 已勾选
□ http 自动跳转 https
□ www 子域名也能访问（如果配了）
```

---

## 八、进阶：用 Cloudflare 托管 DNS

好处：解析快、可加 CDN、免费 SSL。

1. 在 Cloudflare 添加站点，按提示把域名的 NS 改成 Cloudflare 的
2. 在 Cloudflare DNS 里加同样的 4 条 A 记录
3. **代理状态先关（灰云）**，等 GitHub 签发证书成功后再开（橙云）
   - 先开橙云容易导致证书验证失败

---

## 下一步

日常维护：👉 [08 日常维护与排错](08-日常维护与排错.md)
