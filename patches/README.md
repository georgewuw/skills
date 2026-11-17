# Patches

本目录保存本仓库中的文档相对于上游原文件的实际改动，用于回答两个问题：改了哪里，以及为什么改。

补丁以**上游文件**为基线生成，不包含本仓库新增的文件（例如 `NOTICE.md`、顶层 `README.md`），也不包含纯仓库身份类配置（见下文「未纳入补丁的差异」）。

## 基线

本仓库取自两个上游，各自对应 `patches/` 下一个同级目录。

| 目录 | 上游仓库 | 标签 | commit | 打标签时间 | 许可 |
| --- | --- | --- | --- | --- | --- |
| `mattpocock-skills-v1.3.2/` | https://github.com/mattpocock/skills | `v1.3.2` | `d1478fcb140db0b93c0c8df17bcfd311844749d0` | 2026-10-29 | MIT |
| `leonxlnx-taste-skill-v2.1.0/` | https://github.com/Leonxlnx/taste-skill | `v2.1.0` | `a206bbf75a9d80554c0de17c1198ee2fbbc555aa` | 2026-10-18 | MIT |

目录名由「上游 owner-repo-标签」构成，与基线一一对应。若将来同步到新的上游版本，新增同级目录（例如 `mattpocock-skills-v1.4.0/`），不要覆盖旧目录，旧目录即为该版本的改动记录。

第一个来源贡献 22 个技能与仓库脚手架，改动较多。第二个来源只贡献 `redesign-existing-projects` 一个技能，它与上游的差异只有 `SKILL.md` frontmatter 里新增的一行 `disable-model-invocation: true`，其余逐字节一致；该技能下的 `agents/openai.yaml` 上游没有对应文件，属于新增文件而非改动，因此不出补丁。逐条核对结果见 `NOTICE.md`。

## 命名与目录规则

- 补丁文件路径镜像**上游路径**，并在末尾追加 `.patch`，因此 `skills/engineering/ask-matt/SKILL.md.patch` 对应上游 `skills/engineering/ask-matt/SKILL.md`。
- 补丁头部同样使用上游路径（`--- a/<上游路径>` / `+++ b/<上游路径>`），可直接在上游检出目录中用 `git apply` 应用。
- 本仓库中改过名的技能，其补丁仍以上游原名存放，改名动作本身不在补丁内。上游路径与本仓库路径的映射见下表。

## 补丁清单

| 补丁文件 | 本仓库对应文件 | 改动摘要 | 增/删行 |
| --- | --- | --- | --- |
| `CLAUDE.md.patch` | `CLAUDE.md` | 删去 `misc/`、`in-progress/`、`deprecated/` 三个 bucket 的约定、安装命令与文档页约定、triage labels 段落；路由技能名改为 `ask-help`；`link-skills.sh` 说明去掉对 deprecated/misc 的排除描述；新增一段双语说明：`README.md` 为英文版、`README.zh-CN.md` 为简体中文版，两者须保持同形，改动一处须同步另一处 | +5 / -16 |
| `.agents/invocation.md.patch` | `.agents/invocation.md` | 用户自调用技能示例由 `setup-matt-pocock-skills` 改为 `project-preset-for-skills` | +1 / -1 |
| `skills/engineering/README.md.patch` | `skills/engineering/README.md` | 删除 `triage`、`wayfinder`、`pr`、`wizard`、`setup-matt-pocock-skills` 条目；`to-tickets` 条目改写为本地 markdown 形态；`ask-matt` 改为 `ask-help`；`to-spec` 描述去掉「发布到 issue tracker」；补入上游没有的 `project-preset-for-skills` 与 `redesign-existing-projects` 两条，后者排在 User-invoked 一节末尾 | +5 / -8 |
| `skills/productivity/README.md.patch` | `skills/productivity/README.md` | 删除 `to-questionnaire` 条目 | +0 / -1 |
| `skills/engineering/ask-matt/SKILL.md.patch` | `skills/engineering/ask-help/SKILL.md` | `name` 与 H1 改为 `ask-help`；路由表移除 `/triage`、`/wayfinder`、`/wizard`、`/to-questionnaire`、`/pr` 分支，`/to-tickets` 保留但改按本地 `.scratch/<feature>/issues/` 描述；`/wayfinder` 的 on-ramp 改为「无对应技能，拆成多份 spec」；补入 `redesign-existing-projects`；前置条件改为 `project-preset-for-skills` 且只保留 doc layout | +9 / -18 |
| `skills/engineering/ask-matt/agents/openai.yaml.patch` | `skills/engineering/ask-help/agents/openai.yaml` | `display_name` 改为 `Ask Help` | +1 / -1 |
| `skills/engineering/setup-matt-pocock-skills/SKILL.md.patch` | `skills/engineering/project-preset-for-skills/SKILL.md` | `name` 与 H1 改为 `project-preset-for-skills`；`description` 去掉 issue tracker 与 triage label vocabulary；删掉 Section A（issue tracker）与 Section B（triage labels）整节，以及探索阶段的 `git remote`、`.scratch/`、`triage` 安装检查；`## Agent skills` 草稿块只保留 Domain docs 子块；第 5 步收尾改为「调整领域文档布局」 | +8 / -54 |
| `skills/engineering/setup-matt-pocock-skills/agents/openai.yaml.patch` | `skills/engineering/project-preset-for-skills/agents/openai.yaml` | `display_name` 改为 `Project Preset for Skills` | +1 / -1 |
| `skills/engineering/code-review/SKILL.md.patch` | `skills/engineering/code-review/SKILL.md` | 删除「issue tracker 未配置时提示运行 `/setup-matt-pocock-skills`」一行 | +0 / -2 |
| `skills/engineering/implement/SKILL.md.patch` | `skills/engineering/implement/SKILL.md` | 只把「按 ticket 引用从 tracker 取件」改为从 `.scratch/<feature>/issues/` 读取，`description` 与正文的 spec / tickets 表述保持上游原样 | +1 / -1 |
| `skills/engineering/implement-spec/SKILL.md.patch` | `skills/engineering/implement-spec/SKILL.md` | 删除 issue tracker 前置提示与「按 tracker 方式关闭 ticket」表述；去掉 draft PR 步骤；subagent 表述统一为 fresh | +5 / -9 |
| `skills/engineering/implement-spec/agents/openai.yaml.patch` | `skills/engineering/implement-spec/agents/openai.yaml` | `short_description` 去掉 `/to-tickets`，改为按整合分支描述 | +1 / -1 |
| `skills/engineering/implement/agents/openai.yaml.patch` | `skills/engineering/implement/agents/openai.yaml` | `short_description` 去掉「or tickets」 | +1 / -1 |
| `skills/engineering/to-spec/SKILL.md.patch` | `skills/engineering/to-spec/SKILL.md` | `description` 去掉「publish to the project issue tracker」；删除 tracker 与 triage label 前置提示；第 3 步不再发布 spec、不再打 `ready-for-agent` 标签；整份模板（连 `<spec-template>` 标签）用带 `markdown` 标注的围栏代码块包住，标签在块内以字面文本出现，`<user-story-example>` 与 `<actor>` 等占位符保持裸写 | +4 / -4 |
| `skills/engineering/to-tickets/SKILL.md.patch` | `skills/engineering/to-tickets/SKILL.md` | `description` 改为写到 `.scratch/<feature>/`；删除 `/setup-matt-pocock-skills` 前置提示；第 5 步只保留本地 markdown 发布路径，删去真实 tracker 分支（native blocking links、`ready-for-agent`、子 issue）与 `<issue-template>`；末尾「不要关闭父 issue」改为「不要改写 spec」；整份模板（连 `<local-ticket-template>` 标签）用带 `markdown` 标注的围栏代码块包住，占位符保持裸写 | +9 / -33 |
| `leonxlnx-taste-skill-v2.1.0/skills/redesign-skill/SKILL.md.patch` | `skills/engineering/redesign-existing-projects/SKILL.md` | frontmatter 新增 `disable-model-invocation: true`，把该技能改为用户自调用；正文与上游逐字节一致 | +1 / -0 |

合计 16 个补丁，覆盖 12 个 markdown 文件与 4 个 `agents/openai.yaml`：15 个在 `mattpocock-skills-v1.3.2/` 下，1 个在 `leonxlnx-taste-skill-v2.1.0/` 下。markdown 之外的配置差异不在此列，原因见下一节。

## 路径映射（改名）

| 上游路径 | 本仓库路径 |
| --- | --- |
| `skills/engineering/ask-matt/` | `skills/engineering/ask-help/` |
| `skills/engineering/setup-matt-pocock-skills/` | `skills/engineering/project-preset-for-skills/` |

`CLAUDE.md` 一行不在上表：它没有改名，本仓库沿用上游的两个文件名，`CLAUDE.md` 存正文，`AGENTS.md` 是指向它的符号链接（索引里 mode 为 `120000`，内容为 9 字节的目标文本 `CLAUDE.md`，与上游一致）。补丁以上游 `CLAUDE.md` 的内容为基线，应用后修改的也是 `CLAUDE.md`。

## 应用方法

```bash
git -c core.autocrlf=false clone --branch v1.3.2 --depth 1 \
  https://github.com/mattpocock/skills /tmp/upstream

cd /tmp/upstream

for p in $(find /path/to/patches/mattpocock-skills-v1.3.2 -name '*.patch' | sort); do
  git -c core.autocrlf=false apply "$p"
done
```

两点约束：

1. 必须带 `-c core.autocrlf=false`。补丁以 LF 生成，而 Windows 上 `core.autocrlf=true` 时 `git apply` 会把结果写成 CRLF，随后与本仓库文件逐字节比对必然不一致。
2. 应用后 `ask-matt/` 与 `setup-matt-pocock-skills/` 目录名仍是上游原名，改名需自行 `git mv`；`AGENTS.md` 无需处理，上游本来就是指向 `CLAUDE.md` 的符号链接，与本仓库一致。

第二个来源的补丁要在自己的检出目录里应用，同样用 `-c core.autocrlf=false`：

```bash
git -c core.autocrlf=false clone --branch v2.1.0 --depth 1 \
  https://github.com/Leonxlnx/taste-skill /tmp/taste-upstream

cd /tmp/taste-upstream

for p in $(find /path/to/patches/leonxlnx-taste-skill-v2.1.0 -name '*.patch' | sort); do
  git -c core.autocrlf=false apply "$p"
done
```

## 未纳入补丁的差异

以下差异属于本仓库身份或整体重写，做补丁没有意义，统一在 `NOTICE.md` 与顶层 `README.md` 中记录：

| 文件 | 差异性质 |
| --- | --- |
| `README.md` / `README.zh-CN.md` | 整体重写为个人仓库说明（英文版与简体中文版互为镜像），与上游内容无逐行对应关系 |
| `NOTICE.md` | 本仓库新增 |
| `.claude-plugin/plugin.json` | 插件名、作者、仓库地址、版本与 `skills` 数组均不同 |
| `.claude-plugin/marketplace.json` | 市场条目改为 `georgewuw` |
| `package.json` | 包名、描述、仓库地址不同 |
| `.changeset/config.json` | 变更日志仓库改为 `georgewuw/skills` |
| `LICENSE` | 版权人改为 George Wu，许可条款仍为 MIT |
| `skills/engineering/setup-matt-pocock-skills/issue-tracker-*.md`、`triage-labels.md` | 上游存在、本仓库删除的 4 个模板文件，删除而非改动 |

## 重新生成

上游版本不变、仅本仓库文档继续调整时，按以下步骤重做，并同步更新本文件的清单：

```bash
git -c core.autocrlf=false clone --branch v1.3.2 --depth 1 \
  https://github.com/mattpocock/skills /tmp/upstream

# 对每个映射对，分别放置上游文件与本地文件，然后生成补丁
mkdir -p /tmp/pw/a /tmp/pw/b
cp /tmp/upstream/<上游路径> /tmp/pw/a/<上游路径>
cp <本仓库路径>          /tmp/pw/b/<上游路径>

git -C /tmp/pw diff --no-index --no-prefix -U3 \
  a/<上游路径> b/<上游路径> > patches/mattpocock-skills-v1.3.2/<上游路径>.patch
```

生成后务必重新执行「校验记录」中的逐字节比较，确认补丁与应用结果一致，再更新本文件的增删行数。
