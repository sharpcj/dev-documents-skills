---
name: feature-technical-design
description: 为软件工程单个 Feature、新特性、版本需求或功能改造编写技术方案/技术设计/实现方案/方案评审材料。用户要求“写技术方案”“技术设计”“实现方案”“方案评审”“按技术方案模板填写”时使用本 skill；不要因为 Android、后端、Web、iOS、桌面端、云平台等领域不同而选择不同 skill。触发后先判断项目类型：若上下文能确定是 Android App、AOSP/系统应用、APK/AAR、Gradle Android Library、Android SDK/Framework、Kotlin/Java Android 或 Android 端侧模块，读取 references/android-template.md；若能确定是后端、Web、iOS、桌面端、云平台、数据平台、AI/ML 服务、基础设施、中台系统、非 Android SDK/库、CLI 或企业内部系统，读取 references/common-template.md。若用户只说 App/客户端/移动端/端侧/SDK/设计文档/模板而无法判断项目类型，先追问项目类型再选模板。若用户要求概要设计/HLD，使用 hld-generator；若要求拆任务、估人天、排期、需求矩阵或甘特图，使用 feature-requirements-matrix。
---

# Feature 技术方案生成器

## 目标

根据用户提供的需求资料、代码上下文、接口说明、架构约束或文字描述，生成一份用于单个软件工程 Feature、新特性、版本需求或功能改造评审的技术方案文档。

本 skill 不在触发层区分 Android 与通用工程；只按“文档类型 = 技术方案”触发。触发后再选择领域模板。

## 触发场景

使用本 skill 处理以下任务：

- 用户要求写技术方案、技术设计、实现方案、方案评审材料。
- 用户要求基于 PRD、需求资料、接口文档、代码上下文生成单 Feature 方案。
- 用户要求补充业务流程图、数据流程图、技术架构拓扑图、关联模块、异常边界、风险和解决措施。
- 用户要求按技术方案模板填写，但尚未说明是 Android 还是其它工程类型。

不要使用本 skill 处理：

- 概要设计、HLD、高层设计、公司概要设计模板：使用 `hld-generator`。
- 需求矩阵、拆任务、估人天、工作量评估、开发排期、甘特图：使用 `feature-requirements-matrix`。
- 纯产品方案、运营方案、市场方案，不涉及软件工程实现。

## 项目类型判定与模板选择

生成文档前，先判断项目类型。模板选择只影响参考模板和领域知识，不影响本 skill 的触发。

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

如果用户只说“App”“客户端”“移动端”“端侧”“SDK”“Framework”“设计文档”“按模板”，但没有明确 Android 或非 Android 工程类型，不要直接生成完整文档。先追问：

> 这个项目属于 Android 工程，还是后端/Web/iOS/桌面端/云平台等非 Android 工程？我需要先确认项目类型，才能选择正确模板。

如果用户回答能判断为 Android，使用 Android 模板；否则使用通用模板。

## 工作流程

### 1. 收集和阅读输入

先认真阅读用户提供的所有资料。资料可能包括：

- 需求文本、PRD、Jira/Confluence、验收标准、会议纪要。
- 代码仓库路径、模块名、服务名、接口定义、调用链、部署配置。
- UI 原型、流程截图、日志、接口协议、数据结构、系统限制。
- 已有概要设计、旧技术方案、架构图、接口文档或相关历史文档。

如果用户给的是本地工程或文件路径，先用工具读取文件、搜索关键调用链，再写方案。不要只根据文件名或猜测生成内容。

### 2. 读取对应模板

根据“项目类型判定与模板选择”读取其中一个模板：

- Android：`references/android-template.md`
- 通用非 Android：`references/common-template.md`

生成文档时保持所选模板中的必填章节完整，不要删除已列出的一、二、三级标题。可以根据项目需要新增章节，但新增内容应放在模板既有结构之后或相关小节内，不要破坏主结构。

### 3. 提取关键信息

从资料中整理：

- 功能目标、项目背景、系统/应用背景、需求来源。
- 涉及模块、核心流程、数据流、接口依赖。
- 异常和边界：网络、权限、并发、重复提交、生命周期/进程、兼容性等。
- 风险和措施：方案劣势、不可控依赖、性能、稳定性、安全、回滚和验证方法。

### 4. 编写技术方案

- 用 Markdown 输出完整文档。
- 不要保留模板里的斜体示例内容；将示例替换为当前 feature 的实际内容。
- 对缺失信息，不要编造。使用“待补充”“待确认”并说明需要用户补什么。
- 方案描述要落到具体工程实现：涉及哪些系统、服务、模块、接口、数据结构、状态、任务、部署单元或 Android 组件。
- 业务流程图、数据流程图、技术架构拓扑图优先用 Mermaid。
- 异常和边界场景使用表格。
- 风险部分成对给出：风险/劣势 + 影响 + 解决措施/兜底方案 + 验证方式。

## 输出格式

默认直接输出完整 Markdown 文档。若用户指定保存路径，则写入该路径，并在完成后说明文件绝对路径。

若用户明确要求遵循其个人 Markdown 偏好，可用：

```markdown
文章标题：{Feature 名称} 技术方案
```

然后正文从一级标题开始。

## 质量检查清单

输出前检查：

- 是否先确认并选择了 Android 或通用模板。
- 模板必填章节是否全部保留。
- 是否已经阅读并理解原始需求资料和代码/接口上下文。
- 三类图是否都提供，且能表达业务流、数据流和技术拓扑。
- 异常边界是否可验证，不只是泛泛而谈。
- 风险是否有对应解决措施和验证方法。
- 缺失信息是否标注为待补充，而不是猜测。
