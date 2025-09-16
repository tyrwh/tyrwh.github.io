---
title: "Precision, Recall, and F1"
excerpt: "A short guide to the three most fundamental model metrics."
---

Of all the metrics that are commonly used to describe an ML model's performance, the simplest ones are Precision (P), Recall (R), and F1. These three are the foundation for several more complex metrics.

All three metrics range from 0 to 1, with a higher score indicating a better model. You may also see them written as percentages, i.e. rescaled from 0 to 100.

This is a short overview of P, R, and F1 that covers:
* The formal mathematical definitions of each term
* Why they are important
* How adjusting the confidence threshold affects


# Positive and Negative

For the purpose of evaluating an ML model, the human annotations are the **ground truth** against which the model is compared. A model prediction is considered correct only when it matches the human annotation.

If a model is performing perfectly, then when you apply it to an image to produce some sort of output (classifications, bounding boxes, polygons), that output will match the human ground truth in all cases.

The way in which you decide whether a prediction matches a human annotation depends on the type of task the model is doing.

For classification models, both the input and output are binary variables. *Does the image contain a dog, or not? Does the image contain symptoms of X disease, or not?* For a given image, you simply compare the feature(s) that were marked as being present in the image by the model to those marked as present by humans.

For detection models, the input and output are bounding boxes, each with a discrete size, shape, and position within the image. This makes it slightly more complicated to classify each prediction as correct or incorrect, since two boxes drawn around the same target object will never overlap perfectly, regardless of who drew them.

To account for this, we need a way to quantify the extent to which two boxes overlap. The simplest and most common way to do this is by calculating the intersection-over-union (IoU).

For segmentation models, the input and output are polygons that delineate various target features in an object.


## True and False

There are two ways that a model's prediction can be incorrect: it can identify a target object where none exists, and it can fail to identify a target object that is truly there.

A True Positive is an instance where the model has detected something which was present in the ground truth annotations.

A False Positive is an instance where the model has detected something that was not present in the ground truth annotations.

A False Negative is an instance where the model has missed something that was present in the ground truth annotations.

A True Negative is an instance where the model has missed 


For some tasks, the number of True Negatives may be impossible to calculate or simply not helpful. In a detection task, for example, 

## Precision and Recall

**Precision** is a measure of the prevalence of false positives (FP). It is the proportion of the objects detected by the model that are present in the ground truth data.

$$
P = \frac{TP}{TP + FP}
$$

A model with a high P value produces a low number of false positives, while a model with low P has a high number of false positives. That is, it detecting many things that aren't really there.

**Recall** is a measure of the prevalence of false posinegativestives (FN). It is the proportion of the objects identified in the ground truth data that were successfully detected by the model.

$$
R = \frac{TP}{TP + FN}
$$

In other words, recall is the proportion of the target objects that are detected by the model. A model with low R is missing many target objects. A model with P = 1 has zero false negatives (FN).

It is important to report both P and R, because there is often a tradeoff between the two, and a model that excels in one metric may be terrible in the other.

For example, say that you have trained two models to detect aphids in an image. You apply them to an image in which 50 aphids were found and annotated in the ground truth data.

Model A detects 5 aphids, all 5 of which were present in the ground truth. It has made no false positives, so its precision is perfect. It has missed the other 45 aphids, however, meaning it has many false negatives and thus a terrible recall:

$$
\begin{aligned}
P_A &= 5 / (5 + 0) = 1.0
R_A &= 5 / (5 + 45) = 0.05
\end{aligned}
$$

Model B detects 500 aphids, including all 50 of the aphids that were noted in the ground truth. It has no false negatives (i.e. it has not missed anything) but a huge number of false positives. Thus the recall is perfect but the precision is terrible:

$$
\begin{aligned}
P_B &= 50 / (50 + 450) = 0.10
R_B &= 50 / (50 + 0) = 1.0
\end{aligned}
$$

Each of these models would look good if you only looked at precision or recall, but when we look at both terms we can see that both models are performing poorly. A good model will have both high precision and high recall.

## F1

Naturally, you might want to have a single term that summarizes . The **F1 score** is a measure that incorporates both the number of false positives and the number of false negatives:

$$F1 = \frac{2 \cdot TP}{(2 \cdot TP + FP + FN)}$$

More precisely, the F1 is the *harmonic mean* of P and R. The harmonic mean of a set of numbers is the reciprocal of the mean of the reciprocals of that set. That is, for numbers *a*, *b*, and *c*, the harmonic mean is calculated like so:

$$HM = \left( \frac{a^{-1} + b^{-1} + c^{-1}}{3} \right) ^{-1}$$

This is often used to find a meaningful "average" of fractions when the arithmetic mean would be misleading. For example, if you take a round trip of 40 miles each way (80 miles in total), going 20 mph one way and 40 mph on the way back, the trip will take 3 hours. This is equivalent to driving the full distance at an average speed of 26.6 mph, which the harmonic mean of 20 and 40 mph.

If you write out the harmonic mean of P and R and simplify the terms, you can see that it reduces to the equation for F1 given above:

$$
\begin{aligned}
F1 &= \left( \frac{P^{-1} + R^{-1}}{2} \right)^{-1}
&= \left( \frac{\frac{TP + FP}{TP} + \frac{TP + FN}{TP}}{2} \right)^{-1}
&= \left( \frac{2 \cdot TP + FP + FN}{2 \cdot TP} \right)^{-1}
&= \frac{2 \cdot TP}{2 \cdot TP + FP + FN}
\end{aligned}
$$

This reduced form of the F1 equation ($2TP / (2TP + FP + FN)$) is the one you will see most often. The harmonic mean form is not as widely used.

Notice that none of these equations include a term for the number of true negatives (TN). As mentioned in the section above, TN is often not very useful or informative.

## Confidence thresholds

When a deep learning model is applied to an image, it makes a set of predictions: . Typically, each of these predictions has its own associated **confidence score**. This score ranges from 0 to 1, with a higher value indicating that the model is more confident that the prediction in question is correct.

In a well-trained model, this confidence score is closely tied to a : predictions with `confidence = 0.05` are almost exclusively false positives, while predictions with `confidence = 0.95` are almost exclusively true positives. In a poorly performing model, the confidence score will be less accurate.

When you apply a model to new data, you will often set a *confidence threshold* for reporting. Only those predictions with a confidence score equal to or greater than this threshold value will be included in the results.

This filtering can also be done retroactively. If you want to examine the effect of different confidence , you can included in the initial model output and filtered out later on in your workflow.

**P, R, and F1 scores for a model are 100% contingent on the confidence threshold used to filter predictions.** 

A deep learning model which produces confidence values *does not have* a generic or universal value of precision, recall, or F1. It only has values of P/R/F1 at a specific confidence threshold. 

Whenever you report a model's P, R, or F1, you should include the confidence threshold used.

It is very important to check the documentation for whatever tools you are using to see what the confidence threshold. 


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


