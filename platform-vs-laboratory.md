# 两个 CLI 之间的距离

## 量潮思考云 与 情境引擎 是什么关系

同一套认知工程领域模型，在 `apps/qtcloud-think` 和 `examples/project-11` 中分别独立实现了两次。前者是"思维外脑"，从原始想法到结构化笔记；后者是"情境引擎"，从结构化数据到综合报告。方向相反，但心智模型同构。

## 同一个认知层的两个接口

视角 | qtcloud-think | project-11
|----|--------------|------------|
输入 | 用户的原始日志（自然语言） | gallery 的 YAML（事实源）
产出 | 分类的 Markdown 笔记 | 周报 + 关系分析 + 图式
心智模型 | CODE（澄清→联想→精炼→表达） | 情境→意图→图式
元层 | Meta agent（自我反思） | 元领域 + relate/tension/coverage
分层的隐含共识 | L1 本地规则 → L2 本地模型 → L3 云端 LLM | 关键词模式 → 意图层级规则 → LLM 合成

## 精炼管道——两者之间的断层

qtcloud-think 的终点（received/pending/rejected 笔记）正是 project-11 的起点（situation + intention + schema YAML）所需要的原始材料。但两者之间没有自动化的精炼管道：

- **Distill 技能**（CODE 中的 D）目前是 TODO。它的设计目标正是完成这个断层——将澄清后的想法精炼为结构化的情境和意图数据。
- **笔记→YAML 的映射**：qtcloud-think 的 frontmatter（summary/tags/original）缺少直接对应到 situation（agenda/ecology/frame/dynamics）和 intention（agent/level/priority/trigger/risk）的字段。
- **验证机制缺失**：notes 中的 status（received/pending/rejected）是一个审核层，但 gallery 的 situation/intention/schema 没有对应的审核状态标记。

## 两个 CLI 的合并可能性

当前两个 Rust CLI 各自独立：

| 层面 | qtcloud-think CLI | project-11 CLI |
|------|------------------|---------------|
| 状态 | 脚手架（Cargo.toml 就绪，无 .rs） | 完整实现（8 个模块，15+ 命令） |
| 读取 | 用户 stdin + Provider API | gallery 文件系统 |
| 心智模型 | CODE + 三智能体 | 情境→意图→图式 |
| UI | ratatui TUI | 纯文本 REPL |

如果共享类型定义，project-11 的 Situation/Intention/Schema 可以作为 qtcloud-think 的精炼输出格式——收集的思维经过 CODE 管道后，直接产出可供情境引擎消费的结构化数据。这样两个 CLI 就从独立工具变成了同一管道的上下游。

## 一个认知工程工具的两种形态

两者本质上在做同一件事：**将不结构化的人类认知转化为可分析的结构化知识**。区别在于接入点——一个从最原始的日志开始，一个从已经提炼过的 YAML 开始。中间的差距，就是认知工程方法论需要填补的空白。
