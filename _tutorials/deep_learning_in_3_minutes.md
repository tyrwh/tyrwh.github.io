---
title: "Deep Learning in Three Minutes"
excerpt: "A primer for scientists on what deep learning is and how it's used for computer vision tasks."
---

Maybe put some stuff here that can be even more basic than basic. What are the task types? What does "deep learning" mean?



# Overall structure

There is no single project outline that every ML project follows, but the general procedure looks like this:

1. Capture images
2. Annotate the features of interest
3. Train the model
4. Evaluate the model

### Types of tasks

The above was written with three pound signs

Types of tasks can go here:

- Classification
- Detection
- Segmentation

Here's a second view of the list using asterisks to see what that does:

* Classification
* Detection
* Segmentation

# Annotation

ML models are trained on some kind of input data. For computer vision tasks, this data is generally created, or at least curated, by humans. This process of labeling is called **annotation**.

The format of the annotations will generally match the format of the output data:

- For *classification* models, entire images are labeled to denote whether they contain the target feature(s).
- For *detection* models, bounding boxes are drawn around each target feature in the image.
- For *segmentation* models, polygons are drawn around each target feature in the image.

When we say "target feature" here, that could mean a discrete object like a basketball or a horse, or it could be a feature of a larger object, like an eye or a nose. For classification models, it could be a more of a general property that does not really have a discrete location in the image, like "Does this rash look like it is caused by measles?" 

A model could have just one type of target object, or it could have hundreds. 

In the past, training a deep learning model required a vast amount of human-generated annotations, which naturally takes a long time to do. Today, you may be able to generate all the annotation data needed to train a highly accurate model in an hour or two. This is because of two factors:

1. Modern base models require far less data to retrain for your specific task than older ones
2. Semi-automated annotation methods can help you annotate images 10-100x faster