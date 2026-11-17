<a href="README.md">English</a> · <b>简体中文</b>

# Skills

个人自用的 agent 技能仓库。所有技能服务于本机日常工作流，不对外发布，也不再追求与上游同步的完整性。

来源与许可：绝大多数技能派生自 [mattpocock/skills](https://github.com/mattpocock/skills) 的 `v1.3.2`，`redesign-existing-projects` 来自 [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) 的 `v2.1.0`。逐项来源、上游路径与 commit 见 [NOTICE.md](./NOTICE.md)；本仓库相对上游的实际改动见 [patches/](./patches/README.md)。

本地化的主线只有一条：上游把 issue tracker（GitHub / GitLab Issues、triage 标签体系）当作前置设施，本仓库把这层依赖整个拆掉，只保留「本地 markdown + 领域文档」这一条路径。因此 `triage`、`wayfinder`、`wizard`、`pr`、`to-questionnaire` 等依赖 tracker 或本机外部操作的技能未纳入。`to-tickets` 原也在此列，2026-11-17 按本地 markdown ticket（`.scratch/<feature>/issues/`）改写后重新引入。

## 概况

| 项目 | 数量 | 说明 |
| --- | --- | --- |
| 技能总数 | 23 | `engineering` 17 个，`productivity` 6 个 |
| 用户自调用（user-invoked） | 14 | 只能由人输入 `/技能名` 触发 |
| 模型可调用（model-invoked） | 9 | 模型可自行判断触发 |
| 插件清单收录 | 23 | 与磁盘上的技能目录一一对应 |
| 相对上游有改动且已出补丁的文件 | 16 | 12 个 markdown 加 4 个 `agents/openai.yaml`，见 `patches/` |

## 目录结构

```text
.
├── CLAUDE.md                    本仓库约定，维护者与 agent 共同遵守
├── AGENTS.md                    指向 CLAUDE.md 的符号链接，两个文件名读同一份约定
├── README.md                    英文版说明
├── README.zh-CN.md              简体中文版说明（本文件）
├── NOTICE.md                    技能来源、上游路径与 commit
├── LICENSE                      MIT
├── package.json                 changeset 与版本同步脚本入口
├── .agents/
│   └── invocation.md            user-invoked 与 model-invoked 的定义及跨技能调用约定
├── .changeset/
│   └── config.json              版本发布配置
├── .claude-plugin/
│   ├── marketplace.json         市场条目（georgewuw）
│   └── plugin.json              插件清单，skills 数组决定随插件分发的技能
├── patches/
│   ├── README.md                补丁基线、清单、应用与重新生成方法
│   ├── leonxlnx-taste-skill-v2.1.0/   1 个补丁，路径镜像上游路径
│   └── mattpocock-skills-v1.3.2/      15 个补丁，路径镜像上游路径
├── scripts/
│   ├── link-skills.sh           把技能软链进 ~/.claude/skills 与 ~/.agents/skills
│   ├── list-skills.sh           列出仓库内全部 SKILL.md
│   └── sync-plugin-version.mjs  把 package.json 版本写入 plugin.json
└── skills/
    ├── engineering/             日常编码工作
    │   ├── README.md
    │   ├── ask-help/            SKILL.md, PHASE-BOUNDARIES.md, agents/openai.yaml
    │   ├── code-review/
    │   ├── codebase-design/     SKILL.md, DEEPENING.md, DESIGN-IT-TWICE.md, agents/openai.yaml
    │   ├── diagnosing-bugs/     SKILL.md, agents/openai.yaml, scripts/hitl-loop.template.sh
    │   ├── domain-modeling/     SKILL.md, ADR-FORMAT.md, GLOSSARY-FORMAT.md, agents/openai.yaml
    │   ├── grill-with-docs/
    │   ├── implement/
    │   ├── implement-spec/
    │   ├── improve-codebase-architecture/  SKILL.md, HTML-REPORT.md, agents/openai.yaml
    │   ├── project-preset-for-skills/      SKILL.md, domain.md, agents/openai.yaml
    │   ├── prototype/           SKILL.md, LOGIC.md, UI.md, agents/openai.yaml
    │   ├── redesign-existing-projects/
    │   ├── research/
    │   ├── retro/
    │   ├── tdd/                 SKILL.md, mocking.md, tests.md, agents/openai.yaml
    │   ├── to-spec/
    │   └── to-tickets/          SKILL.md, agents/openai.yaml
    └── productivity/            日常非编码工作流
        ├── README.md
        ├── grill-me/
        ├── grilling/
        ├── handoff/
        ├── teach/               SKILL.md, MISSION-FORMAT.md, RESOURCES-FORMAT.md,
        │                        LEARNING-RECORD-FORMAT.md, GLOSSARY-FORMAT.md, agents/openai.yaml
        ├── wait-what/
        └── writing-for-agents/  SKILL.md, SKILL-MECHANICS.md, agents/openai.yaml
```

每个技能目录都带一个 `agents/openai.yaml`（Codex UI 元数据，用户自调用的技能另含 `policy.allow_implicit_invocation: false`），上表中除多文件技能外不再逐个列出。

## 技能清单

来源列的缩写含义：

- `v1.3.2` 指 [mattpocock/skills](https://github.com/mattpocock/skills) 标签 `v1.3.2`，commit `d1478fcb140db0b93c0c8df17bcfd311844749d0`。
- `taste-skill v2.1.0` 指 [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) 标签 `v2.1.0`，commit `a206bbf75a9d80554c0de17c1198ee2fbbc555aa`。
- 「原样」表示与上游文件逐字节一致；「有补丁」表示本仓库对内容做过裁剪，改动记录在 `patches/`。

### Engineering（17）

用户自调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [ask-help](./skills/engineering/ask-help/SKILL.md) | 路由入口：按当前处境推荐该用哪个技能、走哪条流程 | v1.3.2 / `engineering/ask-matt`（改名，有补丁） |
| [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md) | 围绕方案连续追问，同时把术语沉淀进 `GLOSSARY.md` 与 ADR | v1.3.2 / `engineering/grill-with-docs`（原样） |
| [improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md) | 扫描代码库中的「深化模块」机会，产出 HTML 报告，再逐个追问定案 | v1.3.2 / `engineering/improve-codebase-architecture`（原样） |
| [to-spec](./skills/engineering/to-spec/SKILL.md) | 把当前对话直接综合成一份 spec，不再访谈、不发布到 tracker | v1.3.2 / `engineering/to-spec`（有补丁） |
| [to-tickets](./skills/engineering/to-tickets/SKILL.md) | 把计划、spec 或对话拆成若干 tracer-bullet ticket，每个声明自己的阻塞边，落在 `.scratch/<feature>/` 下一个 ticket 一个 markdown 文件 | v1.3.2 / `engineering/to-tickets`（有补丁） |
| [implement](./skills/engineering/implement/SKILL.md) | 按 spec 或单个 ticket 落地实现，在约定接缝处调用 `tdd`，提交前调用 `code-review` | v1.3.2 / `engineering/implement`（有补丁） |
| [implement-spec](./skills/engineering/implement-spec/SKILL.md) | 在单一集成分支上实现整份 spec，把 ticket 当任务图并发推进 | v1.3.2 / `engineering/implement-spec`（有补丁） |
| [retro](./skills/engineering/retro/SKILL.md) | 会话复盘：按严重程度提出对编码 agent 环境（导航、自动检查、规范、steering 文件、工具链）的改进 | v1.3.2 / `engineering/retro`（原样） |
| [project-preset-for-skills](./skills/engineering/project-preset-for-skills/SKILL.md) | 首次使用前的一次性配置：写入 `docs/agents/` 下的领域文档布局 | v1.3.2 / `engineering/setup-matt-pocock-skills`（改名，有补丁） |
| [redesign-existing-projects](./skills/engineering/redesign-existing-projects/SKILL.md) | 把已有站点或应用提升到精细质感：审计现状、识别通用 AI 风格痕迹、在不破坏功能的前提下应用高标准视觉规范 | taste-skill v2.1.0 / `skills/redesign-skill`（有补丁） |

模型可调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [prototype](./skills/engineering/prototype/SKILL.md) | 一次性原型：单文件 HTML 验状态模型与逻辑，或多版本可切换 UI 验界面 | v1.3.2 / `engineering/prototype`（原样） |
| [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md) | 难 bug 与性能回归的诊断闭环：先建能变红的反馈环，再最小化、假设、埋点、修复、补回归测试 | v1.3.2 / `engineering/diagnosing-bugs`（原样） |
| [research](./skills/engineering/research/SKILL.md) | 后台 agent 查一手来源，把结论沉淀为带引用的 Markdown 文件 | v1.3.2 / `engineering/research`（原样） |
| [tdd](./skills/engineering/tdd/SKILL.md) | 红绿重构循环，按纵向切片逐个交付 | v1.3.2 / `engineering/tdd`（原样） |
| [domain-modeling](./skills/engineering/domain-modeling/SKILL.md) | 主动构建并打磨领域模型：质疑术语、用场景压测、同步更新 `GLOSSARY.md` 与 ADR | v1.3.2 / `engineering/domain-modeling`（原样） |
| [codebase-design](./skills/engineering/codebase-design/SKILL.md) | 深模块设计的共享词汇：小接口、干净接缝、可透过接口测试 | v1.3.2 / `engineering/codebase-design`（原样） |
| [code-review](./skills/engineering/code-review/SKILL.md) | 双轴评审：Standards（是否符合仓库规范与常见坏味道）与 Spec（是否忠实实现原 spec），并行子 agent 执行 | v1.3.2 / `engineering/code-review`（有补丁） |

### Productivity（6）

用户自调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [grill-me](./skills/productivity/grill-me/SKILL.md) | 无状态版连续追问，适用于没有工作目录可落盘的场景 | v1.3.2 / `productivity/grill-me`（原样） |
| [handoff](./skills/productivity/handoff/SKILL.md) | 把当前对话压缩成交接文档，供另一个 agent 接续 | v1.3.2 / `productivity/handoff`（原样） |
| [teach](./skills/productivity/teach/SKILL.md) | 以当前目录为有状态教学空间，分多次会话讲清一个概念或技能 | v1.3.2 / `productivity/teach`（原样） |
| [wait-what](./skills/productivity/wait-what/SKILL.md) | 某条消息没听懂时的纠正指令：让 agent 用已有术语重讲一遍并补上缺失上下文 | v1.3.2 / `productivity/wait-what`（原样） |

模型可调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [grilling](./skills/productivity/grilling/SKILL.md) | 追问原语本身：一轮一轮推进设计树，事实归 agent、决策归你 | v1.3.2 / `productivity/grilling`（原样） |
| [writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md) | 写给人之外读者的文档：技能、`AGENTS.md` / `CLAUDE.md`、任何被指针引用的文档 | v1.3.2 / `productivity/writing-for-agents`（原样） |

## 使用方式

### 调用模型

两类技能的分界写在 [.agents/invocation.md](./.agents/invocation.md)：

- **用户自调用**：`SKILL.md` frontmatter 带 `disable-model-invocation: true`，`agents/openai.yaml` 带 `policy.allow_implicit_invocation: false`。只能由人输入 `/技能名` 触发，其他技能也无法通过 Skill 工具调用它们。`description` 面向人写，一句话说明用途。
- **模型可调用**：不带上述两个字段，模型可自行判断后触发。`description` 面向模型写，保留「何时该用」的触发语。

一条硬约束：用户自调用技能可以调用模型可调用技能，但不能反向被调用。因此 `implement`、`implement-spec` 里对 `tdd`、`code-review` 的调用是合法的，而任何技能想调用 `project-preset-for-skills` 时，只能转述成让人去执行的提示。

### 安装到本机

按需选一种即可：

1. **本地软链**

   ```bash
   bash scripts/link-skills.sh
   ```

   脚本会把 `skills/` 下每个技能目录软链到 `~/.claude/skills` 与 `~/.agents/skills`，`git pull` 后即生效。**注意**：目标位置若已存在同名真实目录（非软链），脚本会先 `rm -rf` 再建链，执行前先确认目标目录里没有未提交的本地修改。

2. **手动复制**：把目标技能目录整体拷入所用 harness 的技能目录即可，`SKILL.md` 与 `agents/` 必须保持同级。

### 典型主流程

```text
project-preset-for-skills（每个仓库跑一次）
        │
        ▼
grill-with-docs ──► to-spec ──► to-tickets ──► implement（或 implement-spec 并发推进）
        │                                      │
        │                                      ├──► tdd（实现具体切片）
        │                                      └──► code-review（提交前双轴评审）
        ▼
   GLOSSARY.md / ADR                           retro（会话结束后复盘环境改进）
```

旁路与补充：`prototype` 用于把难以在纸上定论的设计问题做成一次性程序；`research` 把查证工作丢给后台 agent；`diagnosing-bugs` 处理难复现的问题；`grill-me` 与 `grilling` 是无落盘需求的追问入口；`redesign-existing-projects` 独立用于既有项目的视觉重做。

不确定该用哪个时，先跑 `ask-help`，它就是这套流程的路由表。

## 维护说明

### 新增技能

按 [AGENTS.md](./AGENTS.md) 的约束，`engineering/` 与 `productivity/` 是 promoted bucket，新增一个技能需要同步 7 处，缺一处即为文档与实现不一致：

1. `skills/<bucket>/<name>/SKILL.md`，frontmatter 至少含 `name`、`description`，按调用类型决定是否加 `disable-model-invocation: true`。
2. `skills/<bucket>/<name>/agents/openai.yaml`，含 `interface.display_name`、`interface.short_description`；用户自调用时再加 `policy.allow_implicit_invocation: false`。
3. 该 bucket 的 `README.md`，按调用类型归入 User-invoked 或 Model-invoked，技能名链接到 `SKILL.md`。
4. `README.md` 与 `README.zh-CN.md` 两份「技能清单」中对应的表格，两处都要加，且描述须一致。
5. `.claude-plugin/plugin.json` 的 `skills` 数组。
6. 若该技能属于用户可达路径，重读 [ask-help](./skills/engineering/ask-help/SKILL.md) 并更新其路由。缺失或过时的路由条目会让它给出错误建议。
7. [NOTICE.md](./NOTICE.md) 来源表；若内容改动过上游原文件，还需在 `patches/` 下补一个补丁。

### 改名或删除

改名要同时处理目录名、`SKILL.md` 的 `name`、`agents/openai.yaml` 的 `display_name`、两份 bucket README、两份顶层 README、`plugin.json`、`NOTICE.md` 中的上游路径映射，以及 `patches/` 中补丁的文件名。补丁文件名保持上游路径，不跟着改名。

删除则反向清理上述各处，并从 `patches/` 移除对应补丁。

### 版本与变更记录

```bash
npm run changeset              # 生成变更描述文件
npm run version                # changeset version + 同步 plugin.json 版本
npm run check-plugin-version   # 只校验 package.json 与 plugin.json 版本是否一致
```

版本号唯一来源是 `package.json`，`scripts/sync-plugin-version.mjs` 负责写入 `plugin.json`，不要手工改两个文件。当前两侧均为 `1.0.0`。

### 文档一致性自查

```bash
# 全部技能清单（以实际文件为准）
bash scripts/list-skills.sh

# 对比磁盘上的技能目录与 plugin.json 的 skills 数组
# 左侧只出现在磁盘，右侧只在清单
comm -3 \
  <(find skills -name SKILL.md | sed 's|/SKILL.md$||; s|^|./|' | sort) \
  <(python -c "import json;print('\n'.join(sorted(json.load(open('.claude-plugin/plugin.json'))['skills'])))" | tr -d '\r')

# 对比两份 README 的标题层级，确认结构没有走偏
# 跳过围栏代码块，避免把 shell 注释当成标题
diff \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.md | sort | uniq -c) \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.zh-CN.md | sort | uniq -c)
```

前两条命令都没有输出差异时，说明清单与实现一致；第三条比对各层级标题的数量，与语言无关，输出相同即两份文档结构一致。

### 上游同步与补丁维护

同步上游前先读 [patches/README.md](./patches/README.md)。流程是：在 LF 检出下克隆目标标签，按序应用现有补丁，再重做差异。补丁必须以 LF 生成，并以 `git -c core.autocrlf=false apply` 应用；Windows 默认 `core.autocrlf=true` 会把结果写成 CRLF，逐字节校验必然失败。

## 许可

本仓库以 MIT 许可发布，见 [LICENSE](./LICENSE)。参考来源、路径与 commit 见 [NOTICE.md](./NOTICE.md)。
