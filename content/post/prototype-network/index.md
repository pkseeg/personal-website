---
title: What Are Prototypical Networks?
subtitle:

# Summary for listings and search engines
summary: Prototypical networks are trained by mimicking real-world low-resource scenarios to enable few-shot machine learning.

# Link this post with a project
projects: []

# Date published
date: "2023-09-11T00:00:00Z"

# Date updated
lastmod: "2023-09-11T00:00:00Z"

# Is this an unpublished draft?
draft: true

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: ''
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- architectures
- information extraction

categories:
- blog
---

My goal in this article is to describe the prototypical network paradigm in few-shot machine learning. My intended audience is people who have at least some experience in machine learning -- but nothing beyond that. I will try not to get too into mathematical notation, instead I will try to motivate the paradigm and describe why it works with a few simple illustrations. This blog post is an attempt to condense and illustrate the proposed few-shot machine learning framework in the influential NeurIPS 2017 paper ["Prototypical Networks for Few-shot Learning"](https://proceedings.neurips.cc/paper_files/paper/2017/file/cb8da6767461f2812ae4290eac7cbc42-Paper.pdf) by [Jake Snell](https://www.jakesnell.com/), [Kevin Swersky](https://research.google/people/105739/), and [Richard Zemel](http://www.cs.columbia.edu/~zemel/).

# Example Task: Document Labeling

Before we begin, let’s set the stage with an example task: document labeling. In this task, a *text document* is given as input, and a *label* for the document is received as output. Examples of this task in the wild include... 

* News article category classification, in which a news article (*text document*) is assigned a genre (*label*) (e.g. sports, business, politics, entertainment, tech) based on its content.
* Social media hate speech detection, in which a post (*text document*) is labeled as either containing hate speech or not (*label*). This is a growing task in research, see [here](https://aclanthology.org/S19-2007/) and [here](https://arxiv.org/pdf/1903.08983.pdf).
* Telemedical query triage, in which a patient's message to their doctor (*text document*) is determined to be urgent (requiring a doctor's immediate response) or not (*label*). This is a task I've investigated, which you can read about [here](https://medinform.jmir.org/2022/9/e37770).

In this post we'll refer to a specific document labeling task to illustrate prototypical learning: the task of labeling whether a patient medical record (*document*) contains a mention of a specific symptom (*label*). For simplicity's sake we'll assume that each record contains either only one symptom or no symptoms, meaning that if there are L known symptoms, there number of possible labels is L + 1. This task, which we'll call **Symptom Labeling**, is a simplified form of a common medical natural language processing (NLP) subtask which enables all sorts of downstream applications in caregiving and hopsital administration. In our example, we'll assume we've built a model to label symptoms for common respiratory illnesses. **ADD SENTENCE HERE ABOUT HOW OUR MODEL HAS ONLY EVER SEEN COMMON SYMPTOMS LIKE SHORTNESS OF BREATH, COUGHING, ETC. SAY WE NEEDED LIKE 200 OF EACH DOCUMENT TO TRAIN OUR MODEL.** 

[INSERT SYMPTOM LABELING ILLUSTRATION HERE - FIGURE 1]

# Traditional Machine Learning Approach

In a traditional machine learning framework, the training paradigm looks like this.

[INSERT FIGURE 2]

In other words, the goal of the traditional machine learning framework would be to take a medical record as input and give one of the L + 1 labels as output. The model is incrementally trained to do this by feeding it a lot of labeled example records. After processing each record into a machine-learning-ready format (i.e. after *"embedding"* the record), the model gives a probability for each label in the label space. The probabilities are compared to the ground truth label in a loss function, and the results of the loss function are passed back through the model so the internal model weights can be adjusted (i.e. via *"backpropogation"*). After repeating this process enough times, the model can then (hopefully accurately) assign symptom presence labels to unlabeled medical records.

# The Problem(s): New Labels Break the Paradigm

Traditional machine learning frameworks like this suffer from one gigantic problem: they require a *ton* of data. The amount of data required to train your model scales (roughly) with how big your model needs to be, which in turn depends on the complexity of the task, the size of each input, and **the number of possible labels**. The number of possible labels is important here: if you have two types of documents, you need to show the model enough of each type for it to be able to learn *something* about that document class. If you have 30 types of documents, you need at least 15x that amount. What happens when you have 1,000 types of documents? Or in an even more general sense, what happens when you *don’t know how many types of documents you might have?*

### The traditional machine learning paradigm is data-hungry, and falls apart when new labels need to be introduced to the task.

Let’s come back to our symptom labeling example. Say you have a patient with a symptom you've never seen before, maybe they **INSERT SYMPTOM NEW TO THE IDEA**. In a traditional machine learning framework you would need to gather enough samples of this new document type, label each of them, add the samples to your training data, and retrain your model. But what about all the samples you’ve already used to train your model? Shouldn’t the **task** of document labeling transfer to these new labels, too? If your document labeling model were a human being who had learned how to label other documents, you would be able to simply describe the new document class, give a few examples, and then the human would be able to do it. In a tradition machine learning framework, the transfer of this knowledge isn’t so simple.

# The Solution: Few-Shot Learning

Enter protoype learning and prototypical networks. Introduced in NeurIPS conference in 2017, [prototypical networks](https://proceedings.neurips.cc/paper_files/paper/2017/file/cb8da6767461f2812ae4290eac7cbc42-Paper.pdf) gives a new input-output paradigm for machine learning. The goal of this model training framework is simple: the model should be able to label a new sample given only a handful of examples.

