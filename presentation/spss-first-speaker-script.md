# Student burnout | Speaker script

26 slides · Allow about 7 to 8 minutes, including slide changes.
Read the paragraphs aloud. The slide labels are cues.

## Introduction · Slides 1–4


### Slide 1: Opening

We’re Ali Omar and Abdallah Mestrah from Lebanese University. Dr. Kassem Danash supervised this study. We looked at whether study conditions and generative AI use can help us estimate students’ current burnout.

### Slide 2: Research questions

We asked how close we could get to a student’s burnout score and whether adding AI answers improved that estimate. We also tested how well a model could flag students in the High-burnout group.

### Slide 3: Who answered the survey

We had 97 students. Seventeen reached our High-burnout cutoff. That matters later because the warning model had fewer High-burnout examples to learn from.

### Slide 4: How we scored burnout

The main score uses 12 questions covering exhaustion, mental distance, and difficulties with thinking and emotions. We averaged the answers on a scale of one to five. For this study, four or higher counted as High burnout.

## SPSS Analysis · Slides 5–9


### Slide 5: Preparing the answers

In SPSS, we converted answers like study-hour ranges into numeric codes. Because students could select more than one AI use, we gave each option its own yes-or-no column. We checked the prepared data against the original survey export.

### Slide 6: Average scores

Of the four burnout dimensions, exhaustion had the highest average at 3.43 out of five. The main burnout score averaged 3.13 across the group.

### Slide 7: How scores were spread

When we put the 97 burnout scores in order, the middle one was 3.08. Scores ranged from about 1.42 to five. There was a slightly longer tail on the high side.

### Slide 8: Checking the questionnaire

We used Cronbach’s alpha to check how consistently the burnout answers varied together. It was 0.90 for the 12 main questions and about 0.94 for all 23. We kept all the questions in both sets.

### Slide 9: Correlations with burnout

Students who reported putting off their work tended to have higher burnout scores. That was the strongest link among the questions we checked. Of the AI questions tested, dependence on AI had the strongest link.

## How We Tested The Models · Slides 10–16


### Slide 10: Two prediction tasks

One model guesses a score on the one-to-five scale. The other decides whether to flag the student for High burnout. We use the separate burnout questionnaire to check both predictions.

### Slide 11: Testing the AI answers

To see what the AI answers added, we ran a smaller and a broader comparison. Each time, we kept the same kind of model and tested on the same students, with and without the AI questions.

### Slide 12: What the forest sees

Our warning model used eight answers. Five describe study conditions, like workload and sleep. The other three describe how often students use AI, how much they depend on it, and whether they use it in place of thinking through the work themselves.

### Slide 13: Keeping training and testing separate

We split the students into five groups. The model trained on four groups and predicted the fifth, then we rotated which group it tested on. We repeated that process five times.

### Slide 14: Choosing the settings

Within each training split, we tried different settings on smaller groups of training students. Once we picked the settings, we tested the model on the students we’d set aside.

### Slide 15: Making synthetic examples

We started with two similar students with High burnout. For workload ratings of four and five, we picked a value between them and rounded it to a survey option. We copied sleep and study hours together from one student and checked the new profile before keeping it.

### Slide 16: Why we used synthetic examples

Each training run had only 13 or 14 real students with High burnout. The made-up examples gave the model more practice. The training checks favored adding them in 14 of 25 runs. Every test used real students.

## Results · Slides 17–26


### Slide 17: Measuring score error

Suppose a student scores four and the model guesses 3.4. The guess is off by 0.6 points. We average those misses across the students we tested. That’s mean absolute error, or MAE.

### Slide 18: Did the AI answers help?

Adding the AI answers lowered ridge regression’s average error by about 0.03 points in the smaller comparison and 0.02 in the broader one. Those are small changes on a five-point scale.

### Slide 19: What changed with the blend

We averaged the predictions from two models. For the 17 High-burnout students, the blend cut the average error from 0.93 to 0.64 points. Across all 97 students, the error went up slightly, from 0.59 to 0.62.

### Slide 20: How the forest decides to flag

The forest averages scores from 100 decision trees. If that average is 0.40 and the model’s cutoff is 0.35, it flags the student. We check that flag against the actual burnout questionnaire, where four or higher counts as High.

### Slide 21: Who the forest flagged

On average, the forest caught about 15 of the 17 students with High burnout. It also flagged 28 Below-high students by mistake. The chart has decimals because we averaged the counts across five repeats.

### Slide 22: Comparing the forest with workload alone

At the chosen cutoffs, workload alone caught about one more High-burnout student, and both models averaged 28 false warnings. Across cutoffs, the forest did better on average precision, which combines how many High students it catches with how often its warnings are correct.

### Slide 23: Checking against chance

We kept the survey answers and randomly reassigned the High and Below-high labels. Then we reran the test 199 times. We scored each run with balanced accuracy, which gives the two groups equal weight. None reached the 76% we got with the real labels.

### Slide 24: Testing the saved model on made-up profiles

In a separate check, the saved forest flagged 159 of 170 synthetic profiles labeled High. Those profiles came from students the model had already trained on, and the labels came from those original records.

### Slide 25: What the study can tell us

Our study has three main limits. We had only 97 students, including 17 in the High group. We measured their answers once, so we cannot say what caused their burnout. We also tried several models using the same students, which can make the results look better than they would on a new group.

We need an independent group to check whether the results hold up.

### Slide 26: What we found

To conclude, adding AI answers slightly improved burnout score predictions. The forest detected about 15 of the 17 High students, but also gave 28 false warnings on average. Workload alone detected about 16, with the same number of false warnings, although the difference remains uncertain.

These are promising research findings, but they still need testing on new students. Thank you.
