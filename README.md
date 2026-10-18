# LGD Skills Ecosystem Registry · 技能生态聚合索引站

[![Made for GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-static--site-0078d4.svg)](https://zhaoxinghua09-cell.github.io/lgd-skills-index/)
[![Bilingual](https://img.shields.io/badge/i18n-English%20%7C%20中文-brightgreen.svg)](#)
[![Packages](https://img.shields.io/badge/registry-187%20packages-informational.svg)](#)
[![Practice lines](https://img.shields.io/badge/lines-6-8a2be2.svg)](#)
[![AI-protocol ready](https://img.shields.io/badge/AI%20protocol-187%2F187%20ready-2ea44f.svg)](#)
[![Homepage](https://img.shields.io/badge/live-zhaoxinghua09--cell.github.io-b8894a.svg)](https://zhaoxinghua09-cell.github.io/lgd-skills-index/)
[![llms.txt](https://img.shields.io/badge/AI--friendly-llms.txt-101E2C.svg)](llms.txt)

> 一个纯静态、零依赖的双语公开注册站：把面向治理的 **187 个 Agent 技能包** 按六条业务线聚合成一个可搜索、可筛选、机器可读的统一入口。
> A zero-dependency, bilingual static registry: one open entry point to **187 governance-oriented agent skill packages**, organised across six practice lines, with search, filters and machine-readable data.

**在线站点 / Live site**：<https://zhaoxinghua09-cell.github.io/lgd-skills-index/>

这是一个 **GitHub Pages 静态站点仓**（无后端、无构建步骤、无 npm 依赖）。仓内根目录的 `index.html` 即整站：内嵌一份 `DATA` JSON（技能注册表 + 公开资产清单），由浏览器端原生 JavaScript 渲染出统计条、业务线占比条形图、可搜索筛选的技能表与公开资产卡片。

---

## ✨ 特性 / Features

- **187 个技能包统一登记**：SK-001 至 SK-187，全部带机器可读的 SKILL.md 协议契约（何时用 / 用法 / 流程）。
- **六条业务线编排**：L1 理论线(38)、L2 产品线(22)、L3 评测线(12)、L4 生态线(8)、L5 监管线(13)、L6 基础设施线(94)。
- **双语界面**：英文与中文逐段对照，面向国内外 Agent 生态与检索入口。
- **可交互筛选**：按业务线、AI 协议达标状态、可执行状态筛选，并按包名 / slug / ID 关键词搜索。
- **公开入口不臆造**：「Public entry」仅在来源索引核对过远端 URL 时给出；本地暂存的包显示中性的「待发布」标记，不编造链接。
- **脱敏默认开启**：页面不含本地绝对路径、凭据或内部代号；含代号的远端链接以中性包名展示。
- **三个方法论合集**：GovernanceOS、WhoIs agent、PromptShield 各为一条生命周期叙事，子技能按 slug 引用。
- **SEO 就绪**：自带 `robots.txt` 与 `sitemap.xml`，便于搜索引擎与 AI 抓取。
- **零运行时**：打开 `index.html` 即可用，无需安装任何依赖、无需联网构建。

---

## 🚀 快速开始 / Quick Start

前置：一个现代浏览器即可。本仓是静态站点，**不需要安装任何运行时或依赖**。

```bash
# 1. 克隆本仓（浅克隆即可）
git clone https://github.com/zhaoxinghua09-cell/lgd-skills-index.git
cd lgd-skills-index

# 2. 直接用浏览器打开站点首页
#    Windows:
start index.html
#    macOS:
open index.html
#    Linux:
xdg-open index.html
```

或者，直接访问已部署的在线版本：

```text
https://zhaoxinghua09-cell.github.io/lgd-skills-index/
```

打开后，你可以：

1. 在顶部搜索框按 **包名 / slug / ID**（如 `prompt-shield`、`SK-091`）检索；
2. 用业务线、AI 协议、可执行状态三组按钮筛选；
3. 在「Public assets · 公开资产入口」卡片中查看每个公开资产的已核对远端 URL、许可证与可复现命令。

---

## 🧰 用法示例 / Examples

技能注册表以 `var DATA = {...}` 的形式内嵌在 `index.html` 末尾的 `<script>` 中。你可以用脚本直接抽取并统计它，而不必点开浏览器：

```bash
# 用 python 从 index.html 抽取内嵌 JSON，并统计技能包数量
python - <<'PY'
import re, json
html = open('index.html', encoding='utf-8').read()
m = re.search(r'var DATA = (\{.*?\});\s*\nvar LINE_LABEL', html, re.S)
data = json.loads(m.group(1))
print('total packages:', data['stats']['total'])
print('published on ModelScope:', data['stats']['ms_published'])
print('with runnable scripts:', data['stats']['executable'])
PY
```

只列出「已发布到 ModelScope 且含可执行脚本」的技能包：

```bash
python - <<'PY'
import re, json
html = open('index.html', encoding='utf-8').read()
data = json.loads(re.search(r'var DATA = (\{.*?\});\s*\nvar LINE_LABEL', html, re.S).group(1))
for s in data['skills']:
    if s['exe'] and s['pub'] == 'ms':
        print(s['id'], s['slug'], '->', s['url'])
PY
```

抓取线上站点首页（确认部署可达）：

```bash
curl -sS https://zhaoxinghua09-cell.github.io/lgd-skills-index/ -o live.html
grep -c "SK-" live.html   # 应能看到 SK- 编号条目
```

---

## 📁 仓库结构 / Repository layout

```text
lgd-skills-index/
├── index.html            # 站点首页（唯一渲染入口，内嵌 DATA JSON）
├── lgd-skills-index.html # 同名入口副本（历史保留，内容与 index.html 一致）
├── robots.txt           # 爬虫规则 + sitemap 指向
├── sitemap.xml          # 站点地图
├── README.md            # 本文件
├── README.en.md         # 英文版说明
├── llms.txt             # 给 AI 的最小索引（llms.txt 标准）
├── llms-full.txt        # 给 AI 的完整文本
├── AGENTS.md            # 给 AI Agent 的工作指引
├── SECURITY.md          # 安全策略
└── CONTRIBUTING.md      # 贡献 / 勘误指引
```

---

## 📊 数据快照 / Data snapshot

- 数据基准日：**2026-10-16**（头部标注 `Data as of 2026-10-16`）。
- 技能包总数：**187**（SK-001 ~ SK-187）。
- AI 协议达标：187/187；含可执行脚本：142；已发布到公开 ModelScope 远端：152；本地就绪待发布：35。
- 公开资产索引：24 条标记「公开就绪」（来源摘要行写 20，页面按枚举清单 24 呈现）。
- 数量均由来源注册表实际统计得出，而非估算。

---

## 🔒 安全 / Security

如发现站点被注入恶意链接、页面泄漏敏感信息，或本仓内容存在安全问题，请按 [`SECURITY.md`](SECURITY.md) 私下联系维护者，不要在公开 issue 中披露。

## 🤝 贡献 / Contributing

本仓是只读性质的注册展示站。若你发现条目错误、链接失效或建议增补条目，请参阅 [`CONTRIBUTING.md`](CONTRIBUTING.md) 的勘误流程。

## License / 许可

**本仓库当前未附 LICENSE 文件。** 仓库内 `index.html` 所登记的每个技能包 / 资产各自带有其独立许可证（例如 ModelScope 上的各技能仓、`silent-failure-catalog` 的 MIT + ARC、`lgd-theory` 的 CC-BY-4.0 等），本索引站本身不主张任何额外的著作权或许可口径。

在引用、转载或基于本站数据做二次分发前，请先联系维护者确认口径（见下方安全 / 贡献段邮箱），不要臆定本索引站的授权状态。

## ⚠️ 免责声明

本页内容为公开技能生态的聚合登记与转述，不构成对任何具体技能包质量、合规性或可用性的担保；页面所列外部链接、许可证与下载量均以来源索引快照（2026-10-16）为准，正式引用前请独立核实。本仓不含、也不夹带任何可执行的后端逻辑。
