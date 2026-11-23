# 工程师成长手册｜GitHub Pages + MkDocs Material

这是一个可持续维护的个人工程知识库。它不是课程清单，也不是聊天记录归档，而是把已经讨论清楚的成长目标、工程能力模型、AI 协作原则和真实项目训练方法整理成可以持续迭代的 Wiki。

## 这个知识库的核心共识

- 不和 AI 比谁写代码更快；重点是形成独立的工程判断力。
- 核心能力包括：代码理解与构建、软件设计与抽象、问题分析与 Debug、系统运行与工程质量。
- 不按“先学完一堆知识点，再开始做项目”的方式机械推进。
- 以一个有真实代码结构、值得长期研究的软件项目作为训练场，通过理解、设计、修改、验证、诊断和复盘逐步成长。
- AI 可以参与解释、讨论、实现和测试，但关键的问题定义、技术判断、证据评估和结果验收需要由自己掌握。

## 本地预览

要求 Python 3.11 或更新版本（`mkdocs-material==9.8.2` 的硬性要求）。

> 先确认 `python3 --version`：低于 3.11 时装依赖会报 `No matching distribution found for mkdocs-material`（这不是依赖坏了，是版本不够）。
> 这种情况下换一个 3.11+ 的解释器即可，例如：
>
> ```bash
> pip install uv          # 或 brew install uv
> uv venv --python 3.12 .venv
> uv pip install -r requirements.txt
> ```

```bash
# 进入项目目录
cd engineering-growth-wiki

# 创建虚拟环境
python -m venv .venv

# macOS / Linux
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1

# 安装依赖
python -m pip install -r requirements.txt

# 启动本地预览
mkdocs serve
```

打开终端提示的本地地址，通常是 `http://127.0.0.1:8000/`。

正式构建：

```bash
mkdocs build --strict
```

生成的网站在 `site/` 目录中。

## 发布到 GitHub Pages

详细步骤（含本机 GitHub 认证、常见问题）见 [PUBLISH.md](PUBLISH.md)。

1. 在 GitHub 新建一个仓库，例如 `engineering-growth-wiki`。
2. 将本项目全部文件上传到仓库根目录，默认分支使用 `main`。
3. 打开仓库的 **Settings → Pages**。
4. 在 **Build and deployment → Source** 中选择 **GitHub Actions**。
5. 推送到 `main` 后，打开 **Actions**，查看 `Deploy documentation to GitHub Pages` 工作流。
6. 工作流成功后，在 **Settings → Pages** 中查看网站地址。

之后只要修改 `docs/` 下的 Markdown 并推送到 `main`，网站就会自动重新构建和发布。

## 如何维护内容

- 新增页面：在 `docs/` 下相应目录创建 Markdown 文件，并在 `mkdocs.yml` 的 `nav` 中登记。
- 修改页面：直接编辑对应的 `.md` 文件。
- 调整目录：修改 `mkdocs.yml` 中的 `nav`。
- 调整外观：主要修改 `mkdocs.yml` 和 `docs/stylesheets/extra.css`。
- 建议每篇文章只解决一个主题，通过相对链接连接相关页面。

## 隐私提醒

GitHub Pages 发布的网站是公开可访问的。不要提交公司内部代码、真实日志、内部接口地址、访问令牌、账号信息、未脱敏的业务数据或其他不适合公开的内容。即使仓库设置为 Private，也应把最终发布的网站按公开内容管理。

## 关于 MkDocs Material 的维护周期

本项目使用 **MkDocs Material** 构建。官方已宣布其进入维护模式：到 **2027 年 5 月 5 日** 为止只提供关键修复与安全更新，后续方向是 Zensical（不强制迁移）。当前文章尽量使用标准 Markdown，主题相关配置集中在 `mkdocs.yml`，以便未来迁移时保留知识内容。详见[主题与迁移说明](docs/06-维护与发布/主题与迁移说明.md)。

## 目录结构

```text
engineering-growth-wiki/
├── .github/workflows/deploy.yml
├── docs/
│   ├── index.md
│   ├── 01-成长方向/
│   ├── 02-工程能力/
│   ├── 03-AI时代/
│   ├── 04-工程训练/
│   ├── 05-实践模板/
│   └── 06-维护与发布/
├── mkdocs.yml
├── requirements.txt
├── PUBLISH.md            # 发布到 GitHub Pages 的详细步骤
└── README.md
```
