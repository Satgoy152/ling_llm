# Linguistic Problem Dataset for Evaluating Large Language Models (LLMs)

This repository contains a dataset of linguistic problems extracted from The International Linguistics Olympiad (IOL), along with evaluation data generated by several state-of-the-art Large Language Models (LLMs). The dataset is structured to allow for systematic evaluation of LLM performance on linguistic reasoning tasks across various problem types.

## 📚 Data Source

The dataset is derived from problems available on the International Linguistics Olympiad (IOL) website: ioling.org.

* The problems for each year were extracted from the official IOL PDFs and saved in the `data/` subfolder.
* The primary objective was to extract the questions into a text format suitable for direct input into LLMs.
* For problems that used images as inputs/outputs, relevant images were also extracted and included in the dataset.

Each year's folder includes:

* The original IOL problem set PDF and solution set PDF.
* Extracted questions in .txt format.
* Corresponding answers in .txt format.

## 🤖 Evaluated Models

We evaluated the performance of eight different LLMs on the dataset:

1. Claude 3.5 Sonnet
2. Claude 3 Haiku
3. Claude 3 Opus
4. GPT-4 Omni
5. GPT-4 Mini
6. OpenAI o1
7. GPT-4
8. Gemini 1.5 Pro

## 🛠 Data Generation Process

The dataset was generated by querying the models via a chatbot interface. A script provided in the `translation/` folder allows for direct API queries to these models for automating the data generation process.

### Data Folder Structure

All generated data is saved under the /data/ folder, organized by year and model:

```
/data/
    ├── iol_{year}/
    │       ├── iol_{year}.txt
    │       ├── iol_{year}_ans.txt
    │       ├── iol_{year}_problem_set.pdf
    │       ├── iol_{year}_solution_set.pdf
    │       ├── iol_{year}_classification.txt
    │       └── {model_name}/
    │             ├── evaluation.txt
    │             └── iol_{year}_{model_name}.txt
    └── ...
```

## 📊 Data Evaluation

We developed a multi-stage evaluation pipeline to systematically assess model outputs. The evaluation process is automated using scripts stored in the `evaluations/` folder.

### Question Classification

The first step was to classify each question into one of three types:

1. **Type 1 - Questions with One Answer**

   * Example: True/False, Matching, or Single-word answers
   * Grading: 0 (wrong) or 1 (right)
2. **Type 2 - Phrase Answer Questions**

   * Example: Questions requiring a phrase of 3+ words but with one correct answer
   * Grading:
     * 0 (completely wrong)
     * 1 (partially correct)
     * 2 (completely correct)
3. **Type 3 - Explanation Answer Questions**

   * Example: Questions requiring both an answer and an explanation
   * Grading:
     * 0 (completely wrong)
     * 1 (either the answer or explanation is correct)
     * 2 (both are correct)

## 📈 Dataset Summary

Our dataset contains a total of 1250 problems, split into text-only questions and vision-based problems.

| Question Type         | Total Questions | Type 1 | Type 2 | Type 3 |
| --------------------- | --------------- | ------ | ------ | ------ |
| Text-only Problems    | 1198            | 666    | 501    | 31     |
| Vision-based Problems | 52              | 45     | 7      | 0      |

## 🤖 Model Evaluation Pipeline

We used the Claude 3.5 Sonnet API to evaluate model responses against the official solutions provided by IOL. The evaluation process involved the following steps:

1. **Classification:**

   * Each problem for each year was classified into Type 1, Type 2, or Type 3.
   * The classifications were saved under their respective year folders in `/data/`.
2. **Grading:**

   * Using the classifications, we compared model responses with official solutions.
   * Grading was done in two stages:
     * Initial grading using an LLM to compare answers.
     * Secondary grading by converting the data into a standardized JSON format for further analysis.
3. **Verification:**

   * Type 1 problems were verified using one-to-one matching between model answers and real answers.
   * Type 2 problems were evaluated using BLEU scores and diff metrics to measure accuracy.
   * Type 3 problems were manually graded due to their complexity.

## 📂 Scripts and Tools

All the scripts used for data extraction, classification, grading, and evaluation are provided in the following Jupyter Notebooks:

1. `grading.ipynb` – Contains all code and prompts used for model grading and classification.
2. `eval_data.ipynb` – Processes the text files into JSON objects and evaluates model performance.
3. `translation/` – Contains scripts for querying models via API.

## 📊 Data Visualization

The final evaluation results were exported to CSV files for visualization purposes. These results can be used to create charts and graphs that showcase model performance across different problem types and years.

## 🔍 How to Use This Repository

1. Clone this repository:

```bash
git clone https://github.com/Satgoy152/ling_llm.git
cd ling_llm
```

2. Run the grading.ipynb notebook to classify and grade new problems.
3. Use the translation/ API scripts to query new models and generate additional data.
4. Process evaluation results using eval_data.ipynb.

## 📈 Key Findings (from the Paper)

## 📄 Citation

If you use this dataset or scripts in your research, please cite our paper:

```bibtex
@article{
}
```
