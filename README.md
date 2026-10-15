# 错题数据仓 · bio-error-data

**这是你的真实错题与知识点。只放数据，不放代码。**

配套工具在：`~/.config/opencode/skills/bio-error-vault/`（另一个仓库）

---

## ⚠️ 这个仓库是公开的，但只放结构，不放真实错题

远端：`https://github.com/mc-lhz/StudyDbDatabase`（Public）

当前仓里**只有目录骨架，没有任何真实数据**。这是有意保持的。

**真实错题绝不能提交。** 里面有学校名、手写姓名、考号、含水印的卷子照片，
推到公开仓即使后来删掉文件，**git 历史里仍然找得回来**——
这不是道德说教，是 git 的物理特性：删文件只改当前版本，历史对象还在。

⚠️ **现在的 `.gitignore` 并没有拦住真实错题**——
`data/subjects/生物/errors|points|exams/` 下的 `.md` 是会被 `git add` 到的。
所以第一条防线是纪律：**录完真实错题，不要 `git add -A`**。

需要自动兜底的话，往 `.gitignore` 加：

```
data/subjects/*/errors/*
data/subjects/*/points/*
data/subjects/*/exams/*
data/subjects/*/assets/*
data/subjects/*/indexes/*
```

（加了之后目录仍可见，内容不入库。）

本地 git 仍然当**时间机器**用：

```bash
# 看一道错题的完整复习史
git log -p --follow "data/subjects/生物/errors/BIO-20261013-001.md"

# 看某个月所有录入
git log --since="2026-10-01" --stat
```

---

## 目录结构

```
data/subjects/生物/
├── exams/      一次考试一份档案
├── errors/     一道错题一个文件      ← 真源，只改这里
├── points/     一个知识点一个文件    ← 真源，只改这里
├── assets/     图片，命名 {id}-{NN}.ext
└── indexes/    派生索引              ← 全脚本重建，禁止手工编辑
```

`indexes/` 下的文件由 `RebuildIndexes.py` 全量生成。
**手工改它们没有任何意义**——下次重建会被覆盖，而且状态会漂移。

---

## 现在是空的，这是正常的

系统刚建好，还没录第一条错题。

对 AI 说「今天生物做了第三章，选择题错两道……」就会往 `errors/` 里落文件。

**每次录入后 AI 都会请你复核一遍**——
因为 AI 生成的错因判断和标准答案会错，
生物术语错一个字（`线粒体基质` 写成 `线粒体基质胶`）照着背就是学错东西，比不学更糟。
复核之前，这些记录不计入统计、不进复习队列。

---

## 别删这个仓库

它是这套系统里**唯一不可再生**的东西——代码可以重写，错题只能重做一遍。