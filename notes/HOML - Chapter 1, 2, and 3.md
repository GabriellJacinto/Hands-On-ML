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

Some parts of step 4 can be automated with the help of pipelines.

Step 5 can be done with cross-validation so you can get a better look at the model's evaluation, since it take a number K of folds and creates different models to train on them randomly. 

For step number 6, a good way to find the best hyper parameters configuration to fine tune the model is to perform a Grid Search to find the best values. The idea is to create models with varying configurations of hyperparameters and train them using cross-validation. Notice that this technique can take a long time since we are making copies of copies of models with varying inputs (both the hyperparameters for the Grid Search and the dataset for the Cross-validation).
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
But the decision of which of these metrics is the best one to use will depend on the application, as exemplified by page 93, since one will give more importance to how many false positives the model had and the other will give more importance to the false negatives.

### Precision Recall trade-off
Either way it is always necessary to look at the precision if we are looking at the recall or vice-versa since only one metric does not guarantee that the model is performing the best it can. Since classification models rely on a decision function to make their decision, they need a <span class="yellow">threshold value</span> to assert what class the particular instance being analysed belongs to. Depending on this value the model will have a higher or lower recall. What is desired is to have a good trade-off depending on the domain of the problem. 

The lower the threshold value the higher the recall will be since we will basically diminish the likelihood of the model predicting a false negative, if we think of the threshold value as a limiting factor, if its value is low, there will be almost no limiting factor so the odds are the model will guess correctly all the desired instances. However that will mean that it will guess more false positives as well since it is not as selective on its decision function, so the precision will lower. 

The counter-intuitive thing about higher values for threshold is that it not always imply in a higher precision. It does imply in lower scores for recall, but it can decrease the precision slightly if we have remove the density of true positives of the positive predictions in the process while keeping the same number of false positives.  

### ROC curve

The receiving operator characteristic (ROC) curve is another way to analyse the trade-off between the values of the confusion table. Before understanding this particular analysis metric, it is necessary to know two other metrics derived from the confusion matrix:
$$
Sensitivity = Recall = TPR_{\space(True\space Positive \space Ratio)}
$$
$$
False\space Positive\space Ratio = 1 - Specificity_{\space(TNR:\space True\space Negative\space Ratio)}
$$
The idea of the ROC curve is to plot the <span class="red">True Positive Ratio (sensitivity) vs. False Positive Ratio</span>. It will give a log-like graph and the closer to the top-left corner it is the better. It doesn't provide much information on the precision, but the higher the TPR the higher the FPR, so it is important to choose a threshold value that is not to high for these two metrics. 

A good property that we can extract from the ROC curve is the <span class="yellow">area under the curve (AUC) </span>, since this gives us a comparison tool to decide what model is more fit. The closer to 1 the result is the better is the model to the task in question.

It is preferred to use the Precision vs Recall graph over the ROC curve when the number of instances classified in the Positive class or the problem requires more attention to the False Positive values (so the precision needs to be verified, which we can't really get information on the ROC curve).

### Multiclass Classification

Another way to use binary classifiers is to make predictions to more than just one class. There are different strategies to that. We can train a model to differentiate each of the classes from each other two at a time (for example apple or orange, orange or pineapple, apple or banana etc to all possible combinations), this is known as a One vs One (OvO) strategy. The other option is to train the model to decide whether it is the desired class or not, this is known as One vs Rest strategy (apple or not apple, orange or not orange etc). 

Clearly OvO will train more classifiers and will consume more compute, since it will have to take into account $\frac{N*(N-1)}{2}$ combinations, and if we choose to use a training algorithm such as cross-validation we will reach even a higher number of models. However the advantage of OvO is that we have a dimensionality reduction of sorts since we only need to train each classifier on a subset of the dataset that has the data for the two classes to be identified. 

The choice between strategies will vary in performance from model to model, but most of the times libraries such as Sci-kit Learn will already have that choice defaulted as OvR. Algorithms that don't scale well with huge datasets (such as SVMs) will have as default OvO.


---
## Quotes
1. ""

## Questions
1. [[Why is that a random classifier has a AUC score of 0.5? What is the mathematical property in question here? Reminds me of monte carlo for some reason. Is it the probability of its random choices? Oh it is, we are talking binary classifiers, of course it will be 50-50.]]

---
# References
> 