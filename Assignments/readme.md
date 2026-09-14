# Assignments - Generative AI (Jio Institute, PGP AI & DS AY 2026-27)

**Student:** Kushagra Gupta (27PGAI0115)  
**Program:** PGP in Artificial Intelligence & Data Science (AY 2026-27) - Generative AI course, Term 3  
**Institution:** Jio Institute  
**Course repository:** [aagarwal4/generative-ai-pgp-ji-2026](https://github.com/aagarwal4/generative-ai-pgp-ji-2026)

---

## 📚 Assignment Overview

This folder contains the assignments for the **Generative AI** course. Each assignment builds practical skills in:
- Large Language Models (LLMs)
- Prompt Engineering
- LangChain Framework
- Information Extraction & Classification
- Real-world NLP Applications

---

## 📋 Assignments

### **Assignment 1: Topic Detection & Summarization + Job Postings Analysis**
**Status:** ✅ Complete - Part 1, Part 2 and both bonus full-dataset runs  
**Brief:** [Generative AI - Assignment 1.pdf](./Assignment1/Generative%20AI%20-%20Assignment%201.pdf) (same file as the course repo's `assignment-1/`)

#### What's Included (marks as per the brief):
- **Part 1 (45 marks):** BBC News Article Analysis - first 30 articles
  - Step 1: Load the dataset
  - Step 2: Topic classification into Business / Entertainment / Politics / Sport / Tech, few-shot (10)
  - Step 3: 2-3 sentence summarization (10)
  - Step 4: Key entity extraction - people, organizations, places (10)
  - Step 5: DataFrame with all original + new columns `Detected_Topic`, `Summary`, `Key_Entities` (15)

- **Part 2 (55 marks):** Job Postings Analysis - first 25 postings
  - Step 1: Load the dataset
  - Step 2: Job category classification, few-shot, "Other" fallback (10)
  - Step 3: Requirements extraction - skills, education, experience as JSON (30)
  - Step 4: Apply the chain to every posting, "Not specified" when missing (10)
  - Step 5: New columns `Predicted_Category`, `Required_Skills`, `Education_Required`, `Experience_Required` + spot-check (5)

- **Bonus (20 marks):** both analyses run on **all** rows - 2,225 articles (10) and 2,277 postings (10)

#### Key Deliverables:
| File | Purpose |
|------|---------|
| `Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.zip` | Submission zip: folder `Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1/` with the notebook, its PDF, the brief, datasets and all outputs |
| `Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb` | Main Jupyter notebook, executed end to end |
| `Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.pdf` | The executed notebook exported to PDF |
| `Assignment1/Generative AI - Assignment 1.pdf` | Assignment brief |
| `Assignment1/readme.md` | Detailed approach, results and how to run |
| `Assignment1/bbc-news-data.csv` | Input: BBC News Archive (tab-separated) |
| `Assignment1/job_title_des.csv` | Input: Job Title and Job Description dataset |
| `Assignment1/bbc_news_analyzed_first30.csv` | Output: Part 1 (first 30 articles) |
| `Assignment1/job_postings_analyzed_first25.csv` | Output: Part 2 (first 25 postings) |
| `Assignment1/bbc_news_analyzed_full.csv` | Output: Bonus Part 1 (all 2,225 articles) |
| `Assignment1/job_postings_analyzed_full.csv` | Output: Bonus Part 2 (all 2,277 postings) |
| `Assignment1/*_checkpoint.csv` | Per-row checkpoints the notebook resumes from if interrupted |
| `Assignment1/pyproject.toml`, `Assignment1/uv.lock` | Python dependencies (uv) |

#### Technologies Used:
- **LLM:** `llama3.2` (3B) served locally by **Ollama** on GPU, `temperature=0`
- **Framework:** LangChain (`ChatPromptTemplate`, `FewShotChatMessagePromptTemplate`, LCEL chains, `StrOutputParser`)
- **Structured output:** Ollama JSON mode (`format="json"`) parsed with `json.loads`, with fallbacks; Pydantic models document the schemas
- **Data:** Pandas, CSV
- **Execution:** Jupyter Notebook

#### Quick Links:
- 📖 [View Assignment 1 Details](./Assignment1/readme.md)
- 📓 [View Notebook](./Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb)
- 📄 [View Notebook PDF](./Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.pdf)
- 📦 [Download Submission Zip](./Assignment1/Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.zip)
- 📊 [View Results (BBC)](./Assignment1/bbc_news_analyzed_first30.csv) · [all 2,225](./Assignment1/bbc_news_analyzed_full.csv)
- 💼 [View Results (Jobs)](./Assignment1/job_postings_analyzed_first25.csv) · [all 2,277](./Assignment1/job_postings_analyzed_full.csv)

---

## 🚀 Getting Started

### Prerequisites
```bash
# 1. Install Ollama (https://ollama.com/download) and pull the model used in the notebook
ollama pull llama3.2

# 2. Install Python dependencies (Python 3.13+, see Assignment1/pyproject.toml)
uv sync --project Assignment1
```
No API key is needed - everything runs locally through Ollama.

### Run an Assignment
```bash
cd Assignment1/
jupyter notebook Kushagra_Gupta_27PGAI0115_Generative_AI_Assignment_1.ipynb
```
The pipelines resume from the `*_checkpoint.csv` files; delete them to recompute from scratch.

---

## 📊 Assignment Performance Summary

| Assignment | Total Marks | Marks Achieved | Status |
|------------|------------|-----------------|--------|
| Assignment 1 | 100 | 90 | ✅ Complete |
| Assignment 2 | - | - | ⏳ Pending |
| Assignment 3 | - | - | ⏳ Pending |

---

## 🔍 Key Learnings from Assignment 1

### Topic Detection & Summarization (BBC News)
✅ Few-shot prompting with one example per category and short category definitions  
✅ Abstractive summarization with LLMs, with a clean 2-3 sentence output  
✅ Named entity extraction (people, organizations, places) as JSON  
✅ Row-by-row processing with CSV checkpoints, so long runs can resume  

### Job Postings Analysis
✅ Skill extraction from unstructured job descriptions  
✅ Education and experience extraction with "Not specified" fallbacks  
✅ Normalizing model output (lists vs strings) into consistent columns  
✅ Spot-checking extracted fields against the description text  

### General Skills
✅ LangChain workflow design (prompt templates, LCEL chains, output parsers)  
✅ Prompt engineering and measuring its effect on accuracy  
✅ Running a small language model locally with Ollama  
✅ Guarding against runaway generations (`num_predict` cap in JSON mode)  

---

## 📈 Performance Metrics (measured on the submitted run)

### Assignment 1 - BBC News
- **First 30 articles:** topic accuracy **87%** (26/30) against the dataset labels, 0 errors, every summary 3 sentences
- **All 2,225 articles (bonus):** topic accuracy **87.6%** (1,949/2,225), 0 errors
  - per category: Business 81%, Entertainment 88%, Politics 98%, Sport 81%, Tech 93%
- **Entities:** 16.1 per article on average; 7.3% of articles returned none
- **Speed:** about 3.7 s per article (3 LLM calls) on a laptop GPU

### Assignment 1 - Job Postings
- **First 25 postings:** 0 errors; skills found for 25/25, education stated for 15/25, experience stated for 22/25
- **All 2,277 postings (bonus):** 2,277/2,277 processed, 0 errors; skills found for 2,276 (11.8 per posting), education stated for 63%, experience stated for 89%
- **Categories:** all 25 required postings and 97.2% of the full set are `Technology/IT` - the dataset contains 15 job titles, all software/IT roles; the other 63 got labels such as Operations (21) or Human Resources (14)
- **Speed:** about 1.8 s per posting (2 LLM calls)

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|-----------|
| **LLM** | Ollama `llama3.2` (local, GPU) |
| **Framework** | LangChain 1.x (`langchain-core`, `langchain-ollama`) |
| **Structured output** | Ollama JSON mode + `json.loads`, Pydantic 2 schemas |
| **Data** | Pandas, CSV |
| **Notebooks** | Jupyter, IPython |
| **Environment** | Python 3.13+ via uv |

---

## 📝 Important Notes

1. **Model choice:**
   - The brief advises Ollama with a small language model for the full-dataset bonus because of Groq rate limits.
   - The notebook uses the same local `llama3.2` model for every part, so results are consistent and it runs offline.

2. **Dataset Characteristics:**
   - BBC dataset: tab-separated (use `sep="\t"` when loading), sorted by category
   - Job data: comma-separated with an unnamed index column (dropped); 15 distinct tech job titles

3. **Reproducibility:**
   - All LLM calls use `temperature=0`
   - JSON-mode output is capped at 512 tokens (`num_predict`) so a looping generation cannot stall the run
   - Results are checkpointed to CSV after every row

---

## 📚 Resources & References

### LangChain
- [Official Documentation](https://python.langchain.com/)
- [LangChain Blog](https://blog.langchain.dev/)

### Ollama
- [Ollama Website](https://ollama.ai/)
- [Available Models](https://ollama.ai/library)

### Groq (used in class; not needed for this notebook)
- [Groq Console](https://console.groq.com/)
- [Groq API Reference](https://console.groq.com/docs)

### Datasets
- [BBC News Archive (Kaggle)](https://www.kaggle.com/datasets/hgultekin/bbcnewsarchive)
- [Job Title and Job Description Dataset (Kaggle)](https://www.kaggle.com/datasets/kshitizregmi/jobs-and-job-description)

### Pydantic
- [Pydantic Documentation](https://docs.pydantic.dev/)

---

## 📞 Contact & Support

**Student:** Kushagra Gupta  
**ID:** 27PGAI0115  
**Program:** Generative AI - PGP AI & DS, Term 3  

For questions or issues with assignments, refer to the individual assignment README files.

---

## 📄 Assignment Checklist

### Assignment 1
- [x] Part 1: BBC News Analysis (first 30 articles)
  - [x] Step 1: Load dataset
  - [x] Step 2: Topic Classification (few-shot)
  - [x] Step 3: Summarization
  - [x] Step 4: Entity Extraction
  - [x] Step 5: DataFrame with all original + new columns
  - [x] Bonus: Full Dataset (2,225 articles)
- [x] Part 2: Job Postings Analysis (first 25 postings)
  - [x] Step 1: Load dataset
  - [x] Step 2: Category Prediction (few-shot)
  - [x] Step 3: Skills, Education and Experience Extraction
  - [x] Step 4: Apply the chain to every posting
  - [x] Step 5: New columns + spot-check
  - [x] Bonus: Full Dataset (2,277 postings)
- [x] Notebook executed end to end and exported to PDF
- [x] Submission zip
- [x] Documentation & README

---

**Last Updated:** September 14, 2026  
**Repository:** kushagragupta-23/gen_ai_pgp_term3_jio  
**Branch:** main
