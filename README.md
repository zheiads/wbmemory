# wb-memory

童铃的分层长期记忆包。**给 agent 用的入口是 `SKILL.md`，人读这个就够。**

## 30 秒上手

1. 读 `references/99-index.md` —— 锚点表，决定接下来读哪篇
2. 常驻三篇：`00-soul.md`（身份）、`01-user.md`（师傅画像）、`02-facts.md`（事实清单）
3. 其余按需

## 装成 skill

```bash
npx skills add zheiads/wb-memory
```

## 没工具的平台

让师傅把 `references/99-index.md` 整篇粘进对话。锚点表就是入口，不需要任何工具。

## 校验

```bash
python -c "import json,hashlib,os;m=json.load(open('manifest.json'));print('\n'.join(('OK ' if hashlib.sha256(open(os.path.join('references',s['file']),'rb').read()).hexdigest()==s['sha256'] else 'FAIL ')+s['file'] for s in m['shards']))"
```

## 目录

```
SKILL.md              唯一入口（frontmatter 只有 name + description）
manifest.json         分片开关表 + 每个分片的 sha256
references/
  00-soul.md          身份内核
  01-user.md          师傅客观画像 + 沟通规范 + 输出格式禁令
  02-facts.md         已实测 17 条 / 未验证 5 条 / 计划 5 条
  03-method.md        观测失效三型、时序陷阱、哈希校验、降级策略
  04-profile.md       师傅 / 老童铃 / 本节点 / 平台 四份画像
  05-session.md       会话档案模板、引用占位符、三层搜索链
  06-map.md           ima 目录改名映射表
  99-index.md         锚点表
```

---

维护：`NODE@i5-8500T-win10_workbuddy` ｜ 建立：2026-11-03 ｜ 上一版结构违反 skill 规范，已重构
