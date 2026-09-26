# Student Grade Predictor: Early Support Risk Classification

An individual beginner machine-learning project based on the **Student Grade Predictor** topic. It uses study-habit and support information to classify whether a student in the UCI mathematics dataset finished below the passing threshold. The project demonstrates classification, preprocessing, a reproducible train/test split, baseline comparison, and class-aware evaluation.

## Project abstract

This project builds a beginner-friendly classifier to flag possible academic risk in the UCI Student Performance mathematics dataset. The dataset contains 395 records from two Portuguese secondary schools. The target is whether final grade G3 is below 10 out of 20. Only study-habit and support variables are used; G1 and G2 are excluded because they are earlier grades closely related to the target and would make evaluation less useful for early support. A fixed stratified 80/20 split compares a class-balanced logistic regression model with a majority-class baseline. On the held-out 79 records, the logistic model achieves 0.646 accuracy and 0.599 balanced accuracy, with 0.462 recall for at-risk students. The majority baseline has 0.671 accuracy but zero recall for the at-risk class, showing why accuracy alone is misleading. This small observational exercise demonstrates preprocessing, logistic regression, holdout evaluation, and class-aware metrics. It does not establish that any feature causes grades or support decisions about individual students.

## Folder contents

- `student_grade_predictor.py` - complete analysis and model code.
- `notebooks/Student_Grade_Predictor.ipynb` - guided notebook for local Jupyter or Google Colab.
- `data/student-mat.csv` - the mathematics subject file from the UCI dataset.
- `data/uci-dataset-notes.txt` - the dataset's included notes.
- `outputs/results.json` - metrics produced by the included code with the fixed split.
- `report/Project_Report.pdf` - report draft with the results and required sections.
- `report/build_report.py` - regenerate the PDF after editing the student details or project text.
- `report/Project_Report.docx` - editable Word report styled after the supplied sample.
- `report/build_docx_report.py` - rebuild the Word report after editing the author details or text.

## Run on Windows

Open PowerShell in this folder and run:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python .\student_grade_predictor.py
```

The program prints a baseline/model comparison and saves the full metrics to `outputs/results.json`. The included CSV makes the first run work without downloading data. If that CSV is absent, the script tries to fetch the official UCI archive.

## Open the notebook in Colab

After you create a public GitHub repository and upload the contents of this folder, open the notebook from GitHub in Colab. The first setup cell will ask for your repository's HTTPS URL if it needs to clone the files. The notebook installs no packages automatically; if pandas or NumPy is missing in your runtime, run `!pip install -r requirements.txt` from the project folder.

## Model design

- **Target:** at risk/fail when `G3 < 10` on the dataset's 0-20 scale.
- **Inputs:** study time, past failures, school/family support, paid classes, activities, plans for higher education, internet access, absences, travel time, free time, going out, weekday/weekend alcohol-use indicators, and health rating.
- **Excluded:** G1, G2, and G3 grades, plus demographic columns. Excluding G1/G2 avoids relying on earlier grades that are strongly related to the final grade.
- **Model:** class-balanced, L2-regularized logistic regression implemented with NumPy gradient descent.
- **Evaluation:** one stratified 80/20 split with random seed 42; compare against a majority-class baseline. Positive-class precision, recall, F1, and balanced accuracy are reported alongside accuracy.

## Results from the included run

| Model | Accuracy | Balanced accuracy | At-risk precision | At-risk recall | At-risk F1 |
| --- | ---: | ---: | ---: | ---: | ---: |
| Majority-class baseline | 0.671 | 0.500 | 0.000 | 0.000 | 0.000 |
| Logistic regression | 0.646 | 0.599 | 0.462 | 0.462 | 0.462 |

The single split is small: 79 test records. Its scores can vary with another split. The baseline has higher accuracy because most records are in the pass class, yet it misses every at-risk record. The logistic model catches 12 of 26 at-risk records in this test split and also produces 14 false alarms. This is a classroom exercise, not a validated student-screening system.

## Before submitting

1. Replace `[Your Name]`, `[Course / Batch]`, and `[Institution]` in `report/build_report.py`, then regenerate the PDF with `python report/build_report.py`.
2. Run the script or notebook yourself and be ready to explain the target, the excluded grade columns, the confusion matrix, and what recall means.
3. Create a public GitHub repository and upload this folder's contents. Check that a signed-out browser can open the repo and notebook.
4. Submit the exact project title, public link, abstract (under 250 words), and report PDF in the course form. The course reminder also says to email the title to `abpandey.vnsit@gmail.com`.

The reminder lists **26 September 2026** as the minor-project deadline and also says both forms remain open until **10 October 2026**. Treat 26 September as the stated deadline unless your expert confirms the extension.

## Dataset reference

Cortez, P. (2008). *Student Performance* [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5TG7T](https://doi.org/10.24432/C5TG7T). The dataset page lists a CC BY 4.0 license. This repository includes the mathematics CSV and retains the dataset notes for attribution.
