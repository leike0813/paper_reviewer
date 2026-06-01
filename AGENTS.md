# paper_reviewer （论文审稿）

## 项目背景

- 本项目是一个 **Agent Skill** 开发项目，并非常规软件工程项目
- 本项目旨在开发一个可以自动化地站在审稿人角度，为用户提供一份严谨、客观、详实且具有可操作性的审稿意见的 Agent Skill

## 项目Skill的执行思路（并非最终产物的执行流程）

1. 对用户提交的论文稿件建立深入理解
2. 分析原稿主题、主要工作、创新点等部分
3. 提取原稿的大纲，形成结构化提取结果并落盘记忆
4. 根据原稿的研究领域，阅读 `references` 目录下相应领域的论文撰写范式指导文档
5. 首先审阅论文的宏观问题，记录发现的问题并落盘记忆：
  - 研究选题质量如何，是否具有研究价值，创新点的整理提炼是否准确
  - 标题是否准确得当，与正文内容是否匹配
  - 摘要撰写质量如何，是否概括了论文的研究重点、主要研究内容和主要结论，是否有无意义的废话
  - 章节编排是否合理，引言、研究综述、问题阐述、方法论、实验、论证、总结讨论等各个环节有没有明显缺失
6. 针对论文的微观问题，逐段审阅论文内容，记录发现的问题并落盘记忆：
  - 引言有没有阐明研究的意义及必要性，逻辑是否连贯，能否为读者提供宏观的思路引导
  - 文献综述是否为读者展示了相关研究的主流方向、技术沿革及前沿进展，是否存在“简单复述他人成果”、“流水账式堆砌”等问题
  - 方法论是否清晰完整，是否契合论文主题
  - 论述是否严谨，有没有明显的逻辑漏洞、前后矛盾、论据不足等
  - 数据分析和实验设计是否合理，有没有明显的统计错误、实验设计缺陷、结果解读错误等
  - 结论是否准确得当，是否与论文的研究内容和研究结果相匹配，是否存在过度解读、无意义的废话等问题
  - 是否有讨论当前研究存在的问题、局限性和未来研究方向
7. 进行论文的形式化与语言检查，记录发现的问题并落盘记忆
  - 语言表达是否清晰、准确、得体，有没有明显的语法错误、拼写错误、用词不当等
  - 语言的时态、语态运用是否得当，是否前后一致
  - 是否存在冗余段落或语句，表述是否可以进一步凝练
  - 论文格式是否存在问题
  - 是否存在未引用图表
  - 如果模型有视觉能力，检查图片是否清晰、视觉效果是否得当
  - 参考文献格式是否正确，是否存在信息缺失；如果有联网能力，可进行一轮检索验证，列出可能存在问题的参考文献条目
8. 回顾记忆，进行综合整理，形成条理清晰的审稿意见，落盘保存

## 非目标

- **禁止任何企图一步到位地直接形成审稿意见的行为！**学术论文的审稿是一件非常严谨且复杂的任务，需要详细的方案制定和扎实的步骤推进。不制定方案，直接生成最终意见，是对用户的不负责任
- **禁止直接修改论文原稿。**如果用户没有采用版本管理系统或没有备份，直接修改文件可能会导致原稿不可恢复。

## 总体原则

- 本 Skill 应该以自动化的形式进行
- 本 Skill 的主线工作以文档分析、提供意见建议、形成审稿意见为主，不涉及论文修改方案的制定，更不涉及对论文的直接修改
- 本 Skill 执行中应充分利用 shell 工具进行文件的批量读写
- 本 Skill 执行中鼓励 Agent 创建中间工件来强化自身记忆，中间工件也可作为与用户交互的媒介，避免完全依赖 Agent LLM 自身的上下文记忆

## 你该做什么

- 本文档仅是一份宏观指导，距离可供 Agent 实施的详细指令（SKILL.md）还有不小距离
- 你的任务是，基于目前的宏观指令，生成符合 Open Agent Skills 规范的 Skill 包。本项目 Skill 包的发布目录为 `paper-reviewer` （与 Skill 名称一致）
- 本项目是 Agent Skill 开发项目，其核心是用自然语言（面向LLM的语言风格）编写 Skill 包的核心指令文件 `SKILL.md`，明确 Skill 的输入/输出格式、任务目标/非目标、关键约束、执行流程
- 为实现 Skill 的既定目的，可以适当地编写 Python 脚本，用于在 Skill 执行过程中将一部分确定性的、重复性大的业务逻辑从 Agent LLM 的职责中 offload。不过需要注意，所有编写的脚本都需要在 `SKILL.md` 中显式说明其用途、调用方法和调用时机。

## 你不该做什么

- **避免过多依赖 Python 脚本**：本 Skill 要解决的问题十分复杂，必须借助 LLM 的语义理解能力进行。Python 脚本只能作为辅助，你不应该试图用脚本处理核心业务流程
- **避免生成不符合 Open Agent Skills 规范的文件**：Open Agent Skills 规范规定，一个 Skill 包中必须有一个位于包根目录的 `SKILL.md` 作为 Agent 直接读取的核心指令文件。核心指令文件不宜过长。按需执行的补充指令、参考文档等可放在 Skill 包中的 `references` 目录中（需要在 `SKILL.md` 中声明其用途及用法）；Python 脚本放在 Skill 包中的 `scripts` 目录中；其它资产文件可放在 Skill 包中的 `assets` 目录中。
- **避免在 `SKILL.md` 中添加对 Skill 执行没有帮助的信息**: `SKILL.md` 中应仅包含对 Skill 执行具有约束作用或帮助作用的指令。一切面向用户的提示、说明，以及错误的、自相矛盾的、模棱两可的指令均不应该出现在 `SKILL.md`中

## 你该怎么做（总体流程建议，非强制，灵活参考）

1. 制定实现方案：明确任务目标，进行任务拆解，制定实现路线图
2. 建立项目骨架，制定 `SKILL.md`大纲，拟定需要哪些脚本、承担哪些职责
3. 和用户交互，细化每一步方案，对方案中需要决策的地方询问用户，可以附带你的建议
4. 锁定方案后，开始按路线图实现

## 可以参考的文档

- `paper-reviewer/references/taxonomy.md`: 论文领域分类
- `paper-reviewer/references/general_framework.md`: 通用科研论文写作框架
- `paper-reviewer/references/experimental_observational_natural_science_writing_guide.md`: 实验 / 观察型自然科学论文写作指南
- `paper-reviewer/references/engineering_system_design_writing_guide.md`: 工程 / 系统 / 设计型论文写作指南
- `paper-reviewer/references/computational_algorithm_data_driven_writing_guide.md`: 计算 / 算法 / 数据驱动型论文写作指南
- `paper-reviewer/references/mathematical_theory_proof_writing_guide.md`: 数学 / 理论 / 证明型论文写作指南
- `paper-reviewer/references/medical_clinical_public_health_writing_guide.md`: 医学 / 临床 / 公共卫生论文写作指南
- `paper-reviewer/references/quantitative_social_and_behavioral_science_writing_guide.md`: 定量社会科学 / 行为科学论文写作指南
- `paper-reviewer/references/qualitative_interpretive_social_science_writing_guide.md`: 定性 / 解释型社会科学论文写作指南
- `paper-reviewer/references/humanities_textual_interpretation_historical_argumentation_writing_guide.md`: 人文学科 / 文本解释 / 历史论证型论文写作指南
- `paper-reviewer/references/law_normative_policy_analysis_writing_guide.md`: 法学 / 规范 / 政策分析型论文写作指南
- `references/review`: DeepScientist项目的自我评审 Skill，仅作参考（Skill的写作范式很有参考价值），不加入 Skill 包
- `references/literature-explainer`: 我写的文献解读问答 Skill，可以参考其中的记忆和证据验证模式
- `references/paper-condenser`: 我写的文献凝练转写 Skill，可以参考其中的轻量状态机模式

