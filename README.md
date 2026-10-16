# 中国法律法规与案例结构化语料库

> Structured corpus of Chinese laws, regulations, judicial interpretations and court cases in clean JSON.

**520 部法律、司法解释与行政法规（30,069 条逐条结构化，其中 517 部现行有效、3 部已公布尚未生效）+ 278 件最高人民法院指导性案例 + 445 件《最高人民法院公报》案例文书**，全部为干净的结构化 JSON，带效力状态、公布/施行日期与官方来源。

最近同步：2026-10-16。本仓由 [法脉](https://lttxzmj.github.io/lawpulse-site/) 数据管道脚本自动同步，法律随官方公布持续更新（计数由脚本生成，如与官方库有出入请提 Issue）。

## 内容

| 目录 | 内容 | 数量 |
| --- | --- | --- |
| `laws/` | 宪法 1 部、法律 312 部、司法解释 175 件、行政法规 32 件（其中 3 部已公布尚未生效），逐条结构化（编、章、节、条层级），含公布日期、施行日期、效力状态、制定机关 | 520 |
| `guiding-cases/` | 最高人民法院指导性案例（官方现行发布的全部 278 件，含关键词、裁判要点、基本案情、裁判结果、裁判理由、关联法条） | 278 |
| `gazette-cases/` | 《最高人民法院公报》裁判文书选登与案例（判决文书正文与客观元数据） | 445 |

## 数据质量

- 法律文本全部取自[国家法律法规数据库](https://flk.npc.gov.cn/)官方 docx，逐部人工核对名称与效力状态，不含失效法规；诈骗、盗窃、毒品、贪污贿赂等常用罪名的数额与量刑标准司法解释成套收录，工伤保险条例、劳动合同法实施条例等高频行政法规在列。
- 案例取自最高人民法院官方站点，解析零缺段（四代页面排版差异已统一处理）。
- 条文使用稳定 ID（如 `civil-code-0577` = 民法典第五百七十七条），跨版本可引用。
- 数据持续维护：法律随官方公布更新，案例随官方发布更新。

## JSON 结构示例

```jsonc
// laws/*.json（与实际字段一致，可直接照此取值）
{
  "id": "civil-code",
  "title": "中华人民共和国民法典",
  "category": "法律",                 // 宪法 | 法律 | 司法解释 | 行政法规
  "issuingAuthority": "全国人民代表大会",
  "promulgationDate": "2020-05-28",
  "effectiveDate": "2021-01-01",
  "status": "effective",              // effective 现行有效 | pending 已公布尚未生效
  "articleCount": 1260,
  "sections": [{ "id": "civil-code-section-0001", "title": "第一编总则", "level": 1, "path": [] }],
  "articles": [{
    "id": "civil-code-0001",
    "articleNumber": 1,
    "displayNumber": "第一条",
    "path": ["第一编总则", "第一章基本规定"],
    "text": "…"
  }]
}
```

```bash
# 例：取民法典第五百七十七条
jq '.articles[] | select(.id=="civil-code-0577")' laws/civil-code.json
```

## For researchers & legal-AI builders (English)

Structured corpus of Chinese law in clean JSON, released under CC0: **520 statutes,
judicial interpretations and administrative regulations** (article-level, 30,069 articles,
with status and effective dates, incl. 3 promulgated-but-not-yet-effective, curated
from official sources), **278 SPC guiding cases** (holdings / facts / reasoning as
separate fields) and **445 SPC Gazette case documents**. Stable article IDs
(`civil-code-0577` = Civil Code art. 577) make it suitable for legal RAG, retrieval
benchmarks and citation-grounded generation.

```python
# RAG 检索粒度示例：一条 = 一个法条，天然的 chunk 边界
import json, glob
chunks = []
for path in glob.glob("laws/*.json"):
    law = json.load(open(path))
    if isinstance(law, dict) and "articles" in law:
        for art in law["articles"]:
            chunks.append({"id": art["id"], "text": f'{law["title"]} {art["displayNumber"]} {art["text"]}'})
print(len(chunks))  # 30,069
```

## API（免费 JSON，经 jsDelivr CDN）

无需鉴权、支持 HTTPS 与 CORS，可直接在前端/脚本/AI 代理中调用：

```text
# 法律索引（520 部：slug/标题/条数）
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/laws/index.json

# 某部法律全文（逐条结构化），如民法典：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/laws/civil-code.json

# 指导性案例 / 公报案例（按文件名取件）：
https://cdn.jsdelivr.net/gh/lttxzmj/chinese-law-corpus@master/guiding-cases/guiding-1.json
```

AI 助手可直接使用配套 MCP 服务器 [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)：`npx -y github:lttxzmj/chinese-law-mcp`。

## 贡献与反馈

- 发现缺漏、错字或效力状态标注问题：提 Issue（给出官方来源链接最好），会在下次同步修复；
- 希望收录某部法规/司法解释：Issue 里说明用途与官方来源即可；
- 用本语料做了项目（RAG、评测集、工具）？欢迎提 PR 登记到下方生态清单。

## 生态

- [法脉桌面端](https://lttxzmj.github.io/lawpulse-site/)（macOS / Windows）：离线法律库 + 法条笔记 + AI 合同审查，本语料的上游；
- [网页版法规库](https://lttxzmj.github.io/lawpulse-site/laws/index.html)：每条法条一个可直链引用的页面；
- [chinese-law-mcp](https://github.com/lttxzmj/chinese-law-mcp)：把本语料接入任意支持 MCP 的 AI 客户端。

## 版权与免责

- 法律、法规与司法文书依《中华人民共和国著作权法》第五条不适用著作权保护；本仓库对数据的整理与结构化部分以 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) 释出，可自由使用（含商用），无需署名。
- 《公报》案例仅收录司法文书内容与客观元数据，编辑加工的「裁判摘要」未收录。
- 本仓库为非官方整理，正式引用请以[国家法律法规数据库](https://flk.npc.gov.cn/)与最高人民法院官方发布为准；如发现数据错误请提 Issue。

## 关于

本语料库由 **[法脉 LawPulse](https://lttxzmj.github.io/lawpulse-site/)** 整理与维护——一款给中国执业律师的本地优先桌面研究工具（离线法律库 + 法条笔记 + 合同审查，数据不出本机）。这份数据就是它的内置法律库，欢迎法律科技项目取用；觉得有用请点个 star，让更多人找到它。
