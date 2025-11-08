
# AI Intel Hub

An AI-powered content pipeline and dashboard that collects, ranks, and generates ideas from the latest AI news and research. Summaries are sent via Telegram and displayed in a modern web interface.

## 🚀 Features

- Collects AI news from RSS feeds and research papers from arXiv/Semantic Scholar
- Ranks content using OpenAI embeddings
- Generates post and project ideas for each article
- Schedules and sends summaries via Telegram
- Beautiful dark-themed dashboard (Flask + HTML)

## 📁 Project Structure

```
ai-intel-hub/
├── app.py                    # Flask web application and dashboard
├── assistants/
│   ├── content_ranker.py     # Ranks articles using OpenAI
│   ├── idea_generator.py     # Generates ideas for articles
│   └── telegram_bot.py       # Sends summaries via Telegram
├── collectors/
│   ├── research_collector.py # Collects research papers
│   └── rss_collector.py      # Collects news from RSS feeds
├── pipeline/
│   ├── orchestrator.py       # Main pipeline logic
│   └── scheduler.py          # Schedules summary sending
├── data/
│   └── latest_feed.json      # Cached feed data
├── templates/
│   ├── index.html            # Dashboard template
│   └── feed.html             # Feed template
├── requirements.txt          # Python dependencies
├── Dockerfile                # Container setup (optional)
└── README.md                 # Project documentation
```

## 🛠️ Installation

### Prerequisites
- Python 3.8+
- OpenAI API key (for ranking/idea generation)
- Telegram bot token and chat ID (for notifications)

### Setup Instructions

1. Clone the repository:
  ```bash
  git clone <repository-url>
  cd ai-intel-hub
  ```
2. Install dependencies:
  ```bash
  pip install -r requirements.txt
  ```
3. Set environment variables (in `.env` or your shell):
  - `OPENAI_API_KEY` (for OpenAI)
  - `TELEGRAM_BOT_TOKEN` (for Telegram bot)
  - `TELEGRAM_CHAT_ID` (your Telegram chat ID)

## 🚀 Usage

### Run the Dashboard
```bash
python app.py
```
Visit [http://localhost:5000](http://localhost:5000) to view the feed.

### Run the Content Pipeline Manually
```bash
python pipeline/orchestrator.py
```

### Send Summaries via Telegram (Manual)
```bash
python assistants/telegram_bot.py
```

### Schedule Summaries (Automatic)
Edit `pipeline/scheduler.py` to set the schedule (e.g., daily at 9:00 AM):
```python
schedule.every().day.at("09:00").do(run_weekly_summary)
```
Then run:
```bash
python pipeline/scheduler.py
```

## 📊 Dashboard Features

- Scrollable card-based feed of AI news and research
- Ranks and scores articles for relevance
- Shows generated post/project ideas
- Dark theme for comfortable reading

## 🔧 Configuration

RSS and research sources are defined in the collectors. You can add more feeds or sources by editing `rss_collector.py` and `research_collector.py`.

## 🤖 Agents & Pipeline


- **RSS Collector**: Gathers news from top AI sources
- **Research Collector**: Fetches latest papers from arXiv and Semantic Scholar
- **Content Ranker**: Scores articles using OpenAI embeddings
- **Idea Generator**: Suggests posts and projects for each article
- **Telegram Bot**: Sends summaries to your Telegram chat
- **Orchestrator**: Coordinates all steps and saves results

## 📝 Contributing

Pull requests and issues are welcome! Please open an issue for bugs or feature requests.

## 📄 License

MIT License

orchestrator = AITrackerOrchestrator()
orchestrator.start_scheduler()  # Runs automatically every 6 hours
db.cleanup_old_data(days_to_keep=90)
