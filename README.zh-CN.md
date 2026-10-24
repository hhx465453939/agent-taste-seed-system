<p align="right">
  <a href="README.md"><img src="https://img.shields.io/badge/README-English-2f81f7?style=flat-square" alt="English"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/README-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-e05252?style=flat-square" alt="简体中文"></a>
</p>

<img src="demos/_assets/brand/readme-hero.png" width="100%" alt="美学大脑 · Aesthetic Brain —— 给任何 AI Agent 装上审美大脑">

<p align="center">
  <a href="https://github.com/hhx465453939/agent-taste-seed-system/actions/workflows/ci.yml"><img src="https://github.com/hhx465453939/agent-taste-seed-system/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-CC_BY_4.0-lightgrey.svg" alt="许可：CC BY 4.0"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/Code-MIT-blue.svg" alt="代码：MIT"></a>
  <a href="CITATION.cff"><img src="https://img.shields.io/badge/Cite-CITATION.cff-green.svg" alt="引用"></a>
</p>

### ▶︎ [**在线样本墙 —— 12 张真实渲染页：taste.hxalex.com**](https://taste.hxalex.com)

一套可移植的**「审美操作系统 + 风格种子库」**，让 Claude Code / Codex / OpenClaw / pi / workbuddy / codebuddy / Trae / Qoder / hermas 等任何能读文件的 agent，在视觉创作上摆脱**「AI 味默认审美」**。

它修的是几乎所有模型都会犯的那个错：居中的大标题、三张等距卡片、紫色渐变、无意义的圆角。

**它不给你形容词，给你 250+ 艺术家和风格运动**——先拆成五个基因位（**色彩 × 光线 × 笔触 × 构图 × 情绪**），再翻译成可执行参数（CSS 变量 / 提示词关键词 / 版式规则）与像素级断言，于是「品味」第一次变成可以回归测试的东西。

<sub>**v3.0.0** · 2026-10-24（再许可为 CC BY 4.0）· 旧名 `agent-taste-seed-system` · [仓库](https://github.com/hhx465453939/agent-taste-seed-system) · [许可](LICENSE)：文本 **CC BY 4.0** / 代码 **MIT** / 字体 **OFL–Apache** —— 可商用，无 NonCommercial 条款。<br>来源：《艺术风格百科大全》（24 章 250+ 艺术家/风格）→ 提炼为可执行的审美决策体系 · 样本墙源码：[`demos/index.html`](demos/index.html)</sub>

<p align="center">
  <a href="https://taste.hxalex.com"><img src="demos/_assets/shots/01-cyber-neon.webp" width="24%" alt="赛博霓虹"></a>
  <a href="https://taste.hxalex.com"><img src="demos/_assets/shots/03-cixuan-chinese-whitespace.webp" width="24%" alt="中国画留白"></a>
  <a href="https://taste.hxalex.com"><img src="demos/_assets/shots/06-baroque-tenebrism.webp" width="24%" alt="巴洛克聚光"></a>
  <a href="https://taste.hxalex.com"><img src="demos/_assets/shots/09-pop-collage.webp" width="24%" alt="波普拼贴"></a>
</p>

---

## 📍 部署落点铁律（先读这条，再选你的 Agent）

> **种子库只装进 agent 自身 skill 的内部目录（`<skill 根>/taste/references/`），绝不装进 workspace 根或 workspace 下的普通子目录。**

原因：许多 agent 宿主在宿主机配置了 **workspace 自动清理**——定期把 workspace 内的文件转移到 archive 类路径或直接删除。种子库一旦落在 workspace 普通目录里，被清理后注入提示词里写死的路径会**永久失效且没有任何报错**：agent 每次都"查库"，每次都查不到，静默退化成 AI 味默认审美。

放进 `skills/` 内部的理由：`skills/` 的语义是「这个 agent 的能力集合」，清理策略针对的是人格/工作区，不会动能力目录。**按语义分层，而不是按目录是否写保护分层。**

| Agent | skill 根 | 种子库落点 |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `~/.claude/skills/taste/references/art-seeds.md` |
| Codex | `~/.codex/skills/` | `~/.codex/skills/taste/references/art-seeds.md` |
| OpenClaw | `<workspace>/skills/` | `<workspace>/skills/taste/references/art-seeds.md` |
| pi / Kimi | `~/.agents/skills/`（本机为 `~/.claude/skills` 符号链接） | `<agents skill 根>/taste/references/art-seeds.md` |
| 无 skill 机制的 agent | 仓库 clone 目录（**不得位于任何 workspace 内**） | `<clone 根>/references/art-seeds.md` |

**引用形式**：skill 内文档一律用**相对 skill 根**的路径（`references/art-seeds.md`、`references/moods/01-…`）；只有 skill 之外的全局规则文件才用绝对路径。

---

## 🚀 一键部署：复制指令发给你的 Agent，它自己装

> **用法（10 秒）**：在下面找到你的 Agent → 点代码块右上角 📋 复制 → 粘贴发给该 Agent → 等它自己完成部署并向你汇报。指令已自足：含仓库地址、安装步骤、汇报要求、防重复安装的防呆，Agent 无需再问你任何问题。

### 🤖 Claude Code

```text
请为本机 Claude Code 安装「美学大脑」（agent-taste-seed-system）。

仓库：https://github.com/hhx465453939/agent-taste-seed-system

步骤：
1. git clone https://github.com/hhx465453939/agent-taste-seed-system.git ~/agent-taste-seed-system（目录已存在则 cd 进去 git pull 更新）
2. bash ~/agent-taste-seed-system/deploy/install-claude-skill.sh
   （把 taste skill 装进 ~/.claude/skills/taste/，含四层种子库：总库/情绪档/代码基因卡/风格章档；脚本自带旧种子库备份）
3. 在 ~/.claude/CLAUDE.md 末尾追加「🎨 美学大脑（Taste Seed System）」薄注入节——全文逐字取自 ~/agent-taste-seed-system/deploy/claude-code.md 的「薄注入片段」小节；若 CLAUDE.md 已存在同名节则跳过，不要重复追加
4. 完成后向我汇报：skill 安装路径与文件清单、CLAUDE.md 追加结果、让我如何验证生效

注意：
- 不要修改仓库内 references/ 的任何内容（那是种子库本体）。
- 种子库必须装在 skill 内部（~/.claude/skills/taste/references/）。禁止把种子库平铺进任何 workspace 目录——本机多个 agent 配了 workspace 自动清理，会把文件搬进 archive 导致引用永久失效。
```

### 🦞 OpenClaw

```text
请为 OpenClaw 工作区安装「美学大脑」（agent-taste-seed-system）。

仓库：https://github.com/hhx465453939/agent-taste-seed-system

步骤：
1. git clone https://github.com/hhx465453939/agent-taste-seed-system.git ~/agent-taste-seed-system（已存在则 git pull）
2. 先读 ~/agent-taste-seed-system/deploy/openclaw.md，然后按文档执行：
   - 种子库装进 skill 内部：`<workspace>/skills/taste/references/`（四层全库整目录覆盖：`cp -R references/. <workspace>/skills/taste/references/`），决策层随 skill 走（`TASTE.md` 与 `SKILL.md` 放 `<workspace>/skills/taste/`）；**不再平铺到 workspace 根或 workspace/taste/**——workspace 有自动清理，会被搬走导致引用永久失效
   - 已按旧布局（workspace 根 taste/）装过的：按文档「从旧布局迁移」小节操作，先备份风味日志再覆盖、最后清旧落点
   - 把仓库 AGENT-INJECTION.md 里的「注入提示词」整段并入该 workspace 的 AGENTS.md 或 SOUL.md（已有同名节则跳过）
3. 完成后向我汇报：文件放置路径、注入位置，以及对龙虾的验证方式（如让它画一张海报看是否先报情绪关键词）
```

### 🧠 Codex

```text
请为本机 Codex 安装「美学大脑」（agent-taste-seed-system）。

仓库：https://github.com/hhx465453939/agent-taste-seed-system

步骤：
1. git clone https://github.com/hhx465453939/agent-taste-seed-system.git ~/agent-taste-seed-system（已存在则 git pull）
2. 读 ~/agent-taste-seed-system/deploy/generic-agents.md，按「情形 A：有 skill 机制」执行：把四层种子库装进 Codex 的 skill 目录 `~/.codex/skills/taste/references/`（`mkdir -p` + `cp -R references/.`），再把文档中的薄注入片段追加到全局规则文件（如 ~/.codex/AGENTS.md）末尾；已有同名节则跳过
3. 完成后向我汇报：种子库落点、修改的规则文件、追加的行数，以及下次视觉任务你会如何走「情绪定位→选基因→翻译参数→自检→记档」流程
```

### 🧩 Trae / Qoder / pi / workbuddy / codebuddy / hermas 等其他 Agent（通用版）

```text
请为本 Agent 安装「美学大脑」（审美种子系统）。

仓库：https://github.com/hhx465453939/agent-taste-seed-system

步骤：
1. git clone https://github.com/hhx465453939/agent-taste-seed-system.git ~/agent-taste-seed-system（已存在则 git pull）
2. 读仓库的 README.md 和 deploy/generic-agents.md，判断你自己的规则加载机制并按对应情形部署：
   - 有 skill 机制 → 种子库装进你**自己的 skill 目录**内部（`<你的 skill 根>/taste/references/`），注入片段用相对 skill 根路径
   - 只有全局规则文件、无 skill 机制 → 种子库留在仓库 clone 目录（**该目录不得位于任何 workspace 内**），注入片段用该 clone 的绝对路径
   - 只有系统提示词/知识库 → 把 AGENT-INJECTION.md 的注入提示词整段并入，TASTE.md 与 references/art-seeds.md 作为可读取的知识文件（能放目录就把整个 references/ 放进去，四层全库可用）
3. 部署后自检：用一句话复述你的视觉任务工作流（情绪定位 → 查种子库选 1 主 + 1 辅基因 → 五基因翻译成参数 → 一句话自检 → 交付后记风味日志）
4. 向我汇报：部署方式、种子库落点、自检复述

禁止：把种子库平铺进 agent workspace 根或 workspace 下的普通目录（会被 workspace 自动清理搬走导致引用永久失效）。
```

### 🌐 万能版（任意 Agent，含网页 ChatBot）

```text
从现在起装备「美学大脑」。请访问 https://github.com/hhx465453939/agent-taste-seed-system 阅读 README.md、TASTE.md、AGENT-INJECTION.md（种子库 references/ 目录按需读取，不要全量载入）。

之后所有涉及审美与视觉呈现的任务（长图/海报/PPT/图表/插画/UI/封面/配色/文生图提示词/Word 与文档排版，以及生活与社会关系中的审美咨询），你都必须：
先情绪定位（读者该感受什么，一个词）→ 按种子库选 1 主 + 1 辅风格基因 → 把五基因（色彩/光线/笔触/构图/情绪）翻译成具体参数 → 一句话自检（这张作品的风格基因是什么）→ 交付后记录本次搭配。

禁止输出 AI 味默认审美（通用卡片/蓝紫渐变）；一组作品一个主基因，敢混搭只混一层。
```

> 💡 万能版仅适用于**能联网浏览**的 Agent。若对方无法访问 GitHub：把本仓库的 `TASTE.md` 和 `references/art-seeds.md` 下载后作为附件/知识库上传给它，再发上面的指令（去掉第一条访问要求）即可。

### ✅ 部署成功的标准（任何 Agent 通用）

1. 让它「做一张 XX 海报」：它**先报情绪关键词**再动手
2. 交付时它能**一句话说出风格基因**（主 + 辅）
3. 它的种子库副本末尾出现新的风味日志条目

> 无文件写入能力的形态（网页 ChatBot 的附件/知识库）以第 1、2 条为准：风味日志由用户代记进自己的副本，或让它在回复末尾口述记录本次搭配。

### 🔍 验证种子库真的在（且不怕 workspace 清理）

```bash
# 以 Claude Code 为例；换 SKILL_ROOT 即可验任意 agent
SKILL_ROOT="$HOME/.claude/skills/taste"
test -r "$SKILL_ROOT/references/art-seeds.md" && echo "L1 OK"
test -d "$SKILL_ROOT/references/moods"        && echo "L2a OK"
test -d "$SKILL_ROOT/references/code-genes"   && echo "L2b OK"
test -d "$SKILL_ROOT/references/chapters"     && echo "L2c OK"

# OpenClaw 免疫性证明：把 workspace 整体挪走后仍可读
WS=/path/to/workspace
mv "$WS" "$WS.moved" && test -r "$WS.moved/skills/taste/references/art-seeds.md" \
  && echo "IMMUNE OK" && mv "$WS.moved" "$WS"
```

---

## 🖼️ 先看结果：十二风格样本墙

> **一个 Agent，十二种品味。** 下面每一张都是真实浏览器渲染出来的完整页面（不是设计稿、不是文生图）：<br>
> 逻辑画布 **1440 × 900**，以 **2 倍设备像素比**截取 → 高清 **2880 × 1800** 无损 WebP。<br>
> 点任意一张 → 打开可交互的原始页面；[**→ 打开样本墙（含每张的风格说明）**](demos/index.html) ｜ [渲染与质检说明](demos/README.md)

<p align="center">
  <a href="demos/01-赛博霓虹.html"><img src="demos/_assets/shots/01-cyber-neon.webp" width="49%" alt="赛博霓虹：深蓝黑底＋荧光青只施于边线数字的科技控制台"></a>
  <a href="demos/02-瑞士平面.html"><img src="demos/_assets/shots/02-swiss-international.webp" width="49%" alt="瑞士平面：十二列栅格＋唯一强调色的年度数据报告"></a>
</p>
<p align="center">
  <a href="demos/03-中国画留白.html"><img src="demos/_assets/shots/03-cixuan-chinese-whitespace.webp" width="49%" alt="中国画留白：绢色底、竖排一列点睛、朱砂印参与构图的茶页"></a>
  <a href="demos/04-吉卜力手绘.html"><img src="demos/_assets/shots/04-ghibli-handdrawn.webp" width="49%" alt="吉卜力手绘：米白纸感、草木绿与天空蓝、暖色阴影的亲子课程页"></a>
</p>
<p align="center">
  <a href="demos/05-浮世绘扁平.html"><img src="demos/_assets/shots/05-ukiyoe-flat.webp" width="49%" alt="浮世绘扁平：普鲁士蓝平涂、三段横向分层、富士山压角的展览页"></a>
  <a href="demos/06-巴洛克聚光.html"><img src="demos/_assets/shots/06-baroque-tenebrism.webp" width="49%" alt="巴洛克聚光：单一暖光源、黑暗占九成、金色只做线的演出页"></a>
</p>
<p align="center">
  <a href="demos/07-洛可可粉彩.html"><img src="demos/_assets/shots/07-rococo-pastel.webp" width="49%" alt="洛可可粉彩：粉白底、曲线分区、中心对称的甜品花房页"></a>
  <a href="demos/08-极简主义.html"><img src="demos/_assets/shots/08-minimalism-gallery.webp" width="49%" alt="极简主义：白底无圆角、两个灰阶、一整块 Kelly 式蓝面的画廊页"></a>
</p>
<p align="center">
  <a href="demos/09-波普拼贴.html"><img src="demos/_assets/shots/09-pop-collage.webp" width="49%" alt="波普拼贴：同一张脸四色复制、本戴点、粗黑描边的超市海报"></a>
  <a href="demos/10-构成主义海报.html"><img src="demos/_assets/shots/10-constructivism-poster.webp" width="49%" alt="构成主义海报：红黑白三色、一条红色斜带、文字沿对角线排布的招募宣言"></a>
</p>
<p align="center">
  <a href="demos/11-赛璐璐动漫UI.html"><img src="demos/_assets/shots/11-cel-shading-anime-ui.webp" width="49%" alt="赛璐璐动漫 UI：立绘取三色做 UI 主轴、两分 cel 阴影、实心位移按钮的角色主站"></a>
  <a href="demos/12-哥特暗黑.html"><img src="demos/_assets/shots/12-gothic-dark.webp" width="49%" alt="哥特暗黑：铅灰黑底、尖拱图框、占满拱顶的花窗、荆棘纹只出现一次"></a>
</p>

### 十二张作品的风格基因对照

| # | 风格基因（主 + 辅） | 情绪定位 | 场景 | 该守住的纪律 |
|---|---|---|---|---|
| 01 | 赛博霓虹 + 机器美学 | 科技酷感 | 暗色仪表盘 / 科技产品页 | 荧光只给边线数字；暗部 ≥52%；色相 ≤4；禁紫渐变 |
| 02 | 瑞士平面 + 蒙德里安网格 | 清晰理性 | 数据报告 / B 端信息页 | 浅底 ≥45%；色彩像素 ≤12%；色相 ≤3（唯一强调色） |
| 03 | 中国画留白 + 计白当黑 | 东方古韵 | 文化产品页（茶） | 留白 ≥62%；色彩像素 ≤6%；色相 ≤3；一图一印 |
| 04 | 吉卜力手绘 + 水彩淡彩 | 梦幻治愈 | 亲子教育 / 疗愈系 | 浅底 ≥52%；饱和度压一档；阴影永远是暖色 |
| 05 | 浮世绘扁平 + 手作不规则边 | 东方古韵 | 展览专题 / 和风创意页 | 一版一色（色相 ≤3）；平涂无渐变无阴影 |
| 06 | 巴洛克聚光 + 金色细线 | 暗黑崇高 | 演出海报 / 人物故事页 | 暗部 ≥45%；亮部 ≤12%；只有一个光源；金色只做线 |
| 07 | 洛可可粉彩 + 美人绘的柔 | 甜美容爱 | 甜品花店 / 少女向 | 浅底 ≥60%；明度高、饱和度中低；装饰两种封顶 |
| 08 | 极简主义 + Kelly 单色面 | 清晰理性 | 作品集 / 高端产品 hero | 留白 ≥46%；色相 ≤2；点睛色限一个整块 |
| 09 | 波普拼贴 + 沃霍尔复制 | 荒诞幽默 | 潮流品牌 / 传播图 | 色彩像素 ≥18%；本戴点只做局部；色相 ≤4 |
| 10 | 构成主义海报 + 照片拼贴 | 热血冲击 | 活动 KV / 招募宣言 | 三色封顶（色相 ≤3）；零圆角零阴影；一条对角线统治 |
| 11 | 赛璐璐动漫 UI + 斜切动势 | 热血冲击 | 二次元产品 / 角色主站 | UI 色必须从立绘取；两分 cel 阴影；禁高级灰 |
| 12 | 哥特暗黑 + 废墟崇高 | 暗黑崇高 | 恐怖悬疑游戏 / 史诗长图 | 暗部 ≥58%；色相 ≤3；点睛色二选一；禁正黑 |

> 上表的纪律**不是形容词，是程序断言**。`demos/_src/qa_style.py` 直接从截图像素反推亮度 / 暗部 / 留白 / 色相 / 饱和度，逐条比对上表阈值；
> `demos/_src/qa_layout.py` 另查溢出、越界、遮挡、字号与 WCAG 对比度。
> 当前状态：**13 页布局检查 0 问题 · 12 张图共 34 条基因纪律断言全部通过**。

### 这十二张是由谁做出来的

| 项 | 值 |
|---|---|
| 生成者 | **pi agent**（终端里的编码智能体） |
| 驱动模型 | **DeepSeek V4.1 Flash**（shudie 供应商） |
| 风格决策 | 本仓库 `references/` 四层种子库（L1 总库 / L2a 情绪档 ×10 / L2b 代码基因卡 ×12 / L2c 风格章档 ×24+后记） |
| 渲染方式 | headless Chromium 143 实时渲染，2× 设备像素比，无损 WebP |
| 字体 | 全部本地内嵌（约 2MB 子集，开源许可），**断网也能复现同样的图** |

> 📌 **署名在哪**：十二张页面各自底部的 `风格基因 <b>中国画留白</b> · 辅 计白当黑`、`Built by <b>pi agent</b> × <b>DeepSeek V4.1 Flash</b>` 就是署名本身——它不是水印贴纸，而是参与每张作品构图的一部分（用该作品自己的字体气质、颜色与排版规则排的）。

> ⚠️ **这一节是「演示与验收材料」，不是种子库本体。** `demos/` 只读取 `references/` 做风格决策，不改动任何种子；`deploy/` 的部署脚本也只搬运 `references/` 与 `TASTE.md`，所以新增本目录**不影响任何已部署实例**。

---

## 这是什么

核心思想：**风格即基因** —— 色彩 × 光线 × 笔触 × 构图 × 情绪，五个基因位。
任何需要审美的输出，先选基因、再动手。

**适用范围：一切需要美学的产物**——图片与插画、HTML/网页/长图、PPT、Word 与文档排版（简历/报告/公文）、图表与数据可视化、UI 与皮肤、视频分镜，乃至生活与社会关系中的审美（穿搭配色、家居氛围、礼物与请柬、仪式感设计）。人眼需要美学，人与人的关系也需要美学。

```
创作任务 → 情绪定位 → 查种子选基因（1主+1辅）→ 基因按媒介翻译成参数 → 一句话自检 → 交付 → 用户反馈 → 风味日志 → 种子库进化 → 下次更好
```

**激活词原理**：艺术家名/风格名是 LLM 预训练美学基因的激活锚点——prompt 里直接点名「马远一角构图」「卡拉瓦乔 Tenebrism」比任何形容词都精准。本系统的职责：帮你选对激活词 + 把激活出的审美翻译成可执行参数。

## 文件清单

| 文件 | 作用 |
|------|------|
| [`AGENT-INJECTION.md`](AGENT-INJECTION.md) | ⭐ 通用注入提示词 + 部署说明（最小接入看这个） |
| [`SKILL.md`](SKILL.md) | Agent 决策层（四层路由版，安装脚本直接拷贝用） |
| [`TASTE.md`](TASTE.md) | 审美操作系统文档版：审美观 5 条 + 决策流程 + 情绪→种子索引 |
| [`references/art-seeds.md`](references/art-seeds.md) | L1 总库速查：全量种子单行表（250+ 艺术家，按需查询勿全文注入） |
| [`references/ART-SEEDS-LOG.md`](references/ART-SEEDS-LOG.md) | ⭐ 风味日志（活文档）：实战搭配 + 踩坑记录，**贡献只需回填一行** |
| [`references/moods/`](references/moods/) | L2a 情绪档 ×10：每情绪主推种子的五基因详解 + 媒介适配 + 翻车清单 |
| [`references/code-genes/`](references/code-genes/) | L2b 代码基因卡 ×12：写代码出图直接抄的部署提示词 + CSS 变量块 + 反模式 |
| [`references/chapters/`](references/chapters/) | L2c 风格章档 ×24+后记：《艺术风格百科大全》原文全量，每艺术家 2-3 句细述 |
| [`demos/`](demos/) | ⭐ **十二风格样本墙**：12 个真实渲染的演示页 + 高清截图 + 渲染/质检脚本（`index.html` 为浏览入口） |
| [`docs/METHODOLOGY.md`](docs/METHODOLOGY.md) | 五基因方法论白皮书：为什么「风格即基因」、怎么把审美变成可判定的断言 |
| [`deploy/`](deploy/) | 各类智能体的详细部署文档 + 一键脚本（上面指令的权威细节都在这里） |

### 合规与工程化文件

| 文件 | 作用 |
|------|------|
| [`LICENSE`](LICENSE) | ⭐ 单一许可文件：三许可分治说明 + 逐路径对照 + **MIT / CC BY 4.0 / OFL 1.1 三份官方完整正文** |
| [`CITATION.cff`](CITATION.cff) | 学术引用格式（GitHub 自动生成「Cite this repository」按钮） |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | 贡献指南：回填一行风味日志 / 补录新种子 / 新增代码基因卡的门槛 |
| [`docs/ATTRIBUTION.md`](docs/ATTRIBUTION.md) | 出处、署名模板与 **AI 使用披露** |
| [`docs/TRADEMARKS.md`](docs/TRADEMARKS.md) | 商标、作品名与在世创作者姓名声明 |
| [`docs/changes/`](docs/changes/) | 已完成的变更过程档案（CHANGE / HEALTH / PRD / SPEC / TRACEABILITY） |
| [`scripts/`](scripts/) | 合规与完整性闸门（`check_assets.sh` · `check_integrity.py` · `check_links.py`） |

## 知识库分层架构（重 agent 按需加载，禁止全文注入）

```
L0  TASTE.md                      决策层：情绪定位 → 该查哪层（随 skill 安装）
│
├─ L2a moods/（10 份）            知道情绪时第一落点
│    每情绪 2-3 粒主推种子 · 五基因详解 · 媒介适配 · 翻车清单
│
├─ L2b code-genes/（12 张）       写代码出图（网页/长图/dashboard）
│    部署提示词 + CSS 变量块 + 激活词 + 反模式，直接抄参数
│
├─ L2c chapters/（24 章+后记）     深挖某艺术家/流派
│    原文零删减 · 每艺术家 2-3 句细述 + AI Prompt Keywords
│
└─ L1 art-seeds.md                全量单行速查总表（关键词全局搜）
```

### 全仓结构（v2.0.0 开源结构）

```
aesthetic-brain/
├── README.md / SKILL.md / TASTE.md / AGENT-INJECTION.md   门面与决策层
├── LICENSE / LICENSE / LICENSE / LICENSE
├── CITATION.cff / CONTRIBUTING.md / CHANGELOG.md
├── references/
│   ├── art-seeds.md             L1 全量种子库（核心资产）
│   ├── ART-SEEDS-LOG.md         风味日志（活文档）
│   ├── code-genes/  ×12         L2b 代码基因卡
│   ├── moods/       ×10         L2a 情绪档
│   └── chapters/    ×25         L2c 分章（含许可与商标免责头）
├── docs/
│   ├── METHODOLOGY.md           五基因方法论白皮书
│   ├── ATTRIBUTION.md           出处 · 署名 · AI 使用披露
│   ├── TRADEMARKS.md            商标与在世创作者声明
│   └── changes/                 已完成的变更档案
├── demos/                       12 张演示页 + 截图 + 渲染/质检脚本
├── scripts/                     合规与完整性闸门
├── deploy/                      各 agent 形态的部署文档与脚本
└── .github/workflows/ci.yml     三道 CI 闸门

# 不随仓库分发：sources/（百科底稿 docx，私有资产层）
```

### 旁边的 `demos/`（演示与验收材料，不随部署安装）

```
demos/
├── index.html              样本墙：12 张作品 + 每张的风格说明（浏览入口）
├── 01..12-*.html            十二张作品，每张文件头都写明「选自哪粒种子 / 激活词 / 守哪几条纪律」
├── _assets/fonts/*.woff2    开源字体子集（约 2MB／30 字重，随仓库分发，保证断网可复现）
├── _assets/shots/*.webp     高清截图 2880×1800（README 与样本墙使用）
└── _src/                   字体子集化 · 实时渲染截图 · 布局质检 · 风格纪律校验
```

它证明的是**这套方法真的能落成可验收的成品**，而不是只给了一堆风格描述。
部署时不需要它——`deploy/` 的脚本只搬 `references/` 与 `TASTE.md`。

## 手动部署（不想发指令、自己动手时）

| 你的 Agent | 方式 | 文档 |
|-----------|------|------|
| **Claude Code** | skill + CLAUDE.md 薄注入（一键脚本） | [`deploy/claude-code.md`](deploy/claude-code.md) |
| **OpenClaw** | skill 内部放置（`<workspace>/skills/taste/`）+ SOUL/AGENTS 注入 | [`deploy/openclaw.md`](deploy/openclaw.md) |
| **Codex / 有 skill 机制的 agent** | 装 `~/.codex/skills/taste/` 等 skill 目录 + 全局规则文件薄注入 | [`deploy/generic-agents.md`](deploy/generic-agents.md) |
| **pi / workbuddy / codebuddy / Trae / Qoder / hermas**（无 skill 机制） | 全局规则文件薄注入 + 种子库留仓库 clone 目录 | [`deploy/generic-agents.md`](deploy/generic-agents.md) |
| 通用 ChatBot（无文件机制） | 系统提示词整段注入 | [`deploy/generic-agents.md`](deploy/generic-agents.md) |

```bash
# Claude Code 最快路径
git clone https://github.com/hhx465453939/agent-taste-seed-system.git \
  && bash agent-taste-seed-system/deploy/install-claude-skill.sh
```

## 使用原则

1. **种子库按需查询，不注入上下文**——创作时按情绪/章节/关键词检索需要的种子卡即可，全文进上下文是浪费
2. **风味日志是系统的灵魂**——每次交付后把搭配与反馈记进 [`references/ART-SEEDS-LOG.md`](references/ART-SEEDS-LOG.md)，定期同步回本仓库，越陈越香
3. **本仓库是活文档**——新风格、新配方、新混种，欢迎 PR 补录（见 [`CONTRIBUTING.md`](CONTRIBUTING.md)）

## 出处、AI 使用披露与许可

### 出处

本项目由《艺术风格百科大全》（24 章 250+ 艺术家/风格）提炼而成。**底稿不随仓库分发**，仓库只保留结构化后的 Markdown 产物（`references/chapters/` + `art-seeds.md`）。

### AI 使用披露

诚实披露是开源许可体系的基本要求：

| 环节 | 是否使用 AI |
|---|---|
| 百科内容撰写（章节正文、艺术家条目、风格描述） | **编者执笔为主** |
| 结构化整理（分章切分、单行种子卡提炼、情绪归类、CSS 变量翻译） | **AI 辅助** |
| `demos/` 演示页与 `_src/` 脚本 | **AI 生成**（pi agent × DeepSeek V4.1 Flash） |
| 演示截图 | 机器渲染（headless Chromium，非 AI 生图） |

详见 [`docs/ATTRIBUTION.md`](docs/ATTRIBUTION.md)。

### 商标与在世创作者

正文中出现的一切第三方商标、作品名、公司名与创作者姓名，均属**事实性描述**，不构成关联或授权，权利归各自所有者。

> ⚠️ **对外使用红线**：**不得**把「用 XX 画师名字生成」作为产品卖点或宣传话术。
> 在世艺术家姓名 + 商业 AI 生成涉及人格权与不正当竞争争议。
> 本仓库提供的是**审美决策方法**，不是「复刻在世创作者」的工具。详见 [`docs/TRADEMARKS.md`](docs/TRADEMARKS.md)。

### 许可

本项目采用**按资产类型分治的三许可结构**：

```
内容（种子库 / 文档 / 截图）：  CC BY 4.0         署名即可，可商用
代码（脚本 / CI / 配置）：      MIT               可商用，保留版权声明
字体（woff2 子集）：            上游 OFL / Apache 随包可分发，已按 OFL 改名
```

- **完整许可结构与逐路径对照** → [`LICENSE`](LICENSE)
- **只想用脚本**（想嵌进商业产品的构建流程）→ MIT 不限制，直接用 [`demos/_src/`](demos/_src/)
- **想用内容做商业产品** → CC BY 4.0 允许，保留署名并说明是否修改即可（见 [`docs/ATTRIBUTION.md`](docs/ATTRIBUTION.md)）
- **引用本项目的方法论** → 按 [`CITATION.cff`](CITATION.cff) 或 [`docs/ATTRIBUTION.md`](docs/ATTRIBUTION.md) 署名

> ⚠️ 「商业使用」不再受许可限制。义务只有三条：署名、指向许可的链接、说明是否修改。
> 边界情形的最终判断建议咨询执业律师——这是建议，不是法律意见。

### 版本轨迹：v3.0.0 起再许可

**v2.x 及更早**的内容版本以 **CC BY-NC-SA 4.0**（非商业 + 相同方式共享）发布，
那些旧版本继续适用其原始许可 —— 已经授予的许可不可撤销。
**自 v3.0.0 起内容改为 CC BY 4.0**：只保留署名，去掉 NonCommercial 与 ShareAlike，
因此整个仓库现在是**完全开源**。

### 质量与合规闸门（三道 CI）

```bash
bash scripts/check_assets.sh         # 无第三方媒体 · 无外部抄录 · 无敏感信息 · 许可文件齐备
python3 scripts/check_integrity.py   # 种子条目数 · 分章免责头 · 演示与截图配对 · 字体命名合规
python3 scripts/check_links.py       # 全仓相对链接无断链
python3 demos/_src/qa_layout.py      # 布局：溢出 / 越界 / 遮挡 / 字号 / WCAG 对比度
python3 demos/_src/qa_style.py       # 风格基因纪律断言（34 条）
python3 demos/_src/check_font_licenses.py   # 字体子集 OFL 命名合规（§1 §3）
```

当前状态：**6 项闸门全绿**。CI 在每次 push / PR 自动跑（见 [`.github/workflows/ci.yml`](.github/workflows/ci.yml)）。

## License

- 文本资产：**CC BY 4.0** — 详见 [`LICENSE`](LICENSE) §三
- 代码资产：**MIT** — 详见 [`LICENSE`](LICENSE) §二
- 内置字体子集：上游 OFL / Apache-2.0 — 详见 [`LICENSE`](LICENSE) §四

总览入口：[`LICENSE`](LICENSE)
