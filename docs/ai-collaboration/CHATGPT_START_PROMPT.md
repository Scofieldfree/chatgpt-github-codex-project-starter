# ChatGPT 启动 Prompt

## 默认短版

在 ChatGPT 已连接本 GitHub 仓库时使用：

```text
请先读取仓库根目录 AGENTS.md，并按其中的阅读顺序检查相关项目文档。

当前目标：[说明这次想讨论、整理或 Review 的问题]
当前阶段：[Exploration / Documentation / Task Preparation / Review；不确定时请判断]

以仓库中的当前事实为准。先区分 Exploration、Settled Decision 和 Task。
未经确认，不要把探索性内容写成正式决定；不要开始实现或扩大范围。
如果需要更新文档，只修改实际发生变化的权威文件，并说明修改位置、原因和仍未解决的问题。
```

## 首次初始化版

```text
请先读取仓库根目录 AGENTS.md、README.md、docs/PRODUCT.md、docs/ARCHITECTURE.md、docs/DECISIONS.md 和 docs/ROADMAP.md。

我要做：[一句话项目描述]
当前阶段：Exploration

请先帮助我澄清目标用户、核心问题、MVP 边界、关键假设和最大风险。
暂时不要写代码，不要创建执行 Task，也不要把未确认想法写入正式项目文档。
```

## 沉淀文档版

```text
请先读取 AGENTS.md 和所有受影响的项目文档。

把当前对话中已经确认的 Settled Decisions 写入对应的权威文件。
不要收录未确认想法，不要批量重写无关内容，不要覆盖仓库中的其他改动。
完成后列出修改的文件、修改原因、冲突检查结果和仍为 TBD 的事项。
```

