# Midterm 1: answers

GitHub username:orynbassarovaaizere
Session code:EMBER-92
Fingerprint:fc6f4a21

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.5333 | 0.7500 | 0.8167 | 0.6496 |
| B | 0.2500 | 0.4167 | 0.5000 | 0.3576 |
### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.7500 | 0.6277 | 0.8422 |
| A, k=5 | 0.8167 | 0.7008 | 0.8944 |
| B, k=3 | 0.4167 | 0.3006 | 0.5427 |
| B, k=5 | 0.5000 | 0.3773 | 0.6227 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 7799.60 |
| A, k=5 | 10137.99 |
| B, k=3 | 5418.76 |
| B, k=5 | 6169.93 |

### 1d. Decision (at most 150 words)

Chosen candidate: A, k=3

I choose A with k=3. A with k=5 has the best recall, but it costs about 10,138 USD per year, and the budget is only 9,000 USD, so I can not take it. A, k=3 costs 7,800 USD and has recall 0.75 (CI 0.63-0.84). Both B options are cheaper, but their recall is much lower: B, k=5 is 0.50 (0.38-0.62) and B, k=3 is 0.42 (0.30-0.54). These intervals do not overlap with A, k=3, so A, k=3 is really better. A, k=3 and A, k=5 overlap, so we can not say k=5 is better anyway. By language A, k=3 gives EN 0.85, RU 0.75 and KK 0.65. Kazakh users get the worst results, but we have only 20 questions per language and the intervals overlap, so this difference is not proven yet.

(Decision, using your intervals and the budget. Give the recall of your choice for EN, RU and KK separately.)

### 1e. Next measurement (at most 60 words)

I would test A with k=3 and k=4 on a bigger set, for example 200 Kazakh questions and 200 English ones. k=4 should cost about 8,969 USD, so it is still in the budget. More questions would make the KK interval smaller and show if k=4 helps Kazakh users.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | | | | | | |
| L | | | | | | |

Personal-data pages per year sent abroad under H:

### 2b. Memo (at most 300 words)

## Part 3: Explain your own numbers

### Q1

Number:
Why (at most 40 words):

### Q2

Number:
Why (at most 40 words):

### Q3

Number:
Why (at most 40 words):

### Q4

Number:
Why (at most 40 words):

### Q5

Number:
Why (at most 40 words):
