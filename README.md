# sync-docs

English | [简体中文](README.zh-CN.md)

Keep project documentation aligned with changes and leave a concise, searchable changelog.

`sync-docs` is an instruction-only [Agent Skill](https://agentskills.io/specification). It updates relevant explanations and records what changed, without requiring a particular programming language, project type, or changelog format.

## What it does

- Updates affected sections of README files, usage guides, and other relevant documents.
- Records changes in the project's existing changelog, or creates `CHANGELOG.md` when needed.
- Preserves the project's structure, terminology, and document languages. English skill instructions can maintain Chinese documents and vice versa.
- Keeps translations of affected documentation aligned when the project maintains them, unless the user limits the scope.

By default, it handles documentation and the changelog together. Explicit requests such as "only update this README" take precedence. Accurate explanations can stay unchanged while the changelog records an internal change; wording-only edits usually need no new entry.

## Install

The agent needs access to the project files and permission to edit its documentation. Git is used for comparisons when available; supplied change information can also be used without Git. No runtime scripts or packages are required by this skill.

For a personal installation, run **one** of the following commands in Bash or PowerShell with Git installed. The destination should be a new directory.

### Codex

```sh
git clone https://github.com/Dominic-jj/sync-docs.git "$HOME/.agents/skills/sync-docs"
```

In Codex CLI or the IDE extension, invoke it with `$sync-docs`, followed by your request. If it does not appear after installation, restart the agent. See the [official skills documentation](https://learn.chatgpt.com/docs/build-skills).

### Claude Code

```sh
git clone https://github.com/Dominic-jj/sync-docs.git "$HOME/.claude/skills/sync-docs"
```

Invoke it with `/sync-docs`, followed by your request. See the [official skills documentation](https://code.claude.com/docs/en/skills).

### Project installation or another agent

Copy `SKILL.md` and `LICENSE` into the appropriate skill directory:

| Agent | Project destination |
| --- | --- |
| Codex | `.agents/skills/sync-docs/` |
| Claude Code | `.claude/skills/sync-docs/` |
| Other Agent Skills hosts | The host's documented skill directory, named `sync-docs` |

Keep `SKILL.md` as the single entry point. The two README files are user documentation, not separate installable skills.

Installation paths and invocation syntax follow the linked official documentation. This repository does not claim end-to-end validation on every host or model.

## Use

After invoking or loading the skill, describe the task in your preferred language:

```text
Sync the documentation with these project changes and update the changelog.
```

```text
根据最近一次提交更新相关说明和更改记录。
```

```text
Only update the configuration section of README.md.
```

Without an explicit range, the skill inspects relevant staged, unstaged, and untracked changes relative to `HEAD`. It does not automatically switch to the latest commit when the working tree is clean. A specified commit or version range takes precedence; without Git or an initial commit, provide the change information to use.

The result is a documentation patch and a short explanation of the files updated, changes recorded, and scope used.

## Changelog style

Use the target project's existing format. When creating a changelog, simple dated entries are enough. The following is an example, not a required template:

```markdown
## 2026-10-19

- Configuration: added a request timeout setting, defaulting to 30 seconds.
- Refactoring: consolidated configuration loading without changing its callers.
```

Category labels, time of day, and version numbers are optional. Existing history is preserved and changes already recorded are not added again.

## Contribute and verify

Issues and pull requests in English or Chinese are welcome. For a behavior issue, include the agent used, your request, relevant sample changes, and the expected and actual result. Small reproducible examples are useful.

Keep the skill focused on documentation updates and change records. Update both READMEs when their content changes.

Before submitting, check the YAML frontmatter, relative links, and `git diff --check`. When changing behavior, exercise the affected scenarios in a disposable project with a supported agent:

| Scenario | Expected result |
| --- | --- |
| A feature changes documented usage | Update the relevant explanation and record the change. |
| Internal refactoring leaves usage unchanged | Preserve accurate usage docs and add a useful change record. |
| The user says "only update this README" | Limit edits to that document. |
| The same changes are synchronized twice | Do not duplicate changelog entries or modify accurate docs again. |

These are verification criteria, not a claim that automated end-to-end tests are included.

## Releases

Track day-to-day changes with descriptive Git commit messages. Maintainers can publish a Git tag and a short GitHub Release summary for stable versions; wording-only fixes need not create a release. Versioning applies to this skill's releases and does not impose a versioning scheme on target projects.

## License

[MIT](LICENSE). See [SKILL.md](SKILL.md) for the execution rules.
