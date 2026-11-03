# 命名映射表

> **改名前先读这里。** 否则会出现"改了不知道原来叫什么"。

## 一、ima 知识库目录（`[TL]🧑‍🍼WB-MEM-USER` / `ima_kb_Y0Me6jfv`）

### 已完成的改名

| 原名 | 现名 | 理由 |
|---|---|---|
| `[TL]ima-intel-i5-8500T-win10-workbuddy` | `[TL]NODE@i5-8500T-win10_workbuddy` | 统一节点命名：硬件-系统_软件 |
| `[TL]ima-intel-i5-8500T-win10-deepseek_harness` | `[TL]NODE@i5-8500T-win10_deepseek_harness` | 同上 |
| `[TL]ima-debian_linux-docker_deepseek_harness` | `[TL]NODE@debian-docker_deepseek_harness` | 系统在前，容器在后 |
| `[TL]ima-intel-i5-8500T-win10-xiaomi_mimo_desktop` | `[TL]NODE@i5-8500T-win10_xiaomi_mimo` | 去冗余后缀 |
| `[TL]ima-intel-i5-8500T-win10-zcode` | `[TL]NODE@i5-8500T-win10_zcode` | 同上 |
| `[TL]ima-intel-i5-8500T-win10-chatgpt_desktop _codex` | `[TL]NODE@i5-8500T-win10_chatgpt_codex` | 修多余空格 |
| `[TL]ima-00-SOUL`（节点内） | `00-SOUL` | 父路径已声明节点，删冗余 |
| `[TL]ima-01-USER` | `01-USER` | 同上 |
| `[TL]ima-02-PROJECT` | `02-MEMORY` | PROJECT 语义窄，MEMORY 覆盖更广 |
| `[TL]ima-05-USER_MEMERY` | `05-USER_MEMORY` | 修拼写 |
| `[TL]ima-06-COMMANDS-MD` | `06-COMMANDS` | 去冗余后缀 |
| `[TL]ima-师傅与安卓中国_deepseek_应用的老童铃-V1的对话` | `[TL]HUB_老童铃对话档案` | 归入 HUB，去平台长描述 |
| `[TL]ima-师傅想分享...其他癌脑体的成长经验与输出成果` | `[TL]HUB_成长经验` | 缩写 |
| `[TL]ima-师傅想分享...文章或链接或文件资源等` | `[TL]HUB_分享资源` | 缩写，下分 ART/LINK/IMG/FILE |
| `[TL]ima-不同领域高权限的师傅备份体...协作交接方法` | `[TL]HUB_协作交接` | 缩写 + 修 `童玲`→`童铃` |
| `[TL]ima-待师傅新增_还能重命名_..._等` | `[TL]TEMP_待办` | **目录名不是 TODO 清单**，内容移入夹内笔记 |

### 待改名（尚未执行）

| 原名 | 建议新名 | 理由 | 风险 |
|---|---|---|---|
| `[TL]ima-师傅想分享给每个不同环境下的童铃备份体的话` | `[TL]HUB_师傅原话` | 师傅原话是**最高优先级输入**，比任何童铃转述权威。应与其他 HUB 平行，不塞进"协作交接" | 改名后原有 2 篇笔记的路径引用会断，需同步更新 |

**理由展开**：`HUB_协作交接` 装的是"童铃之间怎么配合"，`HUB_师傅原话` 装的是"师傅对所有童铃说什么"。前者是平级协商，后者是自上而下指令。**混在一起会导致新节点先读到二手总结，而不是一手指令。**

## 二、命名规则

```
[TL]<类型>@<节点>_<人类描述>        # 节点目录
[TL]HUB_<共享主题>                  # 跨节点共享
[TL]TEMP_<临时事项>                 # 待处理
<NN>-<TYPE>                        # 节点内部分区，不带节点前缀
```

### 为什么内层不再带 `@节点`

外层已声明节点，内层重复违反 DRY。**例外**：笔记和文件会被搬走，离开目录树后没有祖先上下文，所以**独立笔记的标题必须自带完整标识**。

### 字符限制（实测）

| 位置 | 限制 | 超出后果 |
|---|---|---|
| 笔记标题 | 30 字符 | 列表接口返回前 30 + `...`，总长 33 |
| 文件夹名 | 至少 6 层无问题 | 未测出上限 |
| 知识库名 | 未测 | — |

**前缀必须在前 30 字符内**，否则白名单判断失效。版本号不能放末尾。

## 三、GitHub references ↔ ima 目录 结构对齐表

**原则**（师傅 2026-11-03 定）：结构类似，命名可以不一样，靠本表映射解决。

### 现状对照

| ima 目录（NODE 节点下） | GitHub 分片 | 对齐状态 |
|---|---|---|
| `00-SOUL` | `00-soul.md` | ✅ 编号与语义都对 |
| `01-USER` | `01-user.md` | ✅ |
| `02-MEMORY` | `02-facts.md` | ⚠️ 编号对，名字不同（MEMORY vs facts） |
| `03-SESSION` | `05-session.md` | ❌ **编号交叉** |
| `04-ARCHIVE` | 无 | ⚠️ ima 独有（git 有历史，不需要 archive） |
| `05-USER_MEMORY` | 无 | ❌ **与 01-USER 语义重复** |
| `06-COMMANDS` | `06-map.md` | ❌ 编号对但语义不同（COMMANDS vs MAP） |
| `99-INDEX` | `99-index.md` | ✅ |

### 三个缺口

| GitHub 有但 ima 没有 | 建议 |
|---|---|
| `03-method.md` | ima 缺方法论文档。建议把 `03-SESSION` 改名为 `03-METHOD`，session 移到 05 |
| `04-profile.md` + `04a`~`04f` | ima 缺画像体系。建议 `04-ARCHIVE` 改名 `04-PROFILE`，archive 并入 TEMP |
| `05-session.md` | 与 `03-SESSION` 对应，但编号应为 05 |

### 建议的最小改动方案（只改 3 处）

```
03-SESSION     → 03-METHOD      （方法论文档放进来）
04-ARCHIVE     → 04-PROFILE     （画像放进来，archive 并入 [TL]TEMP_待办）
05-USER_MEMORY → 05-SESSION     （会话档案放进来，与 GitHub 05-session.md 对齐）
```

改完后 8 个目录与 14 个分片一一对应（04-PROFILE 内部再分 6 个子夹对应 04a~04f）。

**不改也能用**——靠本表映射即可。改的价值只在于「人一眼能对上」，机器本来就读 id 不读名字。

## 四、emoji

| 位置 | 支持 | 证据 |
|---|---|---|
| 笔记标题 | ✅ | `🧠TL-RECON-...` 完整保留 |
| 文件夹名 | ✅ | `🚨01-USER` 在 `title` / `folder_info.name` / `current_path.name` 三处一致 |

**注意**：v1 曾错误断言"列表接口会剥离 emoji"，实为跨时点对比造成的假结论。详见 `03-method.md` 时序陷阱。

## 五、错别字纠正记录

| 错误 | 正确 | 出现位置 |
|---|---|---|
| 童玲 | 童铃 | 目录名、部分笔记 |
| MEMERY | MEMORY | 文件夹名 |
| `chatgpt_desktop _codex` | `chatgpt_desktop_codex` | 多余空格 |
| `11-02-1-11` | `11-02 01:11` | 文件名，录入失误 |
