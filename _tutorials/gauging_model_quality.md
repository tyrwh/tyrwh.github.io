---
title: "Gauging model quality"
excerpt: "How do you decide if a model is performing well or not?"
---

One thing many people often want to know whether a model is performing well or not. Is $F1=0.93$ good? Is $mAP_{50-95}=0.78$ bad? 

There is no clear-cut answer, but you can.

# Questions to ask before you look at the metrics

Everyone 

### How hard is the task in question?

ML models are used for a staggering array of image analysis tasks. The task in question can range from the trivially easy to one that only highly experienced experts are qualified to perform. The widely-used Microsoft *Common Objects in Context* (COCO) dataset was explicitly created around "91 objects \[*sic*\] types that would be easily recognizable by a 4 year old" (CITE).

Asking this question may also draw attention to a task that is poorly defined. Say you have a dataset which consists of pictures of apples harvested at different points.

### How good is the image quality?

Even if the task is straightforward in theory, the quality of the images plays a large part in how well the model can perform.

Are target objects often obscured by one another or by non-target objects? Is everything in focus, so that it is very easy to draw a line around each target object, or are the edges blurry and hard to define?

### How good is the human annotation data?
This overlaps somewhat with the previous question.

Have you done any comparisons to gauge how consistent one human is against another?

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

