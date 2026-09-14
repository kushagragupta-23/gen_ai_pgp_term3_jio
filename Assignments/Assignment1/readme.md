# Generative AI - Assignment 1

**Student:** Kushagra Gupta · **Registration No.:** 27PGAI0115  
**Brief:** [Generative AI - Assignment 1.pdf](./Generative%20AI%20-%20Assignment%201.pdf) (Total 100 marks + 20 bonus)  
**Submission zip:** [Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.zip](./Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.zip)

The notebook [Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb](./Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb)
([PDF](./Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.pdf)) solves both parts with LangChain and a local
`llama3.2` model served by Ollama, then runs the same pipelines over the full datasets for the bonus.

## What's in the zip

The zip holds one folder, `Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1/`, with:

| File | Content |
|------|---------|
| `Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb` | Notebook, executed end to end |
| `Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.pdf` | The executed notebook as PDF |
| `Generative AI - Assignment 1.pdf` | Assignment brief |
| `readme.md` | This file |
| `bbc-news-data.csv`, `job_title_des.csv` | Input datasets |
| `bbc_news_analyzed_first30.csv` | Part 1 result - 30 articles |
| `job_postings_analyzed_first25.csv` | Part 2 result - 25 postings |
| `bbc_news_analyzed_full.csv` | Bonus Part 1 result - 2,225 articles |
| `job_postings_analyzed_full.csv` | Bonus Part 2 result - 2,277 postings |
| `pyproject.toml`, `uv.lock` | Dependencies |

## How the notebook maps to the brief

### Part 1 - Topic Detection and Summarization of News Articles (45 marks)
| Step | Marks | Implementation |
|------|-------|----------------|
| 1. Load the dataset | - | `bbc-news-data.csv` (tab-separated), `head(30)`, `Article_ID` added |
| 2. Topic classification | 10 | Few-shot `ChatPromptTemplate` with one example per category plus short category definitions; output normalized to one of Business / Entertainment / Politics / Sport / Tech |
| 3. Summarization | 10 | "Summarize the main points ... in 2-3 sentences" prompt; any "Here is a summary" lead-in is stripped |
| 4. Key entity extraction | 10 | JSON-mode prompt returning `{"entities": [...]}` (people, organizations, places) |
| 5. Update the DataFrame | 15 | Row loop adds `Detected_Topic`, `Summary`, `Key_Entities`; final table keeps all original columns (`category`, `filename`, `title`, `content`); accuracy check against the labels |

### Part 2 - Job Postings Analysis (55 marks)
| Step | Marks | Implementation |
|------|-------|----------------|
| 1. Load the dataset | - | `job_title_des.csv`, columns renamed to `Job_Title` / `Job_Description`, `head(25)` |
| 2. Job category classification | 10 | Few-shot prompt over Technology/IT, Finance, Marketing, Healthcare, Sales, HR, Operations, Design, Education, Other |
| 3. Requirements extraction | 30 | One JSON prompt for skills, education and experience; list answers joined into text; "Not specified" when missing |
| 4. Apply the chain to each posting | 10 | Row loop with per-row checkpointing and error handling |
| 5. New columns + verification | 5 | `Predicted_Category`, `Required_Skills`, `Education_Required`, `Experience_Required`; spot-check of 3 postings and coverage counts |

### Bonus (20 marks)
Both pipelines run over every row: 2,225 BBC articles and 2,277 job postings (Ollama, as the brief advises, to avoid Groq rate limits).

## Results (from the submitted run)

| | Rows | Errors | Quality |
|---|---|---|---|
| Part 1 - first 30 articles | 30/30 | 0 | Topic accuracy 87% (26/30); every summary 3 sentences; 10.6 entities per article |
| Part 2 - first 25 postings | 25/25 | 0 | Skills for 25/25, education stated for 15/25, experience stated for 22/25 |
| Bonus - all 2,225 articles | 2,225/2,225 | 0 | Topic accuracy 87.6% (Business 81%, Entertainment 88%, Politics 98%, Sport 81%, Tech 93%); 16.1 entities per article |
| Bonus - all 2,277 postings | 2,277/2,277 | 0 | 97.2% `Technology/IT`; skills for 2,276 (11.8 per posting); education stated for 63%, experience for 89% |

All 25 required postings and 97.2% of the full set are classified `Technology/IT`, which fits this dataset: it contains 15 job titles, all software/IT roles. The other 63 postings got labels such as Operations (21) or Human Resources (14).

## Design decisions

- **Local model.** `llama3.2` (3B) through Ollama with `temperature=0`, used for every part so results are consistent and nothing is rate-limited.
- **Topic prompt.** The first version (two examples, no definitions) scored 67% on the first 30 articles and never predicted Sport or Entertainment. Adding one example per category and category definitions raised it to 87%.
- **Runaway generations.** In JSON mode llama3.2 occasionally looped until the context filled (about 40,000 tokens, 10+ minutes per call). `num_predict=512` caps each JSON reply.
- **Long job descriptions.** Job boards often list "Education:" and "Experience:" at the end, so the requirements prompt reads up to 8,000 characters (covers 99% of postings) instead of 3,000.
- **Checkpoints.** Each pipeline writes a `*_checkpoint.csv` after every row and skips finished rows, so an interrupted run resumes.

## Known limitations

- Some business stories about trade, courts or regulation are labelled Politics (Business accuracy 81%).
- About 7% of articles come back with no entities.
- The model sometimes misses a degree mentioned only in passing, so a few postings say "Not specified" for education.
- Experience strings keep the posting's own wording (e.g. "2-4 years", "5+ years", "1 year (Preferred)").
- In the full job run, 63 postings (2.8%) with tech job titles were labelled outside `Technology/IT` (e.g. Operations, Human Resources).

## How to run

```bash
ollama pull llama3.2
uv sync --project .        # from this folder; Python 3.13+
jupyter notebook Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb
```
Run all cells. Delete the `*_checkpoint.csv` files first to recompute everything from scratch.
