# 四六级 AI 教练 V1

一套面向大学英语四级（CET-4）和六级（CET-6）备考的本地 Claude Code Skills 工具包。它把 AI 学习教练与本地可视化仪表盘组合在一起：写作、听力、阅读、翻译、词汇和诊断记录保存在用户自己的电脑中，再由浏览器仪表盘汇总趋势。

> 当前 V1 以 Windows 为主要运行环境。默认学习数据目录为 `D:\文档\New project\cet-data`。Dashboard 支持通过环境变量 `CET_HOME` 覆盖该目录；Mac/Linux 用户还需要同步调整各个 `SKILL.md` 中的数据目录说明。

## 功能概览

| 模块 | 能力 | 对应命令 |
|---|---|---|
| 总入口 | 首次摸底、读取进度、路由到不同模块 | `/cet` |
| 诊断 | 根据当前分数、目标分和考试日期生成计划 | `/cet-diagnose` |
| 写作 | 审题、批改、估分、结构升级和范文优化 | `/cet-writing` |
| 听力 | 错题分类、同义替换分析、精听任务 | `/cet-listening` |
| 阅读 | 选词填空、长篇匹配、仔细阅读和同义替换积累 | `/cet-reading` |
| 翻译 | 汉译英批改、主题表达提取和升级改写 | `/cet-translation` |
| 词汇 | 每日推词、复习测试、难词池和已掌握词 | `/cet-vocab` |
| 仪表盘 | 查看分数趋势、分项表现、错因和学习时间线 | `/cet-dashboard` |

## 工作方式

```text
Claude Code 中的 /cet-* skills
        │
        ▼
本地 Markdown / YAML 学习记录
        │
        ▼
Express 后端扫描并聚合数据
        │
        ▼
React + Vite 本地仪表盘
```

学习记录和程序代码分离。升级 skills 时，不会主动删除已有学习数据。

## 项目结构

```text
.
├─ cet/                         # 总入口 skill
├─ cet-diagnose/                # 诊断与备考规划
├─ cet-writing/                 # 写作教练
├─ cet-listening/               # 听力教练
├─ cet-reading/                 # 阅读教练
├─ cet-translation/             # 翻译教练
├─ cet-vocab/                   # 词汇训练
├─ cet-dashboard/
│  ├─ SKILL.md                  # 仪表盘 skill
│  └─ dashboard/                # React + Vite + Express 本地应用
├─ SCHEMA.md                    # 学习数据格式规范
├─ install.bat                  # Windows 安装脚本
├─ install.sh                   # Mac/Linux skill 复制脚本
└─ 【先看这里】.md               # 五分钟安装指南
```

## 环境要求

- 已安装 Claude Code，并能读取 `~/.claude/skills/`。
- Dashboard 需要 Node.js 18 或更高版本。
- 推荐先在 Windows 上使用 V1 默认配置。

## 快速安装

### Windows

双击：

```text
install.bat
```

首次启动 Dashboard：

```powershell
cd "$env:USERPROFILE\.claude\skills\cet-dashboard\dashboard"
npm install
npm start
```

浏览器打开：

```text
http://localhost:5173
```

然后在 Claude Code 中输入：

```text
/cet
```

### 自定义学习数据目录

Dashboard 后端支持通过 `CET_HOME` 环境变量覆盖默认目录。例如 PowerShell：

```powershell
$env:CET_HOME = "$env:USERPROFILE\cet-data"
npm start
```

注意：当前 skills 文档仍写有默认 Windows 路径。若你长期使用自定义目录，请把各个 `SKILL.md` 里的数据路径统一替换为自己的目录，确保 AI 教练和 Dashboard 指向同一位置。

## Dashboard 常用脚本

进入 `cet-dashboard/dashboard/` 后运行：

```bash
npm install        # 安装依赖
npm start          # 同时启动后端与前端
npm test           # 运行项目自带检查
npm run seed       # 生成本地演示数据
npm run validate   # 验证学习数据格式
npm run backup     # 备份学习数据
npm run reset      # 备份后清空学习数据
npm run build      # 构建前端生产版本
```

## 数据隐私

- 项目默认只在本地读取和写入学习数据。
- 仓库不应提交个人学习记录、`.npm-cache/`、`node_modules/`、构建产物或本机日志。
- 发布前请运行 `git status`，确认没有误提交本地资料。

## 数据规范

详细数据结构见 [`SCHEMA.md`](./SCHEMA.md)。Dashboard 会扫描 frontmatter 和 YAML 文件，聚合总分、分项趋势、错因、同义替换、难词池和学习时间线。

## 已知限制

- 当前 V1 主要按 Windows 默认路径设计。
- AI 估分用于训练趋势和相对诊断，不代表官方最终成绩。
- Dashboard 是本地应用，不是可直接部署到 GitHub Pages 的纯静态网站；它依赖本地 Express 后端读取本机数据。

## 发布到 GitHub

完整步骤见 [`GITHUB_PUBLISH_GUIDE.md`](./GITHUB_PUBLISH_GUIDE.md)。

## License

当前仓库尚未自动添加开源许可证。公开发布前，请根据你的授权意愿选择并添加 `LICENSE` 文件。没有许可证时，其他人可以查看代码，但默认不等于获得复制、修改和再分发权限。
