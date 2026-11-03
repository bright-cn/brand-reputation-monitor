<p align="center">
  <a href="https://www.bright.cn/">
    <img src="https://mintlify.s3.us-west-1.amazonaws.com/brightdata/logo/light.svg" width="300" alt="Bright Data 徽标">
  </a>
</p>

# 品牌声誉监控工作流 🛡️

**由 AI 驱动的品牌声誉监控，可自动搜索 Google 新闻、分析情感倾向，并使用 [Bright Data SDK](https://github.com/bright-cn/bright-data-sdk-python)、OpenAI 和 SendGrid 通过电子邮件提供可执行的洞察！**

<div align="center">
  <img src="https://img.shields.io/badge/python-3.8+-blue"/>
  <img src="https://img.shields.io/badge/License-MIT-blue"/>
</div>

---

## 功能 🚀

- **自动发现新闻**：使用 [Bright Data 的搜索引擎 API](https://www.bright.cn/products/serp-api)，通过品牌查询查找 Google 新闻页面。
- **智能内容提取**：使用 [Bright Data 的网络解锁器 API](https://www.bright.cn/products/web-unlocker) 和并行处理，大规模抓取新闻文章。
- **AI 驱动的分析**：利用 OpenAI GPT-5-mini 分析情感倾向、提取洞察，并识别与品牌监控最相关的新闻。
- **智能内容筛选**：自动选择与品牌声誉最相关的热门新闻文章。
- **专业电子邮件报告**：生成格式精美的 HTML 电子邮件报告，其中包含情感分析和可执行的洞察。
- **自动交付**：通过 SendGrid 将监控报告直接发送给利益相关者。
- **可配置监控**：通过 JSON 配置轻松自定义搜索查询和收件人列表。

---

## 工作原理 🔄

1. **加载配置**：从 `config.json` 读取监控设置
2. **发现新闻**：使用品牌查询搜索 Google SERP，以查找 Google 新闻页面 URL
3. **内容提取**：并行抓取所有相关新闻页面并获取 Markdown 内容
4. **内容选择**：AI 从已抓取的页面中识别最重要的新闻文章
5. **单篇文章抓取**：抓取每篇入选的新闻文章，以获取详细内容
6. **详细分析**：对每篇文章进行情感分析并提取品牌洞察
7. **生成报告**：创建专业的 HTML 电子邮件报告
8. **自动交付**：通过电子邮件将报告发送给你的团队

---

## 前提条件 🛠️

- Python 3.8+ 🐍
- [Bright Data API 令牌](https://docs.brightdata.com/api-reference/authentication) 🔑
- OpenAI API 密钥 🔑
- SendGrid API 密钥 🔑

---

## 安装 ⚙️

1. 克隆此代码仓库：
   ```bash
   git clone https://github.com/bright-cn/brand-reputation-monitor
   cd brand-reputation-monitor
   ```
2. 创建并激活虚拟环境：
   ```
   python -m venv .venv
   ```
   在 Linux/macOS 上，使用以下命令激活：
   ```bash
   source .venv/bin/activate
   ```
   在 Windows 上，运行：
   ```bash
   .venv\Scripts\activate
   ```
3. 安装依赖项：
   ```
   pip install python-dotenv brightdata-sdk openai sendgrid pydantic
   ```
4. 在项目根目录中创建 `.env` 文件，并填入你的 API 密钥：
   ```
   BRIGHT_DATA_API_TOKEN=your_bright_data_api_token
   OPENAI_API_KEY=your_openai_api_key
   SENDGRID_API_KEY=your_sendgrid_api_key
   ```

---

## 配置 📝

在根目录中创建 `config.json`，以自定义品牌监控工作流：

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

**配置字段**：

- `search_queries`：用于监控品牌的搜索词列表（支持多个查询）
- `num_news`：要进行详细分析的热门文章数量（默认值：`5`）
- `sender`：用于发送报告的电子邮件地址（必须在 SendGrid 中完成验证）
- `recipients`：用于接收监控报告的电子邮件地址列表

---

## 项目结构 📁

```
brand-reputation-monitor/
├── .venv/
├── .env
├── config.json
└── workflow.py
```

---

## 使用方法 ▶️

使用以下命令运行品牌监控工作流：

```
python workflow.py
```

该工作流将：

1. 🔍 针对已配置的查询搜索 Google SERP，并提取 Google 新闻 URL
2. 📰 爬取 Google 新闻页面，以获取所有可用的文章 URL
3. 🤖 使用 AI 选择与品牌监控最相关的文章
4. 📄 抓取单篇新闻文章，以获取详细内容
5. 🧠 为每篇文章生成 AI 驱动的洞察和情感分析
6. 📧 向你的团队发送专业的 HTML 报告

**输出示例：**

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

## 电子邮件报告功能 📊

每份自动报告均包含：

- **文章摘要**：为每篇新闻生成简洁的 30 词摘要
- **情感分析**：使用彩色标签标注正面、负面或中性的情感分类
- **可执行的洞察**：提供 3–5 条品牌声誉管理的关键要点（每条 10–12 个词）
- **直接链接**：轻松访问原始文章，以便深入审阅
- **专业格式**：简洁的响应式 HTML 设计，可直接提供给利益相关者

---

## 高级配置 🧑💻

### 自定义搜索参数

修改 `config.json` 中的搜索查询以适应不同的监控场景，并配置发件人、收件人和新闻条目数量。

### 自动化调度

使用 cron 任务设置自动监控：

```bash
# Run every Monday at 9 AM
0 9 * * 1 /usr/bin/python3 /path/to/your/project/workflow.py
```

### 自定义分析提示词

修改 `process_news_list()` 函数中的系统提示词，对 AI 分析进行微调，以获得特定行业的洞察。

### 后续步骤与增强功能

- **添加记忆层**：避免多次分析同一篇文章
- **SendGrid 模板**：使用统一的电子邮件模板生成标准化报告
- **云存储**：将报告归档到 S3，以便进行历史分析

---

## API 集成详情 🔧

此工作流通过 Bright Data SDK 利用功能强大的 API：

- **[Bright Data 搜索引擎 API](https://www.bright.cn/products/serp-api)**：用于从搜索结果中发现 Google 新闻 URL
- **[Bright Data 网络解锁器 API](https://www.bright.cn/products/web-unlocker)**：用于以针对 LLM 优化的 Markdown 格式并行提取内容
- **OpenAI GPT-5-mini**：用于内容分析和 HTML 报告生成
- **SendGrid Email API**：用于专业报告交付

---

## 故障排除与技巧 💡

- **API 密钥**：确保所有 API 密钥均已在 `.env` 文件中正确设置
- **电子邮件验证**：发件人电子邮件地址必须在 SendGrid 控制面板中完成验证
- **搜索查询**：使用具体的品牌词及其变体，实现全面监控
- **内容质量**：查询越具体，分析结果越好

### 常见问题：

- **未找到新闻**：尝试使用范围更广的搜索查询，或检查你的品牌近期是否有媒体报道
- **电子邮件未送达**：在 SendGrid 中验证发件人电子邮件地址，并检查收件人的垃圾邮件文件夹
- **分析质量**：优化搜索查询，以获取更相关的文章
- **403 Forbidden 错误**：确保发件人电子邮件地址已在 SendGrid 账户中完成验证

---

## 使用场景 🎯

- **危机管理**：及早发现对品牌的负面提及
- **竞争情报**：监控竞争对手的新闻和市场定位
- **公关活动跟踪**：衡量营销活动的报道量和情感倾向
- **产品发布监控**：跟踪市场对新品发布的反响和反馈
- **高管简报**：定期为管理团队提供品牌健康状况报告

---

**时刻领先一步，守护你的品牌声誉！🚀**

使用 [Bright Data 的 AI 基础设施](https://www.bright.cn/ai)构建 ❤️，提供实时网页数据解决方案。
