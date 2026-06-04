# clarify-skills

两个配合使用的 AI Agent Skill，用于把"模糊需求"先澄清成一份可执行的任务说明书（`task.md`），再由执行器严格按文档落地实现。

| Skill | 作用 |
|---|---|
| **requirement-clarify-first** | 需求澄清器。先自助读码（先读后问），再用提问反复澄清，最后产出 `./tasks/<日期>/<日期>_<前缀>_<名称>.md` 作为下一个 AI 的执行说明书。**只澄清不执行**。 |
| **clarify-task-executor** | 任务执行器。读取上面产出的 `task.md`，按"三色契约"严格落地实现，并在文档末尾追加执行记录，**不改动原作者内容**。 |

二者形成闭环：`requirement-clarify-first` 负责"想清楚 + 写下来"，`clarify-task-executor` 负责"照着做 + 自验收"。

---

## 安装

每个 skill 是一个独立目录，目录下只有一个 `SKILL.md`。把这两个目录放进你的 Agent skills 目录即可。

### 方式一：手动复制（最通用）

1. 克隆本仓库：

   ```bash
   git clone https://github.com/<your-name>/clarify-skills.git
   ```

2. 把两个 skill 目录复制到你的 skills 目录（不同客户端目录可能不同，常见为 `~/.trae/skills/`、`~/.claude/skills/` 或 `~/.config/<client>/skills/`）：

   ```bash
   cp -r clarify-skills/requirement-clarify-first <你的 skills 目录>/
   cp -r clarify-skills/clarify-task-executor   <你的 skills 目录>/
   ```

3. 重启 / 重新加载客户端，即可在 skill 列表看到这两个 skill。

### 方式二：若客户端支持 `skills` CLI

```bash
npx skills add <your-name>/clarify-skills
```

> 具体命令以你所用客户端的 skill 管理工具为准。

---

## 使用

1. 提出一个需求 / bug / 重构，AI 触发 **requirement-clarify-first**，向你提问澄清，并在 `./tasks/<日期>/` 下生成 `task.md`。
2. 复核 `task.md`，确认无误后告诉 AI "开始执行"，触发 **clarify-task-executor** 照文档落地，并在文档末尾追加执行记录与自验收。

---

## License

MIT
