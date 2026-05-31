# 小红书课件一键交付包

> 给 Claude Code（或 Codex、Cursor 等 AI 编程助手）用的 Skill。拖入课件 PDF，AI 自动帮你生成小红书课件商品的全部物料。

## 这是什么？

一个小红书课件电商的 **AI Skill**。

你卖过课件就知道——课件本身做好了只是第一步。你还得做封面图发小红书引流，做逐字稿让买家觉得值，做教学设计显得专业，做样机图让买家看到"上课效果"。一套下来，排版设计的时间比做课件还久。

这个 Skill 就是让 AI 替你干这些活。把它放进 Claude Code 的 skills 目录，对话里把课件 PDF 拖进去，AI 就自动把下面这些东西全给你出出来。

**不需要你会写代码，只需要一个 Claude Code（或者类似的 AI 编程工具）。**

## 它帮你出什么

| 产物 | 用在哪 |
|------|--------|
| 🖼️ **拼图封面** ×3 | 发小红书笔记的封面图（二图/五图/十二图竖版，1200×1600） |
| 📝 **逐字稿** · Word | 买家拿到课件不知道怎么讲？这份稿子就是答案 |
| 📐 **教学设计** · Word | 教学目标、流程、重难点——显得你专业，提高转化率 |
| 📺 **样机展示图** ×36 | 6 种教室场景 × 课件前 6 页，小红书笔记正文必备 |

## 怎么用

### 第一步：把 Skill 装进你的 AI 工具

把 `SKILL.md` 复制到 Claude Code 的 skills 目录：

```
~/.claude/skills/
```

或者在 Codex / Cursor 中把整个仓库作为项目上下文加载。

### 第二步：跟 AI 说句话

打开 Claude Code，把课件 PDF 拖进去，然后说：

> "帮我生成这个课件的小红书交付包"

就行了。AI 会自动完成：

1. 渲染 PDF → 页面图
2. 生成拼图封面（直接能发小红书）
3. 写逐字稿和教学设计 Word 文档
4. 把课件前 6 页套进教室样机场景

所有产物输出到 PDF 同目录，即拿即用。

### 如果你不用 AI 工具，想手动跑脚本

也可以直接用 Python 脚本：

```bash
pip install pymupdf pillow python-docx

# 先复制配置
cp agents/config.example.json agents/config.local.json
cp agents/stage2_content.example.json agents/stage2_content.local.json

# 三段串行执行
python agents/stage1_collage.py   # 拼图封面
python agents/stage2_docs.py      # 逐字稿 + 教学设计
python agents/stage3_mockup.py    # 样机展示图
```

编好 `config.local.json` 里的路径就能跑。

## 适用场景

- 📕 **小红书课件店铺**：批量生成商品笔记的封面和正文配图
- 📦 **课件产品交付**：买家下单后一键出包，不用手工整理
- 🏫 **公开课 / 师训资料**：配套教案+逐字稿+展示图一次出齐

## 仓库结构

```
.
├── SKILL.md              # AI Skill 主文件（Claude Code 读取这个）
├── agents/
│   ├── stage1_collage.py          # 小红书拼图封面
│   ├── stage2_docs.py             # 逐字稿 + 教学设计 Word
│   ├── stage3_mockup.py           # 教室样机图
│   ├── config.example.json        # 配置模板
│   └── stage2_content.example.json
└── references/
    └── 样机图/                    # 6 张教室场景模板
```

> 💡 **关于样机图**：仓库里的 6 张教室场景是我自己放的默认模板。如果你有自己的样机图想用，直接把 `references/样机图/` 里的图片替换掉，然后跟 Claude Code 或 Codex 说一句「样机图我换了，帮我把脚本修一下适配新的图」就行，AI 会帮你搞定。

## 注意事项

- 样机模板图片请确认拥有商业使用或再分发权限
- 不要把真实课件、客户信息、API 密钥提交到公开仓库
- 需要完整版（含真实项目数据）请使用私有 Skill，本仓库仅作公开参考
