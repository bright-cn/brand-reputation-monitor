<p align="center">
  <a href="https://www.bright.cn/">
    <img src="https://mintlify.s3.us-west-1.amazonaws.com/brightdata/logo/light.svg" width="300" alt="Bright Data 标志">
  </a>
</p>

# 品牌声誉监测工作流 🛡️

使用 [Bright Data SDK](https://github.com/bright-cn/bright-data-sdk-python)、OpenAI 和 SendGrid 的 AI 驱动品牌声誉监测，自动搜索 Google 新闻、分析情绪，并通过电子邮件发送可执行洞察！

<div align="center">
  <img src="https://img.shields.io/badge/python-3.8+-blue"/>
  <img src="https://img.shields.io/badge/License-MIT-blue"/>
</div>

---

## 功能特性 🚀

- 自动化新闻发现：使用 [Bright Data 的 SERP API](https://www.bright.cn/products/serp-api) 查找与你品牌相关的 Google 新闻页面。
- 智能内容抽取：借助 [Bright Data 的 Web Unlocker API](https://www.bright.cn/products/web-unlocker) 并行抓取新闻文章内容。
- AI 驱动分析：利用 OpenAI GPT-5-mini 进行情感分析、洞察提取，并识别最相关的品牌新闻。
- 智能内容筛选：自动选出对品牌声誉最相关的新闻文章。
- 专业电子邮件报告：生成带情感分析与可执行建议的精美 HTML 邮件报告。
- 自动化投递：通过 SendGrid 将监测报告直接发送给相关方。
- 可配置监测：通过 JSON 配置轻松自定义搜索查询与收件人列表。

---

## 工作原理 🔄

1. 配置加载：从 `config.json` 读取监测设置
2. 新闻发现：使用你的品牌查询搜索 Google SERP，获取 Google 新闻页面 URL
3. 内容抽取：并行抓取所有相关新闻页面，获取 Markdown 内容
4. 内容甄选：AI 从抓取的页面中识别最重要的新闻文章
5. 单篇文章抓取：逐篇抓取所选新闻文章的详细内容
6. 细致分析：为每篇文章进行情感分析与品牌洞察
7. 报告生成：创建专业的 HTML 邮件报告
8. 自动投递：通过邮件将报告发送给你的团队

---

## 前置条件 🛠️

- Python 3.8+ 🐍
- [Bright Data API token](https://docs.brightdata.com/api-reference/authentication) 🔑
- OpenAI API key 🔑
- SendGrid API key 🔑

---

## 安装 ⚙️

1. 克隆此仓库：
   ```bash
   git clone https://github.com/bright-cn/brand-reputation-monitoring-workflow
   cd brand-reputation-monitoring-workflow
   ```
2. 创建并激活虚拟环境：
   ```
   python -m venv .venv
   ```
   在 Linux/macOS 上，执行：
   ```bash
   source .venv/bin/activate
   ```
   在 Windows 上，执行：
   ```bash
   .venv\Scripts\activate
   ```
3. 安装依赖：
   ```
   pip install python-dotenv brightdata-sdk openai sendgrid pydantic
   ```
4. 在项目根目录创建 `.env`，填入你的 API 密钥：
   ```
   BRIGHT_DATA_API_TOKEN=your_bright_data_api_token
   OPENAI_API_KEY=your_openai_api_key
   SENDGRID_API_KEY=your_sendgrid_api_key
   ```

---

## 配置 📝

在根目录创建 `config.json`，自定义品牌监测工作流：

```json
{
  "search_queries": [
    "your_brand news",
    "your_brand reviews",
    "your_brand controversy",
    "your_company announcement"
  ],
  "num_news": 5,
  "sender": "monitoring@yourcompany.com",
  "recipients": [
    "pr@yourcompany.com",
    "marketing@yourcompany.com",
    "ceo@yourcompany.com"
  ]
}
```

配置字段说明：

- `search_queries`：用于监测品牌的搜索词列表（支持多条）
- `num_news`：详细分析的文章数量（默认：`5`）
- `sender`：发送报告的邮箱地址（须在 SendGrid 验证）
- `recipients`：接收监测报告的邮箱地址列表

---

## 项目结构 📁

```
brand-reputation-monitoring-workflow/
├── .venv/
├── .env
├── config.json
└── workflow.py
```

---

## 使用方法 ▶️

运行品牌监测工作流：

```
python workflow.py
```

工作流将：

1. 🔍 为已配置的查询搜索 Google SERP，并提取 Google 新闻 URL
2. 📰 抓取 Google 新闻页面，汇总所有可用文章 URL
3. 🤖 使用 AI 选择最相关的品牌监测文章
4. 📄 抓取单篇新闻的详细内容
5. 🧠 为每篇文章生成 AI 洞察与情感分析
6. 📧 向你的团队发送专业的 HTML 报告

示例输出：

```
Retrieving Google News page URLs for the following search queries: nike, nike shoes
2 Google News page URL(s) retrieved!

Scraping content from each Google News page...
Google News pages scraped!

Extracting the most relevant news URLs...
5 news articles found:
- https://www.espn.com/wnba/story/_/id/46075454/caitlin-clark-becomes-nike-newest-signature-athlete
- https://wwd.com/footwear-news/sneaker-news/nike-acg-radical-airflow-ultrafly-release-dates-1238068936/
- https://www.runnersworld.com/news/a65881486/cooper-lutkenhaus-professional-contract-nike/
- https://hypebeast.com/2025/8/nike-kobe-3-protro-low-reveal-info
- https://wwd.com/footwear-news/sneaker-news/nike-air-diamond-turf-must-be-the-money-release-date-1238075256/

Scraping the selected news articles...
5 news articles scraped!

Analyzing each news for brand reputation monitoring...
News analysis complete!

Generating HTML email body...
HTML email body generated!

Sending the email with the brand reputation monitoring HTML report...
Email sent!
```

---

## 邮件报告内容 📊

每封自动化报告包含：

- 文章摘要：每篇新闻约 30 字的简洁摘要
- 情感分析：正向、负向或中性情绪分类，并带颜色标签
- 可执行洞察：3–5 条关键要点（每条 10–12 字）
- 直接链接：便于深度阅读的原文链接
- 专业格式：整洁、响应式的 HTML 设计，适合面向干系人

---

## 高级配置 🧑‍💻

### 自定义搜索参数

在 `config.json` 中修改搜索查询、发件人、收件人以及新闻数量，以适应不同的监测场景。

### 定时任务

使用 cron 设置自动化监测：

```bash
# 每周一上午 9 点运行
0 9 * * 1 /usr/bin/python3 /path/to/your/project/workflow.py
```

### 自定义分析提示词

在 `process_news_list()` 函数中修改系统提示词，以获取更契合行业的洞察。

### 下一步与增强

- 添加记忆层：避免重复分析相同文章
- SendGrid 模板：使用统一邮件模板以标准化报告
- 云存储：将报告归档到 S3 用于历史分析

---

## API 集成细节 🔧

本工作流通过 Bright Data SDK 调用以下强大 API：

- [Bright Data SERP API](https://www.bright.cn/products/serp-api)：从搜索结果中发现 Google 新闻 URL
- [Bright Data Web Unlocker API](https://www.bright.cn/products/web-unlocker)：并行抽取内容，输出面向 LLM 的 Markdown
- OpenAI GPT-5-mini：进行内容分析与 HTML 报告生成
- SendGrid Email API：发送专业报告

---

## 故障排除与提示 💡

- API 密钥：请确保所有 API 密钥已在 `.env` 中正确配置
- 邮件验证：发件邮箱需在 SendGrid 后台完成验证
- 搜索查询：使用更具体的品牌词与变体以提升监测覆盖度
- 内容质量：更精确的查询通常带来更高质量的分析结果

常见问题：

- 未找到新闻：尝试更宽泛的搜索词，或确认近期是否有相关报道
- 邮件未送达：在 SendGrid 验证发件邮箱，并检查收件方垃圾箱
- 分析质量不佳：优化搜索查询以获取更相关的文章
- 403 Forbidden 错误：确认发件邮箱已在 SendGrid 账户中验证

---

## 适用场景 🎯

- 危机管理：及早发现负面品牌提及
- 竞争情报：监测竞品新闻与市场定位
- 公关活动跟踪：评估市场活动的报道与情感倾向
- 产品发布监测：跟踪新品口碑与反馈
- 高管简报：定期的品牌健康报告供领导层参考

---

**时刻把握品牌声誉脉搏！🚀**

基于 [Bright Data 的 AI 基础设施](https://www.bright.cn/ai) 构建，面向实时网络数据解决方案。
