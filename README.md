
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

## 🛠️ Installation

### Prerequisites
- Python 3.8 or higher
- Twilio account (for WhatsApp notifications)

### Setup Instructions

1. **Clone and install dependencies**:
```bash
git clone <repository-url>
cd focus-feed
pip install -r requirements.txt
```

2. **Configure Twilio credentials**:
   - Edit `config/config.json`
   - Replace placeholders in the `twilio` section:
     - `account_sid`: Your Twilio Account SID
     - `auth_token`: Your Twilio Auth Token
     - `from_whatsapp_number`: Your Twilio WhatsApp number
     - `recipients`: List of WhatsApp numbers to receive notifications

3. **Optional: Configure Semantic Scholar API**:
   - Get API key from [Semantic Scholar](https://www.semanticscholar.org/product/api)
   - Add to `config.json` under `research_sources.semantic_scholar.api_key`

## 🚀 Usage

### Start the Dashboard
```bash
python app.py
```
Visit http://localhost:5000 to view the dashboard.

### Run Manual Collection
```bash
python orchestrator.py
```

### Run with Scheduling
```python
from orchestrator import AITrackerOrchestrator

orchestrator = AITrackerOrchestrator()
orchestrator.start_scheduler()  # Runs automatically every 6 hours
```

### Test WhatsApp Integration
```bash
python agents/whatsapp_notification_agent.py
```

## 📊 Dashboard Features

### Main Interface
- **System Status**: Real-time monitoring of agent status
- **Collection Controls**: Manual trigger for data collection
- **Category Filters**: Filter by Research, News, Blogs, etc.
- **Analytics View**: Source distribution and keyword trends

### Topic Cards
- **Importance Ranking**: Visual ranking badges (#1, #2, etc.)
- **Source Indicators**: Color-coded source banners
- **Metadata**: Publication dates, citation counts
- **AI Keywords**: Extracted relevant keywords
- **Generated Ideas**: Automated post and project suggestions

## 🔧 Configuration

### RSS Sources (`config.json`)
Add or modify RSS feeds in the `rss_sources` array:
```json
{
  "name": "Source Name",
  "url": "https://example.com/feed.xml",
  "category": "Research Paper",
  "color": "#4CAF50",
  "enabled": true
}
```

### Ranking Criteria
Adjust ranking weights in `ranking_criteria`:
- `recency_weight`: How recent the content is
- `citation_weight`: Citation count importance
- `keyword_weight`: AI keyword relevance
- `source_weight`: Source credibility
- `novelty_weight`: Content novelty
- `engagement_weight`: Estimated engagement potential

### WhatsApp Notifications
Configure notification types in `twilio.notifications`:
- `daily_digest`: Enable/disable daily summaries
- `breaking_news_threshold`: Importance score threshold for alerts
- `weekly_summary`: Enable/disable weekly analytics
- `high_activity_alerts`: Alerts for trending topics

## 🤖 Agent Details

### RSS Agent
- Monitors 10+ AI-focused RSS feeds
- Filters for AI-related content
- Extracts keywords and metadata
- Handles rate limiting and errors gracefully

### Research Agent
- arXiv API integration for latest papers
- Semantic Scholar API for citation data
- Quality filtering based on citations and recency
- Duplicate detection and removal

### Ranking Agent
- Multi-factor importance scoring
- Keyword analysis and trend detection
- Source credibility weighting
- Bonus multipliers for breakthrough content

### WhatsApp Agent
- Twilio API integration
- Multiple notification types
- Error handling and retry logic
- Message formatting and templates

## 📈 Analytics

The system provides comprehensive analytics:
- **Daily Collection Metrics**: Items collected and processed
- **Source Distribution**: Content breakdown by source
- **Keyword Trends**: Most mentioned AI topics
- **Importance Scoring**: Average content quality metrics

## 🔍 API Endpoints

- `GET /api/topics`: Retrieve topics with pagination
- `GET /api/run_collection`: Trigger manual collection
- `GET /api/analytics`: Get system analytics
- `GET /api/system_status`: Check system health

## 🔧 Maintenance

### Database Cleanup
```python
from utils.database import DatabaseManager
db = DatabaseManager()
db.cleanup_old_data(days_to_keep=90)
```

### Log Management
Logs automatically rotate at 10MB with 5 backup files retained.

### Data Backup
The SQLite database is stored in `data/ai_tracker.db` - backup regularly.

## 🚨 Troubleshooting

### Common Issues

1. **Import Errors**: Ensure all dependencies are installed with `pip install -r requirements.txt`

2. **Database Errors**: Check that the `data/` directory exists and is writable

3. **WhatsApp Failures**: Verify Twilio credentials and WhatsApp number format

4. **RSS Feed Timeouts**: Check internet connectivity and RSS source availability

### Debug Mode
Enable debug logging by setting `logging.level` to `DEBUG` in `config.json`.

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- arXiv for providing free access to research papers
- Semantic Scholar for citation data
- Twilio for WhatsApp API integration
- Various AI news sources for RSS feeds