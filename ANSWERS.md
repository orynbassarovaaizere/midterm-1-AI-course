# Midterm 1: answers

GitHub username:orynbassarovaaizere

Session code:EMBER-92

Fingerprint:fc6f4a21

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I used Claude (Anthropic) and Google Colab during this exam.

Claude explained the task to me in Russian and helped me set up Colab. It gave me Python code for the metrics, Wilson intervals and costs. I ran the code in Colab on my own data and checked the results. Claude also helped me with the calculations for Part 3. I asked for explanations, so I understand every number and decision.

No other person helped me. I can explain all my answers. 


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


### 1e. Next measurement (at most 60 words)

I would test A with k=3 and k=4 on a bigger set, for example 200 Kazakh questions and 200 English ones. k=4 should cost about 8,969 USD, so it is still in the budget. More questions would make the KK interval smaller and show if k=4 helps Kazakh users.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.8889 | KK, clean | 0.7000 | 0.5212 | 0.8333 | 24352.80 |
| L | 0.8111 | KK, degraded | 0.7000 | 0.5212 | 0.8333 | 5400 |

Personal-data pages per year sent abroad under H:233600

### 2b. Memo (at most 300 words)

To: Head of operations

About: which pipeline to use for invoices

Accuracy. H is correct on 88.9 % of invoices (160/180, CI 83.5-92.7 %) and L on 81.1 % (146/180, CI 74.8-86.2 %). The intervals overlap, so we can not say H is really more accurate. The overall numbers also hide a problem: both pipelines are worst on Kazakh invoices. For H it is Kazakh clean scans, only 70 % (21/30, CI 52-83 %), and for L it is Kazakh degraded scans, also 70 % (CI 52-83 %). With only 30 invoices per group we are not sure which one is worse for Kazakh.

Personal data. 8 % of pages have a person's name and IIN, that is 233,600 pages per year. The IIN is covered by law No. 94-V. Where does the scan go? With H it goes to a data centre abroad, with L it stays on our server in Kazakhstan. Who stores it? With H the vendor does, and we have not checked their terms; with L we do. For how long? For H we do not know, we need it written in the contract, because a vendor's promise is not a compliance check. For L we have to set our own rule. Before using H we would also need a lawyer to check if sending IIN abroad is allowed.

Safeguards we can check: the L server has no internet access (firewall logs), scans are deleted after 30 days (monthly audit), every access is logged, and every month we check 100 Kazakh invoices by hand.

My choice is L. It costs 5,400 USD per year instead of 24,353 USD, its accuracy is not proven worse, and personal data stays in the country. The remaining risk is that L gets about 30 % of degraded Kazakh invoices wrong (maybe up to 48 %), so these need a human check for now.

## Part 3: Explain your own numbers

### Q1

Number: 1.62
Why (at most 40 words): KK/EN is 1.09 for characters, 2.15 for bytes and 3.48 for tokens. Part comes from encoding (Cyrillic uses 2 bytes per letter), but tokens grow 1.62 times more than bytes, so the tokenizer adds extra cost for Kazakh.

### Q2

Number: 625
Why (at most 40 words): 640 × 263/256 ≈ 657.5 e5 tokens; 95 % of that is 625, after the 512 limit. The sentence is cut off and never embedded, so the question can not retrieve this chunk, and no error appears.

### Q3

Number: 49.6
Why (at most 40 words): With T = 1.5 the probabilities become flatter: Monday goes down from 60.3 % (T = 1) to 49.6 % and the small tokens go up. The order of tokens stays the same and all five can still be sampled.

### Q4

Number: 16
Why (at most 40 words): X gets 66 - 34 = 32 and Y gets 63 - 15 = 48. The public leaderboard prefers X because wrong answers cost nothing. This teaches models to guess instead of saying "I don't know", so they hallucinate more.

### Q5

Number: 12.75
Why (at most 40 words): 8.67T / 34B = 255 tokens per parameter, Chinchilla has 70B / 1.4T = 20, so 12.75 times more. By this rule the model is over-trained. Chinchilla said GPT-3 was under-trained: too many parameters and too few tokens.
