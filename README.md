# Cursor AI Commit

<p align="center">
  <img src="https://img.shields.io/badge/Cursor-IDE-blue?style=flat-square" alt="Cursor IDE">
  <img src="https://img.shields.io/badge/Language-中文%20%7C%20English-green?style=flat-square" alt="Language">
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square" alt="License">
</p>

解决 Cursor IDE 生成 Git Commit 信息时**中英文无法动态切换**的问题。

通过自定义 Rules 和 Commands，让 Cursor AI 基于**实际代码变更内容**生成准确的 Commit 信息，并支持中英文自由切换。

## ✨ 功能特性

- 🌍 **中英文动态切换**：通过简单指令切换 Commit 信息语言
- 📝 **基于代码变更**：分析实际代码改动，生成有意义的 Commit 信息
- 🔧 **跨平台支持**：自动处理 Windows/Mac/Linux 编码问题
- ✅ **交互式确认**：生成后询问确认，避免误提交
- 🚀 **即装即用**：复制配置文件即可使用

## 📦 安装

### 方法一：克隆仓库（推荐）

```bash
git clone https://github.com/your-username/CursorAiCommit.git
```

将 `.cursor` 目录复制到你的项目根目录：

```bash
cp -r CursorAiCommit/.cursor /path/to/your/project/
```

### 方法二：手动创建

1. 在项目根目录创建 `.cursor/rules/` 目录
2. 创建 `.cursor/commands/` 目录
3. 将本仓库中的配置文件复制到对应目录

## 🚀 使用方法

### 基本用法

在 Cursor 的 Chat（`Ctrl+L`）或 Composer（`Ctrl+I`）中输入：

| 命令 | 说明 |
|------|------|
| `commit 中文` | 生成中文 Commit 信息 |
| `commit 英文` | 生成英文 Commit 信息 |
| `/commit 中文` | 使用斜杠命令（支持自动补全） |
| `/commit 英文` | 使用斜杠命令（支持自动补全） |

### 完整流程

1. **暂存文件**
   ```bash
   git add .
   # 或
   git stage .
   ```

2. **生成 Commit 信息**
   
   在 Cursor Chat 中输入：
   ```
   commit 中文
   ```

3. **查看结果**
   
   AI 会分析代码变更并生成：
   ```
   📋 暂存区变更信息：
   - src/login.vue (修改)
   - src/auth.ts (修改)
   
   主要变更内容：
   - 修复了登录成功后页面跳转失败的问题
   
   📝 生成的 Commit Message：
   fix(auth): 修复登录成功后页面跳转失败的问题
   ```

4. **确认提交**
   
   回复 `好的`、`可以`、`yes` 等确认词，AI 会自动执行 `git commit`

## 📁 文件结构

```
your-project/
├── .cursor/
│   ├── commands/
│   │   └── commit.md          # 斜杠命令定义
│   └── rules/
│       └── commit-commands.mdc # 规则定义（自动应用）
└── ...
```

## ⚙️ 配置说明

### Rules 文件 (`.cursor/rules/commit-commands.mdc`)

- **触发方式**：自动应用（`alwaysApply: true`）
- **触发指令**：`commit 中文` / `commit 英文`
- **功能**：定义完整的 Commit 生成逻辑

### Commands 文件 (`.cursor/commands/commit.md`)

- **触发方式**：斜杠命令 `/commit`
- **功能**：提供命令入口和使用说明

## 🔧 技术细节

### 代码变更分析

使用 `git --no-pager diff --cached` 获取暂存区的完整代码变更，确保：
- ✅ 基于实际代码改动生成 Commit 信息
- ✅ 使用 `--no-pager` 避免分页器阻塞

### 编码处理

针对 Windows PowerShell 的中文乱码问题，使用 UTF-8 无 BOM 文件方式：

```powershell
$msg = "commit message"
$bytes = [System.Text.Encoding]::UTF8.GetBytes($msg)
[System.IO.File]::WriteAllBytes("$env:TEMP\commit-msg.txt", $bytes)
git commit -F "$env:TEMP\commit-msg.txt"
```

### Commit 类型

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

| 类型 | 说明 |
|------|------|
| `feat` | 新功能 |
| `fix` | 修复 bug |
| `docs` | 文档变更 |
| `style` | 代码格式（不影响功能） |
| `refactor` | 代码重构 |
| `perf` | 性能优化 |
| `test` | 测试相关 |
| `chore` | 构建/工具相关 |

## 💡 常见问题

### Q: 为什么 `git diff` 会卡住？

A: Git 默认使用分页器显示长输出。本项目使用 `--no-pager` 选项解决此问题。

### Q: 为什么 Commit 信息有时是中文有时是英文？

A: Cursor 原生功能会根据代码内容和历史自动判断语言，无法手动控制。本项目通过自定义规则解决此问题。

### Q: Windows 下中文 Commit 信息显示乱码？

A: 本项目使用 UTF-8 无 BOM 文件方式提交，避免编码问题。

### Q: 如何自定义 Commit 格式？

A: 修改 `.cursor/rules/commit-commands.mdc` 文件中的格式定义。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'feat: Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

## 📄 License

本项目采用 [MIT License](LICENSE) 开源协议。

## 🙏 致谢

- [Cursor IDE](https://cursor.sh/) - AI-first 代码编辑器
- [Conventional Commits](https://www.conventionalcommits.org/) - Commit 信息规范

---

<p align="center">
  如果这个项目对你有帮助，请给个 ⭐ Star 支持一下！
</p>
