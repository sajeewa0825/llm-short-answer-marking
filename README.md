# LLMs as Short-Answer Markers: Data, Marks and Analysis Code

This repository contains the data, LLM marks and analysis notebook for the paper:

> Kumarasingha, K.M.S.S., Hansana, M.M.S.M., Kithulwatta, W.M.C.J.T., Wickramasinghe, W.B.S. Sameepa, H.M.M.S., Rasingolla, R.W.M.S.M., Konara, K.M.H.L.: Large Language Models as Short-Answer Markers: Reference Answers, Rater Bias and the Human Agreement Ceiling on Public Benchmarks. TAIMMA 2027 (under review).

Six LLM rater configurations marked 1,000 sampled answers from two public computer-science short-answer datasets (Mohler and SAF), once with the question only (L1) and once with an added reference answer (L2). The notebook reproduces every table, figure and number in the paper.

## Contents

| Path | Description |
|---|---|
| `data/answers.csv` | All 4,383 answers in the pool, with questions, reference answers, human scores and sampling roles |
| `marks/*.csv` | Marks and rationales from the six configurations analysed in the paper (2,000 rows each: 1,000 answers × 2 guidance levels) |
| `marks/excluded/*.csv` | Six Gemini 3.x runs excluded by the output-integrity screen (Sect. 3.4 of the paper) |
| `prompts/` | The marking prompt templates for L1 and L2 |
| `notebooks/analysis.ipynb` | Statistics and figures; writes all outputs to `results/` |

## Configurations

| File | Model | Access | Request unit |
|---|---|---|---|
| `claude_opus_5.5.csv` | Claude Opus 5.5 | Claude app | Batch per question |
| `gpt_5.6.csv` | GPT-5.6 | ChatGPT app | One answer per request |
| `gemini_4_high.csv`, `gemini_4_low.csv` | Gemini 4 (High / Low thinking) | API, temperature 0 | One answer per request |
| `kimi_k3.csv` | Kimi K3 | Kimi app | Batch per question |
| `llama_4_maverick.csv` | Llama 4 Maverick | Groq API, temperature 0 | One answer per request |

All marks were collected in October 2026.

## Data dictionary

**`data/answers.csv`**

| Column | Description |
|---|---|
| `dataset` | `mohler` (0–5 scale, step 0.5) or `saf` (0–1 scale, step 0.125) |
| `answer_id`, `question_id` | Identifiers used to join with the mark files |
| `question`, `reference_answer`, `student_answer` | Text from the original datasets |
| `human_score` | Gold score (Mohler: mean of the two raters) |
| `human_1`, `human_2` | Individual Mohler rater scores (empty for SAF) |
| `max_score` | Maximum mark for the dataset |
| `split` | Split in the original release |
| `score_norm`, `score_band` | Score divided by `max_score`, and its quartile band |
| `answer_words` | Word count of the student answer |
| `role` | `test` (sampled and marked by the LLMs), `example` (anchor answers) or `unused` (rest of the pool); `example` and `unused` answers form the training pool of the feature-based baseline |
| `pilot` | `True` for the 50 answers used to pilot the prompt |

**`marks/*.csv`**

| Column | Description |
|---|---|
| `answer_id`, `dataset`, `question_id` | Join keys to `data/answers.csv` |
| `guidance_level` | `1` = question only (L1); `2` = question and reference answer (L2) |
| `score` | Mark returned by the model |
| `rationale` | One-sentence rationale returned by the model |

## Known data issues

- 62 sampled answers are non-response placeholders such as "No response" (1 Mohler, 61 SAF). The paper's primary analysis excludes them.
- 9 Mohler answers (3 sampled) were corrupted to `#NAME?` by a spreadsheet program before this study. They are kept as found and excluded from the primary analysis.
- Kimi K3 returned no score for one answer (`mohler_139`, L1) and empty rationales for three marks. 129 of its SAF marks were off the 0.125 grid and are rounded in the analysis.

## Running the analysis

Locally:

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebooks/analysis.ipynb
```

In Google Colab, open `notebooks/analysis.ipynb` from GitHub and run all cells. The first cell clones this repository if the data are not present. Bootstrap and permutation steps take several minutes.

## Licence

- Code (`notebooks/`): MIT, see `LICENSE`.
- LLM marks, rationales and prompts: CC BY 4.0, see `LICENSE-DATA.md`.
- Questions, reference answers, student answers and human scores remain under the terms of the original datasets; cite Mohler et al. (2011) and Filighera et al. (2022) when you use them.

## Citation

Use the "Cite this repository" button on GitHub or `CITATION.cff`. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24479336.svg)](https://doi.org/10.5281/zenodo.24479336).
