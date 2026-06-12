# Android 开发文档 Skills

[English](README.md) | 中文

这是一个面向编码 Agent 的 Android 开发文档技能集合，用来把常见的 Android 研发文档编写流程沉淀成可复用的 agent workflow。当前仓库聚焦三类高频文档：

- 概要设计文档（HLD）
- 单 Feature 技术方案文档
- 需求矩阵与开发排期文档

每个 skill 都包含一个 `SKILL.md` 指令文件；需要固定模板的 skill 会在 `references/` 目录下提供可复用的 Markdown 模板。

## 项目定位

Android 新功能开发通常不只需要写代码，还需要输出可评审、可排期、可验证的工程文档。比如需求范围、模块边界、接口设计、异常场景、非功能要求、风险措施、开发工作量和多人排期等，都需要被清晰记录。

这个仓库的目标就是把这些重复性的文档工作标准化，让编码 Agent 在生成文档时能够：

- 先阅读需求资料、技术资料或工程上下文；
- 按固定模板保留必填章节；
- 用 Android 工程视角补全模块、接口、生命周期、权限、兼容性和测试验证内容；
- 对缺失信息明确标注“待确认”，而不是编造细节。

## 目录结构

```text
.
├── hld-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── technical-design-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── requirements-matrix-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

## 已包含的 Skills

### `hld-generator`

用于生成 Android 概要设计文档，也就是 HLD（High-Level Design）。输入可以是 PRD、ERGO、GD、Jira、Confluence、截图、已有技术方案、接口说明，或者 Android 工程代码上下文。

该 skill 会严格保留概要设计模板中的章节结构，包括：

- 文档历史发放及记录
- 引言与参考资料
- 需求分析
- 总体架构设计
- 二层模块设计
- 接口设计
- 非功能设计
- 并发处理、数据结构、物理数据结构、系统出错处理
- 完整的 20 项概要设计评审 checklist

当目标是正式的概要设计评审文档时，适合使用这个 skill。

### `technical-design-generator`

用于生成单个 Android 新 Feature 或版本需求的技术方案文档。

该 skill 更适合轻量但完整的技术评审场景，覆盖内容包括：

- 背景
- 需求描述
- 技术方案
- 业务流程图
- 数据流程图
- 技术架构拓扑图
- 关联模块具体方案描述
- 异常和边界场景
- 方案劣势、风险和解决措施

当目标是为某一个 Android Feature 输出技术设计或方案评审材料时，适合使用这个 skill。

### `requirements-matrix-generator`

用于生成 Android 新 Feature 的需求矩阵、开发任务拆解、工作量估算和多人排期文档。

该 skill 会从需求资料和技术方案中拆解 Android 开发任务，并关注：

- 先阅读原始需求资料和技术方案；
- 将任务拆到不超过 3 人天的粒度；
- 保留需求矩阵必填列和新功能必写行；
- 处理前置依赖、风险、负责人、适用设备和任务状态；
- 在多人开发时输出 Mermaid 甘特图；
- 对多语言、大字体、EAA、暗黑模式、埋点等质量项做显式评估。

当目标是做开发排期、工作量评估或需求矩阵时，适合使用这个 skill。

## 使用方式

将需要的 skill 目录复制或导入到你所使用编码 Agent 的 skill、rule 或 instruction 目录下。具体路径取决于不同 Agent 的约定，例如：

```bash
cp -R hld-generator /path/to/your-agent/skills/
cp -R technical-design-generator /path/to/your-agent/skills/
cp -R requirements-matrix-generator /path/to/your-agent/skills/
```

如果你的编码 Agent 不会自动识别新增 skill，请按对应工具的方式重启或重新加载。

安装后，可以这样使用：

```text
使用 HLD generator，根据这份 PRD 和现有模块设计生成 Android 概要设计文档。
```

```text
根据这段需求说明和代码路径，生成 Android Feature 技术方案。
```

```text
基于这份 PRD 和技术方案生成需求矩阵，开始时间是 2026-07-01，共 3 名 Android 开发参与。
```

## 输入建议

为了让文档更可靠，建议提供尽可能具体的输入资料，例如：

- PRD、ERGO、GD、Jira、Confluence 或其它需求内容；
- 已有技术方案、概要设计、架构说明；
- Android 工程路径、模块名、包名、类名、接口名或调用链；
- 接口定义、协议字段、截图、交互流程、异常流程；
- 需求矩阵所需的开始时间、结束时间、开发人数和负责人信息。

如果关键资料缺失，这些 skills 会尽量保留模板结构，并在相关章节标注“待确认”或“待补充”。

## 设计原则

- 先理解资料，再生成文档。
- 不删除模板要求的必填章节、表格和 checklist。
- 优先输出 Android 工程可落地的信息，而不是泛泛而谈。
- 对不确定内容明确标注，不伪造接口、指标、验证结论或风险闭环。
- 覆盖生命周期、权限、前后台、并发、兼容性、稳定性、安全、测试、回滚等 Android 常见设计维度。
- 输出可继续评审、修改和落地的 Markdown 文档。

## License

本项目使用 MIT License，详情见 [LICENSE](LICENSE)。
