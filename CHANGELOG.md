# Changelog

## 未发布

### 演示页：从「样本墙」扩成对外落地页

- `demos/index.html` 新增：项目定位句 + 指标条（374 粒种子 / 250+ 艺术家 /
  24 章 / 12 基因卡 / 10 情绪档 / 内容 CC BY 4.0 · 代码 MIT）、
  行动区（安装 / GitHub / QQ 群）、三段一键安装命令（Claude Code · Codex · OpenClaw）、
  「种子库必须装进 skill 目录」硬规则说明，以及 QQ 群 `1027282854` 引流块。
  设计上沿用本页原有的「美术馆灰墙 + 发丝线 + 射灯黄」语言，未引入新风格。
- **修掉页面原有的移动端缺陷**：`.foot-grid` 与新增 `.agents` 改用 `minmax(0,1fr)`
  （`1fr` 的 min-content 会被长命令撑破），长命令 `pre` 允许换行，新增 `≤640px` 断点。
  实测 320–1600px 均无横向溢出（手机 QQ 是主要入口，不能横向滚动）。
- `demos/.assetsignore`：部署时排除 `_src/` 与 `README.md`，站点只留静态产物。

## v3.0.0 · 2026-10-24

**内容许可由 CC BY-NC-SA 4.0 改为 CC BY 4.0 —— 全仓库成为完全开源（fully open source）。**

### 去掉了 NC 与 SA

| 项 | v2.x | v3.0.0 |
|---|---|---|
| 内容资产 | CC BY-NC-SA 4.0（署名 · 非商业 · 相同方式共享） | **CC BY 4.0**（仅署名） |
| 代码资产 | MIT | MIT（不变） |
| 字体子集 | 上游 OFL 1.1 / Apache-2.0 | 上游 OFL 1.1 / Apache-2.0（不变） |

- **商业使用不再需要单独授权**：NC 条款带来的「商用要开 Issue 洽谈」流程整体取消；
- **不再有 ShareAlike**：补录进种子库的新内容与基于本仓库的演绎作品可以自行选择许可；
- 义务只剩三条：署名、指向许可的链接、说明是否修改。

### 许可正文与生成链

- `scripts/license-sources/cc-by-nc-sa-4.0-legalcode.txt` → `cc-by-4.0-legalcode.txt`，
  官方正文重抓（396 行，取自 creativecommons.org/legalcode.txt，逐字未改）；
- `scripts/build_license.py` 的 §零 / §一 / §三 / 三·附 / 变更史全部改写，重生成 `LICENSE`；
- `scripts/check_integrity.py`：`LEGAL_FILES` 文件名同步；分章头断言仍为硬断言，
  仅把被断言字符串由 `CC BY-NC-SA` 换成 `CC BY 4.0`（强度不变，不放宽）；
- `scripts/check_assets.sh`：许可正文清单同步。

### 全仓声明点

25 份分章免责头、`art-seeds.md`、`ART-SEEDS-LOG.md`、`TASTE.md`、`AGENTS.md`、
`CONTRIBUTING.md`、`CITATION.cff`、`docs/ATTRIBUTION.md`、`docs/en/ATTRIBUTION.md`、
双语 README、`profiles/taste.json` 全部改为 CC BY 4.0。

### 迁移说明

v2.x 及更早版本继续按其原始许可（已授予的许可不可撤销），旧内容未做任何修改。

## v2.0.1 · 2026-10-16

**许可文件收口为单一 `LICENSE`**（含三份官方全文），并修掉 v2.0.0 遗留的三处不一致。

### 单一 LICENSE

合并前的结构是「总览 + 三份分拆」，共 4 个文件、17.8 KB。问题是：
**许可的权威文本被拆成四份，谁都可以只读其中一份而漏掉适用范围**。
现在合并为一份 36.6 KB 的 `LICENSE`：

```
零 · 30 秒速览
一 · 适用范围（逐路径对照 + 边界规则）
二 · MIT License                      ← 官方完整正文
三 · CC BY-NC-SA 4.0                  ← 摘要
三·附 · CC BY-NC-SA 4.0 官方完整法律条款  ← 英文权威正文，逐字未改
四 · SIL OFL 1.1                      ← 字体清单 + OFL 三条合规处置
四·附 · OFL 1.1 官方完整正文             ← 逐字未改
五 · 附录（商标 · AI 披露 · 无担保 · 变更史）
```

- 删除 `LICENSE-CODE.md` / `LICENSE-CONTENT.md` / `LICENSE-FONTS.md`；
- 全仓 32 个文件的引用改指 `LICENSE`（含 25 份分章的免责头）；
- README 的许可清单由 4 行合并为 1 行。

### 官方正文固化 + 可重跑

新增 `scripts/license-sources/`（登记官方来源与抓取日期）与 `scripts/build_license.py`：

- CC BY-NC-SA 4.0 官方法律条款全文（438 行，取自 creativecommons.org/legalcode.txt）
- SIL OFL 1.1 正文（85 行）
- MIT 正文

**为什么用脚本而不是手写**：`LICENSE` 内含约 2.6 万字节的许可正文，
手写复制粘贴极易缺行错字——而许可正文**错一个字都是法律风险**；
且日后更新版本时没人能说清改了什么。现在素材与产物分离，`--check` 模式可在 CI 断言两者同步。

### 修掉 v2.0.0 的三处不一致

| 问题 | 位置 | 处置 |
|---|---|---|
| 仍写 `templates/SKILL.md`，而该目录已移到根 `SKILL.md` | `LICENSE` §一 | 已修正 |
| `scripts/*.py` 未被任何许可覆盖（三个文件都只写了 `scripts/*.sh`） | `LICENSE` §一 | 已补全 |
| `deploy/*.md` 未被任何许可覆盖 | `LICENSE` §一 | 已补全 |

**根因是同一类**：许可文件写的是**模式**，仓库里是**具体文件**，两者会悄悄脱节。

### 新增两道 CI 守卫（防再犯）

- **许可覆盖守卫**（`check_integrity.py` §六）：双向断言——
  代码扩展名的文件必须在 MIT 区、内容扩展名的文件不能落在 MIT 区；
  并反向校验 `LICENSE §一` 真实声明了这些模式。新增文件无需手工登记。
- **许可素材同步**（`check_integrity.py` §七）：跑 `build_license.py --check`，
  素材改了却忘了重新生成 LICENSE 就报错。

### 校验状态

七道闸门全绿；许可覆盖守卫报告 **139 个跟踪文件全部落在预期分区、无盲区**。

---

## v2.0.0 · 2026-10-16

**开源合规与专业化改造**（破坏性变更：项目改名 + 结构收敛 + 底稿剥离）。
起因是一份版权的技术预审 —— 复核中发现预审报告本身有若干与仓库事实不符的判断，
因此本轮不照单执行，而是先核对事实、再按实际情况处置。

### ⚠️ 破坏性变更

| 变更 | 原值 | 新值 |
|---|---|---|
| 项目名 | `agent-taste-seed-system` | **美学大脑 / aesthetic-brain**（仓库 URL 不变） |
| skill 模板位置 | `templates/SKILL.md` | **`SKILL.md`**（仓库根，去掉无意义嵌套） |
| 变更档案位置 | `tasks/` | **`docs/changes/`** |
| 百科底稿 | `sources/艺术风格百科大全.docx`（曾被 git 跟踪） | **剥离出版本库**（`.gitignore` 锁定） |
| 内置字体家族名 | `Noto Serif SC` 等原名 | **`AB Noto Serif SC`**（加前缀，OFL §3 合规） |

### 许可体系（新增，按资产类型分治）

- `LICENSE` 许可总览（双许可结构 + 逐路径对照 + 商业使用说明 + NC 边界提示）；
- `LICENSE-CONTENT.md` 文本资产 **CC BY-NC-SA 4.0**（种子库 / 文档 / 截图）；
- `LICENSE-CODE.md` 代码资产 **MIT**（脚本 / CI / 部署）；
- `LICENSE-FONTS.md` 字体子集的上游来源表与 OFL 合规路径。
  > 修订：原预审建议「已落地双许可三件套」与仓库事实不符（当时无任何 LICENSE 文件），
  > 本轮为**新建**，并在措辞上补充了 NC 边界与商用洽谈通道。

### 字体合规（真实存在、预审未发现的问题）

- 实测 `name` 表 nameID 0：**Noto Sans SC（保留名 `Source`）/ Playfair Display / Yeseva One / Marcellus**
  均声明了 Reserved Font Name。子集是 OFL 意义上的 Modified Version，
  按 OFL 1.1 §3 **不得沿用保留字体名**。
- 处置：`build_fonts.py` 新增 `rename_font()`，对**全部** 30 个子集统一加 `AB ` 前缀
  （同步 nameID 1/2/3/4/6/16/17），一条规则覆盖全字体，无需记忆例外；
  **nameID 0（版权）与 13/14（许可）刻意保留**，满足 OFL §1。
- 演示页与 CSS 的字体栈同步改为 `'AB …'`（14 个文件）。
- 新增 `demos/_src/check_font_licenses.py` 把上述两条变成 CI 断言。

### 合规文档（新增）

- `docs/TRADEMARKS.md`：商标 / 作品名 / **在世创作者姓名**声明，
  含「❌ 不得以『用 XX 画师名字生成』作卖点」红线与 72 小时响应承诺；
- `docs/ATTRIBUTION.md`：出处、**AI 使用披露**（逐环节列出编者执笔 vs AI 辅助）、
  署名模板（学术 / 作品 / 代码三种）、SA 再分发两条硬规则；
- `docs/METHODOLOGY.md`：五基因方法论白皮书（首次把「风格即基因」写成可对外传播的完整论述）；
- `CITATION.cff`：学术引用格式（GitHub 自动出「Cite this repository」按钮）；
- `CONTRIBUTING.md`：贡献指南，核心是把「回填一行风味日志」设为最低门槛贡献路径，
  并明确 PR 硬性要求（不得上传图片 / 不得复制他站原文）与新增代码基因卡的四项门槛。

### 结构收敛与专业化

- **风味日志拆出**：`references/art-seeds.md` 末尾的日志独立为
  `references/ART-SEEDS-LOG.md`（主库是「禁止全文注入」的查询表，日志是持续追加的运营文档，混在一起会互相拖累）；
- `docs/changes/README.md` 说明档案不追改历史（本轮改名产生的旧路径引用属历史记录）；
- 25 份分章头部统一补入**许可行 + 商标免责行**；
- `TASTE.md` 与 `art-seeds.md` 去 persona 化（「主人赠我」→ 中性出处表述，全文 `主人` 清零）；
- `README.md` 增补：徽章行、合规文件清单、全仓结构图、**AI 使用披露**、
  **在世创作者使用红线**、许可摘要、三道 CI 闸门说明；结尾 `MIT` 改为完整三许可引用。

### CI 与闸门（新增三道）

- `.github/workflows/ci.yml` 三个 job：
  - **合规与完整性**：`check_assets.sh` + `check_integrity.py` + `check_links.py`；
  - **渲染与审美断言**：实渲染 → 截图新鲜度 → `qa_layout.py` + `qa_style.py`；
  - **字体许可合规**：`check_font_licenses.py`。
- `scripts/check_assets.sh`：媒体资产 / 归档文件 / 外部抄录痕迹 / 外部媒体外链 / 敏感信息 / 许可文件齐备。
- `scripts/check_integrity.py`：种子条目数（12/10/25）· 关键文件体积下限 · 分章免责头 ·
  许可文件齐备 · 演示与截图配对 · 字体命名合规。
- `scripts/check_links.py`：全仓 Markdown/HTML 相对链接断链检查（85 个文件）。
- `scripts/check_shots_freshness.py`：**截图新鲜度**。
  > 设计取舍：不直接 `git diff` 截图字节——CI 的 Chromium / FreeType / WebP 编码器
  > 版本与作者本机不同，逐字节比对必然误报，而**假阳性会卡死正常 PR，危害大于假阴性**。
  > 改为比「结构指纹」：尺寸 / 均值亮度 / 16×16 灰度指纹 / 显著色相数 / 暗部与留白占比。

### 复核结论（对预审报告的核对）

| 预审判断 | 实际核验 |
|---|---|
| P0「已新增双许可三件套」 | ❌ 当时**没有任何** LICENSE 文件，本轮为新建 |
| F6「ch23 条目加免责声明（已打补丁）」 | ❌ ch23 **无任何免责声明**；本轮为 25 份分章统一补入 |
| F8「剥离 sources/」 | ✅ 成立且更严重 —— 该 docx **已被 git 跟踪**并进入历史，需 filter-repo 清史 |
| F1「全库零图片/零二进制」 | ⚠️ 对种子库成立，但**忽略了 `sources/*.docx`**；本轮新增的 `demos/_assets/` 为自产资产，已在闸门中豁免并说明 |
| F2「全文无外部来源标注」 | ⚠️ 把 25 份分章头部的「摘自《艺术风格百科大全》原文」误判为外部来源（实为自著溯源），已复核为否 |
| 未提及 | 🔴 **字体 OFL 保留字体名问题**（本轮发现并修复） |
| 未提及 | 🔴 demo 内嵌字体子集的**许可与署名义务**（本轮补 `LICENSE-FONTS.md`） |
| 未提及 | 🔴 **AI 使用披露**（多平台实践要求，本轮补入 README + `docs/ATTRIBUTION.md`） |

### 校验状态

- 6 项闸门全绿：资产扫描 · 完整性 · 链接 · 布局（13 页）· 风格（34 条断言）· 字体许可（30 个子集）；
- 139 处字体引用全部真实加载（改名后无回落）；
- 截图新鲜度比对通过（12 张）。

---

## v1.1.0 · 2026-10-15

**把「审美」变成看得见的验收材料**：新增 `demos/` 十二风格样本墙 —— 12 个真实浏览器渲染的完整页面 + 高清截图 + 两道自动质检闸门。种子库本体（`references/`）与部署脚本均未改动，已部署实例零影响。

- **新增 `demos/`（演示与验收材料）**
  - `01..12-*.html`：十二张完整页面，覆盖 12 粒代码基因（赛博霓虹 / 瑞士平面 / 中国画留白 / 吉卜力手绘 / 浮世绘扁平 / 巴洛克聚光 / 洛可可粉彩 / 极简主义 / 波普拼贴 / 构成主义海报 / 赛璐璐动漫 UI / 哥特暗黑）、12 个场景类型、10 种情绪档。
  - `index.html`：样本墙（浏览入口），逐张标注「主基因 + 辅基因 + 情绪 + 场景 + 该守的纪律 + 激活词」。
  - 每个 HTML 文件头写明**选自哪粒种子、用了哪些激活词、守了哪几条纪律**，可直接对照 `references/` 复核。
- **`demos/_src/` 四条可复现管线**
  - `build_fonts.py`：扫描页面可见文本 → 从源字体裁 woff2 子集（30 个字重 / 约 2.05MB），**仓库不再依赖联网取字体**；本机无中文衬线（`fc-match "Noto Serif SC"` 落到 DejaVu）是新增此步的根因。
  - `render_shots.py`：headless Chromium 实时渲染，2× 设备像素比，无损 WebP（超 700KB 自动降级为 q92）；支持 `data-canvas="WxH"`（定尺）与 `"Wxfull"`（整页长图），`data-shots="skip"` 标记展示页不产图。
  - `qa_layout.py`：溢出 / 越界 / 遮挡 / 字号 / **WCAG 对比度（按实际背景色计算，大字 3:1、正文 4.5:1）** / JS 错误。
  - `qa_style.py`：把每粒基因卡的硬纪律变成像素断言（亮度、暗部%、留白%、显著色相数、彩色像素%），共 34 条。
- **README**：新增「🖼️ 先看结果：十二风格样本墙」章节（位于部署面板之后），含 12 图编排展示、风格基因对照表（含每张的纪律阈值）、制作者与渲染环境说明、以及「demos/ 是演示材料而非种子库本体」的边界声明；文件清单与分层架构补入 `demos/`。
- **署名可见性**：12 张页面各自底部的 `风格基因 …/ Built by pi agent × DeepSeek V4.1 Flash` 采用该作品自身的字体气质与配色排版（参与构图，非水印贴纸）。
- **校验**：13 页布局 0 问题；12 张 × 34 条基因纪律断言全部通过。

## v1.0.2 · 2026-10-13

部署形态纠偏：**种子库落点从 agent workspace 收敛到 agent 自身 skill 内部**，彻底隔离 workspace 自动清理。

- **问题根因**：许多 agent 宿主在宿主机配置了 workspace 自动清理（把 workspace 内文件搬进 archive 或删除）。旧版把种子库平铺进 `<workspace>/taste/`（OpenClaw 形态）或引导用户 clone 到可能位于 workspace 内的路径（通用形态），被清理后注入提示词里写死的路径**永久失效且无任何报错**，agent 静默退化成 AI 味默认审美。
- **改造内容**：
  - Claude Code 落点 `~/.claude/skills/taste/references/`（原本就正确，本次补「为什么」说明与验证命令）；
  - OpenClaw 落点改为 `<workspace>/skills/taste/references/`（`skills/` 是能力目录，清理策略不会动），新增「从旧布局迁移」小节（先备份风味日志）；
  - Codex 等有 skill 机制的 agent 落点 `~/.codex/skills/taste/references/`（按端 skill 根取值表）；
  - 无 skill 机制的 agent 兜底为仓库 clone 目录，并显式声明「不得位于任何 workspace 内」；
  - `TASTE.md` 文首路径段收敛为「skill 内部相对路径」单一说法；`templates/SKILL.md` 增加「种子库装在哪 / 引用规则」段；
  - `install-claude-skill.sh` 同步安装 `TASTE.md`、落点提示更明确；
  - README 新增「部署落点铁律」表 + 验证命令（含 workspace 搬迁免疫性证明）；`AGENT-INJECTION.md` 部署表全量对齐。
- **兼容**：已按旧形态部署的实例可照 `deploy/openclaw.md` 迁移节一条命令搬家，风味日志不丢（先备份再覆盖）。
- **立项**：`docs/changes/CHG-20261013-seed-internal-path/`（CHANGE / HEALTH / PRD / SPEC / TRACEABILITY）。
- ⚠️ 本版把上一版 v1.0.1 的「路径自适配」口径**推翻**：不再宣称“仓库 / OpenClaw 两套布局等价”，改为单一落点（skill 内部）+ 无 skill 机制时的仓库路径兜底。

## v1.0.1 · 2026-09-25

部署路径一致性修复（OpenClaw 实际部署反馈发现，经多路对抗核查补全）。

**路径自适配**
- `TASTE.md` 路径适配各部署形态：种子库引用不再写死仓库布局路径，文首标注「仓库 = `references/`、OpenClaw workspace = `taste/`」，并给出按文件名 `art-seeds.md` 定位的兜底方式；速查说明补入 `moods/`/`code-genes/`/`chapters/` 深挖层（标注"部署了全库时"）。
- 种子库侧导航同步自适配：`references/art-seeds.md` 头部「四层知识库导航」不再写死 `../TASTE.md`（该路径在 Claude Code skill 形态必失效），改为按部署形态定位 + 按文件名兜底；`references/chapters/` 全部 25 个文件头部注释同步修正。
- 修复 `TASTE.md` 决策流程 Step 5 的日志位置残留 `taste/log.md`（该文件在任何部署形态都不存在）→ 统一为「种子库 `art-seeds.md` 末尾风味日志」，与全部部署文档及实际约定一致。

**部署文档修正**
- `deploy/openclaw.md` 升级为四层全库部署：`references/` 目录内容平铺进 workspace `taste/`（旧两文件部署重跑命令即可补齐），新增覆盖前自动备份风味日志的步骤、装后结构说明与「在仓库根目录执行」前提。
- `deploy/claude-code.md`：手动方式（方式 B）由只拷两个文件改为 `references/` 整目录覆盖拷贝（原方式装完 `moods/`/`code-genes/`/`chapters/` 三层缺失，四层路由会落空）；一键脚本描述修正为与脚本实际行为一致（脚本内注释同步对齐）；补方式 B 的目录前提；种子库体积口径 400KB → 约 300KB。
- `AGENT-INJECTION.md` 部署说明表按形态拆行：原表把 OpenClaw / Claude Code / Codex 压成一行 OpenClaw 式指令，与三份权威部署文档冲突（Claude Code 走 skill 方案、Codex 走 clone 原样布局），现各自指向对应部署文档。
- `README.md` 一键指令、文件清单、「部署成功的标准」同步以上约定；新增无文件写入形态（ChatBot 附件/知识库）的验收豁免口径。

**口径杂项**
- `chapters/` 实为 24 章 + 后记（25 个文件）——原 `ch00-前言.md` 正文即全书后记，错名已纠正为 `ch25-后记.md`，各处计数标注统一；TASTE.md 艺术家数量口径 200+ → 250+（与全仓一致）；百科章系枚举补漏「样式主义」；TASTE.md「原文由编制者自留」旧说法改为指向仓库内 `references/chapters/` 与 `sources/`；版本戳更新。

## v1.0.0 · 2026-09-24

首个公开发布版本。

- 收录《艺术风格百科大全》全量提炼三件套：`TASTE.md`（审美 OS）、`references/art-seeds.md`（24 章 250+ 艺术家全量种子库）、`AGENT-INJECTION.md`（通用注入提示词），内容与 OpenClaw 工作站原始版本一致（零删减）。
- **四层知识库建档**（重 agent 按需加载）：
  - `references/chapters/` ×24+1：《艺术风格百科大全》docx 原文逐章拆分，零删减（源 docx 归档于 `sources/`）；
  - `references/moods/` ×10：情绪选种档案（科技酷感/梦幻治愈/热血冲击/庄重典雅/甜美容爱/孤独诗意/荒诞幽默/暗黑崇高/清晰理性/东方古韵），每份含主推种子五基因详解 + 媒介适配 + 混种配方 + 翻车清单；
  - `references/code-genes/` ×12：代码基因卡（瑞士平面/赛博霓虹/中国画留白/极简/吉卜力/浮世绘/巴洛克聚光/洛可可粉彩/波普/构成主义/赛璐璐/哥特暗黑），每张含激活词 + 可直接生效的部署提示词 + CSS 变量块 + 反模式。
- **激活词原理**写入 skill：艺术家名/风格名是 LLM 预训练美学基因的激活锚点，prompt 点名 > 形容词。
- 相对原始工作站版本的适配（仅路径与分发说明，内容未动）：
  - `TASTE.md` 中种子库路径 `taste/art-seeds.md` → `references/art-seeds.md`（适配本仓库布局）；
  - 原始 README（系统总览）内容并入本仓库 `README.md` 并扩写为部署矩阵入口。
- 新增部署层：Claude Code skill 方案（`templates/SKILL.md` 四层路由版 + `deploy/install-claude-skill.sh` 整目录同步 + CLAUDE.md 薄注入）、OpenClaw workspace 方案、通用规则文件/系统提示词方案。
