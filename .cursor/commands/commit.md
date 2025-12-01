# commit

生成符合 Conventional Commits 规范的 Git Commit Message，支持中英文动态切换。

**核心原则**：commit 信息必须基于**实际代码变更内容**生成，而不是仅根据文件名猜测。

## 使用方法

在 Chat 中输入以下命令：
- `/commit 中文` - 生成中文 commit 信息
- `/commit 英文` - 生成英文 commit 信息
- `/commit` - 默认生成中文 commit 信息

## 执行流程

1. **检查暂存区**：执行 `git status --short` 检查是否有暂存文件
2. **获取代码变更**：执行 `git diff --cached` 获取**完整代码变更内容**
3. **分析代码变更**：阅读实际代码，理解改了什么功能、修复了什么问题
4. **生成 commit message**：基于实际变更内容，按 Conventional Commits 规范生成
5. **显示结果并询问确认**：展示变更内容摘要和跨平台提交命令
6. **执行提交**：用户确认后执行 git commit

## Commit 类型

- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档变更
- `style`: 代码格式
- `refactor`: 代码重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建/工具

## 输出格式

---

**📋 暂存区变更信息：**

变更文件：
- <文件1> (状态)

**主要变更内容：**
<基于 git diff 的实际代码变更，简要说明改了什么>

变更摘要：新增 X 个 | 修改 Y 个 | 删除 Z 个

---

**📝 生成的 Commit Message：**

```
<type>(<scope>): <subject>
```

---

**💻 提交命令（跨平台）：**

**Windows PowerShell（避免乱码）:**
```powershell
$msg = "<commit message>"; $bytes = [System.Text.Encoding]::UTF8.GetBytes($msg); [System.IO.File]::WriteAllBytes("$env:TEMP\commit-msg.txt", $bytes); git commit -F "$env:TEMP\commit-msg.txt"
```

**Mac/Linux/Git Bash:**
```bash
git commit -m "<commit message>"
```

---

**❓ 确认提交：**

是否需要执行此 commit？回复'好的'、'可以'、'yes'等即可执行。

---

## 确认词

用户回复以下任一词语即执行提交：
- 中文：好的、可以、行、没问题、执行、提交、确认
- 英文：yes、y、ok、okay、sure、go、execute、commit
