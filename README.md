# NLP Fitness Review Insights

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Runtime](https://img.shields.io/badge/runtime-Python%203.11-blue)
![License](https://img.shields.io/badge/license-Not%20Specified-lightgrey)

Problem: fitness equipment teams struggle to convert thousands of scattered customer reviews into clear, actionable product insights.

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
This project analyzes customer reviews for digital treadmills and exercise bikes using NLP + ML to identify recurring themes and sentiment drivers at scale.

It was built to answer practical product questions: what customers repeatedly praise or complain about, how sentiment shifts by feature and price segment, and where expectation gaps appear after purchase.

It is for product managers, category teams, marketplace ops, and data teams who need evidence-backed decisions for feature prioritization, catalog strategy, and review intelligence workflows.

## Screenshots / Demo 📷
![Dashboard Placeholder](./assets/demo-dashboard.png)
![Topic & Sentiment Output Placeholder](./assets/topic-sentiment-output.gif)

Backend-style sample output:
```json
{
  "product_type": "digital_treadmill",
  "dominant_topics": ["assembly_experience", "motor_noise", "app_connectivity"],
  "topic_sentiment": {
    "assembly_experience": -0.41,
    "motor_noise": -0.33,
    "app_connectivity": 0.18
  },
  "recommendation_score": 0.62
}
```

## Technologies Used ☕️ 🐍 ⚛️
- **Language/Runtime:** Python 3.x
- **NLP & ML:** NLTK, spaCy, Gensim (LDA), scikit-learn
- **Data Processing:** pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Notebooks/Analysis:** Jupyter
- **Storage (typical):** CSV/Parquet + SQL database for review metadata
- **Automation (typical):** GitHub Actions for CI

## Setup / Installation 💻
```bash
# 1) Clone
git clone https://github.com/raghuveer9303/NLP-Fitness-Review-Insights.git
cd NLP-Fitness-Review-Insights

# 2) Create environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 3) Install dependencies
pip install -r requirements.txt

# 4) Run pipeline / notebooks
jupyter notebook
```

## Approach 🚶
The system follows a modular NLP pipeline:
1. **Ingestion & Cleaning**: collect review text, ratings, timestamps, helpful votes, and product metadata; normalize noisy user text.
2. **Topic Modeling (LDA)**: tune topic count and priors, then extract interpretable topic-word distributions and per-review topic mixtures.
3. **Sentiment Layer**: compute overall and feature-level sentiment to connect “what customers talk about” with “how they feel.”
4. **Insight Synthesis**: aggregate by category, brand, and price bucket to produce product and marketing recommendations.

Design decisions: batch-first processing for reproducibility, interpretable models over black-box models for stakeholder trust, and separable stages for easy extension.

## Example Usage / Output
```text
input:
"Setup took 3 hours and instructions were confusing, but the ride quality is excellent."

output:
topics -> ["assembly_experience", "ride_quality"]
sentiment -> {"assembly_experience": "negative", "ride_quality": "positive"}
```

```text
input:
product_type=exercise_bike, price_bucket=mid_range

output:
top_topics -> ["subscription_cost", "app_classes", "seat_comfort"]
net_sentiment -> {"subscription_cost": -0.52, "app_classes": +0.64, "seat_comfort": -0.21}
```

```text
input:
date_range=2024-Q1, feature="bluetooth_connectivity"

output:
mention_volume=842
positive=39%, neutral=22%, negative=39%
trend="high volatility after firmware updates"
```

## Project Structure 📁
```text
NLP-Fitness-Review-Insights/
├── README.md                 # Project overview, setup, and usage
├── data/                     # Raw and processed review datasets
├── notebooks/                # EDA, topic modeling, and sentiment experiments
├── src/                      # Reusable pipeline code (preprocessing, modeling, reporting)
├── outputs/                  # Generated charts, topic tables, and summary artifacts
└── requirements.txt          # Python dependencies
```

## Status 📶
- **Current state:** In progress and actively maintained.
- **Stable:** Core review cleaning, baseline topic modeling, and sentiment scoring workflow.
- **Experimental:** Cross-platform normalization, dynamic topic labeling, and production-grade serving API.

## Limitations ⚠️
- LDA topics can drift with seasonal vocabulary and new product jargon.
- Scraped reviews may be biased toward extreme experiences (very happy/very unhappy users).
- Feature-level sentiment extraction can miss nuanced context (sarcasm, mixed sentiment in one sentence).
- Large batch recomputation can be slow without distributed processing for 85k+ reviews.

## Improvements / Roadmap 🚀
- Add **BERTopic + sentence-transformer embeddings** and benchmark against LDA coherence/stability.
- Introduce **incremental processing** (daily review deltas) to avoid full recomputation.
- Build a **FastAPI inference service** for topic/sentiment scoring with versioned models.
- Add **data quality gates in CI** (schema checks, duplicate detection, drift alerts).

## Credits 📝
- [Latent Dirichlet Allocation (Blei, Ng, Jordan)](https://www.jmlr.org/papers/v3/blei03a.html)
- [Gensim Topic Modeling](https://radimrehurek.com/gensim/)
- [VADER Sentiment](https://github.com/cjhutto/vaderSentiment)
- Community reviewers and open e-commerce review datasets that inspired this analysis approach.

## Author
Raghuveer (`@raghuveer9303`) • LinkedIn: [your-linkedin](https://www.linkedin.com/) • GitHub: [raghuveer9303](https://github.com/raghuveer9303)
