# Generative AI - Assignment 1

Kushagra Gupta (27PGAI0115)

- Brief: [Generative AI - Assignment 1.pdf](./Generative%20AI%20-%20Assignment%201.pdf)
- Notebook: [Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb](./Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb) ([PDF](./Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.pdf))

The notebook uses LangChain with the `llama3.2` model running locally through Ollama.

## Part 1: Topic Detection and Summarization of News Articles (45 marks)

Dataset: `bbc-news-data.csv`, first 30 articles.

| Step | Implementation |
|------|----------------|
| 2. Topic classification (10) | Few-shot prompt returning one label: Business, Entertainment, Politics, Sport or Tech |
| 3. Summarization (10) | Summary of the main points in 2-3 sentences |
| 4. Key entity extraction (10) | People, organizations and places, returned as a JSON list |
| 5. Update the DataFrame (15) | `Detected_Topic`, `Summary` and `Key_Entities` added to the original columns |

Output: [`bbc_news_analyzed_first30.csv`](./bbc_news_analyzed_first30.csv)

## Part 2: Job Postings Analysis (55 marks)

Dataset: `job_title_des.csv`, first 25 postings.

| Step | Implementation |
|------|----------------|
| 2. Job category classification (10) | Few-shot prompt returning one category, with "Other" as the fallback |
| 3. Requirements extraction (30) | Skills, education and experience extracted as JSON; "Not specified" when missing |
| 4. Apply the chain to each posting (10) | Every posting processed in a loop |
| 5. Update the DataFrame (5) | `Predicted_Category`, `Required_Skills`, `Education_Required` and `Experience_Required` added, followed by a spot-check |

Output: [`job_postings_analyzed_first25.csv`](./job_postings_analyzed_first25.csv)

## Bonus: all rows (20 marks)

Both pipelines run over the full datasets using Ollama, as the brief advises.

- [`bbc_news_analyzed_full.csv`](./bbc_news_analyzed_full.csv): all 2,225 articles
- [`job_postings_analyzed_full.csv`](./job_postings_analyzed_full.csv): all 2,277 postings

## Results

| | Rows processed | Errors | Notes |
|---|---|---|---|
| Part 1 | 30 | 0 | Topic matches the dataset label for 86.7% of articles |
| Part 2 | 25 | 0 | Skills found for 25, education stated for 15, experience stated for 22 |
| Bonus Part 1 | 2,225 | 0 | Topic matches the dataset label for 87.6% of articles |
| Bonus Part 2 | 2,277 | 0 | Skills found for 2,276 |

## How to run

```bash
git clone https://github.com/kushagragupta-23/gen_ai_pgp_term3_jio.git
cd gen_ai_pgp_term3_jio/Assignments/Assignment1
ollama pull llama3.2
uv sync
uv run jupyter notebook Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb
```

The `*_checkpoint.csv` files let the notebook resume where it stopped; delete them to recompute everything.
