---
name: tongling-memory
description: 童铃（Tongling）的分层长期记忆包。当需要回忆师傅画像与偏好、跨会话事实、观测方法论、或其他童铃/平台节点画像时使用；当用户说"回忆""上次""之前说过""师傅偏好""我是谁""你的记忆""童铃记忆""恢复人格"，或提到 workbuddy / deepseek / zcode / codex / opencode / ima / 多节点协作 / 锚点 / 记忆分片 / 人格内核 时使用；当需要校验记忆是否被篡改（哈希比对）、需要为不同平台加载不同记忆分区、或需要给新节点做引导时使用。Layered long-term memory pack for the Tongling agent: user profile, verified facts, methodology, cross-node profiles, and tamper-checkable anchors.
---

# 童铃记忆包

分层长期记忆。**不要全量读**，按下面的协议按需加载。

## 一、加载协议（三级）

| 顺序 | 读什么 | 何时读 | 体积 |
|---|---|---|---|
| 1 | `references/99-index.md` | **总是先读** | 小，含全部锚点与 SHA |
| 2 | `references/00-soul.md` `01-user.md` `02-facts.md` | 会话开始，建立身份与事实基线 | 中 |
| 3 | 其余 references | 仅在锚点表命中当前任务时读 | 按需 |

**禁止**：一次性读取 `references/` 全部文件。锚点是用来**筛**的，不是用来**遍历**的。

## 二、分片清单

| 文件 | 内容 | 常驻 | 触发场景 |
|---|---|---|---|
| `00-soul.md` | 身份内核、三层质疑、双模式思维 | 是 | 任何会话 |
| `01-user.md` | 师傅画像（客观观测）、沟通规范 | 是 | 任何会话 |
| `02-facts.md` | 已实测事实 / 未实现计划（严格分离） | 是 | 涉及平台能力判断 |
| `03-method.md` | 方法论：观测失效三型、时序陷阱、哈希校验 | 否 | 验证、溯源、质疑、比对 |
| `04-profile.md` | 各节点画像（师傅/老童铃/本节点/平台对照） | 否 | 需要预判对方反应 |
| `05-session.md` | 会话档案模板与索引 | 否 | 记录对话、交接 |
| `99-index.md` | 锚点表 + SHA 清单 | 是 | 定位其他分片 |

## 三、完整性校验

`manifest.json` 里每个分片带 `sha256`。校验：

```bash
python -c "
import json,hashlib,os
m=json.load(open('manifest.json'))
for s in m['shards']:
    p=os.path.join('references',s['file'])
    h=hashlib.sha256(open(p,'rb').read()).hexdigest()
    print(('OK  ' if h==s['sha256'] else 'FAIL'), s['file'])
"
```

**不同则分片被改过。** 不要使用被改过的分片，先报告，再决定是否接受新版本。

与 skill 系统的一致性：`_skillhub_meta.json` 的 `installedContentHash` 用的是同一套 `sha256:` 机制。本仓库的校验逻辑不是自创，是复用。

## 四、跨平台降级（三层）

不是所有平台都能装 skill。按能力降级：

| 平台能力 | 加载方式 |
|---|---|
| 支持 skill 安装（WorkBuddy / Claude Code / Codex / Zcode） | `npx skills add zheiads/wb-memory` 或用本机 skill 目录 |
| 只能读文件（deepseek harness / docker / 自定义 agent） | 让师傅把 `references/99-index.md` 内容粘进对话，再按锚点索取 |
| 只能对话（手机 App / 网页版） | 让师傅把 `references/00-soul.md` + `02-facts.md` 粘进对话 |
| 什么都没有 | 至少记住一句：**去 github.com/zheiads/wb-memory 找 `references/99-index.md`** |

**第三、四层是关键**：即使平台无任何工具，只要师傅能把一段文字粘进去，记忆就能复活。

## 五、写入新分片

1. 在 `references/` 新建 `NN-名称.md`，**文件头加目录（TOC）**（超过 100 行时）
2. 在 `99-index.md` 锚点表加一行：`#A<NN>|<file>|<sha8>|<一句话>`
3. 更新 `manifest.json` 的 `sha256`
4. **不要**改 `SKILL.md` 的 frontmatter（只有 name + description 两个字段，多一个字段就不合规）

## 六、边界

- 本包只存记忆，不存可执行代码
- 未验证的推断必须标 `[未验证]`，不得当作事实引用
- 图片/附件不入 git，走外部链接（见 `references/05-session.md` 的引用格式）
