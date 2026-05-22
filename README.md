# Recommendation System for Twitter Using Sentiment Analysis

A real-time Twitter analytics web application that fetches live tweets, performs sentiment analysis using TextBlob, and presents interactive visualizations — all through a Streamlit-based UI.

---

## Overview

This project builds an interactive dashboard to analyze public Twitter sentiment by user handle or keyword/hashtag. It combines the Twitter API (via Tweepy), NLP-based sentiment scoring, and visual outputs including word clouds and bar charts. The goal is to surface actionable insights about how users and public discourse are feeling about any topic or personality on Twitter.

---

## Features

- **Tweet Analyzer by Twitter Handle** — Fetches recent tweets from any public account and performs sentiment breakdown
- **Tweet Analyzer by Keyword/Hashtag** — Searches Twitter for a keyword or hashtag and analyzes the resulting tweets
- **Generate Twitter Data** — Outputs a full DataFrame with cleaned tweets, polarity scores, subjectivity scores, and sentiment labels
- **Filter Data** — Displays tweets filtered into positive/neutral vs. negative categories, with a toggle to see what was filtered out
- **View Public Response by Keyword** — Shows tweets split into Positive, Neutral, and Negative tables for quick comparison

---

## Tech Stack

| Component | Library/Tool |
|---|---|
| Twitter Data Collection | `tweepy` (Twitter API v1.1) |
| Sentiment Analysis | `TextBlob` |
| Text Preprocessing | `regex`, `emot` |
| Visualization | `matplotlib`, `seaborn`, `wordcloud` |
| Web Framework | `streamlit` |
| Data Handling | `pandas`, `numpy` |
| Image Handling | `PIL` (Pillow) |

---

## Sentiment Scoring

Sentiment is computed using **TextBlob's polarity score**, which ranges from -1.0 (most negative) to +1.0 (most positive). Scores are mapped to five labels:

| Polarity Range | Label |
|---|---|
| ≤ -0.5 | Very Negative |
| -0.5 to -0.001 | Negative |
| ~0.0 | Neutral |
| 0.001 to 0.5 | Positive |
| ≥ 0.5 | Very Positive |

---

## Text Preprocessing Pipeline

Before sentiment scoring, each tweet is cleaned through the following steps:

1. Remove `@mentions`
2. Remove `#` hashtag symbols
3. Remove retweet markers (`RT`)
4. Remove hyperlinks
5. Remove special characters (`!`, `?`, `"`, `;`, etc.)
6. Convert Unicode emojis to readable text labels using the `emot` library

---

## Installation

```bash
pip install numpy emot streamlit tweepy textblob wordcloud pandas matplotlib seaborn regex Pillow plotly
```

---

## Setup

This project uses the **Twitter API v1.1**. You will need a Twitter Developer account and app credentials. Replace the placeholder values in `app.py` with your own:

```python
consumerKey = 'YOUR_CONSUMER_KEY'
consumerSecret = 'YOUR_CONSUMER_SECRET'
accessToken = 'YOUR_ACCESS_TOKEN'
accessTokenSecret = 'YOUR_ACCESS_TOKEN_SECRET'
```

> **Note:** The Twitter API v1.1 `search` and `user_timeline` endpoints used here require at least **Basic (Elevated)** access. Free-tier access may restrict these endpoints.

---

## Running the App

```bash
streamlit run app.py
```

Or, to run on a specific port (e.g., for Colab/remote environments):

```bash
streamlit run --server.port 80 app.py
```

---

## Project Structure

```
├── app.py                  # Main Streamlit application
├── WC.jpg                  # Saved word cloud output (auto-generated)
└── README.md
```

---

## Conference Publication

This project was presented at **IEEE Technicoknockdown 2021** — a National Level Student Conference — as a paper titled *"Recommendation System for Twitter Using Sentiment Analysis"*.

---

## Notes

- The app was originally developed and run in **Google Colab**, with remote tunneling via `connectd_installer` to expose the Streamlit server.
- Emoji handling uses the `emot` library's `UNICODE_EMO` dictionary to convert emojis to descriptive text before NLP processing.
- Empty or whitespace-only tweets are dropped before displaying results to avoid noise in the output tables.
