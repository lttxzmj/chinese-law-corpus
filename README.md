# 中国法律法规与案例结构化语料库

> Structured corpus of Chinese laws, regulations, judicial interpretations and court cases in clean JSON.

## 本仓库已迁移 → [chinese-law-dataset](https://github.com/lttxzmj/chinese-law-dataset)

数据已整体迁移到新仓库并在那里持续更新：

**https://github.com/lttxzmj/chinese-law-dataset**

内容与口径不变：**1513 部现行法律、司法解释与行政法规（56,182 条逐条结构化，带效力状态、公布/施行日期与官方来源）+ 278 件最高人民法院指导性案例 + 445 件《最高人民法院公报》案例文书**，整理与结构化部分以 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) 释出，可自由使用（含商用）。

## jsDelivr API 新地址

原来形如 `…/gh/lttxzmj/chinese-law-corpus@master/…` 的链接，把仓库名换成 `chinese-law-dataset` 即可：

```text
# 法律索引（slug/标题/条数）
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-dataset@master/laws/index.json

# 某部法律全文（逐条结构化），如民法典：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-dataset@master/laws/civil-code.json

# 指导性案例 / 公报案例（按文件名取件）：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-dataset@master/guiding-cases/guiding-1.json
```

AI 助手可直接使用配套 MCP 服务器 [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)（已指向新仓库）：`npx -y github:lttxzmj/chinese-law-mcp`。

## For researchers & legal-AI builders (English)

This corpus has moved to **[chinese-law-dataset](https://github.com/lttxzmj/chinese-law-dataset)**: 1,513 current Chinese statutes, judicial interpretations and administrative regulations (56,182 articles, article-level JSON with status and effective dates), 278 SPC guiding cases and 445 SPC Gazette case documents, released under CC0. Stable article IDs (`civil-code-0577` = Civil Code art. 577) make it suitable for legal RAG, retrieval benchmarks and citation-grounded generation.

## 生态

- [chinese-law-dataset](https://github.com/lttxzmj/chinese-law-dataset)：本语料库的新家，数据在那里持续更新；
- [法脉桌面端](https://lttxzmj.github.io/lawpulse-site/)（macOS / Windows）：离线法律库 + 法条笔记 + AI 合同审查，本语料的上游；
- [网页版法规库](https://lttxzmj.github.io/lawpulse-site/laws/index.html)：每条法条一个可直链引用的页面；
- [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)：把本语料接入任意支持 MCP 的 AI 客户端。

## 版权与免责

- 法律、法规与司法文书依《中华人民共和国著作权法》第五条不适用著作权保护；本仓库及新仓库对数据的整理与结构化部分以 CC0 1.0 释出。
- 本仓库为非官方整理，正式引用请以[国家法律法规数据库](https://flk.npc.gov.cn/)与最高人民法院官方发布为准。
