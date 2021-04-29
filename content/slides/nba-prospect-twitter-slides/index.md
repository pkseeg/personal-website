---
title: NBA Prospect Twitter Analaysis Slides
summary: Short presentation of the project
authors: []
tags: []
categories: []
date: "2021-04-15T00:00:00Z"
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: black
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  highlight_style: dracula
---

# Scoring NBA Prospects via Social Media

[Parker Seegmiller](https://pkseeg.com/)

---

## Project Goal

- Use social media to develop additional informative inputs for an NBA draft prospect predictive model
  - Determine whether a relationship exists between an NBA player’s social media presence and their on-court play
  - Use that relationship to aid in draft prospect projections

---

## Project Timeline

- Downloaded draft data (2010-2020)
- Scraped twitter
- Used [IBM Natural Language Understanding API](https://www.ibm.com/cloud/watson-natural-language-understanding)
- 3 sets of scores - Sentiment, Usage Rates, Topics
  - XGBoost models predicting BPM
  - BPM projection percentiles
- Dashboard
  - Projections functionality

---

## Modeling

- Trained on 80% of the draft data (2010-2020)
- XGBoost worked slightly more effectively than multiple regression
- Filled null BPM values (never debuted) at the 5th percentile
- Scores were not very predictive on their own
  - Added a projection percentile to my analysis
  |             |      RMSE   |             |
  | Sentiment   | Usage       | Topic       |
  | ----------- | ----------- | ----------- |
  | 3.14        | 3.64        | 4.26        |

---

## Next Steps

- Determine helpfulness of scores when used in other draft models
- Obtain all NBA player data
  - Initially focused on current draft prospects
- Add similarity portion to projections tab
