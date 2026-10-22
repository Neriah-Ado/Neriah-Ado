# Neriah 仓库文档风格规范 v1.1

> 状态：正式 · 生效日期：2026-10-22
> 适用：`Neriah-Ado` 名下全部自有仓库（不含 fork）。依据：9 仓库全量文档盘点
> （`docs-style-survey.md`，624 行 / 138 条文档记录）与安全审计结论。
> 原则：只统一**结构与写法**，不统一内容深度；事实密度优先于修饰。

---

## 0. 文档分级

| 级别 | 文件 | 要求 |
|---|---|---|
| A 必改 | 根 `README.md`、`README.en.md`（存在即必须与中文版逐节镜像）、仓库 About 描述、`CHANGELOG.md` | 100% 套用本规范 |
| B 统一 | `docs/` 用户向文档、`docs/releases/*`、`marketplace.json` / `step.plugin.json` / `package.json` 的 description | 统一抬头、术语、链接、代码块；正文按内容 |
| C 不动 | `AGENTS.md`、`CLAUDE.md`、`SKILL.md` 正文、`commands/`、`references/` 等内部/Agent 文档 | 仅保证术语一致；SKILL frontmatter 约定「description 英文、正文中文」 |

---

## 1. README 骨架（14 节，按需裁剪但**不调序**）

| # | 章节 | 必备 | 要求 |
|---|---|---|---|
| 1 | H1 `产品名 — 一句话定位` | 是 | 唯一 H1；含仓库名与产品名不同时用括号/引用说明；**无 emoji、无版本号** |
| 2 | 版本 + 语言切换行 | 双语仓库必备 | `**vX.Y.Z** · [简体中文](README.md) \| [English](README.en.md)` |
| 3 | 徽章区（2–4 枚） | 是 | 顺序：License → 运行时/平台 →（可选）测试状态；不放版本徽章 |
| 4 | 简介 / 功能特性 | 是 | 60 字定位 + 5–8 条 `**能力** —— 说明`，无 emoji 项目符号 |
| 5 | 效果预览 | 有 UI 者必备 | 1 张截图/GIF + 1 行说明；图片放 `assets/` 或 `docs/images/` 并写 alt |
| 6 | 安装 | 是 | 方式一（推荐）/二/三，命令块标 `bash`，给出运行环境最低版本 |
| 7 | 使用 / 命令 | 是 | 命令表 + 最小示例 |
| 8 | 配置 | 有配置必填 | 表格：`参数 \| 类型 \| 默认值 \| 说明`；环境变量另表 `变量 \| 必填 \| 说明` |
| 9 | 架构 / 工作原理 | 有复杂度必填 | 架构图 + 分层职责表；细节下沉 `docs/` |
| 10 | 验证状态 / 测试 | 是 | 运行命令 + 「已实测 / 未验证」表（吸收 StepFun-Code-GUI 写法） |
| 11 | 已知限制 | 是 | 每条说明影响与绕行方案（吸收 StepFun-Code-GUI 写法） |
| 12 | 故障排查 / FAQ | 是 | 表格或 Q/A，≥5 条 |
| 13 | 许可证（+ 上游署名） | 是 | 中文文档 `## 许可证`、英文 `## License`；版权行 `© YYYY Neriah` |
| 14 | 文档地图 | 多子文档仓库必备 | 列出各文档职责与入口（private-knowledge-base 需要） |

- 内部开发内容（工作原理细节、本地预览、测试脚本）保留但下沉 `docs/development.md`，README 只放链接。
- 小仓库（`Neriah-Ado` 主页、`Web`）用精简版：H1 → 简介 → 使用/示例 → 许可证；不强行补徽章与 FAQ。
- 模板：新建仓库直接复制 `docs/templates/README.zh.md`、`docs/templates/README.en.md`、`docs/templates/CHANGELOG.md`。

---

## 2. 文案与格式细则

1. **双语只有一种方案**：`README.md` 中文 + `README.en.md` 英文全量镜像（逐节对应）；头部互链。不接受「单文件双 H1」或残缺英文版。
2. **标题**：H1 唯一；正文只用 H2/H3；标题无 emoji、不编号（`DEPLOY-*.md` 长手册除外，且 1→2→3 连续）。
3. **emoji**：正文状态标记可保留 ✅/❌，不得进入标题；单篇 ≤10 个。
4. **代码块**：围栏必须带语言（`bash`/`json`/`yaml`/`text`/`sql`/`go`/`ts`）；目录树用 `text`；注释行不可单独以 `#` 开头（会渲染成标题）。
5. **表格**：配置、命令、能力矩阵一律用表；表头语言跟随文档语言。
6. **标点**：中文全角、中英文间留空格；英文文档半角；同一文件不混用。
7. **链接**：仓库内相对链接必须实际存在；跨仓库/主页用绝对 URL；发布说明与 CHANGELOG 必须在根 README 有索引（GUI 目前缺）。
8. **术语单一写法**：

   | 统一写法 | 禁止 |
   |---|---|
   | 插件 / 插件市场 | 扩展、market |
   | 技能 / 技能市场 | skill 市场 |
   | 斜杠命令 | 命令、slash 指令 |
   | 上下文快照 | 快照文件、context 存档 |
   | 仪表盘 / 大屏 | 面板（指可视化界面） |
   | 本地优先 | local-first（正文） |

9. **对外文档不出现内部代号**（G1、C4、TM-130-1 等）；仓库名/产品名/包名/市场名在首段建立对照。
10. **版本号**：README 只在切换行显示当前版本；`package.json` / `manifest` / `CHANGELOG` / Release 三处一致。
11. **description 模板**：`<产品名> — <一句话定位>：<核心能力 1、2、3>`；与 README tagline 同源；不用 `inspired` 等营销词；同一插件在多清单中「短/长」两版需明确对应关系。
12. 中文文档不用「您」，不写「！！！」，不堆形容词；技术断言给可验证依据（版本号、命令、实测结果）。

---

## 3. CHANGELOG 与发布说明

- **CHANGELOG**（有发布物的仓库必备；`Neriah-Ado`、`Web` 可不建）：
  - 头注：遵循 Keep a Changelog、SemVer；
  - 版本标题固定 `## [X.Y.Z] - YYYY-MM-DD`，版本连续不跳段（usage 需补 v1.x）；
  - 小节固定 `### 新增 / ### 变更 / ### 修复 / ### 移除 / ### 安全`，只保留有内容者；
  - 只写用户可感知变更，内部任务号放条目尾部。
- **发布说明 `docs/releases/vX.Y.Z.md`**：
  - `# vX.Y.Z — 中文主题 / English Theme`；
  - H1 下引用块：`> 发布日期 / Date:`、`> 范围 / Scope:`、`> 门禁 / Gate:`；
  - 正文 `## 中文` → 内容 → `## English` → 内容（**单文件单 H1**）；
  - 根 README 建发布说明索引表，与 CHANGELOG 互链。

---

## 4. 单点整改清单（按仓库，来自盘点报告 §2/§5）

| 仓库 | 必改项 |
|---|---|
| stepfun-usage-monitor | 去 8 个 emoji 标题；CHANGELOG 补 v1.x；发布说明改单 H1 + `## 中文/English`；`## License`→`## 许可证`；三份 manifest 描述收敛 |
| StepFun-Code-GUI | 补「功能特性」；补 CHANGELOG；发布说明加日期与索引；README 链到 `docs/releases/` |
| stepcode-plugins | 13 个插件 README 套统一 6 节模板；删内部代号；根 README 补 tagline 与语言策略；CHANGELOG 去掉 `Other Changes` |
| dsh-resident-theme | H1 对齐包名/产品名；README 与 AGENTS 去重；「开发」下沉；description 同源 |
| private-knowledge-base | 三套部署文档收敛为「根 README 概览 + DEPLOY 全流程 + kb-server 第 5 章细节」并互链；补 CHANGELOG；代码块标语言；修 `#` 注释行 |
| step-code-context-compaction | 补 `README.en.md` 并与中文逐节对应；与通用版 SKILL/参考表去重；加语言切换行 |
| context-compaction-skill | `## License`→`## 许可证`；版本节去硬编码；补示例 |
| Neriah-Ado | 修 H1；`./PICTURE`、`./YesPlayMusic`、`./Web` 改绝对 URL；补简介与仓库索引表 |
| Web | 重写 `#1111` 为最小 README（定位/示例/许可证）；补 package description 与 LICENSE 声明 |

---

## 5. 落地与校验

1. 本规范是全账号文档的单一事实源，位于 `Neriah-Ado/docs/DOCS-STYLE.md`；其他仓库 README 末尾加一行「文档规范：[DOCS-STYLE](https://github.com/Neriah-Ado/Neriah-Ado/blob/main/docs/DOCS-STYLE.md)」。
2. 每仓库一个 `docs:` commit，与安全修复 commit 分开；不 force push。
3. 校验脚本（提交前跑）：
   - 相对链接存在性；
   - 标题层级与 emoji 残留；
   - 中英 README 章节标题集合是否一致；
   - 术语黑名单；
   - 代码围栏语言标注率；
   - CHANGELOG 版本标题格式与连续性；
   - 仓库 About 描述与 README tagline 同源。
4. 新仓库直接复制模板（`docs/templates/README.zh.md`、`docs/templates/README.en.md`、`docs/templates/CHANGELOG.md`）。

---

## 附录：改造示例

| 现状 | 规范后 |
|---|---|
| `## ✨ 功能特性` | `## 功能特性` |
| `## License` | `## 许可证` |
| `#1111` | 按 §1 精简骨架重写 |
| 同一插件 `marketplace.json` 与 `step.plugin.json` 描述措辞不同 | 短/长两版，长版以 README tagline 为首句 |
| 中文有 FAQ、英文没有 | 两版章节集合一致 |
| `# stepfun-usage-monitor — ZCode Token 速率监控（zcode-tps-monitor）` | `# stepfun-usage-monitor — ZCode Token 速率监控`（正文首段说明别名） |
