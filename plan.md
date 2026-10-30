# AI 系统学习计划书 — 计划记录

- 类型：交互式学习计划 / 路线图文档（路线 B 算法研究为主体，路线 A 应用开发穿插插入，12 个月 48 周每日任务）
- 受众：有 C++ 背景的工程师，个人自学使用
- 语言：中文

视觉决策：
- Color preset: Business Blue — cue: 结构化技术学习计划，正式、面向工程师的严肃规划
- Intro mode: contained — cue: 正式技术报告默认，无 Hero 图（通用主题，走无图路径）

结构：
1. Intro（含总进度、开始日期设置）
2. 总览：使用说明 / 12 个月路线图 / 单主体结构说明（B 主体 + A 穿插）/ 周节奏与时间预算
3. 环境与资源清单
4. Q1–Q4 四个季度章节（每季度：目标、月、周、每日任务、毕业标准）
5. 风险与调整策略 + 学习心法
6. Sources

交互（原生 JS + localStorage，无外部依赖）：
- 每日任务勾选、周/月/季度/总进度统计
- 设定开始日期 → 自动定位当前周
- 周折叠展开；数据与渲染在 assets/app.js，HTML 为静态骨架

无 ECharts（无量化图表）；路线图时间线用 HTML/CSS；无图片资源。

## 2026-10-22 结构调整：双线并行 → 路线 B 主体（用户要求）

用户反馈：「优先完成算法研究部分，A 先放一放，或者把 A 插进来学习，主体还是 B」。

调整后的编排（app.js 全量重写，HTML 展示层同步更新）：
- Q1（周 1–12）共用地基不变（Python / 数学 / ML / DL）
- Q2（周 13–24）B 主线：Transformer 吃透 → 优化理论 → 从零预训练 mini-GPT（数据工程 / tokenizer / scaling / 现代架构）→ 分布式训练 + SFT/LoRA → RLHF/DPO 对齐；W24 插入 API/Prompt 两个速成日（route: both）
- Q3（周 25–36）B 深水：论文三遍读法与精读 → W27–28 插入路线 A 应用核心两周（RAG / 最小 Agent / 微调部署，W27 route: a）→ 深耕方向选定与两代方法复现 → 自主改进实验 → 三周研究毕业项目
- Q4（周 37–48）B 冲刺 + A 融合：前沿专题 + 评估工程（lm-eval-harness / LLM-as-Judge / CI 回归）→ Capstone 三周（主实验 / 消融 / 工程化发布，量化与 C++ 推理服务）→ 求职冲刺（两版简历 / 八股 / 模拟面试 / 投递）→ 知识终检与毕业周
- 作品集 6 个 → 7 个（新增研究毕业项目）
- 存储键 ailp-progress → ailp-progress-v2（数据结构变化，v1 勾选记录不迁移）

校验记录（临时脚本，已删除）：
- validate.cjs：季度 q1–q4 / 12 月 / 48 周周号连续无重复 / 每周 7 天 / 627 任务非空 / route 合法 / HTML 容器与静态文案一致 — ALL PASSED
- smoke.cjs（DOM 桩）：app.js 全程执行无异常，四季度各渲染 12 周，周号唯一，进度写入 v2 键 — SMOKE PASSED

## 2026-10-22 增强：每周资源链接与实操项目建议（用户要求）

用户要求：「为路线 B 补充具体的每日学习资源链接和实操项目建议」。

实现方式（app.js 新增 RES 表 + weekHtml 渲染扩展 + HTML 样式）：
- RES 表：周号 → { res: [[标题, URL, 适用日], ...], proj: '实操建议' }，48 周全覆盖，共 106 条链接（唯一 URL 100 个）
- 适用日标注 D1–D7 对应周一至周日，与每日任务对齐
- 每周任务列表底部渲染「资源」链接行 + 「实操项目」建议行（week-extra 区块，dashed 分隔线区分任务区）
- 外链统一 target="_blank" rel="noopener"；移动端 wk-row 降为单列
- HTML 总览新增一段使用说明

链接验证（Explore 子代理逐一 WebFetch 验证）：
- llama.cpp 已从 ggerganov 迁移至 ggml-org/llama.cpp（已修正）
- CS336 当前主页 http://cs336.stanford.edu/（已修正）
- 其余 18 项全部有效：HF LLM Course、李沐论文精读 B 站空间、modded-nanogpt、lm-evaluation-harness、alignment-handbook、Coursera ML、CS224n/231n、Karpathy backprop 博客、Illustrated GPT-2、hh-rlhf、Transformer Explainer、DDP 教程、zh.d2l.ai、minbpe、3B1B、llm.c
- 其余论文 arXiv 链接（Attention/Llama/DeepSeek/DPO/RoPE/FlashAttention/Chinchilla/PointNet/R1/CoT/CAI/MMLU/GSM8K/C-Eval/MT-Bench 等）按 arXiv ID 规则给出

资源选型原则：
- 资源与当日任务强绑定（D 标注），不堆砌通用清单
- 实操建议含具体选型（Qwen2.5 基座、ModelNet40 数据集、AutoDL 算力预算）与跨周复用关系（W16→W28、W24→W38、W26→W35）
- 复盘周/求职周链接从简，以方法论建议为主

校验记录（verify-res.cjs，已删除）：
- 48 周 RES 全覆盖、proj 非空、res 结构合法
- 106 条链接格式合法（https 起始、无空格中文引号）、D 标注格式合法
- 渲染冒烟：48 个 week-extra 区块、链接数与数据一致、锚点抽查通过、noopener 齐全 — ALL PASSED
