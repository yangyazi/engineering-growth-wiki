# Mac 全栈开发者生产力工具配置指南

> 适用环境：Apple Silicon（M 系列）｜macOS Sequoia 15｜全栈开发｜免费优先  
> 目标：建立一套键盘优先、稳定、可迁移，并适合现代 AI 编程工作流的 Mac 开发环境。

## 1. 配置原则

1. **键盘优先**：高频操作尽量通过快捷键完成。
2. **免费优先**：优先选择免费、开源、维护活跃的工具。
3. **避免重复**：同一类功能只保留一个主力工具。
4. **渐进配置**：先装基础工具，再按实际需求扩展。
5. **配置可迁移**：用 Homebrew、配置文件和 Git 管理环境。

## 2. 推荐工具总览

| 工具 | 用途 | 费用与建议 |
|---|---|---|
| Homebrew | macOS 包管理器 | 免费，必装 |
| iTerm2 | 终端模拟器 | 免费，推荐 |
| Oh My Zsh | Zsh 配置框架 | 免费，按需 |
| fnm | Node.js 版本管理 | 免费，推荐 |
| uv | Python 版本与项目环境管理 | 免费，推荐 |
| pnpm | JavaScript 包管理 | 免费，推荐 |
| fzf / zoxide | 模糊搜索、智能目录跳转 | 免费，推荐 |
| ripgrep / bat / eza / jq | 搜索与终端效率 | 免费，推荐 |
| lazygit | 终端 Git 界面 | 免费，推荐 |
| Maccy | 剪切板历史 | 免费、开源，推荐 |
| Rectangle | 窗口布局管理 | 免费、开源，推荐 |
| AltTab | 按窗口切换应用 | 免费、开源，按需 |
| Shottr | 截图、标注、OCR | 有免费使用方式，按需 |
| VS Code | 代码编辑器 | 免费，推荐 |
| OrbStack | Docker / Linux 环境 | 个人使用有免费方案，按需 |
| AppCleaner | 卸载应用及相关文件 | 免费，按需 |

**避免同时安装重复工具：**

- iTerm2 与 Ghostty：先选一个主力终端。
- Maccy 与 Raycast Clipboard：先用 Maccy；以后选择 Raycast 时再评估是否替换。
- Docker Desktop 与 OrbStack：保留一个 Docker 主力环境。
- Rectangle 与其他窗口管理工具：保留一个主力工具。

## 3. 安装顺序

### 3.1 安装 Homebrew

官网：https://brew.sh/

\`\`\`bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
\`\`\`

Apple Silicon 默认安装目录为 \`/opt/homebrew\`。安装结束后按安装程序提示配置 shell 环境，通常可以执行：

\`\`\`bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
brew --version
brew doctor
\`\`\`

### 3.2 安装开发基础工具

\`\`\`bash
brew install git fnm uv pnpm gh fzf zoxide ripgrep bat eza jq lazygit
\`\`\`

- \`fnm\`：管理多个 Node.js 版本。
- \`uv\`：管理 Python 版本、虚拟环境和依赖。
- \`pnpm\`：管理 JavaScript / TypeScript 项目依赖。
- \`gh\`：GitHub CLI。
- \`fzf\`：模糊查找文件、历史命令等。
- \`zoxide\`：根据访问历史快速跳转目录。
- \`ripgrep\`：快速搜索代码和文本。
- \`bat\`、\`eza\`、\`jq\`：增强文件查看、目录列表和 JSON 处理。
- \`lazygit\`：终端内可视化 Git 操作。

### 3.3 安装 Mac 图形应用

\`\`\`bash
brew install --cask iterm2 rectangle alt-tab shottr appcleaner font-jetbrains-mono-nerd-font
\`\`\`

Maccy 官网：https://maccy.app/  
OrbStack 官网：https://orbstack.dev/  
如需 Docker 环境再安装 OrbStack；如果 Docker Desktop 已经稳定可用，不需要迁移。

### 3.4 检查安装结果

\`\`\`bash
brew list
brew list --cask
git --version
fnm --version
uv --version
pnpm --version
fzf --version
\`\`\`

## 4. iTerm2 终端配置

官网：https://iterm2.com/

### 4.1 外观建议

在 \`iTerm2 → Settings → Profiles → Text\` 中设置：

| 项目 | 建议 |
|---|---|
| 字体 | JetBrainsMono Nerd Font |
| 字号 | 13–14 |
| 光标 | Vertical Bar |
| 主题 | 深色主题 |
| 透明度 | 轻微或关闭 |
| Scrollback | 10,000 行以上 |

字体：https://www.jetbrains.com/lp/mono/

### 4.2 常用快捷键

| 快捷键 | 功能 |
|---|---|
| \`⌘ + T\` | 新建 Tab |
| \`⌘ + W\` | 关闭当前 Tab |
| \`⌘ + D\` | 左右分屏 |
| \`⌘ + ⇧ + D\` | 上下分屏 |
| \`⌘ + ⌥ + ← / →\` | 切换分屏 |
| \`⌘ + 1…9\` | 切换 Tab |
| \`⌘ + F\` | 搜索终端输出 |

建议配置全局呼出终端快捷键，例如 \`⌥ + Space\`：  
\`Settings → Keys → Hotkey → Create a Dedicated Hotkey Window\`。如与其他软件冲突，换成未占用组合键。

### 4.3 安装 Oh My Zsh 与插件

官网：https://ohmyz.sh/

\`\`\`bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-autosuggestions \\
  \${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting \\
  \${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
\`\`\`

编辑 \`~/.zshrc\`，将插件加入列表：

\`\`\`bash
plugins=(
  git
  docker
  npm
  node
  zsh-autosuggestions
  zsh-syntax-highlighting
)
\`\`\`

语法高亮插件建议放在插件列表末尾。然后加入常用配置：

\`\`\`bash
eval "$(fnm env --use-on-cd --shell zsh)"
eval "$(zoxide init zsh)"
source <(fzf --zsh)

alias ll="eza -lah --icons"
alias cat="bat"
alias gs="git status"
alias gp="git pull"
alias lg="lazygit"
\`\`\`

保存后执行 \`source ~/.zshrc\`。如果某个命令尚未安装，先安装对应工具，或暂时删除相应别名。

### 4.4 Shell Integration

在 iTerm2 菜单中选择 \`iTerm2 → Install Shell Integration\`，增强命令边界、工作目录识别和终端历史相关体验。

## 5. Mac 日常效率工具

### 5.1 Maccy：剪切板历史

官网：https://maccy.app/

- 设置全局快捷键，例如 \`⌥ + V\`。
- 历史记录可先设为约 100 条，再按实际需求调整。
- 可开启登录时启动。
- 不要把密码、访问令牌、私钥等敏感内容当作普通剪切板内容长期保存；检查密码管理器的剪切板清理设置。

### 5.2 Rectangle：窗口管理

官网：https://rectangleapp.com/

| 示例快捷键 | 操作 |
|---|---|
| \`⌃ + ⌥ + ←\` | 左半屏 |
| \`⌃ + ⌥ + →\` | 右半屏 |
| \`⌃ + ⌥ + ↑\` | 上半屏 |
| \`⌃ + ⌥ + ↓\` | 下半屏 |
| \`⌃ + ⌥ + Enter\` | 最大化 |

快捷键可自定义；若与系统或其他应用冲突，以 Rectangle 设置页面为准。

### 5.3 AltTab：按窗口切换

官网：https://alt-tab.app/

可将窗口切换设置为 \`⌥ + Tab\`，获得接近 Windows 的按窗口切换体验。若已习惯 macOS 原生 \`⌘ + Tab\`，也可以保留默认操作。

### 5.4 Shottr：截图与标注

官网：https://shottr.cc/

适合 Bug 反馈、界面标注、长截图和 OCR。可保留 macOS 原生截图快捷键，再为 Shottr 设置不冲突的快捷键。

### 5.5 其他小工具

- AppCleaner：https://freemacsoft.net/appcleaner/
- Keka：https://www.keka.io/
- Hidden Bar：https://github.com/dwarvesf/hidden

按需安装即可，不必一次性全部配置。

## 6. 全栈开发环境

### 6.1 Node.js：fnm + pnpm

\`\`\`bash
fnm install 22
fnm default 22
node --version
npm --version
pnpm --version
\`\`\`

Node.js 版本应优先遵循项目中的 \`.nvmrc\`、\`.node-version\`、\`package.json\` 的 \`engines\` 字段或团队规范。上面的 22 仅为示例。

### 6.2 Python：uv

\`\`\`bash
uv python install 3.13
uv venv
source .venv/bin/activate
uv pip install fastapi
\`\`\`

Python 版本应遵循项目的 \`pyproject.toml\` 或团队约定。每个项目尽量使用独立虚拟环境。

### 6.3 Git 与 GitHub CLI

\`\`\`bash
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global fetch.prune true
git config --global core.editor "code --wait"

git config --global user.name "Your Name"
git config --global user.email "your@email.com"

gh auth login
\`\`\`

将示例姓名和邮箱替换成自己的 Git 身份信息。不要把访问令牌写入仓库文件。

### 6.4 Docker：OrbStack（按需）

官网：https://orbstack.dev/

\`\`\`bash
brew install --cask orbstack
\`\`\`

示例 \`compose.yaml\`：

\`\`\`yaml
services:
  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: dev
    ports:
      - "3306:3306"
  redis:
    image: redis:7
    ports:
      - "6379:6379"
\`\`\`

启动和停止：

\`\`\`bash
docker compose up -d
docker compose ps
docker compose down
\`\`\`

示例仅用于本地开发。真实项目应使用安全的密码管理方式，不要将生产密码提交到 Git。

## 7. VS Code 配置

扩展建议：

| 扩展 | 用途 |
|---|---|
| Error Lens | 行内错误提示 |
| GitLens | Git 历史与代码追踪 |
| Prettier | 代码格式化 |
| ESLint | JavaScript / TypeScript 检查 |
| EditorConfig | 编辑器规范 |
| Docker | 容器管理 |
| REST Client | API 请求测试 |
| Todo Tree | TODO / FIXME 管理 |
| Markdown All in One | Markdown 编辑 |

扩展市场：https://marketplace.visualstudio.com/vscode

建议的 \`settings.json\`：

\`\`\`json
{
  "editor.fontSize": 14,
  "editor.fontFamily": "JetBrainsMono Nerd Font",
  "editor.fontLigatures": true,
  "editor.minimap.enabled": false,
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "editor.wordWrap": "on",
  "files.autoSave": "onFocusChange",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "workbench.startupEditor": "none",
  "explorer.confirmDelete": false
}
\`\`\`

如果 Nerd Font 在编辑器中显示异常，可将编辑器字体改为普通 JetBrains Mono；终端继续使用 Nerd Font。项目级格式化规则优先于个人全局设置。

## 8. AI 编程工作流

可关注以下工具：

- OpenAI Codex：https://developers.openai.com/codex/
- Claude Code：https://docs.anthropic.com/en/docs/claude-code/overview
- Continue：https://www.continue.dev/

建议分工：

| 工具 | 适合承担的工作 |
|---|---|
| VS Code | 日常编辑、代码阅读、调试 |
| iTerm2 | 启动服务、运行测试、Git 操作 |
| Codex / Claude Code | 代码分析、任务实现、重构和测试 |
| Continue | 编辑器内 AI 辅助 |

AI 工具可以参与实现，但需求定义、技术判断、证据检查和结果验收仍应由开发者负责。涉及密钥、生产数据和公司代码时，遵循相应的数据安全政策。

## 9. 常用快捷键总表

| 快捷键 | 工具 | 功能 |
|---|---|---|
| \`⌘ + Space\` | Spotlight | 搜索应用 |
| \`⌥ + V\` | Maccy | 剪切板历史（自定义） |
| \`⌥ + Space\` | iTerm2 | 呼出终端（自定义） |
| \`⌥ + Tab\` | AltTab | 按窗口切换（自定义） |
| \`⌃ + ⌥ + ← / →\` | Rectangle | 左右半屏（自定义） |
| \`⌘ + D\` | iTerm2 | 左右分屏 |
| \`⌘ + ⇧ + D\` | iTerm2 | 上下分屏 |
| \`⌘ + P\` | VS Code | 搜索文件 |
| \`⌘ + ⇧ + P\` | VS Code | 命令面板 |
| \`⌘ + B\` | VS Code | 显示 / 隐藏侧边栏 |

快捷键可按个人习惯调整。配置时注意检查系统快捷键、输入法和其他应用的冲突。

## 10. 配置备份与迁移

建议创建独立的配置仓库（例如 \`mac-dev-config\`），保存可公开的环境配置：

\`\`\`text
mac-dev-config/
├── README.md
├── Brewfile
├── zsh/
│   └── .zshrc
├── git/
│   └── .gitconfig
├── iterm2/
│   └── README.md
└── vscode/
    └── settings.json
\`\`\`

\`Brewfile\` 示例：

\`\`\`ruby
brew "git"
brew "fnm"
brew "uv"
brew "pnpm"
brew "gh"
brew "fzf"
brew "zoxide"
brew "ripgrep"
brew "bat"
brew "eza"
brew "jq"
brew "lazygit"

cask "iterm2"
cask "rectangle"
cask "alt-tab"
cask "shottr"
cask "appcleaner"
cask "font-jetbrains-mono-nerd-font"
\`\`\`

恢复软件：

\`\`\`bash
brew bundle
\`\`\`

Brewfile 只负责记录和安装软件，不会自动恢复所有应用偏好设置。iTerm2、VS Code 等还需要分别备份配置。

**安全要求：** 不要提交 API Key、密码、SSH 私钥、访问令牌、生产环境配置或其他敏感信息。提交前检查 Git diff 和仓库可见性。

## 11. 分阶段实施清单

- [ ] 安装 Homebrew 并检查环境。
- [ ] 安装 iTerm2，配置字体、分屏和 Hotkey Window。
- [ ] 安装 Oh My Zsh、自动建议和语法高亮。
- [ ] 安装 fnm、uv、Git、pnpm 和 GitHub CLI。
- [ ] 安装 fzf、zoxide、ripgrep 和 lazygit。
- [ ] 安装 Maccy、Rectangle 和 AltTab。
- [ ] 配置 VS Code 和常用扩展。
- [ ] 按项目需要安装 OrbStack。
- [ ] 建立配置仓库并备份非敏感配置。

## 12. 推荐的最终工作流

一个典型的全栈开发桌面布局：

- 左侧：VS Code，负责代码阅读、编辑和调试。
- 右侧：浏览器，查看文档、运行页面和调试网络请求。
- iTerm2：通过分屏运行前端、后端、测试和日志。
- Maccy：管理复制过的命令、代码片段和文本。
- Rectangle：快速调整窗口布局。
- lazygit：在终端内查看变更、暂存和提交。

最终目标不是安装最多的软件，而是建立一套稳定、清晰、可重复使用的开发工作环境。
