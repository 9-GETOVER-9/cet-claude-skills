# 发布到 GitHub：详细操作指南

本文档适用于本项目的清理版目录 `cet-claude-skillsV1-github-ready`。

## 1. 建议的仓库信息

- 仓库名：`cet-claude-skills`
- 简介：`CET-4/CET-6 本地 AI 备考教练：Claude Code Skills + React/Express 学习仪表盘`
- 推荐 Topics：`cet4`、`cet6`、`claude-code`、`skills`、`english-learning`、`react`、`vite`、`express`、`education`
- 可见性：准备公开分享时选择 `Public`；仅自己使用或尚未整理完成时选择 `Private`

## 2. 发布前确认

本清理版已经排除：

```text
.npm-cache/
node_modules/
dist/
*.log
.env*
.claude/
cet-data/
backups/
```

发布前仍建议在终端中检查：

```bash
git status
```

确认列表里没有个人学习数据、截图、账号信息、Token 或本机日志。

## 3. 方法 A：命令行发布（推荐）

### 3.1 检查 Git

打开 PowerShell、Windows Terminal 或 Git Bash：

```bash
git --version
```

首次使用 Git 时设置提交信息：

```bash
git config --global user.name "你的 GitHub 昵称"
git config --global user.email "你的 GitHub 邮箱"
```

### 3.2 在 GitHub 创建空仓库

1. 登录 GitHub。
2. 右上角点击 `+`，选择 `New repository`。
3. Repository name 填写：`cet-claude-skills`。
4. Description 填写：`CET-4/CET-6 本地 AI 备考教练：Claude Code Skills + React/Express 学习仪表盘`。
5. 选择 `Public` 或 `Private`。
6. 不要勾选自动创建 README、`.gitignore` 或 License。本地清理版已经有 README 和 `.gitignore`；License 建议单独确认后再添加。
7. 点击 `Create repository`。

### 3.3 初始化本地仓库并提交

在终端中进入解压后的清理版目录。示例：

```powershell
cd "D:\你的目录\cet-claude-skillsV1-github-ready"
```

运行：

```bash
git init
git add .
git status
git commit -m "Initial release: CET AI coach skills and local dashboard"
git branch -M main
```

### 3.4 连接 GitHub 仓库并推送

把 `<你的GitHub用户名>` 替换为真实用户名：

```bash
git remote add origin https://github.com/<你的GitHub用户名>/cet-claude-skills.git
git push -u origin main
```

如果系统要求输入密码，不要输入 GitHub 登录密码。HTTPS Git 操作应使用浏览器授权、Git Credential Manager、GitHub CLI，或使用 Personal Access Token 代替密码。

### 3.5 检查发布结果

刷新 GitHub 仓库页面，确认首页能看到：

```text
README.md
GITHUB_PUBLISH_GUIDE.md
SCHEMA.md
install.bat
install.sh
cet-*/
```

并确认没有：

```text
node_modules/
.npm-cache/
dist/
cet-data/
```

## 4. 方法 B：GitHub Desktop 发布（不熟悉命令行时使用）

1. 安装并登录 GitHub Desktop。
2. 选择 `File` → `Add local repository`。
3. 选择解压后的 `cet-claude-skillsV1-github-ready` 目录。
4. 如果提示它还不是 Git 仓库，选择创建仓库。
5. 在左下角填写提交说明，例如：`Initial release`。
6. 点击 `Commit to main`。
7. 点击 `Publish repository`。
8. 填写仓库名 `cet-claude-skills`，选择是否公开，再发布。

发布后在浏览器中打开仓库，检查 README 和文件列表。

## 5. 方法 C：网页上传（仅适合第一次快速发布）

清理版体积较小，也可以在 GitHub 仓库页面点击 `Add file` → `Upload files`，拖入目录中的文件。网页上传适合第一次尝试，但后续维护更建议使用 Git 或 GitHub Desktop。

注意：上传时不要把原始压缩包中的 `.npm-cache/`、`node_modules/` 和 `dist/` 重新拖进去。

## 6. 后续更新仓库

以后修改代码后，进入本地仓库目录运行：

```bash
git status
git add .
git commit -m "描述本次修改"
git push
```

例如：

```bash
git add .
git commit -m "docs: improve Windows setup guide"
git push
```

## 7. 建议补充 License

公开发布并不自动等于开源授权。准备允许别人使用、修改或再分发时，请添加 `LICENSE` 文件。常见选择：

- MIT：宽松、简洁，适合希望别人方便使用和修改的项目。
- Apache-2.0：宽松，同时包含更明确的专利授权条款。
- GPL-3.0：要求衍生作品继续使用相同开源许可证。

不确定时，可以先公开展示但暂不添加 License，之后再决定。

## 8. 发布页可直接使用的文案

### 仓库简介

```text
CET-4/CET-6 本地 AI 备考教练：Claude Code Skills + React/Express 学习仪表盘
```

### 首次 Release 标题

```text
v1.0.0 - Initial release
```

### 首次 Release 说明

```markdown
## 四六级 AI 教练 V1

首次公开版本，包含：

- CET-4/CET-6 总入口与诊断 skill
- 写作、听力、阅读、翻译和词汇训练 skills
- 本地 React + Vite + Express 学习仪表盘
- Markdown / YAML 学习数据规范
- Windows 安装脚本与 Mac/Linux skill 复制脚本

说明：当前 V1 以 Windows 默认路径为主；学习数据仅保存在本地。AI 估分用于备考趋势参考，不代表官方最终成绩。
```

## 9. 常见问题

### 为什么不能上传 `node_modules`？

依赖目录体积大，而且包含特定操作系统的二进制文件。仓库只提交 `package.json` 和 `package-lock.json`；用户克隆后执行 `npm install` 即可重新安装适合自己系统的依赖。

### 为什么不能上传 `.npm-cache`？

缓存没有发布价值，还可能包含本机目录、用户名和安装日志。

### 能不能直接部署为 GitHub Pages？

当前版本不能直接作为 GitHub Pages 使用。Dashboard 依赖本地 Express 后端读取用户电脑上的学习数据。GitHub Pages 只能托管静态页面，不会运行这个本地后端。

### 用户克隆后怎么启动？

```powershell
cd "$env:USERPROFILE\.claude\skills\cet-dashboard\dashboard"
npm install
npm start
```
