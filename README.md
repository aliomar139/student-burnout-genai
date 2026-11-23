# Student burnout, study conditions, and generative AI

Can a short questionnaire estimate current burnout symptoms among university students? We compared study conditions, such as workload and sleep, with reported generative AI habits. The study used one survey from 97 students. It measures symptoms reported at the time of the survey, so the results describe associations in this sample.

Start with the [validation report](results/25-random-forest-validation-report.md) for the model comparisons, or read the [questionnaire](research/02-student-survey-questionnaire.md) to see what students answered.

## What we found

We defined High as a score of at least 4 on a 1?5 study scale built from 12 Burnout Assessment Tool items. Seventeen students met that threshold. The table averages five validation repetitions over the same students.

| Warning model | High students detected out of 17 | False warnings out of 80 | Recall | Precision |
| --- | ---: | ---: | ---: | ---: |
| Eight-input random forest | 14.8 | 28 | 87.1% | 34.7% |
| Workload-only logistic regression | 16.0 | 28 | 94.1% | 36.4% |

A workload-only model caught more High cases at the same number of false warnings. The random forest scored higher on average precision (.527 versus .423) and exceeded all 199 shuffled-label runs on mean balanced accuracy (permutation p = .005). The paired uncertainty intervals include zero, and the study has no independent validation cohort. The warning threshold was defined for this study and has no clinical validation.

For numerical score prediction, the fixed Ridge/SVR blend averaged .616 points of absolute error overall and .642 among High-score students. The [experiment history](research/06-data-analysis-and-experiment-history.md) records the model choices and unsuccessful trials. The [comparison CSV](results/25-model-comparison-summary.csv) contains the warning metrics.

## Run the software tests

From the repository root, create a Python 3.12 environment. The commands below use PowerShell. On macOS or Linux use `.venv/bin/python` for the last two commands.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r experiments/dependencies-xgboost.txt
.\.venv\Scripts\python.exe -m unittest discover -s experiments -p "test_*.py"
```

The tests cover synthetic fixtures, scoring, and repository links. Tests for participant files or the original validation archive skip when those local inputs are absent.

## Reproduce experiment 25 with authorized data

Use the approved source files `data/01-original-student-survey.csv` and `data/03-prepared-student-burnout-data.sav`. The [preparation notes](research/13-dataset-preparation-and-corrections.md) document the columns, recoding and corrections. Participant files, local predictions, trained models, and the full validation archive stay outside Git.

```powershell
.\.venv\Scripts\python.exe experiments/25-validate-random-forest-against-baselines-and-chance.py --stage real
$runFolder = Read-Host "Paste the run folder printed by the first command"
.\.venv\Scripts\python.exe experiments/25-validate-random-forest-against-baselines-and-chance.py --stage permutations --out $runFolder
.\.venv\Scripts\python.exe experiments/25-report-and-verify-random-forest-validation.py $runFolder
```

Use the timestamped directory created by the first command under `results/25-random-forest-validation/`. The full permutation run took about 6.7 hours with four workers. Older experiments may require their own dependency files or historical outputs and are indexed in the experiment history.

| Folder | Contents |
| --- | --- |
| `experiments/` | Numbered scripts, settings, and tests |
| `research/` | Study design, data preparation, and experiment history |
| `results/` | Validation report, aggregate tables, and figures |
| `paper/` and `presentation/` | Manuscript sources and presentation materials |
