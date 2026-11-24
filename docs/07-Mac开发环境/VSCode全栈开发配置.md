# VS Code 全栈开发配置指南

> 适用环境：Apple Silicon Mac｜全栈开发｜免费优先
> 目标：先建立稳定的编辑器基础，再根据项目技术栈选择扩展，避免插件堆积和功能重复。

## 1. 配置方式：先选基础，再按需叠加

不建议一次性安装所有扩展。推荐采用「基础配置 + 技术栈配置 + 工作流配置」的方式：

| 配置层 | 解决的问题 | 建议 |
|---|---|---|
| 基础配置 | 编辑体验、格式化、代码提示、Git | 所有人启用 |
| 前端配置 | HTML、CSS、React、Vue、Tailwind | 做前端时启用 |
| 后端配置 | Python、API 调试、Docker | 做后端时启用 |
| GitHub / 文档配置 | PR、Actions、Markdown、YAML | 经常维护仓库和文档时启用 |
| AI 编程配置 | AI 代码补全、代理式编码 | 按现有工具选择，不要重复安装 |

**推荐默认组合：** 基础配置 + GitHub / 文档配置 + 自己当前项目所需的语言扩展。全栈开发不等于每个插件都要安装。

## 2. 扩展清单

### 2.1 基础必备

| 扩展 | 扩展 ID | 用途 |
|---|---|---|
| Prettier | `esbenp.prettier-vscode` | 统一代码格式 |
| ESLint | `dbaeumer.vscode-eslint` | JavaScript / TypeScript 代码检查 |
| GitLens | `eamodio.gitlens` | 查看代码作者、提交历史和变更 |
| Error Lens | `usernamehw.errorlens` | 在代码行内显示错误和警告 |
| EditorConfig | `editorconfig.editorconfig` | 统一缩进、换行等编辑器规则 |
| Path Intellisense | `christian-kohler.path-intellisense` | 文件路径自动补全 |

### 2.2 前端开发（按项目选择）

| 扩展 | 扩展 ID | 适用场景 |
|---|---|---|
| Auto Rename Tag | `formulahendry.auto-rename-tag` | HTML / JSX 标签联动改名 |
| Tailwind CSS IntelliSense | `bradlc.vscode-tailwindcss` | 使用 Tailwind CSS |
| ES7+ React/Redux/React-Native snippets | `dsznajder.es7-react-js-snippets` | React 代码片段 |
| Vue - Official | `Vue.volar` | 使用 Vue 3 |

React 和 Vue 扩展按项目选择；不使用对应框架时无需安装。

### 2.3 后端开发（按项目选择）

| 扩展 | 扩展 ID | 适用场景 |
|---|---|---|
| Python | `ms-python.python` | Python 语言支持、调试 |
| Pylance | `ms-python.vscode-pylance` | Python 类型分析和智能提示 |
| Ruff | `charliermarsh.ruff` | Python lint 与格式化 |
| Docker | `ms-azuretools.vscode-docker` | Dockerfile、镜像和容器管理 |
| REST Client | `humao.rest-client` | 在编辑器中发送 HTTP 请求 |

Python 项目建议优先采用 Ruff 统一 lint / format；不要同时配置多个工具争抢格式化职责。

### 2.4 GitHub、配置文件与知识库

| 扩展 | 扩展 ID | 用途 |
|---|---|---|
| GitHub Pull Requests | `GitHub.vscode-pull-request-github` | 在 VS Code 中查看和处理 PR |
| GitHub Actions | `github.vscode-github-actions` | 查看 Actions 工作流 |
| Markdown All in One | `yzhang.markdown-all-in-one` | Markdown 编辑增强 |
| markdownlint | `DavidAnson.vscode-markdownlint` | Markdown 规范检查 |
| YAML | `redhat.vscode-yaml` | YAML 语法、校验和补全 |

维护 MkDocs / GitHub Pages 知识库时，建议安装 Markdown All in One、markdownlint 和 YAML。

## 3. 一键安装：推荐基础组合

先在 VS Code 中安装并启用命令行工具：

1. 打开 VS Code。
2. 按 `⌘ + ⇧ + P` 打开命令面板。
3. 搜索并执行 `Shell Command: Install 'code' command in PATH`。
4. 重新打开终端，执行 `code --version` 验证。

安装基础扩展：

```bash
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension eamodio.gitlens
code --install-extension usernamehw.errorlens
code --install-extension editorconfig.editorconfig
code --install-extension christian-kohler.path-intellisense
```

如果你正在维护 GitHub 仓库和 Markdown 文档，再安装：

```bash
code --install-extension GitHub.vscode-pull-request-github
code --install-extension github.vscode-github-actions
code --install-extension yzhang.markdown-all-in-one
code --install-extension DavidAnson.vscode-markdownlint
code --install-extension redhat.vscode-yaml
```

前端项目可按需安装：

```bash
code --install-extension formulahendry.auto-rename-tag
code --install-extension bradlc.vscode-tailwindcss
code --install-extension dsznajder.es7-react-js-snippets
```

Python / 后端项目可按需安装：

```bash
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension charliermarsh.ruff
code --install-extension ms-azuretools.vscode-docker
code --install-extension humao.rest-client
```

查看已安装扩展：

```bash
code --list-extensions
```

卸载扩展示例：

```bash
code --uninstall-extension publisher.extension-name
```

## 4. 基础 settings.json

打开命令面板，执行 `Preferences: Open User Settings (JSON)`，可先使用以下配置：

```json
{
  "editor.fontSize": 14,
  "editor.fontFamily": "JetBrainsMono Nerd Font",
  "editor.fontLigatures": true,
  "editor.minimap.enabled": false,
  "editor.wordWrap": "on",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.formatOnSave": true,
  "editor.renderWhitespace": "selection",
  "files.autoSave": "onFocusChange",
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "explorer.confirmDelete": false,
  "workbench.startupEditor": "none",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "git.autofetch": true
}
```

说明：

- 如果字体显示异常，将 `editor.fontFamily` 改成 `JetBrains Mono`，或换成已安装的字体。
- 如果不喜欢自动保存，将 `files.autoSave` 改成 `off`。
- 如果项目使用 4 空格缩进，应以项目规范为准，不要强行统一成 2 空格。
- `formatOnSave` 只是开启保存时格式化；还需要为对应语言选择默认格式化工具。

## 5. 格式化与代码检查：避免互相冲突

建议将 Prettier 用于 JS / TS / HTML / CSS / JSON 等格式化，将 ESLint 用于 JS / TS 代码质量检查。不要让多个格式化工具同时处理同一种语言。

可在项目根目录创建 `.vscode/settings.json`，示例：

```json
{
  "editor.formatOnSave": true,
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

这只是项目级示例。团队已有配置（例如 `.prettierrc`、`.editorconfig`、ESLint 配置）时，应优先遵循项目规则。不要把个人机器路径、密钥或私人配置写进项目设置。

## 6. 配置选项：按你的开发内容勾选

可以把下面这份清单当作自己的安装决策表：

- [ ] **基础编辑能力**：Prettier、ESLint、GitLens、Error Lens、EditorConfig、Path Intellisense
- [ ] **React 前端**：Auto Rename Tag、ES7+ React snippets
- [ ] **Vue 前端**：Vue - Official
- [ ] **Tailwind 样式**：Tailwind CSS IntelliSense
- [ ] **Python 后端**：Python、Pylance、Ruff
- [ ] **容器开发**：Docker
- [ ] **接口调试**：REST Client
- [ ] **GitHub 协作**：GitHub Pull Requests、GitHub Actions
- [ ] **Markdown / MkDocs 文档**：Markdown All in One、markdownlint、YAML
- [ ] **AI 辅助编码**：只选择当前实际使用的一套主力工具或扩展

**我的建议起步方案：** 先装基础 6 个，再加 GitHub / 文档 5 个。前端框架、Python、Docker 和 API 工具等到项目确实用到时再装。

## 7. AI 编程工具如何选择

AI 工具的形态和能力变化较快，建议把「编辑器扩展」和「独立编程代理」分开考虑：

- 如果主要使用 Codex 桌面端或 CLI，不必为了追求插件数量再安装多个同类 AI 扩展。
- 如果希望在编辑器里获得补全或对话体验，再根据实际使用的服务选择扩展。
- 同时运行多个会改写代码的 AI 代理时，要明确各自负责的文件和任务，避免并发修改冲突。
- 提交前检查 diff、运行测试，并确认没有把密钥、个人数据或不应上传的代码发给第三方服务。

## 8. 日常快捷键

| 快捷键 | 功能 |
|---|---|
| `⌘ + P` | 快速打开文件 |
| `⌘ + ⇧ + P` | 打开命令面板 |
| `⌘ + B` | 显示 / 隐藏侧边栏 |
| `⌘ + ⇧ + F` | 全局搜索 |
| `⌘ + ⇧ + E` | 聚焦文件资源管理器 |
| `⌘ + ` ` | 打开 / 关闭集成终端 |
| `F12` | 跳转到定义 |
| `⌥ + F12` | 查看定义预览 |

## 9. 推荐落地顺序

1. 安装基础 6 个扩展。
2. 配置基础 `settings.json`。
3. 在当前项目中确认格式化工具和 ESLint 规则。
4. 按项目技术栈增加 React / Vue / Python / Docker 等扩展。
5. 如果维护 GitHub Pages / MkDocs，再安装文档相关扩展。
6. 使用一周后，卸载没有实际使用价值的扩展。

**原则：** VS Code 的目标不是插件越多越好，而是打开项目后能可靠地阅读、编辑、检查、调试和提交代码。
