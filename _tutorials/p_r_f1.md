---
title: "Precision, Recall, and F1"
excerpt: "A short guide to the three most fundamental model metrics."
---

Of all the metrics that are commonly used to describe an ML model's performance, the simplest ones are Precision (P), Recall (R), and F1. They  are the foundation for several more complex metrics.

All three metrics range from 0 to 1, with a higher score indicating a better model. You may also see them written as percentages, i.e. rescaled from 0 to 100.

This is a short overview of P, R, and F1 that covers:
* The formal definition of each metric
* A plain-language explanation of what they measure
* Why these metrics are important
* How adjusting the confidence threshold affects each one

## Positive and Negative

For the purpose of evaluating an ML model, the human annotations are the **ground truth** against which the model is compared. A model prediction is considered correct only when it matches the human annotation.

If a model is performing perfectly, then when you apply it to an image to produce some sort of output (classifications, bounding boxes, polygons), that output will match the human ground truth in all cases.

The way in which you decide whether a prediction matches a human annotation depends on the type of task the model is doing.

For classification models, both the input and output are binary variables. *Does the image contain a dog, or not? Does the image contain symptoms of X disease, or not?* For a given image, you simply compare the feature(s) that were marked as being present in the image by the model to those marked as present by humans.

For detection models, the input and output are bounding boxes, each with a discrete size, shape, and position within the image. This makes it slightly more complicated to classify each prediction as correct or incorrect, since two boxes drawn around the same target object will never overlap perfectly, regardless of who drew them.

To account for this, we need a way to quantify the extent to which two boxes overlap. The simplest and most common way to do this is by calculating the intersection-over-union (IoU).

For segmentation models, the input and output are polygons that delineate various target features in an object.

A model may have many different **classes** of target object that is seeking. 

## True and False

There are two ways that a model's prediction can be incorrect: it can identify a target object where none exists, and it can fail to identify a target object that is truly there.

A True Positive is an instance where the model has detected something which was present in the ground truth annotations.

A False Positive is an instance where the model has detected something that was not present in the ground truth annotations.

A False Negative is an instance where the model has missed something that was present in the ground truth annotations.

A True Negative is an instance where the model .

The total number of target objects detected by the model is equal to $\mathrm{TP+FP}$, while the total number of target objects detected in the ground truth is equal to $\mathrm{TP+FN}$.

## Precision and Recall

It is not very useful to know the number of false positives or true negatives in isolation, since it obviously depends on the number of images, the frequency of the target object, random sampling, *etc*. We need metrics that are properly scaled in order to get a good sense of model performance.

**Precision** (P) is a metric that describes the prevalence of false positives. It is equal to the number of correct detections ($\mathrm{TP}$) divided by the total number of detections ($\mathrm{TP+FP}$):

$$
P = \frac{\mathrm{TP}}{\mathrm{TP} + \mathrm{FP}}
$$

If a model has high P, any objects that are detected by the model are very likely to be correct detections. If it has low P, then the majority of its detections are liable to be incorrect, *i.e.* it is often seeing things that aren't there.

**Recall** (R) is is a metric that describes the prevalence of false positives. It is equal to the number of correct detections (`TP`) divided by the total number of objects that were present in the ground truth (`TP+FN`):

$$
R = \frac{\mathrm{TP}}{\mathrm{TP} + FN}
$$

If a model has high R, it has correctly detected most of the target objects that were noted in the ground truth. If it has low R, then it failed to detect many of these targets.

**It is important to look at both both P and R**, because there is often a tradeoff between the two and a model that excels in one metric may be terrible in the other.

For example, say that you have trained two models to detect aphids in an image. You apply them to an image in which 50 aphids were identified and annotated in the ground truth data.

Model A detects 5 aphids, all 5 of which were present in the ground truth. There are no false positives, so its precision is perfect. It has missed the other 45 aphids, however, meaning it has many false negatives and thus a terrible recall:

$$
\begin{aligned}
P_A &= \frac{5}{(5 + 0)} = 1.0 \\
R_A &= \frac{5}{(5 + 45)} = 0.05 \\
\end{aligned}
$$

Model B has the opposite problem. It detects 500 aphids, including all 50 that were noted in the ground truth, meaning that there are no false negatives and its recall is perfect. There is a huge number of false positives, however, so its precision is terrible:

$$
\begin{aligned}
P_B &= \frac{50}{(50 + 450)} = 0.10 \\
R_B &= \frac{50}{(50 + 0)} = 1.0 \\
\end{aligned}
$$

Each of these models might look good if you only looked at P or R, but when we look at both terms we can see that both models are not very useful. A good model will have both high precision and high recall.

## F1 score

Naturally, you might want to have a single term that accounts for both types of error. The **F1 score** is a metric incorporating both the number of false positives (FP) and the number of false negatives (FN) relative to the number of true positives (TP):

$$\mathrm{F1} = \frac{2 \cdot \mathrm{TP}}{(2 \cdot \mathrm{TP + FP + FN})}$$

More precisely, the F1 is the *harmonic mean* of P and R. The harmonic mean of a set of numbers is the reciprocal of the mean of the reciprocals of that set. That is, for numbers *a*, *b*, and *c*, the harmonic mean is calculated like so:

$$HM = \left( \frac{a^{-1} + b^{-1} + c^{-1}}{3} \right) ^{-1}$$

This is often used to find a meaningful average of fractions when the arithmetic mean would be misleading. For example, say you take a round trip of 40 miles each way (80 miles in total), going 20 mph one way and 40 mph on the way back. The trip will take 3 hours: 2 hours there and 1 hour back. This is equivalent to driving the full distance at an average speed of 26.6 mph, which is the harmonic mean of 20 and 40 mph.

If you write out the harmonic mean of P and R and simplify the terms, you can see that it reduces to the equation for F1 given above:

$$
\begin{aligned}
\mathrm{F1} &= \left( \frac{P^{-1} + R^{-1}}{2} \right)^{-1} \\
&= \left( \frac{\frac{\mathrm{TP + FP}}{\mathrm{TP}} + \frac{\mathrm{TP + FN}}{\mathrm{TP}}}{2} \right)^{-1} \\
&= \left( \frac{2 \cdot \mathrm{TP + FP + FN}}{2 \cdot \mathrm{TP}} \right)^{-1} \\
&= \frac{2 \cdot \mathrm{TP}}{2 \cdot \mathrm{TP + FP + FN}} \\
\end{aligned}
$$

This reduced form of the F1 equation ($2TP / (\mathrm{2TP + FP + FN})$) is the one you will see most often. The harmonic mean form is not as widely used.

### Why no True Negatives?

Notice that none of these equations include a term for the number of true negatives (TN). There are two reasons for this.

First, when a given class of target object is rare, then the number of TNs will be exceedingly large compared to the number of TP/FP/FNs. 

For example, say that you . 

A model that simply returns `False` no matter what the image 

For example, 

Second, the number of true negatives may be hard to define in any meaningful way in the first place. In an object detection task, both the ground truth and predictions take the form of boxes with a discrete shape, size, and position. The 



### F beta

As a metric, F1 gives equal weight to a false positive and a false negative. What if one type of error is worse than the other? Can you use a different metric to push the model into being more or less cautious in its predictions?

It is easy to envision a scenario where this is the case. If your model is trained to detect symptoms of a rare and dangerous disease, then a false negative may be fatal, while a false positive merely f.

This can be done using the $F_{\beta}$ metric. 

# Confidence thresholds

When a model is applied to an image, it makes a set of predictions. Typically, each of these predictions has its own associated **confidence score**. This score ranges from 0 to 1, with a higher value indicating that the model is more confident that the prediction in question is correct.

In an ideal model, this confidence score is a good reflection of the true state of things: predictions with `confidence = 0.05` are almost exclusively false positives, while predictions with `confidence = 0.95` are almost exclusively true positives. In a poorly performing model, the confidence score will be less accurate.

When you apply a model to new data, you will often set a **confidence threshold** for reporting. Only those predictions with a confidence score equal to or greater than this threshold value will be included in the results.

This filtering can also be done retroactively. If you want to examine the effect of different confidence , you can included in the initial model output and filtered out later on in your workflow.

**P, R, and F1 scores for a model are 100% contingent on the confidence threshold used to filter predictions.** 

A deep learning model which produces confidence values *does not have* a generic, universal value of precision, recall, or F1. It only has a P/R/F1 at a given confidence threshold.

It is important, therefore, to know what confidence interval was used to produce P/R/F1 when evaluating another model, and to include the confidence threshold used when reporting your own model's performance. Check the documentation for whatever tool you're using to .

## How does the confidence threshold affect P and R?

As you increase the confidence threshold, a model's precision tends to go up and its recall tends to go down.

At a very low threshold, you accept a large number of predictions. This includes many low-confidence predictions, which are more likely to be false positives, so the precision will be very low. However, it is likely that this large set of predictions includes most or all of the , meaning that there are fewer false negatives and thus the recall will be very high.

At a very high threshold, you accept only a small number of high-confidence predictions. This is unlikely to include many false positives, so the precision will be high, but you are likely filtering out many correct results, causing a 

One type of plot you will often see is a line plot showing P/R at difference confidence thresholds. This is called a *precision-confidence curve* or *recall-confidence curve*.

Below are several plots of this type. 

Examining these plots is a good way to roughly evaluate a model's quality. If the model is functioning well, then you want a large range of confidence thresholds to work well.

In the precision-confidence curve, the .

## How does the confidence threshold affect F1?

As the confidence threshold increases from 0 to 1, the precision increases and the recall decreases. In practice, this means that the F1 score will tend to plateau.

Again, you can use the F1-confidence plot as a good visual gauge for model quality.

This will give you some idea of how robust your model is when it comes to choosing a confidence threshold. If the model has a consistently high F1 across a wide range of values, then the exact value of confidence threshold . If the F1 value peaks at a very specific threshold and falls off dramatically outside of that, the model 


