# 中国法律法规与案例结构化语料库

> Structured corpus of Chinese laws, judicial interpretations and court cases in clean JSON.

**412 部现行有效法律与司法解释（26,000+ 条逐条结构化）+ 278 件最高人民法院指导性案例 + 445 件《最高人民法院公报》案例文书**，全部为干净的结构化 JSON，带效力状态、公布/施行日期与官方来源。

## 内容

| 目录 | 内容 | 数量 |
| --- | --- | --- |
| `laws/` | 现行有效国家法律 300 部 + 司法解释 112 件，逐条结构化（编、章、节、条层级），含公布日期、施行日期、效力状态、发布机关 | 412 |
| `guiding-cases/` | 最高人民法院指导性案例全量（含关键词、裁判要点、基本案情、裁判结果、裁判理由、关联法条） | 278 |
| `gazette-cases/` | 《最高人民法院公报》裁判文书选登与案例（判决文书正文与客观元数据） | 445 |

## 数据质量

- 法律文本全部取自[国家法律法规数据库](https://flk.npc.gov.cn/)官方 docx，逐部人工核对名称与效力状态，不含失效法规。
- 案例取自最高人民法院官方站点，解析零缺段（四代页面排版差异已统一处理）。
- 条文使用稳定 ID（如 `civil-code-0577` = 民法典第五百七十七条），跨版本可引用。
- 数据持续维护：法律季度更新，案例随官方发布更新。

## JSON 结构示例

```jsonc
// laws/*.json
{
  "id": "civil-code",
  "title": "中华人民共和国民法典",
  "issuingAuthority": "全国人民代表大会",
  "promulgationDate": "2020-05-28",
  "effectiveDate": "2021-01-01",
  "status": "现行有效",
  "articleCount": 1260,
  "articles": [{ "id": "civil-code-0001", "number": "第一条", "text": "…" }]
}
```

```bash
# 例：取民法典第五百七十七条
jq '.articles[] | select(.id=="civil-code-0577")' laws/civil-code.json
```

## For researchers & legal-AI builders (English)

Structured corpus of Chinese law in clean JSON, released under CC0: **412 statutes
and judicial interpretations in force** (article-level, 26k+ articles, with status
and effective dates, curated from official sources), **278 SPC guiding cases**
(holdings / facts / reasoning as separate fields) and **445 SPC Gazette case
documents**. Stable article IDs (`civil-code-0577` = Civil Code art. 577) make it
suitable for legal RAG, retrieval benchmarks and citation-grounded generation.

```python
# RAG 检索粒度示例:一条 = 一个法条,天然的 chunk 边界
import json, glob
chunks = []
for path in glob.glob("laws/*.json"):
    law = json.load(open(path))
    if isinstance(law, dict) and "articles" in law:
        for art in law["articles"]:
            chunks.append({"id": art["id"], "text": f'{law["title"]} {art["number"]} {art["text"]}'})
print(len(chunks))  # 26,000+
```

## API（免费 JSON，经 jsDelivr CDN）

无需鉴权、支持 HTTPS 与 CORS，可直接在前端/脚本/AI 代理中调用：

```text
# 法律索引（412 部：slug/标题/条数）
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/laws/index.json

# 某部法律全文（逐条结构化），如民法典：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/laws/civil-code.json

# 指导性案例 / 公报案例（按文件名取件）：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/guiding-cases/guiding-1.json
```

AI 助手可直接使用配套 MCP 服务器 [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)：`npx -y github:lttxzmj/chinese-law-mcp`。

## 版权与免责

- 法律、法规与司法文书依《中华人民共和国著作权法》第五条不适用著作权保护；本仓库对数据的整理与结构化部分以 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) 释出，可自由使用（含商用），无需署名。
- 《公报》案例仅收录司法文书内容与客观元数据，编辑加工的「裁判摘要」未收录。
- 本仓库为非官方整理，正式引用请以[国家法律法规数据库](https://flk.npc.gov.cn/)与最高人民法院官方发布为准；如发现数据错误请提 Issue。

## 关于

本语料库由 **[法脉 LawPulse](https://lttxzmj.github.io/lawpulse-site/)** 整理与维护——一款给中国执业律师的本地优先桌面研究工具（离线法律库 + 法条笔记 + 合同审查，数据不出本机）。这份数据就是它的内置法律库，欢迎法律科技项目取用；觉得有用请点个 star，让更多人找到它。
