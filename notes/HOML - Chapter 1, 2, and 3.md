---
date: December 12, 2023 (13h42)
tags:
  - lesson
  - done
topic: "[[Machine Learnig]]"
class: "[[Courses#^ddc1b1|Hands-On Machine Learning]]"
professor: Aurélien Géron
place: Coffee Shop
---
`=this.file.tags`
# HOML - Chapter 1, 2, and 3

## Types of Machine Learning Systems

1. Online vs. Batch learning
2. Supervised, unsupervised, semi-supervised, reinforcement learning
3. Instance vs. Model based

The way these models learn vary. On the case for Model based supervised learning, they have <span class="blue">parameters</span> that compose a function that will describe the behavior of the data. To set the values of such parameters, the algorithm has to practice and learn from the data. In order to assure that it is learning, the objective is to reduce a certain metric, called the <span class="red">cost function</span>. 

But having a low cost function is not enough. To verify if the algorithm is not memorizing the data but learning, we evaluate it by using data it was not trained on and measure it with a <span class="blue">performance measure</span> to check if the predictions are as expected.

The best practice to check for the overfit is to use a validation set and a train-dev set, which are subsets from the training set.

![[Datasets-HOML-Ch1.excalidraw]]
*The train-dev set is also used to verify for <span class="red">data mismatch</span>*
*The validation is also mainly used to compare models*

If the model stills overfits, the three common solutions are to reduce the models complexity, get more data or to remove noise from the data.
Furthermore, to improve the performance even more, it is recommended that a fine-tuning is done on the learning algorithm's <span class="blue">hyperparameters</span>, that will help to tailor better values to the model's <span class="blue">parameters</span>.

Thus, the 8 main steps to complete a Machine Learning projects is:

	1. Understand the problem            5. Select models and train
	2. Get the data                      6. Finetune the best model
	3. Gain                              7. Present the solution
	4. Clean and prepare the dataset     8. Launch and maintain

## Classifiers 

Another common task for Machine Learning is classification. Even though the difference between a regression and classification can be blurry sometimes, one thing is sure: it's <span class="red">harder to evaluate a classification model</span>.

There are many performances measures in order to evaluate. One way is using <span class="blue">Cross-Validation</span>, since it evaluates the model on k-folds (k copies of the same model with different configurations). However, since we are measuring for <span class=red>accuracy</span> (ratio of correct predictions), this value might not mean much for analysis, especially for <span class="blue">skewed datasets</span> (see the example on page 90). Therefore there is a better method, which uses calculations based on the <span class=yellow>Confusion Matrix</span>. 

A Confusion Matrix has the following structure:

| Negative Class      | Positive Class      |
| ------------------- | ------------------- |
| True Negative (TN)  | True Positive (TP)  |
| False Positive (FP) | False Negative (FN) |

From these classes, we can extract ratios that help inspect the data.
$$
Precision = \frac{TP}{TP+FP}
$$
$$
Recall_{\space or \space TPR \space or \space Sensitivity} = \frac{TP}{TP+FN}
$$
*Notice that these formulas don't use the True Negative (TN) class*

<span class="yellow">These metrics are inversely related due to the</span> <span class="red">threshold value</span>. To illustrate this relation, see below:

![[recall-precision-relation.excalidraw]]

Therefore we have different metrics: accuracy, precision, and recall. We can also combine the precision and the recall in one metric, called the <span class="blue">F1-score</span>. It is a mathematical ratio called <span class="yellow">harmonic mean</span>. The key idea here is that this mean gives more weight to low values.
$$
F1\space score = \frac{2}{\frac{1}{Precision} + \frac{1}{Recall}} = \frac{2 TP}{2TP + FN + FP} = \frac{TP}{TP + \frac{FN + FP}{2}}
$$
The consequence of the F1-score being a harmonic mean is that it will give better measurements values to <span class="yellow">classifiers that have similar precision and recall.</span>
But the decision of which of these metrics is the best one to use will depend on the application, as exemplified by page 93. 

### Precision Recall trade-off
- decision function
- threshold value
- what higher and lower values for threshold mean for precision and for recall?

### ROC curve
- What does the name mean?
- What precisely it plots?
- Sensitivity, specificity, TPR, TNR, FPR.
- When to choose ROC or PR curves?
- AUC, what is used for?



---
## Quotes
1. ""

## Questions
1. [[]]

---
# References
> 