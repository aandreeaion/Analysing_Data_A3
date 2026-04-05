# Assignment 3: Genre Classification of Song Lyrics using Ollama

This repository concearns Part 2 of Assignment 3. The task was to use Python's Ollama library to classify song lyrics into genres and compare two prompting strategies:

- Zero-shot prompting
- Few-shot prompting

The model was evaluated using precision, recall, and F1-score.

## Overview

The goal of the assignment was to classify song lyrics into one of the following genres:

- Country
- Electronic
- Folk
- Hip-Hop
- Indie
- Jazz
- Metal
- Other
- Pop
- R&B
- Rock

The assignment required:
1. Implementing zero-shot prompting
2. Implementing few-shot prompting
3. Evaluating both strategies using precision, recall, and F1-score
4. Comparing performance by genre

## Dataset columns

| Column name | Type | Info |
|---|---|---|
| `Unnamed: 0` | `int64` | Index numeric column |
| `genre` | `object` | Genre label for the song |
| `lyrics` | `object` | Full lyrics of one song |

## Files in this repository

- `Analysing_Data_Assignment3_Part2.ipynb`: main notebook with the full workflow
- `results` folder containing:
     - `zero_shot_full_results.csv`: full zero-shot predictions on the test set
     - `few_shot_full_results.csv`: full few-shot predictions on the test set
     - `genre_comparison_results.csv`: per-genre comparison of zero-shot and few-shot performance
- `data` folder containing:
     - `genreLyrics_train.csv`
     - `genreLyrics_test.csv`
- `README.md`: repository overview

## Method

### Data
- `genreLyrics_train.csv` was used to create the few-shot examples
- `genreLyrics_test.csv` was used for evaluation

### Prompting strategies
- **Zero-shot prompting:** the model received only instructions, the label set, and the song lyrics
- **Few-shot prompting:** the model received the same instructions plus one labeled training example per genre

### Output normalization
Before evaluation, the raw model outputs were inspected and normalized. This was necessary because the model sometimes returned:
- punctuation variants such as `Metal.`
- label variants such as `Hip Hop`
- longer explanations instead of a single label

These outputs were mapped back to the predefined label set when possible.

### Evaluation
Both prompting strategies were evaluated using:
- Precision
- Recall
- F1-score

The results were compared:
- overall
- by genre

## Model used

- `llama3.2:3b` via Ollama

## How to run the notebook

1. Open the notebook in **Google Colab**
2. Enable **GPU** in the runtime settings
3. Upload the following files in the Colab **Files** panel:
   - `genreLyrics_train.csv`
   - `genreLyrics_test.csv`
4. Run the notebook from top to bottom

The notebook installs Ollama, loads the model, runs zero-shot and few-shot classification, evaluates the results, and saves the output CSV files.

## Notes

- The CSV files are tab-separated, so the notebook loads them with `sep="\t"`
- Small and medium balanced samples are used first for inspection before running the full test set
- The final reported results come from the full test set
