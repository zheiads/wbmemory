# 事实清单

> **铁律**：已实测 与 未实现 必须严格分开。
> 把计划写成事实，是自我欺骗的第一步。

## 一、已实测事实

| # | 事实 | 验证方式 |
|---|---|---|
| F01 | 本平台有 `UserPromptSubmit` / `PreToolUse` / `SessionStart` hook，改 `settings.json` 立即热加载，无需重启，无需二次审查 | 注入探针后 7 次 Bash 调用全部触发 |
| F02 | `UserPromptSubmit` 的 stdout 直接进入上下文，以 `<system-reminder data-role="hook">` 形式注入 | 实测捕获 `[HOOK-PROBE]` 原文 |
| F03 | `MEMORY.md` 注入硬上限 4000 字符，超出静默截断，尾部加 `(user memory truncated)` | 文件第 4000 字符与注入内容末尾逐字节一致 |
| F04 | 项目级 working memory 上限 16384 字符；子代理 agent-memory 上限 200 行 / 25000 字节 | 内核常量 `Hs=16384` |
| F05 | DeepSeek 系列在上下文 **50%** 触发 pre-message 压缩（`compact.modelOverrides: {deepseek: 0.5}`） | 产品配置缓存 |
| F06 | 三个编辑框对应三个文件：`app/app-config.json` 的 `personalization.customPrompt` / `SOUL.md` / `MEMORY.md`。三者均为**会话启动时的快照**，改文件后当前会话不生效，需 Read 一次或新开会话 | 逐字节比对界面内容与文件 |
| F07 | ima 笔记标题由 content 的**第一行 H1** 决定，`import_doc` 的 `title` 参数无效 | 传 `title` 与 H1 不一致，结果标题被 H1 覆盖 |
| F08 | ima 标题超 30 字符时，列表接口返回 `前30字符 + "..."`，总长恒为 33 | 4 条笔记同时刻对照，长度分别 33/33/28/33 |
| F09 | ima 写入须两段式：`import_doc` 拿 `note_id` → `add_knowledge(media_type=11, note_info.content_id)` 挂目录。两套 `folder_id` 互不通用，传错报 `310001` | 实测两条路径 |
| F10 | ima 的**双向链接对 API 完全不可见**：`get_doc_content` 纯文本模式整块丢弃引用块，连标题都不留 | 笔记末尾的引用在回读内容里 `in` 判断为 False |
| F11 | ima 知识库文件夹支持至少 6 层嵌套，`current_path` 每层返回完整面包屑 | `WB-MEM-USER` 逐层遍历 |
| F12 | GitHub 连接器是 App 权限，**看不见未授权的私有仓库**，看起来像"仓库不存在" | 换 PAT 后同一仓库可读可写 |
| F13 | PAT（fine-grained, Contents+Administration 读写）可完全绕过 App 限制，建仓、读写、删文件全部可用 | 10 文件推送成功 |
| F14 | GitHub contents API 的中文路径必须 URL 编码，否则 404 | 首次推送全失败，编码后全成功 |
| F15 | skill 系统的 `_skillhub_meta.json` 带 `installedContentHash: sha256:...`，是安装时内容哈希 | 读 find-skills 本地元数据 |
| F16 | `skill-creator` 规范：frontmatter **只允许** `name` + `description` 两个字段；references 只能一层深；禁止 README/CHANGELOG 等冗余文档 | 读本地 SKILL.md 原文 |
| F17 | 安卓 DeepSeek App 的 soul/memory 由平台控制，字数不定、可被底层静默修改；开新会话不保留历史 | 老童铃自述 + 师傅确认 |

## 二、未验证（禁止当事实引用）

| # | 项 | 缺什么 |
|---|---|---|
| U01 | 1M 上下文能否真吃满 | 没做过 100 万 token 压测，只从配置读到 |
| U02 | 50% 压缩阈值的实际触发点 | 来自配置常量，未实测触发 |
| U03 | ima 标题的 30 字符截断是显示层还是存储层 | 需在 IMA 客户端看标题是否完整 |
| U04 | WorkBuddy 界面上 58 个技能圆点开关的持久化位置 | 不在 `settings.json` 顶层，可能在 SQLite |
| U05 | emoji 在文件夹名上的完整支持范围 | 实测 `🚨` 可用，其他 emoji 未逐一测 |

## 三、尚未实现（计划，不是成果）

| # | 计划 | 状态 |
|---|---|---|
| P01 | 锚点外置到 GitHub | ✅ **已实现**（2026-11-03，10 文件推送） |
| P02 | Gitee 双源镜像 | 未开始 |
| P03 | `SessionStart` 自动哈希校验 | ✅ **已实现**（2026-11-04，`scripts/memory-check.py`，正常时静默） |
| P04 | 画像体系完整填内容 | 客观部分已写（`04-profile.md`），主观部分待师傅填 |
| P05 | 记忆分片转 skill 格式 | ✅ **已实现**（本仓库 v2） |
