# smart-search

> 一个让 Claude 真正会搜索的 Skill —— 强制多源交叉验证、反 SEO 过滤、内置偏见检测，彻底解决 AI 搜索"知道了但说错了"的问题。

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-blue)](https://agentskills.io)
[![兼容 Claude Code](https://img.shields.io/badge/Claude%20Code-原生支持-blueviolet)](https://code.claude.ai)
[![兼容 Cursor · Gemini CLI · Codex](https://img.shields.io/badge/Cursor%20%7C%20Gemini%20CLI%20%7C%20Codex-兼容-green)](https://agentskills.io)
[![License: Apache 2.0](https://img.shields.io/badge/许可证-Apache%202.0-brightgreen)](LICENSE)

[English → README.md](README.md)

---

## 痛点：Claude 搜索为什么经常不靠谱？

Claude 是优秀的分析师，但有一个结构性盲区：**它默认使用训练数据回答问题**，即使那些数据已经过时 12 到 24 个月。更糟糕的是，即便它真的去搜索，通常也会拿回这些东西：

- 📰 **SEO 内容农场**：标题是"2024年最佳工具 Top 10"，内容没有任何实测，全是广告位
- 🔄 **信源循环引用**：每篇文章都指向同一个原始来源，看起来多元实则单一
- 🌐 **单一文化圈视角**：地缘政治问题只给西方主流媒体观点，完全忽略其他视角
- 📣 **叙事而非分析**：接受表面的"官方说法"，不追问谁在说、谁受益、什么被隐瞒
- ❌ **虚假的确定性**：对有争议的问题给出单一结论，好像不存在任何分歧

你有没有问过 Claude"推荐一个 X 工具"，结果收到的是某个测评网站的软文总结？或者问一个国际事件，得到的是没有任何批判分析的单一视角？这就是没有 smart-search 时的状态。

---

## 这个 Skill 做了什么？

`smart-search` 是一个**搜索策略层**，在 Claude 回答任何研究类问题之前激活。它不新增工具，它改变的是 **Claude 思考搜索这件事的方式**。

安装一次，遇到搜索类请求自动触发，无需手动调用。

### 安装前后对比

| 没有 smart-search | 有 smart-search |
|---|---|
| 默认用训练数据，可能过时 1-2 年 | 先判断时效性，快变信息强制实时搜索 |
| 拿回 SEO 排名靠前的结果 | 优先 GitHub、Reddit、HN、一手来源 |
| 引用 1-2 个来源就下结论 | 至少 2 个独立来源交叉验证后才作结 |
| 输出单一自信结论 | 显式标注分歧，不掩盖争议 |
| 接受主流叙事 | 追问：谁在说？谁受益？什么被隐瞒了？ |
| 通用关键词搜索 | 结构化查询 + 反向搜索（问题/批评/替代品） |

---

## 五个核心行为

**① 时效分级** — 每次搜索前先判断信息"保鲜期"：政治事件要当天来源，技术趋势要 6 个月内，历史原理可以用训练数据。不再用过时信息装扮成实时答案。

**② 分场景信源路由** — 内置 5 个领域的信源矩阵：地缘政治（RAND/CFR/Polymarket）、技术工具（GitHub Stars/Reddit/HN）、投资金融（监管文件/官方数据）、生活消费（社区论坛）、AI 前沿（arXiv/实验室博客）。不同问题用对应的权威来源，而不是通用搜索。

**③ 反 SEO 搜索构造** — 明确避开"best / top / recommended"等 SEO 陷阱词。每次搜索都附加反向查询（`[话题] problems`、`[话题] criticism`、`[话题] alternatives`），把促销内容掩盖的信息翻出来。

**④ 利益层分析** — 对地缘政治和经济话题，Claude 被要求追问：*谁在说这句话？谁受益？什么被刻意省略？历史上有没有相似的模式？* 大多数 AI 工具只回答表面问题，这个 Skill 让 Claude 往深处挖一层。

**⑤ 置信度标注 + 矛盾显式呈现** — 每个主要结论都有高/中/低置信度标签。信源矛盾时，不做静默调和，而是并列呈现各方立场，让你自己判断。

---

## 安装方式

### Claude Code（推荐）

```bash
# 全局安装 —— 对你所有的 Claude Code 会话生效
git clone https://github.com/YOUR_USERNAME/smart-search ~/.claude/skills/smart-search

# 项目级安装 —— 仅对当前项目生效
git clone https://github.com/YOUR_USERNAME/smart-search .claude/skills/smart-search
```

克隆后 Claude Code 自动识别，无需重启。

### Claude.ai（网页版 / 桌面版）

1. 下载本仓库 ZIP（GitHub 页面 → **Code** → **Download ZIP**）
2. 解压后，把里面的 `smart-search/` 文件夹重新压缩成 ZIP
3. 打开 Claude.ai → **Settings → Features → Custom Skills → Upload**

> 需要 Pro、Max、Team 或 Enterprise 订阅计划。

### Cursor

```bash
cp -r smart-search ~/.cursor/skills/smart-search
```

### Gemini CLI

```bash
cp -r smart-search ~/.gemini/skills/smart-search
```

### OpenAI Codex CLI

```bash
cp -r smart-search ~/.codex/skills/smart-search
```

---

## 自动触发时机

只要请求包含以下类型的信号，Claude 就会自动加载本 Skill：

```
"搜索一下..."        "最新的...是什么"      "帮我找..."
"推荐一个..."        "对比 X 和 Y"          "分析一下...的局势"
"查一下..."          "现在...怎么样了"      "...是真的吗"
"研究一下..."        "为什么 X 会发生"      "有没有..."
```

不需要输入斜杠命令，由模型根据上下文自动判断触发。

---

## 文件结构

```
smart-search/
├── SKILL.md        ← Claude 运行时加载的指令文件
├── README.md       ← 英文文档
├── README.zh.md    ← 中文文档（本文件）
└── LICENSE         ← Apache 2.0
```

**SKILL.md 内容结构：**

| 章节 | 内容 |
|---|---|
| 第一步 — 启动检查 | 时效分级表；何时搜索、何时用训练数据 |
| 第二步 — 分场景信源矩阵（×5） | 5 个领域的权威信源：地缘、技术、金融、生活、AI 学术 |
| 第三步 — 搜索执行规范 | 关键词构造策略；反 SEO 词表；多轮搜索节奏 |
| 第四步 — 结果处理规范 | 置信度标注；矛盾信息处理；信息缺口声明 |
| 第五步 — 输出前偏见检查 | 6 项清单：来源多样性、过度自信、利益层分析 |
| 附：信源速查表 | 覆盖 5 个领域的常用可信来源 |

---

## 兼容性

| 工具 | 支持状态 |
|---|---|
| Claude Code | ✅ 原生支持，文件系统自动发现 |
| Claude.ai（Pro / Max / Team / Enterprise） | ✅ 通过 Settings → Features 上传 |
| Cursor | ✅ SKILL.md 标准 |
| Gemini CLI | ✅ SKILL.md 标准 |
| OpenAI Codex CLI | ✅ SKILL.md 标准 |
| Antigravity IDE | ✅ SKILL.md 标准 |
| Claude API | ✅ 通过 Skills API（`/v1/skills`） |

本 Skill 遵循 [Agent Skills 开放标准](https://agentskills.io)，该标准由 Anthropic 于 2025 年 12 月发布，OpenAI 随后也为 Codex CLI 采用了相同格式。同一份 `SKILL.md` 文件可跨工具直接使用。

---

## 零依赖

- 无需 API 密钥
- 无需外部服务
- 无可执行脚本 —— 纯指令文本
- 完全可审计：整个 Skill 就是一份可读的 Markdown 文件

---

## 参与贡献

欢迎提 Issue 和 PR。如果你想为某个特定领域增加信源矩阵（法律研究、医学文献、特定语言的本地化来源等），欢迎开 PR 贡献。

---

## 许可证

[Apache 2.0](LICENSE) —— 可自由使用、修改和再分发。注明出处不是必须的，但我们很感谢。
