# 安全生产标准顾问（safety-standards-advisor）

一个 WorkBuddy 技能：以**国家法律法规为基础、以各行业领域标准（GB / AQ / TSG / JGJ 等）为细则**，帮助解决工作中遇到的安全生产问题。

> 设计原则：**法律层级优先** —— 法律 > 行政法规 > 部门规章 > 规范性文件 > 强制性国标 > 行业标准。
> 回答任何安全生产问题时，先给适用的法定义务来源，再补对应的技术标准条款。

---

## 能做什么

- 按主题回答安全生产合规要求（用电安全、高处作业、有限空间、特种设备、粉尘防爆、机械安全、危化品、职业健康、建筑施工、消防、应急管理等）
- 检索适用的**法律法规**（按四级法律渊源排序）与**行业标准**（按标准号 / 关键词）
- 读取具体标准的正文要点（标准库文字版可直接引用；扫描件无文字层会提示找文字版）
- 给出「法定义务 → 标准条款 → 落实建议」的可执行回答

## 安装

把整个 `safety-standards-advisor` 目录复制到你的 WorkBuddy 技能目录：

```bash
# Windows
cp -r safety-standards-advisor "$USERPROFILE/.workbuddy/skills/"

# macOS / Linux
cp -r safety-standards-advisor ~/.workbuddy/skills/
```

在 WorkBuddy 对话中直接说「安全生产标准顾问」或描述你的安全生产问题即可触发。

## 数据资产（随技能附带的索引，不含标准全文）

| 文件 | 说明 |
| --- | --- |
| `references/标准目录.csv` | 全量标准索引（标准号 / 标题 / 主题 / 格式 / 相对路径），约 7000 条 |
| `references/stdno_index.json` | 标准号 → 文件路径 的去重映射 |
| `references/law_index.json` | 108 部国家法律法规四级分层索引（法律 / 行政法规 / 部门规章 / 规范性文件） |
| `references/topics/*.md` | 11 篇主题手册（含「核心适用法律法规」章节）+ 法律层级速查 |
| `scripts/lookup.py` | 检索：法律法规 / 标准号 / 关键词 / 正文 |
| `scripts/read_std.py` | 读取标准正文（自动适配 .docx 副本、跳过加密件） |

## 用自己的标准库重建索引（可选）

技能自带的 `标准目录.csv` 等索引是从作者整理好的标准库蒸馏而来。如果你想**用自己的标准库**重建：

```bash
python scripts/setup.py --root "D:/你的标准库"
```

它会遍历目录、用正则识别标准号、按文件夹推断主题，生成 `references/标准目录.csv` 和 `references/stdno_index.json`。

如需正文级检索，再把你的标准库抽取成文本并生成 `index.jsonl`（参考脚本 `scripts/extract_text.py`），用环境变量指定：

```bash
export SAFETY_STANDARDS_ROOT="D:/你的标准库"
export SAFETY_CORPUS="D:/你的语料库"   # 含 index.jsonl
```

## 合规与版权声明

- 国家/行业标准**受版权保护**，本技能**只做索引与要点归纳，不随附、不重新分发标准全文**。
- 标准正文请通过正规渠道获取（国家标准全文公开系统、行业标准出版机构等）。
- 本技能输出**仅供参考**，不能替代具有资质的安全评价、法律意见或现场专业判断。涉及重大安全决策，请依规委托有资质的机构。

## 目录结构

```
safety-standards-advisor/
├── SKILL.md                 # 技能定义与工作流
├── README.md
├── references/
│   ├── 标准目录.csv
│   ├── stdno_index.json
│   ├── law_index.json
│   └── topics/*.md
└── scripts/
    ├── lookup.py
    ├── read_std.py
    ├── extract_text.py
    └── setup.py
```
