# Claude Code 项目规则

本仓库的治理规则见 @AGENTS.md —— Claude Code 会把该文件作为项目指令一并加载。**本文件不另立规则，只补充 Claude Code 特有的操作细节。**

---

## 这个仓库是什么（先建立正确预期）

**不是一个应用代码库，是一个「内容资产 + 闸门」仓库。**

- 主要工作对象是 Markdown 与 HTML，不是业务逻辑
- `scripts/` 与 `demos/_src/` 是闸门与演示工具，改动频率远低于内容
- 因此「跑测试」通常意味着跑六道合规闸门，而不是单元测试
- `references/` 是核心资产，**读它、检索它，但不要改它**（除非任务明确要求增改种子）

## 本机命令适配（Windows）

```powershell
# 本机没有 python3 别名，用 py
py scripts/check_links.py

# 终端默认 GBK，会因 ANSI 彩色符号与中文报 UnicodeEncodeError
$env:PYTHONIOENCODING = "utf-8"
```

```bash
# CI 与 Linux/macOS 环境下按 AGENTS.md §4 的 python3 写法执行
```

## 常见任务的执行顺序

| 任务 | 顺序 |
|---|---|
| 改门面文档 | 先跑一遍六道闸门建立基线 → 改 → 再跑一遍；双语事实变更按 AGENTS.md §1.3 两侧同步 |
| 改种子库 | 改源文件 → `seedbrain build --profile profiles/taste.json` → 提交 `SEED-INDEX.md` + `seed-index.jsonl` → 跑闸门 |
| 改演示页文本 | 改 HTML → `build_fonts.py` → `render_shots.py` → `qa_layout.py` + `qa_style.py` |
| 改许可 | 四处同改（AGENTS.md §3.3：素材 / `build_license.py` / `check_integrity.py` / `check_assets.sh`）→ `py scripts/build_license.py` → 六道闸门 |
| 发版 | 五处版本号同步（AGENTS.md §3.1）→ 六道闸门 → `git push origin main` → `gh release create vX.Y.Z --target main` |
| 新增英文文档 | 放 `docs/en/`，相对链接比中文版多一层（`../x` → `../../x`）→ `check_links.py` |

## 不要做

1. **不要手改 `LICENSE`** —— 它是 `scripts/build_license.py` 的产物，手改会被 `check_integrity.py` 第 7 项判为不同步。
2. **不要为了过闸门而放宽断言** —— 见 AGENTS.md §4 末尾。断言错了可以改，但要在提交说明里给出理由。
3. **不要在 `references/` 里新建子目录** —— 会打破条目数下限断言。
4. **不要把种子库翻成英文** —— AGENTS.md §1.2 的硬约束。
5. **不要用 bash 重定向或 heredoc 写文件** —— 用编辑工具，否则编码与行尾会把中文写坏。
6. **不要提交 `sources/`、`__pycache__`、`node_modules`、任何第三方图片或 PDF**。
7. **不要只改一处版本号就发版** —— 五处（AGENTS.md §3.1）**没有自动断言**，靠人逐条 grep 核对。
8. **不要为了「宣传」往仓库里塞截图或统计数据** —— 演示页只放真实渲染结果，见 AGENTS.md §5 内容红线。

## 双语相关的两个易错点

- `docs/en/*.md` 里的向上跳转比中文版**多一层**（`../LICENSE` → `../../LICENSE`）。写错不会立刻报错，直到 `check_links.py` 跑起来。
- 语言切换头必须**两侧成对**。只改一侧的 PR 视为未完成（AGENTS.md §1.5）。
