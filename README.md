# Sentinel KE — Social Media Threat Intelligence

AI service that watches public social feeds (EN/SW), flags **incitement / hate / violent threats** in real time, and pushes **actionable alerts** to analysts.

---

## How It Works (Pipeline)

1. **Ingest** → Stream public posts via API/feeds (Twitter/X to start).
2. **Preprocess** → Clean text, detect language (EN/Swahili), normalize slang.
3. **Classify** → Transformer (e.g., XLM-R) or GPT API → `violent_threat | incitement | hate | benign` + confidence.
4. **Enrich** → NER (people/places/groups), rule boosts, embeddings for similarity.
5. **Rank** → Model score + rules → `High | Medium | Low` severity.
6. **Store** → Persist post, labels, entities, embeddings.
7. **Alert** → High severity → email/SMS/push; all alerts visible on dashboard.
8. **Review** → Analysts triage; feedback loops back to improve models/thresholds.

---

## Key Features

- **Real-time alerts** (snippet, link, severity, entities, context)
- **Bilingual** EN + Swahili
- **Similar cases** via vector search (cluster coordinated messaging)
- **Trends** by topic/hastag/region/time
- **Human-in-the-loop** feedback to reduce false positives

---

## MVP Stack

- **Ingest:** Tweepy/Streaming API or SNScrape cron
- **API/Orchestration:** FastAPI + Celery/Redis
- **Models:** HuggingFace (XLM-R fine-tuned) or OpenAI GPT classification
- **Embeddings/Vector DB:** sentence-transformers + Milvus/Pinecone
- **DB:** PostgreSQL or MongoDB
- **Dashboard:** React + simple charts; WebSocket for live feed
- **Alerts:** SMTP (email) / Twilio (SMS)

---

## Config (`.env`)

