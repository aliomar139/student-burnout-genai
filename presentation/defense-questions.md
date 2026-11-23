# Presentation Q&A

## 1. Why did you choose BAT-S? What other options were there?

### What to say aloud

“We chose the Burnout Assessment Tool for Students because it was designed for students. Its 12-item version gives us a score from 1 to 5 and covers four areas of burnout. Two of those, difficulty concentrating and feeling detached from studying, were especially relevant to our question about relying on AI for academic work. We used the 12-item score as our main outcome and also checked our results using all 23 core items.”

### If someone asks for more detail

- **What are the four areas?** Exhaustion, mental distance, cognitive impairment, and emotional impairment. The short form uses three items per area. In the 23-item analysis, we gave each area equal weight by averaging its items first, then averaging the four area scores. [Study methods](../paper/md/study-design-and-evaluation.md)
- **What was the paid option?** Earlier studies used the **Maslach Burnout Inventory–Student Survey (MBI-SS)**. It’s a questionnaire that measures exhaustion, cynicism, and academic efficacy. Mind Garden licenses its student form under the name **MBI-GS (S)**. The BAT developers make their questionnaire available free of charge. [Original study blueprint](../research/92-original-study-blueprint.md) · [Mind Garden student form](https://www.mindgarden.com/313-mbi-general-survey-for-students) · [BAT access terms](https://burnoutassessmenttool.be/start_eng/)
- **What evidence supports BAT-S?** A 2024 study reported evidence for the 12-item scale in 461 Chilean undergraduates. In our 97-student sample, the 12 items had a Cronbach’s alpha of **0.90**, which tells us how consistently the items varied together. A score of **4 or higher** was our study cutoff for the High group. A clinical cutoff would require separate validation. [BAT-S validation study](https://doi.org/10.3389/fpsyg.2024.1434412) · [Our SPSS results](../research/06-data-analysis-and-experiment-history.md#3-statistical-analyses-completed)

## 2. What is Cronbach’s alpha?

### What to say aloud

“We used Cronbach’s alpha to check how consistently the burnout questions worked together. For our 12 main questions, it was **0.90**, which shows high internal consistency in our sample.”

### If someone asks for an example

If students who often feel exhausted also tend to report difficulty concentrating, those answers vary together. Cronbach’s alpha summarizes how consistently the answers vary together across the whole set of questions. In SPSS, we got **0.900 for the 12 main items** and **0.944 for all 23 core items**. [Our SPSS results](../research/06-data-analysis-and-experiment-history.md#3-statistical-analyses-completed)

## 3. What is Spearman’s ρ?

### What to say aloud

“Spearman’s rho tells us whether higher answers on one question tend to go with higher or lower scores on another. For AI dependence and burnout, we got **+0.377**. Students who reported more dependence on AI tended to have higher burnout scores.”

### If someone asks for more detail

- **How does it work?** Spearman’s rho compares the order of the scores, from low to high. That works well for survey answers such as “strongly disagree” through “strongly agree,” where the options have an order.
- **How do you read the number?** It runs from **−1 to +1**. A positive value means higher scores tend to go together. A negative value means higher scores on one measure tend to go with lower scores on the other. A value near zero means little overall tendency in either direction.
- **What did we find?** AI dependence had the strongest positive correlation among the AI questions tested (**+0.377**). Putting off study tasks had the strongest correlation among all 11 questions tested (**+0.445**). The survey measured both at the same time, so the direction of any causal effect remains open. [Our SPSS results](../research/06-data-analysis-and-experiment-history.md#3-statistical-analyses-completed)

## 4. Slide 13. How did we test on students the model hadn’t seen?

### What to say aloud

“We divided the 97 students into five groups. We trained on four groups and tested on the fifth, then rotated the test group until every student had one test prediction. We repeated the whole process five times with different groups. That gave each student five predictions from models that had never trained on their answers.”

### Questions you might get

- **What’s a fold?** It’s one of the five groups. In the diagram, each row shows one train-and-test split. The highlighted group is the one we set aside for that test.
- **Why did you repeat it five times?** The score can depend on how students fall into groups. Repeating the split lets us average results across five different groupings of the same 97 students.
- **How did you get 25 training runs?** Each repetition has five test groups, so we train five models, one for each test group. Five repetitions give 25 fits. Every fit starts with 77 or 78 real training students and tests on 19 or 20 real students.
- **Can a student appear in both training and testing?** Yes, across different runs. For any one prediction, the model trained only on the other groups. The evaluation still uses the same 97 students. Testing on an independent group would be a separate step.

## 5. Slide 16. Why did we try adding none, half, or the full number of synthetic examples?

### What to say aloud

“Each run had only 13 or 14 real students with High burnout to learn from. We tried adding different numbers of synthetic examples to see how much extra practice helped the model catch High-burnout students while keeping false warnings in view. We chose the amount using the training data in each run. The checks picked none in 11 runs, half in 9, and the full amount in 5.”

### Questions you might get

- **What do ‘half’ and ‘full’ mean?** Both refer to the number of real High-burnout students in that training run. If there were 13, ‘half’ meant adding 7 synthetic examples after rounding up, and ‘full’ meant adding 13. All the real training students stayed in the dataset.
- **Why did some runs choose none?** We let the training checks choose the settings, including how many examples to add. They used **F₂**, a score that puts more weight on catching High-burnout students while still accounting for how often warnings are correct.
- **Did the synthetic examples go into the test?** Every test used real students who were set aside before training. The 11, 9, and 5 counts tell us which setting the training checks chose. A comparison with a real-data-only forest is what lets us examine how the two training approaches performed. [Study methods](../paper/md/study-design-and-evaluation.md)

## 6. What is the F₂ score, and how is it different from F1?

### What to say aloud

“F1 and F₂ both combine precision and recall. Precision asks how many of our warnings were correct. Recall asks how many students with High burnout we caught. F1 gives both equal weight. We used F₂ because catching more of the High-burnout students was our priority, while the score still accounts for incorrect warnings.”

### If someone asks for an example

Suppose a model catches **8 out of 10** High-burnout students and issues **20 warnings** in total. Recall is **80%** because it caught 8 of the 10. Precision is **40%** because 8 of its 20 warnings were correct.

| Score | What it prioritizes | Example result |
| --- | --- | ---: |
| F1 | Precision and recall equally | 0.53 |
| F₂ | Recall gets more weight | 0.67 |

Both scores run from 0 to 1. They use the same predictions here. The difference comes from how much weight each score puts on recall. In our study, we used F₂ within the training data to choose the warning model settings. We reported recall, precision, and false-warning counts separately so each part of the result is visible. [Study methods](../paper/md/study-design-and-evaluation.md)

## 7. What does SVR on Broad D do, and how does it differ from our random forest?

### What to say aloud

“We used SVR for regression, which means predicting a number. It gives an estimated burnout score, like 3.7 out of 5. We used the random forest for classification, which means predicting a group. It decides whether to flag a student for High burnout.”

### If someone asks for more detail

- **SVR on Broad D.** SVR stands for Support Vector Regression. Broad D is the set of 23 inputs from 19 survey questions about student background, study conditions, and AI use. We averaged the SVR prediction with the prediction from weighted ridge on Small B to make the score blend. The blend reduced average error for students in the High group, while average error across all students rose slightly.
- **Random forest on Small B.** The forest used eight survey answers. It averaged the decision trees’ scores and checked that average against a warning cutoff to predict High or Below-high. [Study methods](../paper/md/study-design-and-evaluation.md)

## 8. Slide 21. What do recall and precision mean for our warnings?

### What to say aloud

“In general, **recall** asks how many of the real cases a model found. **Precision** asks how many of the model’s flags were correct. In our study, the forest caught about 15 of the 17 students with High burnout, giving us **87.1% recall**. It flagged about 43 students in total, and about 15 of those had High burnout, giving us **34.7% precision**.”

### If someone asks for more detail

| Measure | In general | In our study |
| --- | --- | --- |
| Recall | Correct flags divided by all real cases | Of the 17 students with High burnout, the forest caught 14.8 and missed 2.2 on average. |
| Precision | Correct flags divided by all flags | The forest averaged 14.8 correct warnings and 28.0 false warnings. |

We calculated both percentages in each of the five repeats and then averaged them. Dividing the average counts on the slide can give a slightly different result, particularly for precision. [Random forest validation report](../results/25-random-forest-validation-report.md)

## 9. How much did the GenAI questions help?

### What to say aloud

“The GenAI answers helped a little with score prediction. Adding them lowered the average error by about **0.02 to 0.03 points** on our 1–5 burnout scale. Their contribution to High-burnout warnings is still unclear.”

### Which slide supports that?

- **Slide 18** compares ridge models with and without the GenAI answers on the same test students. This is where we can see what adding those answers contributed to score prediction.
- **Slide 19** shows that the blend made closer score estimates for the High group. Both the blend and ordinary ridge already used GenAI answers.
- **Slide 22** compares a forest that uses eight questions with a logistic model that uses workload alone. Both the model type and the questions changed, so that comparison can’t tell us how much GenAI helped with warnings. [Study results](../paper/md/manuscript.md)

## 10. Slide 23. What did the shuffled-label test tell us?

### What to say aloud

“We kept everyone’s survey answers and randomly mixed up who was labeled High or Below-high. We then reran the evaluation **199 times**. With the real labels, the forest scored **76.0% balanced accuracy**. With the mixed-up labels, it averaged **49.6%**, and none of the reruns reached 76.0%. That suggests the forest picked up a pattern in this group.”

### If someone asks for more detail

- **What did mixing up the labels do?** It broke the link between each student’s answers and their real burnout group, while keeping the same number of High and Below-high labels.
- **What is balanced accuracy?** It averages how often the model correctly identifies each group. High and Below-high get equal weight, even though one group is larger.
- **What does p = 0.005 mean here?** Zero of the 199 reruns matched or beat the result with real labels. The corrected calculation is **(0 + 1) / (199 + 1) = 0.005**. This is evidence of a pattern in the survey data. How well the forest performs with new students is a separate question. [Random forest validation report](../results/25-random-forest-validation-report.md)
