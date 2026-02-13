---
description: 自动搜寻并筛选当前最热门、最具传播价值的 AI/科技选题。
---

# 选题挖掘助手 (Topic Selector)

这个 Skill 用于从全网挖掘高潜力的 AI 和科技选题，确保内容的时效性和爆款潜质。

## 目标 (Goal)
找到当下公众最感兴趣、或者信息差最大的 AI/科技新闻或工具。

> [!IMPORTANT]
> **CRITICAL RULE**: 任何新闻如果超过 **72小时**（以当前时间 2026-02-05 倒推），**绝对禁止**入选。如果日期模糊，必须查证。

## 搜索源 (Data Gathering)
使用以下策略进行搜索，确保信息绝对新鲜：
1.  **Search Query**: 
    - `latest artificial intelligence news`
    - `latest AI news "DeepSeek" OR "OpenAI" OR "Anthropic" OR "Google"`
    - `viral AI agents tools news`
    - `trending AI social apps`
    - `site:reddit.com (r/LocalLLaMA OR r/Singularity OR r/ArtificialInteligence) "AI" "news" when:24h`
    - `site:x.com "AI" "trending" when:24h`
2.  **Time Window**: `when:3d` (严格限制在最近 **72小时** 内)
3.  **Result Verification**: **再次人工核对日期**。例如：今天是 2月5日，那么 2月1日及以前的新闻直接丢弃。


## 爆款指数 (Viral Index)
对所有候选选题进行打分 (0-100)，评分维度如下：

| Metric | Weigh | Points | Description |
| :--- | :--- | :--- | :--- |
| **Timeliness (时效性)** | 20% | 0-20 | 必须是 Breaking News (<24h 满分)。 |
| **Practicality (实操性)** | 40% | 0-40 | **核心权重**。能否直接解决用户痛点？是否有立即可用的工具/教程？能否提升效率？ |
| **Novelty (新颖性)** | 20% | 0-20 | 是不是新产品线？技术突破？(常规更新低分) |
| **Visual (视觉性)** | 10% | 0-10 | 是否有演示视频/动图？(适合视频化) |
| **SEO (搜索热度)** | 10% | 0-10 | 关键词趋势是否在上涨？ |

**筛选门槛**:
*   计算总分：`Total = Timeliness + Practicality + Novelty + Visual + SEO`
*   只有 **Total >= 80** (或实操性单项 > 35) 的选题才能进入 Top 10 推荐池。

## 排序与输出 (Ranking & Output)
1.  按总分从高到低排序。
2.  严格使用以下 Markdown 格式输出 Top 10。

### Output Format Template

```markdown
# 🚀 今日AI热点 Top 10 (YYYY-MM-DD)

### 1. [新闻标题] - 爆款指数: [分数]
- **来源**: [Source Name](URL)
- **关键词**: #Tag1 #Tag2
- **评分理由**:
  - ⚡ 时效性 ([分数]): [简短理由]
  - 🛠 实操性 ([分数]): [简短理由]
  - 👁 视觉性 ([分数]): [简短理由]
- **摘要**: [简要介绍新闻内容，1-2句话]

### 2. ...
```

## 示例 (Example)
### 1. Anthropic 发布 "Cowork"：非程序员的AI文件管理Agent - 爆款指数: 86
- **来源**: [Indiatimes](https://...)
- **关键词**: #Anthropic #Cowork #AIAgent
- **评分理由**:
  - ⚡ 时效性 (95 -> 28.5): 刚刚发布，属于最新动态。
  - 🛠 实操性 (90 -> 22.5): 直接面向普通用户的文件管理工具，上手即用。
  - 👁 视觉性 (70 -> 10.5): 交互界面适合演示。
- **摘要**: Anthropic 推出了一款名为 "Cowork" 的新工具，旨在帮助非编程人员通过AI代理自动管理文件和浏览器任务，大幅降低了使用门槛。
