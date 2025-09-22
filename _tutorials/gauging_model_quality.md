---
title: "Gauging model quality"
excerpt: "How do you decide if a model is performing well or not?"
---

One thing many people often want to know whether a model is performing well or not. Is $F1=0.93$ good? Is $mAP_{50-95}=0.78$ bad? Is it worth your time to gauge thow 

There is no clear-cut answer, but below are some steps that you can use to gauge the performance of your model.

# Questions to ask before you look at the metrics

### How difficult is the task in question?

Some computer vision tasks are profoundly simple, such as the widely-used Microsoft *Common Objects in Context* (COCO) dataset that was structured around objects that are "easily recognizable by a 4 year old" (CITE). Others may require a qualified expert with years of experience to accurately annotate.

Is the 

Asking this question may also draw attention to a task that is poorly defined. Say you have a dataset which consists of pictures of apples harvested at different points.

### How good is the image quality?

Even if the task is straightforward in theory, the quality of the images plays an enormous role in how well the model can ultimately perform.

Are target objects often obscured by one another or by non-target objects? Is everything in focus, so that it is very easy to draw a line around each target object, or are the edges blurry and hard to define?

If two humans can look at an image and .

### Have you measured the rate of agreement between humans?

If you have 

Have you done any comparisons to gauge how consistent one human is against another? If not, is this feasible to do?

It is difficult for your model to surpass the level of human-human agreement, 


# Know what dataset you are looking at

Are you looking at test set performance?

# Examine the confidence curves

The tool you use to train and evaluate the model may spit out curves of P, R, and F1 vs. confidence. Sometimes these are drawn separately, while other times they are drawn as one. If you have multiple classes?

For P, R, and F1, you want to see a *plateau* on the curve. As the confidence threshold is riased, the

In a model that is performing well, the confidence score of each prediction will track very closely to the ground truth:
* True Positives will have a 

### Understanding what a total failure looks like

One thing to consider is what a model that has absolutely no predictive ability would look like.

This is analogous to the concept behind a *p*-value:

