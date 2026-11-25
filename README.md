# MangoSource · 投资资源地图

按「你遇到什么」分层的投资资源导航。七个层：

| 层 | 内容 |
|---|---|
| 投资场景 | 20 个真实处境，每条给「为什么卡住 → 三步解决 → 现在就做一件」 |
| 投资工具 | 按用途分组的长清单（官方披露、行情、数据、研报、基金、监管与自查、港美股、数据终端、开源量化…） |
| 投资大师 | 19 位，按派别分组；每位有一句理念、战绩、三条可学的要点、书籍/官方入口 |
| 投资 Skill | 52 个，GitHub 与 SkillHub 上真实在用的，标作者与星数 |
| 投资词典 | 9 类身份 × 12 个词，点词进词典 |
| 投资提示词 | 6 条「say to AI」提示词，按你会问的那句话分 tab，可一键复制 |
| AI 知识库 | 整站打包成 Markdown：复制全部 / 复制精选 / 下载 .md / 收藏说明 |
| 投资工作台 | 敬请期待 |

作者：燃冰（10 年金融产品人）。做的是投资平权。

## 目录

```
index.html              单文件站点（零依赖、零外部请求、无构建）
knowledge.md            整站知识库（Markdown，25KB，可喂给任何模型）
llms.txt                给 AI 抓取的结构化索引
share/                  可分享卡片源文件（1080×1440）
  01-can-i-buy.html     能不能买 · 五问拆解卡
assets/                 卡片成品图
docs/migration-playbook.md  从 Topinspo 迁移的全过程复盘与坑点清单
docs-用户卡点设想.txt    200 条用户卡点的原始整理（内容源头）
```

## AI 知识库

站点内置「AI 知识库」层，把全部内容组装成 Markdown：

- **复制全部**：25K 字，含 21 个场景（带提示词全文）、44 个工具、19 位大师、52 个 Skill、9 类词典、6 条提示词
- **复制精选**：约 15K 字，每层取前几条，适合发群 / 存备忘录 / 做内容集
- **下载 .md**：`knowledge.md`
- 静态版同源：仓库根目录的 `knowledge.md`，改完内容后重新生成即可（见下）

**改完内容要重新生成 `knowledge.md`**：用无头浏览器打开 `index.html`，调用 `kbMarkdown(true)` 写文件即可（脚本见 `docs/gen-knowledge.md` 说明）。

## 复制给 AI

每个 Skill 卡片右下角有「复制给 AI」：会复制一段说明 + 仓库地址 + 兜底指令（打不开链接时，让 AI 按名字给等效做法）。解决"很多人打不开 GitHub"的问题。

## 内容原则

- 不荐股、不预测、不承诺收益
- 每条资源写清「什么时候用」
- 有书的给微信读书入口，有官方资源的给官方入口；都没有的如实标「暂无公开资源」
- 工具与 Skill 的链接都实测过可打开，失效的标注而不是删除

## 埋点

站点自带一套轻量埋点，和 ranbing 主页的事件命名保持一致（`cta_click`），不引入第三方 SDK：

- 每次点击带 `data-track` 的元素会上报一条 `cta_click`
- 公共字段：`ref`（URL 里的 `?ref=`，比如从主页来的 `ref=home`）、`page`、`utm_source/medium/campaign`、`ts`
- 已埋的事件：

| 事件 | 触发 | sub |
|---|---|---|
| `page_view` | 进入页面 | 当前层 |
| `nav` | 切换左侧导航 | 层名 |
| `scene_open` | 点开一个场景 | 场景标题 |
| `prompt_open` | 点开一条提示词 | 提示词标题 |
| `copy_prompt` | 点了「复制这段」 | 提示词标题 |
| `resource_open` | 点开任意工具 / Skill / 大师资源 | 资源名 |
| `skill_cat` / `prompt_cat` | 切换分类 tab | 分类名 |
| `join_circle` | 点「加入圈子」 | — |

- 数据去向：`window.dataLayer`（可直接接 GTM）+ `navigator.sendBeacon`
- **要接统计平台**：把 `index.html` 里的 `TRACK_ENDPOINT` 填成收集地址即可自动上报；不填则只在本地 `?debug=1` 时打印
- 推荐填 Cloudflare Web Analytics 的 beacon 地址（免费、无 cookie、GitHub Pages 可用）

调试：打开 `index.html?debug=1`，每次点击都会在 console 打印 `[track] {...}`

## 发布

GitHub Pages，主分支根目录：`https://lj22503.github.io/mangosource/`

## 更新

```powershell
cd D:\claudework\mangosource
git add -A; git commit -m "更新内容"; git push
```
