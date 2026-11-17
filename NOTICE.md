# NOTICE

本文件记录本仓库每一项内容的来源：上游仓库地址、上游具体路径、对应 commit，以及本仓库是否改动过它。

核对方法：以 `git hash-object` 计算本地文件的对象哈希，与上游该 commit 的 git tree 中同路径文件的对象哈希逐字节比对。比对时间 2026-11-17，比对基准为下表两个 commit 的原始对象（LF 内容），不经过工作区换行转换。

## 一、来源总表

| 编号 | 上游仓库 | 标签 | commit | 提交日期 | 许可 | 被本仓库采用的技能数 |
| --- | --- | --- | --- | --- | --- | --- |
| S1 | https://github.com/mattpocock/skills | `v1.3.2` | `d1478fcb140db0b93c0c8df17bcfd311844749d0` | 2026-10-29 | MIT | 22 |
| S2 | https://github.com/Leonxlnx/taste-skill | `v2.1.0` | `a206bbf75a9d80554c0de17c1198ee2fbbc555aa` | 2026-10-18 | MIT | 1 |

两个来源仓库均为 MIT 许可，与本仓库 [LICENSE](./LICENSE) 兼容。下表 commit 列使用 7 位短哈希，完整哈希见本节。

## 二、技能来源（23 项）

状态取值：**原样** 表示该技能下所有文件与上游逐字节一致；**部分修改** 表示该技能下至少一个文件被改动；**改名** 表示本地目录名或技能名与上游不同。所有改动均可复现，补丁见 [patches/README.md](./patches/README.md)。

### 来自 S1 mattpocock/skills v1.3.2

| 技能 | 本仓库路径 | 上游路径 | commit | 状态 | 差异与补丁 |
| --- | --- | --- | --- | --- | --- |
| ask-help | `skills/engineering/ask-help/` | `skills/engineering/ask-matt/` | `d1478fc` | 改名 + 部分修改 | `SKILL.md` 与 `agents/openai.yaml` 改名；删去 triage / wayfinder / wizard / to-questionnaire / pr 分支与真实 tracker 的 blocking links 表述，`/to-tickets` 保留但改按本地 `.scratch/` 描述；补入上游没有的 `redesign-existing-projects` 条目；`PHASE-BOUNDARIES.md` 原样。补丁：`skills/engineering/ask-matt/SKILL.md.patch`、`skills/engineering/ask-matt/agents/openai.yaml.patch` |
| code-review | `skills/engineering/code-review/` | `skills/engineering/code-review/` | `d1478fc` | 部分修改 | 仅删去「提示运行 `/setup-matt-pocock-skills`」一行。补丁：`skills/engineering/code-review/SKILL.md.patch` |
| codebase-design | `skills/engineering/codebase-design/` | `skills/engineering/codebase-design/` | `d1478fc` | 原样 | 无 |
| diagnosing-bugs | `skills/engineering/diagnosing-bugs/` | `skills/engineering/diagnosing-bugs/` | `d1478fc` | 原样 | 无 |
| domain-modeling | `skills/engineering/domain-modeling/` | `skills/engineering/domain-modeling/` | `d1478fc` | 原样 | 无 |
| grill-with-docs | `skills/engineering/grill-with-docs/` | `skills/engineering/grill-with-docs/` | `d1478fc` | 原样 | 无 |
| implement | `skills/engineering/implement/` | `skills/engineering/implement/` | `d1478fc` | 部分修改 | `description` 与正文去掉 ticket / issue tracker 相关表述；`agents/openai.yaml` 的 `short_description` 去掉「or tickets」。补丁：`skills/engineering/implement/SKILL.md.patch`、`skills/engineering/implement/agents/openai.yaml.patch` |
| implement-spec | `skills/engineering/implement-spec/` | `skills/engineering/implement-spec/` | `d1478fc` | 部分修改 | 删去 tracker 前置与 draft PR 步骤；`agents/openai.yaml` 的 `short_description` 去掉 `/to-tickets` 引用。`SKILL.md` 正文仍按 ticket 组织，见 [README.md](./README.md) 的「已知不一致」。补丁：`skills/engineering/implement-spec/SKILL.md.patch`、`skills/engineering/implement-spec/agents/openai.yaml.patch` |
| improve-codebase-architecture | `skills/engineering/improve-codebase-architecture/` | `skills/engineering/improve-codebase-architecture/` | `d1478fc` | 原样 | 无 |
| project-preset-for-skills | `skills/engineering/project-preset-for-skills/` | `skills/engineering/setup-matt-pocock-skills/` | `d1478fc` | 改名 + 部分修改 | `SKILL.md` 与 `agents/openai.yaml` 改名；`SKILL.md` 中 issue tracker 与 triage label 相关内容已删净（Section A / B 整节、frontmatter 描述、草稿块子块），H1 改为 `Project Preset for Skills`；`domain.md` 原样；上游 4 个模板文件未纳入。补丁：`skills/engineering/setup-matt-pocock-skills/SKILL.md.patch`、`skills/engineering/setup-matt-pocock-skills/agents/openai.yaml.patch` |
| prototype | `skills/engineering/prototype/` | `skills/engineering/prototype/` | `d1478fc` | 原样 | 无 |
| research | `skills/engineering/research/` | `skills/engineering/research/` | `d1478fc` | 原样 | 无 |
| retro | `skills/engineering/retro/` | `skills/engineering/retro/` | `d1478fc` | 原样 | 无 |
| tdd | `skills/engineering/tdd/` | `skills/engineering/tdd/` | `d1478fc` | 原样 | 无 |
| to-spec | `skills/engineering/to-spec/` | `skills/engineering/to-spec/` | `d1478fc` | 部分修改 | 不再发布 spec 到 tracker、不再打 `ready-for-agent`。补丁：`skills/engineering/to-spec/SKILL.md.patch` |
| to-tickets | `skills/engineering/to-tickets/` | `skills/engineering/to-tickets/` | `d1478fc` | 部分修改 | 去掉 `/setup-matt-pocock-skills` 前置提示与真实 tracker 分支（GitHub / Linear、native blocking links、`ready-for-agent` 标签、子 issue），只保留 `.scratch/<feature>/issues/` 每 ticket 一个 markdown 文件的本地路径；删除 `<issue-template>` 与「不要关闭父 issue」一句；`agents/openai.yaml` 原样。补丁：`skills/engineering/to-tickets/SKILL.md.patch` |
| grill-me | `skills/productivity/grill-me/` | `skills/productivity/grill-me/` | `d1478fc` | 原样 | 无 |
| grilling | `skills/productivity/grilling/` | `skills/productivity/grilling/` | `d1478fc` | 原样 | 无 |
| handoff | `skills/productivity/handoff/` | `skills/productivity/handoff/` | `d1478fc` | 原样 | 无 |
| teach | `skills/productivity/teach/` | `skills/productivity/teach/` | `d1478fc` | 原样 | 无 |
| wait-what | `skills/productivity/wait-what/` | `skills/productivity/wait-what/` | `d1478fc` | 原样 | 无 |
| writing-for-agents | `skills/productivity/writing-for-agents/` | `skills/productivity/writing-for-agents/` | `d1478fc` | 原样 | 无 |

### 来自 S2 Leonxlnx/taste-skill v2.1.0

| 技能 | 本仓库路径 | 上游路径 | commit | 状态 | 差异与补丁 |
| --- | --- | --- | --- | --- | --- |
| redesign-existing-projects | `skills/engineering/redesign-existing-projects/` | `skills/redesign-skill/` | `a206bbf` | 部分修改（另加本地文件） | `SKILL.md` 与上游仅差 frontmatter 一行 `disable-model-invocation: true`（改为用户自调用），其余逐字节一致，未改名；`agents/openai.yaml` 上游没有对应文件，为本地新增，内容为 Codex UI 元数据，含 `policy.allow_implicit_invocation: false`。补丁：`skills/redesign-skill/SKILL.md.patch`（位于 `patches/leonxlnx-taste-skill-v2.1.0/`） |

## 三、仓库脚手架来源

非技能类文件同样来自 S1 的 `v1.3.2`（commit `d1478fc`），区别只在于是否改动。

| 本仓库文件 | 上游路径 | 状态 | 说明 |
| --- | --- | --- | --- |
| `CLAUDE.md` | `CLAUDE.md` | 部分修改 | 正文按本仓库裁剪；`AGENTS.md` 保持上游形态，即指向 `CLAUDE.md` 的符号链接（索引 mode `120000`，内容为 9 字节目标文本），本仓库不再落成普通文件；补丁：`CLAUDE.md.patch` |
| `.agents/invocation.md` | `.agents/invocation.md` | 部分修改 | 用户自调用技能示例改为 `project-preset-for-skills`；补丁：`.agents/invocation.md.patch` |
| `skills/engineering/README.md` | `skills/engineering/README.md` | 部分修改 | 删去未纳入技能的条目；补丁：`skills/engineering/README.md.patch` |
| `skills/productivity/README.md` | `skills/productivity/README.md` | 部分修改 | 删去 `to-questionnaire` 条目；补丁：`skills/productivity/README.md.patch` |
| `.gitignore` | `.gitignore` | 原样 | 无 |
| `scripts/link-skills.sh` | `scripts/link-skills.sh` | 原样 | 无 |
| `scripts/list-skills.sh` | `scripts/list-skills.sh` | 原样 | 无 |
| `scripts/sync-plugin-version.mjs` | `scripts/sync-plugin-version.mjs` | 原样 | 无 |
| `.claude-plugin/plugin.json` | `.claude-plugin/plugin.json` | 已修改 | 名称、作者、仓库地址、版本、`skills` 数组均按本仓库重写 |
| `.claude-plugin/marketplace.json` | `.claude-plugin/marketplace.json` | 已修改 | 市场名与所有者为 `georgewuw` |
| `package.json` | `package.json` | 已修改 | 包名、描述、仓库地址按本仓库重写 |
| `.changeset/config.json` | `.changeset/config.json` | 已修改 | 变更日志仓库改为 `georgewuw/skills` |
| `LICENSE` | `LICENSE` | 已修改 | 条款仍为 MIT，版权人改为 George Wu |
| `README.md` / `README.zh-CN.md` | `README.md` | 重写 | 英文版与简体中文版互为镜像，两份均与上游无逐行对应关系，不保留补丁 |

## 四、本仓库新增（上游无对应）

| 文件 | 说明 |
| --- | --- |
| `NOTICE.md` | 本文件 |
| `patches/` | 相对 S1 与 S2 的改动记录与说明 |
| `skills/engineering/redesign-existing-projects/agents/openai.yaml` | 为来自 S2 的技能补的 Codex UI 元数据 |

## 五、上游存在但本仓库未纳入

以下内容存在于 S1 `v1.3.2`，本仓库没有对应技能或文件。列出它们是为了让「来源清单」闭合，避免把缺失误读为遗漏。

- 技能：`triage`、`wayfinder`、`wizard`、`pr`（`engineering/`），`to-questionnaire`（`productivity/`）。
- 模板：`setup-matt-pocock-skills/issue-tracker-github.md`、`issue-tracker-gitlab.md`、`issue-tracker-local.md`、`triage-labels.md`。
- bucket：`misc/`、`in-progress/`、`deprecated/` 三个目录整体未同步。

共同点是它们都依赖 issue tracker、triage 标签或本机外部操作，与本仓库「去掉 tracker 依赖」的取向一致，为有意排除。
