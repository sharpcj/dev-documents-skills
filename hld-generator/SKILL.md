---
name: hld-generator
description: 为软件工程系统、模块、Feature 或产品能力生成概要设计文档（HLD，High-Level Design）。用户要求“概要设计”“HLD”“High-Level Design”“高层设计”“公司概要设计模板”“概要设计评审 checklist”时使用本 skill；不要因为 Android、后端、Web、iOS、桌面端、云平台等领域不同而选择不同 skill。触发后先判断项目类型：若上下文能确定是 Android App、AOSP/系统应用、APK/AAR、Gradle Android Library、Android SDK/Framework、Kotlin/Java Android 或 Android 端侧模块，读取 references/android-template.md；若能确定是后端、Web、iOS、桌面端、云平台、数据平台、AI/ML 服务、基础设施、中台系统、非 Android SDK/库、CLI 或企业内部系统，读取 references/common-template.md。若用户只说 App/客户端/移动端/端侧/SDK/设计文档/模板而无法判断项目类型，先追问项目类型再选模板。若用户要求技术方案/技术设计/实现方案，使用 feature-technical-design；若要求拆任务、估人天、排期、需求矩阵或甘特图，使用 feature-requirements-matrix。
---

# 概要设计文档生成器（HLD Generator）

## 目的

根据用户提供的需求资料、已有设计资料、工程/系统上下文，生成一份结构完整、内容规范、可用于评审的概要设计文档（Markdown 格式）。

本 skill 不在触发层区分 Android 与通用工程；只按“文档类型 = 概要设计/HLD”触发。触发后再选择领域模板。

## 触发场景

使用本 skill 处理以下任务：

- 用户要求写概要设计、HLD、High-Level Design、高层设计。
- 用户要求按公司/团队概要设计模板填写。
- 用户要求生成带概要设计评审 checklist 的系统/模块设计文档。
- 用户提供已有技术方案、架构说明、模块说明、接口协议或工程代码上下文，希望转换或补充为概要设计模板。

不要使用本 skill 处理：

- 单 Feature 技术方案、技术设计、实现方案、方案评审材料：使用 `feature-technical-design`。
- 需求矩阵、拆任务、估人天、工作量评估、开发排期、甘特图：使用 `feature-requirements-matrix`。
- 纯产品方案、运营方案，不涉及软件工程系统设计。

## 项目类型判定与模板选择

### 1. Android 项目

如果用户资料、工程路径、术语或上下文明确出现以下信息，选择 Android 模板：

- Android App、AOSP、系统应用、端侧 Android 模块。
- APK、AAR、Gradle Android Library、AndroidManifest、minSdk、targetSdk。
- Android SDK、Android Framework、Framework API、系统服务、AIDL、Intent、Broadcast、ContentProvider。
- Kotlin/Java Android、Activity、Fragment、ViewModel、Repository、Service、Receiver、Provider、Worker、Compose/XML。

读取：`references/android-template.md`。

### 2. 通用非 Android 软件工程

如果用户资料、工程路径、术语或上下文明确属于以下项目，选择通用模板：

- 后端服务、Web 前端、iOS、桌面端、云平台、数据平台、AI/ML 服务、基础设施、中台系统。
- 非 Android SDK/库、CLI 工具、企业内部系统、数据管道、服务端批处理。
- HTTP/RPC/GraphQL/WebSocket、API 网关、数据库、缓存、消息队列、对象存储、CI/CD、部署、灰度、监控告警。

读取：`references/common-template.md`。

### 3. 无法判断项目类型

如果用户只说“App”“客户端”“移动端”“端侧”“SDK”“Framework”“设计文档”“按模板”，但没有明确 Android 或非 Android 工程类型，不要直接生成完整 HLD。先追问：

> 这个项目属于 Android 工程，还是后端/Web/iOS/桌面端/云平台等非 Android 工程？我需要先确认项目类型，才能选择正确概要设计模板。

如果用户回答能判断为 Android，使用 Android 模板；否则使用通用模板。

## 输入资料类型

用户可能以以下任意形式提供资料：

- 文字描述、会议纪要、设计说明。
- PRD、Jira、Confluence、需求清单、验收标准。
- Markdown、PDF、Word、TXT、表格等文档文件。
- 界面原型、流程图、架构图、状态图、接口截图等。
- 已有技术方案、概要方案、详细设计、接口协议、模块划分、架构约束。
- 工程或代码上下文：仓库路径、模块路径、包名/命名空间、类/接口名、配置文件、部署描述、调用链说明。

## 必要输入检查

开始生成完整 HLD 前，先确认是否具备足够输入：

1. 原始需求资料：至少包含需求目标、范围、核心功能、约束或验收标准中的一部分。
2. 技术上下文：已有技术方案、架构说明、模块说明、接口说明、代码路径，或用户对实现方向的描述。
3. 文档对象：本 HLD 对应的功能、系统、模块、服务、平台、SDK/库或产品能力名称。

如果缺少原始需求资料，或者完全无法判断设计对象，不要直接生成完整 HLD；先让用户补充资料。

如果技术上下文不足，但需求资料已经足够，可以继续生成概要设计初稿，但必须在相关章节标注“待确认”，并在输出说明中列出需要补充的技术信息。

## 工作流程

### 第一步：解读需求和工程上下文

1. 仔细阅读/识别用户提供的所有资料，不要只根据标题、文件名或模板示例生成内容。
2. 如果用户给的是本地文件路径，先读取文件内容。
3. 如果用户给的是工程路径、模块路径、服务名、类名或接口名，先搜索并阅读相关入口、调用链、配置、接口定义、数据模型和部署描述。
4. 如果资料较长，先梳理需求范围、业务流程、系统边界、关键依赖和待确认点，再开始编写。
5. 若资料不足以填写某章节，在该章节保留“待确认/暂无/不涉及”的说明，禁止捏造内容。

### 第二步：读取对应模板

根据“项目类型判定与模板选择”读取其中一个模板：

- Android：`references/android-template.md`
- 通用非 Android：`references/common-template.md`

严格按照所选模板的章节顺序和编号生成文档。保留模板中的全部必填章节和“方案概要设计评审 checklist”的完整 20 项表格。

### 第三步：生成概要设计文档

必须包含的章节以所选模板为准，通常包括：

- 文档历史发放及记录。
- 1 引言。
- 2 需求分析。
- 3 总体架构设计。
- 4 二层设计。
- 5 接口设计。
- 6 非功能设计。
- 7 并发处理。
- 8 数据结构设计。
- 9 物理数据结构。
- 10 系统出错处理。
- 方案概要设计评审 checklist。

## 工程理解要求

如果用户提供工程、代码路径或已有实现，先理解真实代码再写 HLD：

1. 读取项目清单和构建配置，例如 `package.json`、`pyproject.toml`、`go.mod`、`pom.xml`、`build.gradle`、`Cargo.toml`、Dockerfile、CI 配置，或 Android 的 Manifest/Gradle 配置。
2. 读取入口配置：页面路由、Controller/Handler、服务启动入口、任务调度入口、CLI 命令、云函数入口、Android Activity/Service/Receiver/Provider 等。
3. 搜索功能入口：页面入口、API endpoint、消息 topic、定时任务、Webhook、Intent action、deep link、命令行参数。
4. 梳理主调用链：入口 → 应用服务/领域服务/组件 → Repository/DAO/外部客户端 → 数据库/缓存/消息/SDK/Framework/第三方服务 → 回调/状态更新/响应返回。
5. 文档中尽量引用真实模块名、类名、接口名、表名、配置项和路径；无法确认时标注“待确认”。

## 图表输出规范

模板中需要结构图、流程图、时序图时，默认使用 Mermaid，除非用户指定其它格式。

- 架构图/结构图：优先使用 `flowchart`。
- 关键时序：优先使用 `sequenceDiagram`。
- 状态流转：优先使用 `stateDiagram-v2`。
- 复杂流程：可使用 `flowchart` 分层表达。
- 不确定节点或依赖用“待确认”标注。
- 每个图后给出简短文字解释，不要只放图。

## 格式规范

- 文档标题使用需求/功能/系统的实际名称，而非“概要设计模板”。
- 章节编号严格与模板一致，不得删除、重排或随意新增章节。
- 表格使用标准 Markdown 表格语法。
- 接口名、字段名、配置项、类名、模块名、资源名使用反引号标注。
- 生成的 HLD 中禁止出现具体代码实现、代码片段、伪代码、大段命令或可直接复制执行的实现逻辑；只能描述设计思路、模块职责、接口契约、流程、时序、数据结构和约束。
- 不要残留无意义模板占位符；如果内容未知，用“待确认/暂无/不涉及”表达。

## 输出文档

默认直接输出完整 Markdown 文档内容。若文档较长，可以分段输出，但要确保完整性。

若用户指定保存路径，则写入该路径，并在完成后说明文件绝对路径。若用户未指定保存路径，生成完成后可以简要询问是否需要保存为文件，文件名建议为：`{功能名称}_概要设计.md`。

## 输出前质量检查清单

在最终输出前检查：

- 是否先确认并选择了 Android 或通用模板。
- 是否已经阅读并理解用户提供的原始需求资料、已有设计资料和工程/系统上下文。
- 是否严格遵循所选模板的章节顺序、编号和标题。
- 是否完整保留所有必填章节和 20 项评审 checklist。
- 是否没有删除模板章节，也没有在用户未要求时新增模板外章节。
- 是否所有不确定内容都标注“待确认/暂无/不涉及”，而不是编造。
- 是否覆盖总体结构图、关键流程/时序、模块分解、接口、非功能设计、并发、数据结构、物理资源、系统出错处理。
- 是否全文没有出现具体代码实现、代码片段、伪代码、大段命令或可直接复制执行的实现逻辑。
