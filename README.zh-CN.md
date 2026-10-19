# sync-docs

[English](README.md) | 简体中文

根据项目改动更新相关说明，并维护简洁、便于回查的更改记录。

`sync-docs` 是一个仅包含指令的 [Agent Skill](https://agentskills.io/specification)。它更新相关说明并记录变化，不限定编程语言、项目类型或更改记录格式。

## 做什么

- 更新 README、使用指南和其他相关文档中受影响的部分。
- 在项目已有的更改记录中说明变化；没有合适位置时创建 `CHANGELOG.md`。
- 沿用项目的结构、术语和文档语言。英文 skill 指令可以维护中文文档，反之亦然。
- 项目维护了相关文档的翻译时，一并同步对应内容；用户限定范围时按要求执行。

默认同时处理说明文档和更改记录；“只更新这份 README”等明确要求优先。已有说明准确时可以保持原样，仅记录内部变化；没有新增事实的纯措辞调整通常不需要新增记录。

## 安装

Agent 需要能访问项目文件并有权修改文档。有 Git 时使用 Git 比较变化，没有 Git 时也可以依据提供的改动信息处理。本 skill 不需要运行脚本或安装依赖包。

个人安装时，选择下面的一条命令，在已安装 Git 的 Bash 或 PowerShell 中运行。目标目录应为新目录。

### Codex

```sh
git clone https://github.com/Dominic-jj/sync-docs.git "$HOME/.agents/skills/sync-docs"
```

在 Codex CLI 或 IDE 扩展中，用 `$sync-docs` 加上具体需求调用。安装后未出现时，重启 agent。参见[官方 skills 文档](https://learn.chatgpt.com/docs/build-skills)。

### Claude Code

```sh
git clone https://github.com/Dominic-jj/sync-docs.git "$HOME/.claude/skills/sync-docs"
```

用 `/sync-docs` 加上具体需求调用。参见[官方 skills 文档](https://code.claude.com/docs/en/skills)。

### 项目级安装或其他 agent

将 `SKILL.md` 和 `LICENSE` 复制到对应的 skill 目录：

| Agent | 项目内目标目录 |
| --- | --- |
| Codex | `.agents/skills/sync-docs/` |
| Claude Code | `.claude/skills/sync-docs/` |
| 其他支持 Agent Skills 的工具 | 工具文档规定的位置，目录命名为 `sync-docs` |

`SKILL.md` 是唯一执行入口。两份 README 供使用者阅读，不是两个需要分别安装的 skill。

安装路径和调用方式依据上述官方文档编写。本仓库不宣称已在所有宿主工具或模型上完成端到端验证。

## 使用

调用或加载 skill 后，用习惯的语言描述需求：

```text
把这次项目改动同步到相关文档，并补充更改记录。
```

```text
根据最近一次提交更新相关说明和更改记录。
```

```text
这次只更新 README.md 中的配置说明。
```

没有明确指定范围时，检查相对 `HEAD` 的相关已暂存、未暂存和未跟踪变化。工作区没有相关改动时，不自动切换到最近一次提交。指定提交或版本范围时，以指定范围为准；没有 Git 或尚无提交时，请提供可依据的改动信息。

完成后会得到文档修改，以及对更新文件、记录内容和采用范围的简要说明。

## 更改记录格式

优先沿用目标项目已有格式。新建更改记录时，简单的日期分组和条目即可。以下仅为示例，不是强制模板：

```markdown
## 2026-10-19

- 配置：新增请求超时参数，默认 30 秒。
- 重构：合并配置读取逻辑，调用方式保持不变。
```

分类标签、时分秒和版本号均为可选项。保留已有历史，不重复添加已经记录过的变化。

## 贡献与验证

欢迎使用中文或英文提交 Issue、Pull Request。报告行为问题时，请附上所用 agent、你的请求、相关示例改动，以及预期和实际结果，尽量提供便于复现的小例子。

保持 skill 聚焦于文档同步和更改记录。修改 README 内容时同步两种语言。

提交前核对 YAML 元数据、相对链接并执行 `git diff --check`。修改行为规则时，在临时项目中使用支持的 agent 验证受影响的场景：

| 场景 | 预期结果 |
| --- | --- |
| 功能变化影响已有用法说明 | 更新对应说明并记录变化。 |
| 内部重构不影响用法 | 保留准确的使用说明，补充有用的更改记录。 |
| 用户明确要求“只更新这份 README” | 只修改指定文档。 |
| 对同一组改动重复执行同步 | 不重复写记录，也不再次修改已准确的说明。 |

以上是验证标准，不代表仓库已经包含自动化端到端测试。

## 发布

通过清楚的 Git 提交说明记录日常变化。维护者可以为稳定版本创建 Git tag，并在 GitHub Release 中简要说明变化；纯措辞修订无需单独发布版本。版本管理针对本 skill 的发布，不强制目标项目采用某种版本规则。

## 许可证

[MIT](LICENSE)。完整执行规则见 [SKILL.md](SKILL.md)。
