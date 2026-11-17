<a href="README.md">English</a> · <b>简体中文</b>

# Skills

个人自用的 agent 技能集合，服务于本机日常工作流。仓库不对外发布，也不以与上游保持完整对齐为目标。

来源：多数技能派生自 [mattpocock/skills](https://github.com/mattpocock/skills) `v1.3.2`，`redesign-existing-projects` 派生自 [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) `v2.1.0`。逐项来源、上游路径与 commit 见 [NOTICE.md](./NOTICE.md)，相对上游的实际改动见 [patches/](./patches/README.md)。

本地化遵循一条原则：上游把 issue tracker（GitHub 或 GitLab Issues 加 triage 标签体系）当作前置设施，本仓库移除该依赖，只保留基于本地 markdown 与领域文档的路径。依赖 tracker 或仓库外操作的技能因此未纳入，包括 `triage`、`wayfinder`、`wizard`、`pr` 与 `to-questionnaire`。`to-tickets` 原属此类，已改写为基于本地 markdown ticket（`.scratch/<feature>/issues/`）后重新引入。

## 概况

| 项目 | 数量 | 说明 |
| --- | --- | --- |
| 技能总数 | 23 | `engineering` 17 个，`productivity` 6 个 |
| 用户自调用 | 14 | 仅可由人输入 `/技能名` 触发 |
| 模型可调用 | 9 | 模型可自行判断触发 |
| 插件清单收录 | 23 | 与磁盘上的技能目录一一对应 |
| 相对上游有改动的文件 | 16 | 12 个 markdown 与 4 个 `agents/openai.yaml`，见 `patches/` |

## 目录结构

```text
.
├── CLAUDE.md                    仓库约定，维护者与 agent 共同遵守
├── AGENTS.md                    指向 CLAUDE.md 的符号链接，两个文件名读同一份约定
├── README.md                    英文版说明
├── README.zh-CN.md              简体中文版说明（本文件）
├── NOTICE.md                    技能来源、上游路径与 commit
├── LICENSE                      MIT
├── package.json                 changeset 与版本同步脚本入口
├── .agents/
│   └── invocation.md            调用类型定义与跨技能调用规则
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
│   ├── link-skills.sh           把技能软链至 ~/.claude/skills 与 ~/.agents/skills
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

每个技能目录都含 `agents/openai.yaml`（Codex UI 元数据；用户自调用技能另含 `policy.allow_implicit_invocation: false`）。上表只展开多文件技能，单文件技能不逐项列出。

## 技能清单

来源列缩写：

- `v1.3.2`：[mattpocock/skills](https://github.com/mattpocock/skills) 标签 `v1.3.2`，commit `d1478fcb140db0b93c0c8df17bcfd311844749d0`。
- `taste-skill v2.1.0`：[Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) 标签 `v2.1.0`，commit `a206bbf75a9d80554c0de17c1198ee2fbbc555aa`。
- `原样`：与上游文件逐字节一致。`有补丁`：内容经过裁剪，改动记录在 `patches/`。

### Engineering（17）

用户自调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [ask-help](./skills/engineering/ask-help/SKILL.md) | 路由入口：按当前处境推荐技能与流程 | v1.3.2 / `engineering/ask-matt`（改名，有补丁） |
| [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md) | 围绕方案连续追问，同步把术语沉淀进 `GLOSSARY.md` 与 ADR | v1.3.2 / `engineering/grill-with-docs`（原样） |
| [improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md) | 扫描代码库中的模块深化机会，产出 HTML 报告，再逐个追问定案 | v1.3.2 / `engineering/improve-codebase-architecture`（原样） |
| [to-spec](./skills/engineering/to-spec/SKILL.md) | 把当前对话直接综合为 spec，不访谈、不发布到 tracker | v1.3.2 / `engineering/to-spec`（有补丁） |
| [to-tickets](./skills/engineering/to-tickets/SKILL.md) | 把计划、spec 或对话拆成 tracer-bullet ticket，各自声明阻塞边，按 `.scratch/<feature>/` 一文件一 ticket 落盘 | v1.3.2 / `engineering/to-tickets`（有补丁） |
| [implement](./skills/engineering/implement/SKILL.md) | 按 spec 或单个 ticket 实现，在约定接缝调用 `tdd`，提交前调用 `code-review` | v1.3.2 / `engineering/implement`（有补丁） |
| [implement-spec](./skills/engineering/implement-spec/SKILL.md) | 在单一集成分支上实现整份 spec，把 ticket 当任务图并发推进 | v1.3.2 / `engineering/implement-spec`（有补丁） |
| [retro](./skills/engineering/retro/SKILL.md) | 会话复盘：按严重程度列出编码 agent 环境（导航、自动检查、规范、steering 文件、工具链）的改进项 | v1.3.2 / `engineering/retro`（原样） |
| [project-preset-for-skills](./skills/engineering/project-preset-for-skills/SKILL.md) | 首次使用前的一次性配置：写入 `docs/agents/` 下的领域文档布局 | v1.3.2 / `engineering/setup-matt-pocock-skills`（改名，有补丁） |
| [redesign-existing-projects](./skills/engineering/redesign-existing-projects/SKILL.md) | 把既有站点或应用提升至精细质感：审计现状、识别通用 AI 风格、在不破坏功能的前提下套用高标准视觉规范 | taste-skill v2.1.0 / `skills/redesign-skill`（有补丁） |

模型可调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [prototype](./skills/engineering/prototype/SKILL.md) | 一次性原型：单文件 HTML 验证状态模型与逻辑，或可切换的 UI 变体验证界面 | v1.3.2 / `engineering/prototype`（原样） |
| [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md) | 难 bug 与性能回归的诊断闭环：先建立可失败的反馈环，再最小化、假设、埋点、修复、补回归测试 | v1.3.2 / `engineering/diagnosing-bugs`（原样） |
| [research](./skills/engineering/research/SKILL.md) | 后台 agent 查阅一手来源，把结论沉淀为带引用的 Markdown 文件 | v1.3.2 / `engineering/research`（原样） |
| [tdd](./skills/engineering/tdd/SKILL.md) | 红绿重构循环，按纵向切片逐个交付 | v1.3.2 / `engineering/tdd`（原样） |
| [domain-modeling](./skills/engineering/domain-modeling/SKILL.md) | 主动构建并打磨领域模型：质疑术语、以场景压测、同步维护 `GLOSSARY.md` 与 ADR | v1.3.2 / `engineering/domain-modeling`（原样） |
| [codebase-design](./skills/engineering/codebase-design/SKILL.md) | 深模块设计的共享词汇：小接口、干净的接缝、可透过接口测试 | v1.3.2 / `engineering/codebase-design`（原样） |
| [code-review](./skills/engineering/code-review/SKILL.md) | 双轴评审：Standards（是否符合仓库规范、规避常见坏味道）与 Spec（是否忠实实现原 spec），由并行子 agent 执行 | v1.3.2 / `engineering/code-review`（有补丁） |

### Productivity（6）

用户自调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [grill-me](./skills/productivity/grill-me/SKILL.md) | 无状态的连续追问，适用于没有工作目录可落盘的场景 | v1.3.2 / `productivity/grill-me`（原样） |
| [handoff](./skills/productivity/handoff/SKILL.md) | 把当前对话压缩为交接文档，供另一个 agent 接续 | v1.3.2 / `productivity/handoff`（原样） |
| [teach](./skills/productivity/teach/SKILL.md) | 以当前目录为有状态教学空间，跨多次会话讲清一个概念或技能 | v1.3.2 / `productivity/teach`（原样） |
| [wait-what](./skills/productivity/wait-what/SKILL.md) | 针对没读懂的消息发起纠正：让 agent 用已有术语重讲，并补上缺失上下文 | v1.3.2 / `productivity/wait-what`（原样） |

模型可调用：

| 技能 | 用途 | 来源 |
| --- | --- | --- |
| [grilling](./skills/productivity/grilling/SKILL.md) | 追问原语：逐轮推进设计树，事实归 agent，决策归你 | v1.3.2 / `productivity/grilling`（原样） |
| [writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md) | 面向非人类读者的文档：技能、`AGENTS.md` / `CLAUDE.md`，以及任何被指针引用的文档 | v1.3.2 / `productivity/writing-for-agents`（原样） |

## 使用

### 调用模型

两类技能的分界定义在 [.agents/invocation.md](./.agents/invocation.md)：

- **用户自调用（user-invoked）**：`SKILL.md` frontmatter 含 `disable-model-invocation: true`，`agents/openai.yaml` 含 `policy.allow_implicit_invocation: false`。仅可由人输入 `/技能名` 触发，其他技能也无法通过 Skill 工具调用。`description` 面向人撰写，一句话说明用途。
- **模型可调用（model-invoked）**：不含上述两个字段，模型可自行判断触发。`description` 面向模型撰写，保留“何时该用”的触发语。

一条硬约束：用户自调用技能可以调用模型可调用技能，反向不成立。因此 `implement`、`implement-spec` 调用 `tdd`、`code-review` 合法；任何技能若需 `project-preset-for-skills`，只能转述为让人执行的提示。

### 安装到本机

任选一种：

1. **本地软链**

   ```bash
   bash scripts/link-skills.sh
   ```

   脚本把 `skills/` 下每个技能目录软链至 `~/.claude/skills` 与 `~/.agents/skills`，`git pull` 后立即生效。**注意**：目标位置若已存在同名真实目录（非软链），脚本会先 `rm -rf` 再建链，执行前须确认目标目录内无未提交的本地修改。

2. **手动复制**

   把技能目录整体拷入所用 harness 的技能目录，`SKILL.md` 与 `agents/` 须保持同级。

### 典型流程

```text
project-preset-for-skills（每个仓库执行一次）
        │
        ▼
grill-with-docs ──► to-spec ──► to-tickets ──► implement（并发推进时改用 implement-spec）
        │                                      │
        │                                      ├──► tdd（实现单个切片）
        │                                      └──► code-review（提交前双轴评审）
        ▼
   GLOSSARY.md / ADR                           retro（会话结束后复盘环境改进）
```

旁路与补充：`prototype` 把难以纸面定论的设计问题做成一次性程序；`research` 把查证交给后台 agent；`diagnosing-bugs` 处理难复现的问题；`grill-me` 与 `grilling` 是无落盘需求的追问入口；`redesign-existing-projects` 独立用于既有项目的视觉重做。

不确定该用哪个技能时，先运行 `ask-help`，它是上述流程的路由表。

## 维护

### 新增技能

按 [AGENTS.md](./AGENTS.md) 的约束，`engineering/` 与 `productivity/` 是 promoted bucket，新增技能须同步 7 处，缺一处即造成文档与实现不一致：

1. `skills/<bucket>/<name>/SKILL.md`：frontmatter 至少含 `name`、`description`；用户自调用技能另加 `disable-model-invocation: true`。
2. `skills/<bucket>/<name>/agents/openai.yaml`：含 `interface.display_name` 与 `interface.short_description`；用户自调用技能另加 `policy.allow_implicit_invocation: false`。
3. 该 bucket 的 `README.md`：归入“用户自调用”或“模型可调用”分组，技能名链接至 `SKILL.md`。
4. `README.md` 与 `README.zh-CN.md` 中对应的技能表：两处都要新增，描述须一致。
5. `.claude-plugin/plugin.json` 的 `skills` 数组。
6. 若技能位于用户可达路径，重读 [ask-help](./skills/engineering/ask-help/SKILL.md) 并更新路由；缺失或过时的条目会导致错误建议。
7. [NOTICE.md](./NOTICE.md) 的来源表；若内容改动过上游文件，另在 `patches/` 下补一个补丁。

### 改名或删除

改名涉及目录名、`SKILL.md` 的 `name`、`agents/openai.yaml` 的 `display_name`、两份 bucket README、两份顶层 README、`plugin.json`、`NOTICE.md` 的上游路径映射，以及 `patches/` 中的补丁文件名。补丁文件名沿用上游路径，不随改名调整。

删除按上述各处反向清理，并从 `patches/` 移除对应补丁。

### 版本与变更记录

```bash
npm run changeset              # 生成变更描述文件
npm run version                # 执行 changeset version 并同步 plugin.json 版本
npm run check-plugin-version   # 仅校验 package.json 与 plugin.json 版本是否一致
```

版本号唯一来源是 `package.json`，由 `scripts/sync-plugin-version.mjs` 写入 `plugin.json`，不要手工修改两个文件。当前两侧均为 `1.0.0`。

### 文档一致性检查

```bash
# 全部技能清单（以实际文件为准）
bash scripts/list-skills.sh

# 对比磁盘技能目录与 plugin.json 的 skills 数组
# 左列为仅在磁盘、右列为仅在清单
comm -3 \
  <(find skills -name SKILL.md | sed 's|/SKILL.md$||; s|^|./|' | sort) \
  <(python -c "import json;print('\n'.join(sorted(json.load(open('.claude-plugin/plugin.json'))['skills'])))" | tr -d '\r')

# 对比两份 README 的标题层级，检查结构是否偏移
# 跳过围栏代码块，避免把 shell 注释计为标题
diff \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.md | sort | uniq -c) \
  <(awk '/^```/{f=!f;next} !f&&/^#/{match($0,/^#+/);print RLENGTH}' README.zh-CN.md | sort | uniq -c)
```

前两条命令无输出差异时，清单与实现一致。第三条比对各层级标题数量，与语言无关，输出相同即两份文档结构一致。

### 同步上游

同步前先读 [patches/README.md](./patches/README.md)。流程：以 LF 检出克隆目标标签，按序应用现有补丁，再重做差异。补丁须以 LF 生成，并以 `git -c core.autocrlf=false apply` 应用；Windows 默认 `core.autocrlf=true` 会把结果写成 CRLF，导致逐字节校验必然失败。

## 许可

本仓库以 MIT 许可发布，见 [LICENSE](./LICENSE)。上游两个仓库同为 MIT，来源、路径与 commit 见 [NOTICE.md](./NOTICE.md)。
