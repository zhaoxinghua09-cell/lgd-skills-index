# AGENTS.md — 给 AI Agent 的工作指引

本文件面向自动化 AI Agent（编码助手、静态站维护机器人、抓取器）。人类读者请看 [README.md](README.md)。

## 这个仓库是什么

`lgd-skills-index` 是一个 **纯静态 GitHub Pages 注册站仓**，不是可运行的 SDK、不是 npm 包、不是带后端的 Web 服务。唯一的产物是 `index.html`：它内嵌 `var DATA = {...}` 注册表并由原生 JS 渲染。整站无构建、无依赖、无网络回源。

## 可用的工作命令

```bash
# 克隆并查看站点
git clone https://github.com/zhaoxinghua09-cell/lgd-skills-index.git
cd lgd-skills-index
ls

# 本地预览（直接用浏览器打开，无需 dev server）
start index.html

# 校验内嵌 DATA JSON 是否可解析
python - <<'PY'
import re, json
html = open('index.html', encoding='utf-8').read()
data = json.loads(re.search(r'var DATA = (\{.*?\});\s*\nvar LINE_LABEL', html, re.S).group(1))
print('packages:', len(data['skills']))
PY
```

前置依赖：仅一个现代浏览器 +（可选）Python 3 做数据抽取。无需 npm / node / 构建工具。

## 约定（Do）

- 修改注册表数据时，只动 `index.html` 里 `var DATA = {...}` 这一段；保持 JSON 合法、字段与现有条目一致（`id` / `slug` / `name` / `line` / `lkey` / `ai` / `exe` / `pub` / `url`）。
- 新增公开链接前先核对远端 URL 真实存在；未核对的条目 `url` 设为 `null` 并保持 `pub: "local"`，由页面显示中性「待发布」。
- 保持页面脱敏：不写入本地绝对路径、凭据、内部代号。
- 同步更新头部数据快照日期与 `stats` 计数，使统计与实际条目一致。

## 禁止（Don't）

- 不要臆造远端链接、下载量或「公开就绪」状态。
- 不要在仓内提交任何密钥、令牌或真实内部路径。
- 不要新增 LICENSE 文件或改写任何权属 / 许可主张——本仓未附 LICENSE，许可口径只由维护者决定。
- 不要把 `lgd-skills-index.html` 与 `index.html` 做成内容漂移的两份；它们应保持一致。
- 不要声称本站「已认证 / 已商用 / 已服务特定客户」。

## 边界

本仓只做注册展示与静态渲染；不提供技能包的运行、分发或托管（分发走 ModelScope / GitHub 远端）。
