# Research Skills for Life Science

三个面向生命科学科研工作的独立 AI Skills：

1. `experimental-method-research`：实验方法调研——回答“怎么做”。
2. `mechanism-research`：科学机制调研——回答“为什么、凭什么”。
3. `field-onboarding`：领域快速入门——回答“这个领域是什么、从哪里学起”。

本套 Skills 借鉴 [bear-research-skills](https://github.com/fei0810/bear-research-skills) 的模块化设计、检索透明度、证据账本、正反证据、概念地图与文献溯源思路，并针对生命科学实验研究重新组织。没有复制其 SciMaster CLI 实现；默认采用 Google Scholar 作为文献发现入口，并用 PubMed/PMC、期刊官网、DOI 页面和 Supplementary Information 核验。

## 1. 怎么选

| 你的问题 | 使用 |
|---|---|
| 某个实验怎么做？哪种 protocol 最适合我的样本？ | `experimental-method-research` |
| 某个分子、RNA、蛋白或染色质标记如何发挥作用？ | `mechanism-research` |
| 我对一个新方向不熟，想快速建立知识框架 | `field-onboarding` |

组合工作流：
- 陌生领域 → 具体机制：先 `field-onboarding`，再 `mechanism-research`。
- 机制假设 → 实验验证：先 `mechanism-research`，再 `experimental-method-research`。
- 实验方法需要机制依据：先做方法调研；若关键参数依赖生物学机制，再补做机制调研。

## 2. 安装到 Codex（macOS）

```bash
mkdir -p "$HOME/.agents/skills"
```

解压 ZIP 后，假设解压目录是 `/Users/lidanfeng/Downloads/research-skills-v1/`。一次安装全部三个：

```bash
cp -R "/Users/lidanfeng/Downloads/research-skills-v1/skills/experimental-method-research" "$HOME/.agents/skills/"
cp -R "/Users/lidanfeng/Downloads/research-skills-v1/skills/mechanism-research" "$HOME/.agents/skills/"
cp -R "/Users/lidanfeng/Downloads/research-skills-v1/skills/field-onboarding" "$HOME/.agents/skills/"
```

检查：

```bash
ls "$HOME/.agents/skills"
```

应看到 `experimental-method-research`、`mechanism-research`、`field-onboarding`。若 Codex 没有立即识别，重启 Codex 后再检查 Skill 列表。

显式调用：

```text
$experimental-method-research
$mechanism-research
$field-onboarding
```

更新 Skill 时，建议先备份旧目录，再用新版目录替换，避免旧文件残留。

## 3. Google Scholar 与全文阅读策略

Google Scholar 是首选文献发现入口，但不假定每个 AI 环境都能稳定访问它。
- 能访问 Scholar：记录实际搜索式、日期、筛选条件和结果范围。
- 遇到验证码、访问限制或浏览器不可用：不绕过验证、不声称已检索；改用 PubMed、Europe PMC、PMC、Crossref、期刊官网、预印本平台，或请用户导出 Scholar 结果/上传 PDF。
- Scholar 搜索结果只用于发现文献，不等于已经核验论文内容。
- 关键论文优先读取全文、Methods、Supplementary Methods、Figure legends 和补充图表。
- 只有摘要时标记 `abstract-only`，不得写成“已全文精读”。

## 4. 默认工作量

| Skill | 默认检索范围 | 精读策略 | 主要交付 |
|---|---|---|---|
| 实验方法 | 6–10 组不同角度检索式 | 逐篇阅读最匹配的 5–12 篇；分批进行 | 方法比较表、推荐 protocol、优化矩阵 |
| 机制调研 | 6–10 组正交检索式 | 精读 5–10 篇关键原始研究 | 机制图、证据矩阵、竞争模型 |
| 领域入门 | 6–10 组主题检索式 | 精读 3–5 篇核心论文，其余先摘要筛选 | 知识地图、发展时间线、阅读路径 |

数量是默认工作量，不是完整性保证。用户明确要求更多或更少时按任务调整。

## 5. 通用原则

- 不编造论文、作者、DOI、实验参数、序列或图表结论。
- 每个关键结论回指具体论文 ID；重要结论尽量定位到 Figure/Table/Methods。
- 区分原文直接报告、作者解释、模型推断和 AI 提出的建议。
- 保留反面证据、零结果方向和检索缺口。
- 不把“本次没搜到”写成“领域里不存在”。
- 不把相关性、共定位或 ChIP 富集直接写成因果机制。
- 不把某篇论文的条件直接照搬到不同物种、细胞、发育阶段或检测终点。

## 6. 目录结构

```text
research-skills-v1/
├── README.md
├── PROMPTS.md
├── NOTICE.md
├── LICENSE
└── skills/
    ├── experimental-method-research/SKILL.md
    ├── mechanism-research/SKILL.md
    └── field-onboarding/SKILL.md
```

## 7. 参考与许可

设计思路受到 [fei0810/bear-research-skills](https://github.com/fei0810/bear-research-skills) 启发。本套改编材料按 CC BY-NC-SA 4.0 发布，详见 `NOTICE.md` 与 `LICENSE`。
