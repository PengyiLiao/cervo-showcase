# Cervo 第一视角数据展示网站

网址：**https://showcase.cervo-tech.com**

仓库：https://github.com/PengyiLiao/cervo-showcase

这个仓库就是网站本身。在 GitHub 网页上改了文件并点 **Commit changes**，大约 1 到 2 分钟后网站会自动更新，不需要其他操作。

> 这个仓库是**公开的**，谁都能看到里面的内容。不要放客户名称、采集员的个人信息、密码、钥匙之类的东西。

## 文件都是干什么的

| 文件 | 内容 |
| --- | --- |
| `data.json` | 网站上的**数字和卡片**：首屏数字、首屏 6 段视频、场景和每张视频卡片的文字、任务表、难度例子、metadata 字段、设备参数。大部分修改都在这里。 |
| `index.html` | 页面的样子，以及**固定的说明文字**（标题、各段介绍、pipeline 那 9 条过滤规则等）。 |
| `v/` | 视频（每段十几秒的 mp4）。 |
| `p/` | 视频封面图（jpg），名字和视频一一对应。 |
| `vercel.json`、`robots.txt` | 网站设置（不让搜索引擎收录），一般不用动。 |

## 在 GitHub 网页上怎么改一个文件

1. 点开文件（比如 `data.json`），右上角点铅笔图标 ✏️。
2. 直接改文字。
3. 点右上角绿色的 **Commit changes**，写一句改了什么，再点一次 **Commit changes**。
4. 等 1 到 2 分钟，刷新 https://showcase.cervo-tech.com 看效果。

上传新视频：进入 `v/` 文件夹，点 **Add file → Upload files**，把文件拖进去，再点 **Commit changes**。封面图同样传到 `p/`。

## 常见修改

### 改某张视频卡片上的文字

在 `data.json` 里搜卡片上的那句话（比如任务描述），找到后改。每张卡片是这样一段（箭头后面是说明，`data.json` 里没有箭头）：

```
{
  "video": "v/278ecfad.mp4",      ← 视频文件
  "poster": "p/278ecfad.jpg",     ← 封面图，没有可以写 ""
  "dur": 328,                     ← 整段 episode 的时长（秒），卡片上显示成 5:28
  "lv": "hard",                   ← 难度：hard / medium / easy
  "task_id": "watch_repair",
  "task_zh": "钟表维修",           ← 卡片标题（中文）
  "task_en": "Watch repair",      ← 卡片标题（英文）
  "desc_zh": "……", "desc_en": "……",       ← 任务描述
  "reason_zh": "……", "reason_en": "……",   ← 难度判断理由
  "skill": "Repair & Maintenance", "skill_zh": "维修保养",
  "job": "Watch repairer", "job_zh": "修表师",
  "l2": "Watch Repair Station", "l2_zh": "修表工作台",   ← 视频左上角的场所
  "l1": "Retail and Consumer Goods"
}
```

中文和英文是分开的两项，**两个都要改**，切换语言时才一致。

### 删掉一段视频

1. 在 `data.json` 里找到那张卡片，把从 `{` 到对应的 `}` 整段删掉，连同它后面的逗号（如果它是最后一张，就删前面的逗号）。
2. 再到 `v/` 和 `p/` 里把对应的文件删掉（点开文件，右上角 `…` → Delete file）。不删也不影响网页，只是占地方。

### 加一段视频

1. 把视频传到 `v/`，封面传到 `p/`。文件名只用英文字母、数字和横线。
2. 在 `data.json` 里复制同一个场景下的一张卡片，粘贴在它后面（两张之间用逗号隔开），把里面的内容改成新视频的。

视频建议：mp4（H.264），宽 800 左右，10 到 20 秒，5 MB 以内，不要声音。没有封面图就写 `"poster": ""`，网页会用视频第一帧。视频文件太大，国内打开会很慢。

### 改首屏的数字

`data.json` 最上面的 `stats` 一段：`hours` 小时数、`episodes` 个数、`hard_pct` hard 占比、`sites` 场地数等。改完首屏会跟着变。

### 改固定的说明文字

在 `index.html` 里搜那句话。同一句话一般有中文和英文两处，形如：

```html
<span class="zh">中文这句</span><span class="en">English sentence</span>
```

两处都改。

## 让 AI 帮忙改（推荐）

把要改的文件内容整个复制给 Claude 或 ChatGPT，并说清楚要改什么，例如：

> 下面是一个网站的 data.json。请在「维修服务」场景里删掉 task_id 为 smart_lock_repair 的那张卡片，其他内容不要动，返回完整的 data.json。

拿到结果后，在 GitHub 上打开 `data.json`，点铅笔，全选后粘贴替换，再 Commit。

## 改坏了怎么办

- 如果网页底部出现红色提示「data.json 读不出来」，多半是少了逗号或引号。把 `data.json` 交给 AI 检查格式，或者退回上一版。
- 退回上一版：打开那个文件，点右上角 **History**，找到改坏之前的那一版，点进去复制旧内容，再回到文件用铅笔整段替换并 Commit。
- 实在弄不好，告诉 Peter。所有修改都有记录，不会丢。

## 谁能改

只有被加为本仓库协作者（Collaborator）的人能直接改。其他人能看、能复制，但改不了网站。
