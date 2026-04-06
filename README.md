# NLP Fitness Review Insights

![Build Status](https://img.shields.io/badge/build-notebook%20pipeline-informational)
![Runtime](https://img.shields.io/badge/runtime-Python%203-blue)
![License](https://img.shields.io/badge/license-Not%20Specified-lightgrey)

Problem: fitness brands and marketplace teams struggle to convert large volumes of noisy customer reviews into reliable product insights.

## Table of Contents 📑
- [About the Project 📚](#about-the-project-)
- [Screenshots / Demo 📷](#screenshots--demo-)
- [Technologies Used ☕️ 🐍 ⚛️](#technologies-used-️-🐍-️)
- [Setup / Installation 💻](#setup--installation-)
- [Approach 🚶](#approach-)
- [Example Usage / Output](#example-usage--output)
- [Project Structure 📁](#project-structure-)
- [Status 📶](#status-)
- [Limitations ⚠️](#limitations-️)
- [Improvements / Roadmap 🚀](#improvements--roadmap-)
- [Credits 📝](#credits-)
- [Author](#author)

## About the Project 📚
This project builds an NLP pipeline for fitness-product reviews: sentence splitting, language filtering, sentiment classification, and topic modeling (LDA) to surface recurring themes and pain points.

It was built to answer practical questions such as: which features cause negative sentiment, what topics dominate by product type, and what should product teams prioritize next.

It is for product managers, category analysts, CX teams, and data practitioners working with review-heavy e-commerce products.

## Screenshots / Demo 📷
![LDA Topic Modeling Output Placeholder](./assets/lda-topic-output.png)
![Sentiment Classification Output Placeholder](./assets/sentiment-output.gif)

Backend-style sample output:
```json
{
  "review_id": 59955,
  "sentences": [
    "The bike works great.",
    "Very smooth and stable ride."
  ],
  "language": "en",
  "topics": ["ride_quality", "stability"],
  "sentiment": ["positive", "positive"]
}
```

## Technologies Used ☕️ 🐍 ⚛️
- **Language:** Python 3
- **Notebooks:** Jupyter / Google Colab
- **NLP:** spaCy (`en_core_web_sm`), NLTK, `sentencex`, `langdetect`
- **Topic Modeling:** Gensim (`LdaMulticore`, coherence scoring)
- **Sentiment Modeling:** Hugging Face Transformers (`microsoft/deberta-v3-base` fine-tuned workflow)
- **Data Processing:** pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Data/Infra Integrations:** PostgreSQL (`psycopg2`), Google Sheets CSV ingestion, Google Gemini API (for punctuation/splitting retries)

## Setup / Installation 💻
```bash
# 1) Clone
git clone https://github.com/raghuveer9303/NLP-Fitness-Review-Insights.git
cd NLP-Fitness-Review-Insights

# 2) Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 3) Install core dependencies used in notebooks
pip install pandas numpy gensim nltk spacy matplotlib seaborn transformers psycopg2-binary langdetect sentencex google-generativeai python-dotenv
python -m spacy download en_core_web_sm

# 4) Launch notebooks
jupyter notebook
```

## Approach 🚶
The system is implemented as a notebook-driven NLP pipeline:
1. **Ingest & Normalize** review text from sheets/database.
2. **Split Reviews into Sentences** with deterministic segmentation and fallback prompting.
3. **Language Gate** to skip non-English entries.
4. **Sentiment Scoring** using a fine-tuned DeBERTa classifier.
5. **Topic Discovery** using LDA and coherence checks for interpretable themes.
6. **Aggregate Insights** by product/review cohorts for downstream decision-making.

Design choices favor interpretability and iterative experimentation over premature service abstraction.

## Example Usage / Output
```text
input:
"Setup was easy, but after two weeks the belt started making noise."

output:
sentences -> ["Setup was easy.", "After two weeks the belt started making noise."]
sentiment -> ["positive", "negative"]
topics -> ["assembly_experience", "motor_noise"]
```

```text
input:
review_id=59948, review_text="Buen producto pero envío lento"

output:
language -> "so" (non-English)
action -> "skipped_from_sentiment_topic_pipeline"
```

```text
input:
corpus=12,251 review sentences

output:
lda_topics -> 8
dominant_topic_example -> "app_connectivity"
coherence_tracking -> "used to compare topic-count candidates"
```

## Project Structure 📁
```text
NLP-Fitness-Review-Insights/
├── README.md                                        # Project overview, setup, and usage
├── split_reviews.ipynb                              # Sentence splitting + language filtering + DB/Gemini-assisted processing
├── Sentiment_Classification_Final_Model.ipynb       # Main sentiment model training/inference workflow
├── Sentiment_Classify_Create_File_Create_Bucket.ipynb # Sentiment inference + bucket/file generation workflow
└── Topic_Modelling_Colab_Notebook_LDA.ipynb         # LDA topic modeling, preprocessing, and coherence experiments
```

## Status 📶
- **Current state:** Active and in progress.
- **Stable:** Notebook workflows for sentence splitting, sentiment scoring, and LDA topic extraction.
- **Experimental:** Prompt-based punctuation fallback and production-grade orchestration outside notebooks.

## Limitations ⚠️
- Notebook-first architecture makes reproducible production deployment harder than package/script-based pipelines.
- LDA topics can drift when vocabulary changes across seasons, brands, or new product lines.
- External dependencies (Google Sheets, DB connectivity, Gemini API) can introduce runtime fragility.
- Current language handling can skip valid mixed-language reviews instead of translating/normalizing them.

## Improvements / Roadmap 🚀
- Convert notebook logic into a reusable `src/` pipeline package + CLI entrypoints.
- Add experiment tracking (metrics, model/version lineage) for sentiment and topic runs.
- Benchmark LDA against embedding-based topic models (e.g., BERTopic) on coherence and stability.
- Add containerized local run path (Docker Compose with Postgres + notebook/runtime service).
- Add CI checks for notebook execution and data-contract validation.

## Credits 📝
- [LDA paper (Blei, Ng, Jordan)](https://www.jmlr.org/papers/v3/blei03a.html)
- [Gensim Documentation](https://radimrehurek.com/gensim/)
- [Hugging Face Transformers](https://huggingface.co/docs/transformers/index)
- [spaCy](https://spacy.io/)

## Author
Raghuveer • LinkedIn: [linkedin.com/in/raghuveer](https://www.linkedin.com/) • GitHub: [@raghuveer9303](https://github.com/raghuveer9303)
