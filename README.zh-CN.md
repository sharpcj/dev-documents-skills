# 开发文档 Skills

[English](README.md) | 中文

这是一个面向编码 Agent 的软件工程文档技能集合，用来把常见研发文档编写流程沉淀成可复用的 agent workflow。当前仓库按文档类型提供三类 skill：

- 概要设计文档（HLD）
- 单 Feature 技术方案文档
- 需求矩阵与开发排期文档

每个 skill 先按文档类型触发。触发后，再根据项目类型选择对应模板：

- `references/android-template.md`：Android 项目模板
- `references/common-template.md`：非 Android 软件工程通用模板

这样不需要在外层安装 Android 和通用两套同类 skill，也方便后续继续增加更多项目类别模板。

## 项目定位

新功能开发通常不只需要写代码，还需要输出可评审、可排期、可验证的工程文档。比如需求范围、模块边界、接口设计、异常场景、非功能要求、风险措施、开发工作量和多人排期等，都需要被清晰记录。

这个仓库的目标是把这些重复性的文档工作标准化，让编码 Agent 在生成文档时能够：

- 先根据用户目标选择文档类型 skill；
- 再根据项目类型选择 Android 或通用模板；
- 先阅读需求资料、技术资料或工程上下文；
- 按固定模板保留必填章节；
- 对缺失信息明确标注“待确认”，而不是编造细节。

适用场景包括 Android App/系统模块、后端服务、Web 前端、iOS、桌面端、云平台、数据平台、AI/ML 服务、基础设施、SDK/库、CLI 工具和企业内部系统等。

## 目录结构

```text
.
├── hld-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── technical-design-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── requirements-matrix-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

## 已包含的 Skills

### `hld-generator`

用于生成概要设计文档，也就是 HLD（High-Level Design）。输入可以是 PRD、Jira、Confluence、截图、已有技术方案、接口说明、架构说明，或者工程代码上下文。

当目标是正式的概要设计、HLD、高层设计、公司/团队概要设计模板，或者带概要设计评审 checklist 的文档时，适合使用这个 skill。

触发后，该 skill 会根据项目类型选择：

- Android 模板：适用于 Android App、系统应用、AOSP、APK/AAR、Android SDK/Framework、Android Gradle Library、Kotlin/Java Android 模块。
- 通用模板：适用于后端、Web、iOS、桌面端、云平台、数据平台、AI/ML、基础设施、非 Android SDK/库、CLI、企业内部系统。

### `technical-design-generator`

用于生成单个 Feature 或版本需求的技术方案文档。

当目标是技术方案、技术设计、实现方案、Feature 级方案评审材料时，适合使用这个 skill。

该 skill 覆盖内容包括：

- 背景
- 需求描述
- 技术方案
- 业务流程图
- 数据流程图
- 技术架构拓扑图
- 关联模块具体方案描述
- 异常和边界场景
- 方案劣势、风险和解决措施

### `requirements-matrix-generator`

用于生成需求矩阵、开发任务拆解、工作量估算和多人排期文档。

当目标是拆任务、估人天、工作量评估、开发排期、需求矩阵或甘特图时，适合使用这个 skill。

该 skill 会从需求资料和技术方案中拆解开发任务，并关注：

- 先阅读原始需求资料和技术方案；
- 将任务拆到不超过 3 人天的粒度；
- 保留需求矩阵必填列和新功能必写行；
- 处理前置依赖、风险、负责人、适用端/平台或设备和任务状态；
- 在多人开发时输出 Mermaid 甘特图。

## 项目类型选择规则

这些 skill 不再通过外层目录区分 Android 和非 Android。每个 skill 触发后，会先判断或询问项目类型，再选择模板。

当上下文明确包含以下 Android 信号时，使用 Android 模板：

- Android App、AOSP、系统应用、APK、AAR
- Gradle Android Library、AndroidManifest、minSdk、targetSdk
- Android SDK、Android Framework、AIDL、Intent、Broadcast、ContentProvider
- Kotlin/Java Android、Activity、Fragment、ViewModel、Service、Receiver、Provider、Worker、Compose/XML

当上下文明确属于以下非 Android 软件工程时，使用通用模板：

- 后端服务、Web 前端、iOS、桌面端、云平台
- 数据平台、AI/ML 服务、基础设施、中台系统
- 非 Android SDK/库、CLI、企业内部系统
- API 网关、数据库、缓存、消息队列、对象存储、CI/CD、部署、可观测性

如果用户只说“App”“客户端”“移动端”“SDK”“Framework”“设计文档”“按模板”，但没有足够上下文判断项目类型，skill 应先追问项目类型，再选择模板。

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
使用 HLD generator，根据这份 PRD 和现有模块设计生成概要设计文档。
```

```text
根据这段需求说明和代码路径，生成 Feature 技术方案。
```

```text
基于这份 PRD 和技术方案生成需求矩阵，开始时间是 2026-07-01，共 3 名开发参与。
```

## 输入建议

为了让文档更可靠，建议提供尽可能具体的输入资料，例如：

- PRD、ERGO、GD、Jira、Confluence 或其它需求内容；
- 已有技术方案、概要设计、架构说明；
- 工程路径、模块名、包名/命名空间、类名、接口名、服务名或调用链；
- 接口定义、协议字段、截图、交互流程、异常流程、部署说明或日志；
- 需求矩阵所需的开始时间、结束时间、开发人数和负责人信息。

如果关键资料缺失，这些 skills 会尽量保留模板结构，并在相关章节标注“待确认”或“待补充”。

## 设计原则

- 先按文档类型触发 skill，再按项目类型选择模板。
- 项目类型不明确时先追问，不盲目选择模板。
- 先理解资料，再生成文档。
- 不删除模板要求的必填章节、表格和 checklist。
- 选择模板后，补充对应领域的工程化信息。
- 对不确定内容明确标注，不伪造接口、指标、验证结论或风险闭环。
- 输出可继续评审、修改和落地的 Markdown 文档。

## License

本项目使用 MIT License，详情见 [LICENSE](LICENSE)。
