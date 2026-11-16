# 中国法律法规与案例结构化语料库

> Structured corpus of Chinese laws, regulations, judicial interpretations and court cases in clean JSON.

## 本仓库已迁移 → Gitee [chengzi_h/chinese-law-corpus](https://gitee.com/chengzi_h/chinese-law-corpus)

数据已整体迁移到 Gitee 并在那里持续更新：

**https://gitee.com/chengzi_h/chinese-law-corpus**

内容与口径不变：**1513 部现行法律、司法解释与行政法规（56,182 条逐条结构化，带效力状态、公布/施行日期与官方来源）+ 278 件最高人民法院指导性案例 + 445 件《最高人民法院公报》案例文书**，整理与结构化部分以 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) 释出，可自由使用（含商用），无需署名。

## 怎么取数据

推荐直接克隆（匿名可用，全量约 67MB）：

```bash
git clone --depth 1 https://gitee.com/chengzi_h/chinese-law-corpus.git
# 例：取民法典第五百七十七条
jq '.articles[] | select(.id=="civil-code-0577")' chinese-law-corpus/laws/civil-code.json
```

单文件在线直读走 Gitee raw 路径（形如 `https://gitee.com/chengzi_h/chinese-law-corpus/raw/master/laws/civil-code.json`）；原 jsDelivr 链接（`…/gh/lttxzmj/chinese-law-corpus@master/…`）已随迁移停用。

## For researchers & legal-AI builders (English)

This corpus has moved to **[Gitee: chengzi_h/chinese-law-corpus](https://gitee.com/chengzi_h/chinese-law-corpus)**: 1,513 current Chinese statutes, judicial interpretations and administrative regulations (56,182 articles, article-level JSON with status and effective dates), 278 SPC guiding cases and 445 SPC Gazette case documents, released under CC0. Stable article IDs (`civil-code-0577` = Civil Code art. 577) make it suitable for legal RAG, retrieval benchmarks and citation-grounded generation. Anonymous `git clone` of the Gitee repository is the recommended way to fetch the data.

## 生态

- [Gitee 数据仓](https://gitee.com/chengzi_h/chinese-law-corpus)：本语料库的新家，数据在那里持续更新；
- [法脉桌面端](https://lttxzmj.github.io/lawpulse-site/)（macOS / Windows）：离线法律库 + 法条笔记 + AI 合同审查，本语料的上游；
- [网页版法规库](https://lttxzmj.github.io/lawpulse-site/laws/index.html)：每条法条一个可直链引用的页面；
- [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)：把本语料接入任意支持 MCP 的 AI 客户端。

## 版权与免责

- 法律、法规与司法文书依《中华人民共和国著作权法》第五条不适用著作权保护；本仓库及 Gitee 新仓对数据的整理与结构化部分以 CC0 1.0 释出。
- 本仓库为非官方整理，正式引用请以[国家法律法规数据库](https://flk.npc.gov.cn/)与最高人民法院官方发布为准。
