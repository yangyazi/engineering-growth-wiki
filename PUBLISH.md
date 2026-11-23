# 发布到 GitHub Pages

> **当前状态：已上线** → https://yangyazi.github.io/engineering-growth-wiki/
> 仓库：https://github.com/yangyazi/engineering-growth-wiki （Public，Pages 源 = GitHub Actions）
> 日常只需改 `docs/` 下的文件并 `git push`，Actions 会自动重新构建发布（约 40 秒）。


已经完成的部分：依赖装在项目内的 `.venv/`（Python 3.12 + MkDocs 1.6.1 + Material 9.8.2），`mkdocs build --strict` 构建通过，并且验证过站点放在子路径 `/engineering-growth-wiki/` 下时样式、脚本和搜索都能正常加载。仓库已在本地初始化并提交到 `main`，剩下两步：**推送到 GitHub**、**在仓库里打开 Pages**。

---

## 第 1 步：让本机能推 GitHub

先检查：

```bash
ssh -T git@github.com
```

出现 `Hi <你的用户名>! You've successfully authenticated` 说明已配好，跳到第 2 步；如果返回 `Permission denied (publickey)`，二选一：

### 方式 A：SSH Key（推荐，一次配置长期可用）

```bash
# 1. 复制公钥（已有 ~/.ssh/id_ed25519.pub 时直接用；没有就先 ssh-keygen -t ed25519）
cat ~/.ssh/id_ed25519.pub | pbcopy

# 2. 打开 https://github.com/settings/keys → New SSH key
#    Title 随意（例如 macbook），Key 粘贴刚复制的内容，保存

# 3. 再验证一次
ssh -T git@github.com
```

### 方式 B：HTTPS + Personal Access Token

GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)，勾选 `repo` 权限，生成后复制（只显示一次）。推送时用户名填 GitHub 用户名，密码处粘贴 token。

---

## 第 2 步：建仓库并推送

1. 打开 https://github.com/new
2. Repository name 填 `engineering-growth-wiki`
3. 可见性选 **Public**（GitHub Free 账号的 Pages 只支持 Public 仓库）
4. **不要**勾选 "Add a README / .gitignore / license"（会与本地提交冲突）
5. 创建后回到终端：

```bash
cd engineering-growth-wiki

# SSH
git remote add origin git@github.com:<你的用户名>/engineering-growth-wiki.git

# 或 HTTPS
# git remote add origin https://github.com/<你的用户名>/engineering-growth-wiki.git

git push -u origin main
```

---

## 第 3 步：打开 Pages

1. 仓库页 → **Settings** → 左侧 **Pages**
2. **Build and deployment → Source** 选择 **GitHub Actions**
3. 打开 **Actions** 标签，看 `Deploy documentation to GitHub Pages` 这次运行
4. 绿色对勾出现后，站点地址是：

```text
https://<你的用户名>.github.io/engineering-growth-wiki/
```

首次部署通常 1～2 分钟内完成。

---

## 第 4 步（建议）：补上 site_url

仓库地址确定后，把 `mkdocs.yml` 顶部注释里的示例改成真实值：

```yaml
site_url: https://<你的用户名>.github.io/engineering-growth-wiki/
```

作用：生成正确的 `sitemap.xml`、canonical 链接和社交分享卡片。不填也能正常访问——没有 `site_url` 时 MkDocs 生成相对链接，因此站点放在任意子路径下都能跑（已验证），代价是 sitemap 为空。

---

## 日常使用

```bash
cd engineering-growth-wiki

.venv/bin/mkdocs serve            # 本地预览 http://127.0.0.1:8000/
.venv/bin/mkdocs build --strict   # 构建检查，与 CI 完全一致
git add -A && git commit -m "补充 xxx" && git push    # 推送后自动重新发布
```

`strict: true` 的含义：任何失效的内部链接、未在 `nav` 登记的页面都会让构建直接失败——故意这样设置，防止发布半成品页面。

---

## 备选方案：不用 Actions，一条命令发布

```bash
.venv/bin/mkdocs gh-deploy --clean
```

构建结果会推到 `gh-pages` 分支，然后在 **Settings → Pages → Source** 选择 **Deploy from a branch**，分支 `gh-pages`、目录 `/ (root)`。不依赖 CI，但每次更新都要在本地手动执行。

---

## 常见问题

**Q：为什么站点地址带 `/engineering-growth-wiki/` 这一层？**
GitHub Pages 的项目站点规则是「仓库名即路径」。当前未设置 `site_url`，MkDocs 生成相对链接，所以放在任意子路径下都能正常工作。若以后绑定自定义域名或改用 `用户名.github.io` 仓库，再补 `site_url` 即可。

**Q：中文文件名会不会出问题？**
页面地址会被编码成 `%E5%B7%A5%E7%A8%8B...`，功能正常，只是地址栏不好看。介意的话把目录改成英文名，同时修改 `mkdocs.yml` 的 `nav` 和正文里的相对链接。

**Q：Material 2027 年停止维护怎么办？**
内容全部是标准 Markdown，迁移成本集中在 `mkdocs.yml` 的主题配置。将来换 Zensical 或其他生成器时，`docs/` 基本可以原样搬过去。详见站内「维护与发布 → 主题与迁移说明」。

**Q：为什么本机用系统自带的 python3 装不上依赖？**
`mkdocs-material` 9.8.x 要求 Python ≥ 3.11，若系统 `python3` 低于该版本就会报 `No matching distribution found`。换 3.11+ 的解释器创建虚拟环境即可（仓库里已有可用的 `.venv/`，它不会进 Git）。

---

## 自定义域名的一个坑（已经踩过一次）

`yangyazi.github.io` 名下如果存在用户站点仓库（本账号是 `yangyazi/yangyazi.github.io`，2024 年的 Hexo 博客），
并且那个仓库绑定了自定义域名（当时是 `CNAME` 文件里的 `younglo.love`），那么
**该用户名下所有项目站点也会被 301 重定向到那个自定义域名**。

如果那个域名没有解析（`dig younglo.love` 为空），整站就会打不开——2026-11-23 上线当天就是这样。

处理方式：删掉 `yangyazi/yangyazi.github.io` 仓库里的 `CNAME` 文件，并在
`Settings → Pages → Custom domain` 里清空域名。改完后 CDN 边缘缓存可能还要几分钟才过期。

以后如果真的要绑自己的域名：

1. DNS 加 `A` 记录指向 `185.199.108.153` / `.109.153` / `.110.153` / `.111.153`；
2. `www` 加 `CNAME` 指向 `yangyazi.github.io`；
3. 在 Pages 设置里填域名，等证书签发完再勾选 **Enforce HTTPS**。

注意：如果以后再用 Hexo 重新部署那个老博客，`hexo deploy` 可能会把 `CNAME` 文件写回来，
届时本项目会被再次重定向，记得检查。
