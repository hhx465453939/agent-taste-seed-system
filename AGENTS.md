# 仓库治理规则 / Repository Governance

> **适用对象**：在本仓库内工作的人与 agent（改文件、跑闸门、提 PR 的一方）。
> **不适用**：把本仓库当作 skill 安装到别处之后的审美行为 —— 那由 [`AGENT-INJECTION.md`](AGENT-INJECTION.md) / [`SKILL.md`](SKILL.md) / [`TASTE.md`](TASTE.md) 管，与本文件无关。
>
> **为什么本文件用中文**：它治理的主体是中文资产层（`references/` 与决策层文档）。英文读者请先看 [`README.md`](README.md) 与 [`docs/en/`](docs/en/)；门面之外的内容本身就是中文的，这一点不打算改（理由见 §1.2）。

---

## 0. 三条不可协商的前提

任何改动都不得牺牲这三条。它们不是偏好，是仓库的存在条件。

| # | 前提 | 为什么 |
|---|---|---|
| 1 | **纯文本，零第三方资产** | 不得提交任何第三方图片、截图、扫描件、PDF、音视频；`demos/_assets/` 里的截图与字体子集是本项目自产，属唯一例外。混入一件第三方素材，整个仓库的合规前提就塌了 |
| 2 | **许可按资产类型分区** | 代码 MIT（`*.py` / `*.sh` / `.github/**`）· 内容 CC BY 4.0（Markdown / HTML / 截图）· 字体上游 OFL / Apache。LICENSE 是脚本产物，不许手改 |
| 3 | **六道闸门全绿才算完成** | 见 §4。红着提交等于把静默故障转嫁给下游使用者 |

---

## 1. 双语治理（本仓库的核心约定）

### 1.1 语言分区：什么语言，写在哪里

| 层 | 文件 | 语言 | 理由 |
|---|---|---|---|
| **门面** | `README.md` | **英文** | GitHub 默认首页，承担站外检索与英文读者承接 |
| **门面镜像** | `README.zh-CN.md` | 中文 | 中文读者入口，与英文版信息量对等 |
| **门面文档** | `docs/en/*.md` | **英文** | 方法论、出处、商标、验证证据的英文版 |
| **资产文档** | `docs/*.md`（不含 `en/`） | 中文 | 与种子库正文同语言，保持术语一致 |
| **决策层** | `SKILL.md` · `TASTE.md` · `AGENT-INJECTION.md` | 中文 | agent 读取，模型多语言无碍；与种子库术语一致 |
| **种子库** | `references/**` | 中文 | 见 §1.2，**硬约束：不翻译** |
| **部署手册** | `deploy/*.md` | 中文 | 英文读者由英文 README 内嵌的自足指令覆盖 |
| **贡献 / 变更** | `CONTRIBUTING.md` · `CHANGELOG.md` | 中文 | 与维护者语言一致 |
| **治理** | `AGENTS.md` · `CLAUDE.md` | 中文 | 本文件 |

**判定新增文档归属的决策树**（按顺序问，命中即停）：

1. 它是否承担**对外检索曝光**（GitHub 首页、搜索引擎、英文读者第一落点）？→ 英文，放门面位。
2. 它是否**解释门面里已经说过的事**，且面向英文读者？→ `docs/en/`。
3. 它是否**描述种子本身**（风格、艺术家、情绪、CSS 基因、风味日志）？→ 中文，进 `references/`。
4. 它是否是**给 agent 的执行指令**？→ 中文，进决策层。
5. 其余 → 中文，跟随所在目录的既有语言。

> 语言选择只由「读者是谁」决定，不由「作者顺手用哪种语言」决定。

### 1.2 种子库不翻译（硬约束）

`references/` 下的 21 万字符（art-seeds 全量单行表、24 章分章、10 份情绪档、12 张代码基因卡）**保持中文单语**。禁止提交「把种子库翻成英文」的 PR。三条理由：

1. **会反噬核心机制。** 本仓库的原理是「艺术家名 / 风格名 = LLM 预训练美学基因的激活锚点」。同一粒种子在库里存中英两个名字，检索时权重会被拆散，风味日志与外部引用也会对不上号。
2. **维护必然腐烂。** 每加一粒种子要同步两处，单人项目撑不过三个月，最终变成「英文库停在半年前」——比没有英文库更糟，因为它会误导读者。
3. **ROI 断崖。** 门面 + 装机手册（约 5.7 万字符）值得翻，因为决定「要不要用」；种子库正文服务的是「已经决定要用的人」，而他们已经在中文语境里了。

**英文读者的替代路径**：`docs/en/METHODOLOGY.md` 解释方法论，`docs/en/ATTRIBUTION.md` 给出引用方式，英文 README 的文件清单逐项标注了哪些文件是中文。

### 1.3 同步规则：什么时候必须两边都改

| 改动类型 | 英文门面 | 中文镜像 | 中文资产 |
|---|---|---|---|
| 版本号、安装命令、文件路径、种子数量、闸门数量 | ✅ 必改 | ✅ 必改 | 视情况 |
| 新增/删除门面小节 | ✅ | ✅ | — |
| 许可条款、商用口径 | ✅ | ✅ | — |
| 种子正文、情绪档、基因卡、风味日志 | — | — | ✅ |
| 决策层流程（SKILL / TASTE） | — | — | ✅ |
| 修错别字（仅限单侧语言） | 单侧 | 单侧 | 单侧 |

**硬规则**：门面事实性变更必须**同一次提交**内两侧同步。只改一侧的 PR 视为未完成。

### 1.4 链接分流：每种语言的页面只链自己那一版

```
README.md        →  docs/en/METHODOLOGY.md  docs/en/ATTRIBUTION.md
                    docs/en/TRADEMARKS.md   docs/en/EVIDENCE-seed-brain.md
README.zh-CN.md  →  docs/METHODOLOGY.md     docs/ATTRIBUTION.md
                    docs/TRADEMARKS.md      docs/EVIDENCE-seed-brain.md
```

- 英文页不得链中文 docs 来「代替」英文版；中文页同理。
- 允许跨语言链接的唯一情形：目标文件只有单语版本，且**必须显式标注语言**（例：``[`CONTRIBUTING.md`](CONTRIBUTING.md) — *Chinese*``）。
- `docs/en/*.md` 内的相对链接比中文版多一层：`../demo` → `../../demo`。这是最容易漏的地方，`scripts/check_links.py` 会兜住。

### 1.5 语言切换头：必须成对

两个 README 顶部各有一组 badge，且互为镜像：

```markdown
<p align="right">
  <a href="README.md"><img src="https://img.shields.io/badge/README-English-2f81f7?style=flat-square" alt="English"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/README-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-e05252?style=flat-square" alt="简体中文"></a>
</p>
```

- 两组 badge 内容完全一致，位置都在文件第一行之前。
- 不许只在一侧挂切换头；不许新增第三种语言而不更新两处。
- 新增语言时：文件名用 `README.<bcp47>.md`（如 `README.ja.md`），并且**所有版本**的切换头都要加进去。

### 1.6 已知的不对称，不要「顺手修」

当前结构是刻意选择的，不是历史遗留：

```
README.md          英文默认
README.zh-CN.md    中文镜像
docs/*.md          中文原地（CI、CITATION、LICENSE 全部依赖这些路径）
docs/en/*.md       英文增量
```

**为什么中文 docs 不搬进 `docs/zh/`**：有四处硬编码依赖它们的位置——

1. `scripts/check_integrity.py` 的 `LEGAL_FILES`（三个路径 + >200 字节断言）
2. `scripts/check_assets.sh` 第 6 节的许可文件清单
3. `scripts/build_license.py` 生成的 LICENSE 正文（两处指向 `docs/ATTRIBUTION.md` / `docs/TRADEMARKS.md`）
4. `CITATION.cff` 的说明字段

搬目录 = 一次**迁移**，必须同时改这四处并重新生成 LICENSE。不许在无关 PR 里顺手做。

同理：`deploy/` 无英文版是刻意的——英文 README 内嵌了可直接复制的完整安装指令，英文读者零跳转即可装完。补 `deploy/en/` 属于新功能，不是修 bug。

---

## 2. 目录语义：什么放哪，什么不许放

| 路径 | 语义 | 不许放 |
|---|---|---|
| `references/` | 种子库本体（内容资产） | 脚本、演示页、临时笔记 |
| `references/moods/` `code-genes/` `chapters/` | 三个分层，条目数有下限断言 | 新建子目录（会打破 `check_integrity` 的计数） |
| `demos/` | 演示与验收材料，不随部署安装 | 种子内容、私有素材 |
| `demos/_assets/` | 自产截图与字体子集（唯一允许的二进制） | 任何外部下载的图片 / 字体 |
| `scripts/` | 闸门脚本（MIT） | 内容资产 |
| `deploy/` | 各 agent 的部署文档与脚本 | 种子库副本 |
| `docs/changes/` | 已完成的变更档案，只增不改 | 未完成的草稿 |
| `sources/` | 百科底稿（私有，**不入库**） | 任何会被 commit 的文件 |

---

## 3. 提交与版本

**格式**（Conventional Commits + 中文描述）：

```
<type>(<scope>): <中文描述>

type:  feat | fix | refactor | chore | docs | ci | test | style
scope: 受影响的模块名，如 i18n / seed-brain / license / demos / ci
```

- 破坏性变更在 type 后加 `!`：`refactor(seed-brain)!: 删除本地算法脚本`
- 版本号变动写进标题尾部：`（v0.3.0）`
- 一个提交只做一件事。翻译门面与修闸门不要混在一起。
- 用户可见的变更必须同步更新 `CHANGELOG.md`（中文）。

### 3.1 版本号出现在 5 处（本仓库没有 pyproject）

本仓库**不发包**，所以没有 `pyproject.toml`，版本号只活在文档与元数据里。
发版时必须**五处同时改**，缺一处就是对外不一致：

| 位置 | 字段 | 谁读它 |
|---|---|---|
| `CITATION.cff` | `version:` + `date-released:` | GitHub 的 Cite this repository、学术引用 |
| `README.md` | `> Version **vX.Y.Z** · YYYY-MM-DD` | 英文门面第一屏 |
| `README.zh-CN.md` | `> 版本：**vX.Y.Z** · YYYY-MM-DD` | 中文门面第一屏 |
| `CHANGELOG.md` | `## vX.Y.Z · YYYY-MM-DD` | 人读；Release notes 的来源 |
| `AGENTS.md` 本节 | 最近发布记录 | 维护者与 agent 读的现状 |

自检（四条必须同号）：

```bash
grep -m1 '^version:' CITATION.cff
grep -m1 'Version \*\*v' README.md
grep -m1 '版本：\*\*v' README.zh-CN.md
grep -m1 '^## v' CHANGELOG.md
```

### 3.2 发布：手动建 GitHub Release（无 PyPI、无 release.yml）

```bash
# 1. 五处版本号同步（§3.1），六道闸门全绿（§4）
# 2. 提交并推送
git push origin main
# 3. 建 Release（在当前 main HEAD 打 tag）
gh release create vX.Y.Z --title "..." --notes-file <notes> --target main
```

- tag 命名 `vX.Y.Z`，与 `CITATION.cff` 的 `version` 一致（**没有自动断言**，靠人工核对）；
- Release notes 必须写清：许可/行为变化、迁移边界、闸门结果；
- 已发布的 tag / Release **不改写**（历史许可不可撤销）。

### 3.3 许可治理：改许可要同时动四处

`LICENSE` 是 `scripts/build_license.py` 的产物，**永远不手改**。改许可时的完整耦合面：

| 文件 | 改什么 |
|---|---|
| `scripts/license-sources/*.txt` | 官方正文原文（逐字），来源与抓取日期登记在同目录 `README.md` |
| `scripts/build_license.py` | §零/§一/§三/§五 的说明文字、`SPDX` 行、`read_source()` 的文件名 |
| `scripts/check_integrity.py` | `LEGAL_FILES` 清单；`check_chapter_headers` 的断言字符串 |
| `scripts/check_assets.sh` | 第 6 节「三份官方正文必须在场」的清单 |

然后 `py scripts/build_license.py` 重生成 `LICENSE`，再跑六道闸门。
**改文件名（如 `cc-by-nc-sa-*` → `cc-by-4.0-*`）会同时命中这四处**，改漏一处闸门就红。

当前许可：内容 **CC BY 4.0** · 代码 MIT · 字体上游 OFL/Apache。
v3.0.0（2026-10-24）起为 CC BY 4.0；**v2.x 及更早为 CC BY-NC-SA 4.0，旧版本保留原许可**。

---

## 4. 闸门纪律（全绿才算完成）

CI 分三个 job，本地对应六条命令。**改动前先跑一遍建立基线，改动后必须全绿。**

```bash
# 本机 Windows 用 py；CI 与 Linux/macOS 用 python3
# 若终端报 UnicodeEncodeError，先 export PYTHONIOENCODING=utf-8

bash scripts/check_assets.sh         # 合规：无第三方媒体 / 无抄录痕迹 / 无敏感信息 / 许可文件齐备
py scripts/check_integrity.py        # 完整性：条目数 / 体积下限 / 分章免责头 / 演示配对 / 许可分区 / LICENSE 同步
py scripts/check_links.py            # 全仓相对链接（含双语分流与 docs/en 的层级）
py demos/_src/qa_layout.py           # 布局：溢出 / 越界 / 遮挡 / 字号 / WCAG 对比度
py demos/_src/qa_style.py            # 风格基因纪律断言（34 条）
py demos/_src/check_font_licenses.py # 字体子集 OFL 命名合规
```

**会静默退化的三类改动，必须连带执行**：

| 改动 | 必须连带做 | 不做的后果 |
|---|---|---|
| `references/art-seeds.md` / `moods/` / `code-genes/` / `chapters/` | `seedbrain build --profile profiles/taste.json` 并提交 `SEED-INDEX.md` + `seed-index.jsonl` | CI 报索引不同步；检索结果与源文件脱节 |
| `demos/*.html` 的可见文本 | `build_fonts.py` → `render_shots.py` | 字变豆腐块但测试不报错 |
| LICENSE 素材或 `LICENSE_ZONES` 语境 | `py scripts/build_license.py` | `check_integrity` 第 7 项报不同步 |

**禁止**：为了让 CI 过而放宽断言、删断言、注释掉检查。若确判断言本身错了，改断言可以，但必须在 PR 说明里写清「旧断言为什么错、新断言为什么对」。

---

## 5. 内容红线

| 红线 | 依据 |
|---|---|
| 不得复制 / 转述他人原文（书籍、访谈、社媒、画集） | 只写自己组织的**事实性描述**；表达方式受著作权保护 |
| 不得提交任何作品图像 | 复制权与信息网络传播权 |
| 在世创作者只写**可公开讨论的视觉特征** | 见 [`docs/TRADEMARKS.md`](docs/TRADEMARKS.md) |
| 不得把「用 XX 画师名字生成」写成卖点或宣传话术 | 人格权 / 不正当竞争 |
| 提交信息与文档里不得出现真实姓名、邮箱、内网地址、凭据、本机绝对路径 | `check_assets.sh` 会拦 |

---

## 6. 修改这份文件本身的规则

1. 改 `AGENTS.md` / `CLAUDE.md` 需要在 PR 说明里写**动机**（是哪次事故或哪类重复劳动促成的）。
2. 两份文件的规则不得互相矛盾。`CLAUDE.md` 通过 `@AGENTS.md` 导入本文件，只允许追加 Claude Code 专属的操作细节，**不许另立一套治理规则**。
3. 规则必须可执行：要么指向一个脚本、一条命令、一个阈值，要么给出可判定的判定顺序。写「保持一致性」「注意质量」这类无法判定的要求视为无效条目。
4. 新增规则前先确认它**不是**已有闸门已经覆盖的事——重复规则会让人以为闸门不可靠。

---

## 7. 当前已知的未覆盖项（诚实清单）

| 项 | 现状 | 风险 |
|---|---|---|
| 中英门面同步 | 靠人工，无 CI 断言 | 改了英文忘改中文，两侧事实不一致 |
| `docs/en/*` 与 `docs/*` 内容漂移 | 同上 | 英文读者拿到过时信息 |
| 种子库单语 | 刻意设计（§1.2） | 英文读者无法直接检索种子正文 |

前两项如果出现实际事故，再加 `scripts/check_i18n_sync.py`：比对成对文件的结构化指纹（标题层级序列、相对链接目标集合、代码块命令集合），偏差超阈值即 fail。**在那之前不预先建空壳检查**——没有事故史的空断言只会被绕过。

---

## 8. 待开工（已登记，尚未进入规范）

| 项 | 要点 |
|---|---|
| 宣传静态站 | `demos/` 的 12 张实时渲染页作为效果展示；首屏放项目信息、README 里的 agent 部署命令（GitHub 链接）、QQ 群 `1027282854` 引流；部署到 Cloudflare 子域（个人域名根下加项目名）；DNS 记录需单独配置 |

> 上线后删掉本行条目——本表不是待办清单的长期居所。

---

*本文件是仓库治理约定，不是法律意见。许可与合规问题以 [`LICENSE`](LICENSE) 与 [`docs/ATTRIBUTION.md`](docs/ATTRIBUTION.md) 为准。*
