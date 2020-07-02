---
title: "Code Example"
teaching: 5
exercises: 10
questions:
- "How do you use the sci-kit learn and tensorflow packages for machine learning?"
objectives:
- "Train a support vector machine for classification."
- "Train a random forest for classification."
- "Train a simple neural network for classification."
keypoints:
- "The basic features of sci-kit learn and tensorflow are very simple to use."
- "To perform more sophisticated model construction, one should carefully read the textbook."
---

# Alternative Metrics

As seen in the previous section, accuracy is typically not the preferred metric for classifiers. In this section we will define some new metrics. Let TP, FP, TN, FN be the number of true positives, false positives, true negatives, and false negatives classified using a given model.

Before getting into these metrics, it is important to note that a machine learning binary classifier does not predict something as "signal" or "background" but rather gives a probability that a given instance corresponds to a signal or background (i.e. it would output `[0.271, 0.799]` where the first index corresponds to background and the second index as signal). It is then up to a human user to specify the probability threshhold at which something is classified as a signal. For example, you may want the second index to be greater than 0.999 to classify something as a signal. As such, the TP, FP, TN and FN can be altered for a given machine learning classifier based on the threshhold requirement for classifying something as a signal event.

> ## Classifiers in Law
> In criminal law, Blackstone's ratio (also known as the Blackstone ratio or Blackstone's formulation) is the idea that it is better that ten guilty persons escape than that one innocent suffer. If background = person is innocent and signal = person is guilty, then this corresponds to the requirement that one needs to be at least 90% confidence that somebody commited a crime in order to classify them as guilty in a court of law. It is obviously difficult to get such precise probabilities when dealing with probabilities of crimes being commited. 
{: .callout}

## Precision

Precision is defined as

$$\text{precision}=\frac{\text{TP}}{\text{TP}+\text{FP}}$$

It is the ratio of all things that were **correctly** classified as positive to all things that **were** classified as positive. Precision itself is an imperfect metric: a trivial way to have perfect precision is to make one single positive prediction and ensure it is correct (1/1=100%) but this would not be useful. As such, precision is typically combined with another metric: recall.

## Recall / True Positive Rate

Recall is defined as 

$$\text{recall}=\frac{\text{TP}}{\text{TP}+\text{FN}}$$

It is the ratio of all things that were **correctly** classified as positive to all things that **should have been** classified as positive. Recall itself is also an imperfect metric: a trivial way to have perfect recall is to classify everything as positive; doing so, however, would result in a poor precision score. As such, precision and recall need to be considered together. They can also be combined using a harmonic mean to give a metric that considers both scores.

## F1-Score

The F1-Score is defined as 

$$F_1 = \frac{2}{\frac{1}{\text{precision}}+\frac{1}{\text{recall}}} = \frac{\text{TP}}{\text{TP}+\frac{\text{FN}+\text{TP}}{2}} $$


## The ROC Curve
The ROC curve is a plot of the recall (or true positive rate) vs. the false positive rate: the ratio of negative instances incorrectly classified as positive. A classifier may classify many instances as positive (i.e. has a low tolerance for classifying something as positive), but in such an example it will probably also incorrectly classify many negative instances as positive as well








~~~
decisions_nn = NN_clf.predict_proba(X_test)[:,1]
decisions_rf = RF_clf.predict_proba(X_test)[:,1]
fpr_nn, tpr_nn, thresholds = roc_curve(y_test, decisions_nn)
fpr_rf, tpr_rf, thresholds = roc_curve(y_test, decisions_rf)
~~~
{: .language-python}

~~~
plt.plot(fpr_rf,tpr_rf, label='Random Forest')
plt.plot(fpr_nn,tpr_nn, color='r', ls='--', label='Neural Network')
plt.plot([0, 1], [0, 1], '--', color=(0.6, 0.6, 0.6), label='Luck')
plt.grid()
plt.legend()
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.show()
~~~
{: .language-python}
