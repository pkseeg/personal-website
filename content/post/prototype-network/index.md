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
* Social media hate speech detection, in which a post (*text document*) is labeled as either containing hate speech or not (*label*). This is a growing task in research, see [here]() and [here]().
* Telemedical query triage, in which a patient's message to their doctor (*text document*) is determined to be urgent (requiring a doctor's immediate response) or not (*label*). [[Insert a link to my own work here]](https://medinform.jmir.org/2022/9/e37770).

In this post we'll refer a specific document labeling task to illustrate prototypical learning: the task of labeling whether a patient medical record (*document*) contains a mention of a specific symptom (*label*). This task, which we'll call **Symptom Labeling**, is a simplified form of a common medical natural language processing (NLP) subtask which enables all sorts of downstream applications in caregiving and hopsital administration.

[INSERT SYMPTOM LABELING ILLUSTRATION HERE]

Inputs and outputs, baby, that’s what computers are all about.

# Traditional Machine Learning Approach

In a traditional machine learning framework, you would have two sets of documents. One would be your “training” dataset, and one would be your “test” dataset. A single instance in your “training” dataset would be a document with a label, and the task of labeling that document would take as input the document and give as output a label. [yada yada] Machine learning has given us amazing things! [Maybe talk about my google photos and how it can recognize plants on the fly so I’ve learned a bunch about different types of flowers in New England.]

# The Problem: 

Traditional machine learning frameworks suffer from one gigantic (literally) problem: they require a **ton** of data. The amount of data required to train your model scales (roughly) with how big your model needs to be, the complexity of the task, the size of each input, and *the number of possible labels*. The number of possible labels is important here: if you have two types of documents, you need to show the model enough of each type for it to be able to learn **something** about that document class. If you have 30 types of documents, you need at least 15x that amount. What happens when you have 1,000 types of documents? Or in an even more general sense, what happens when you *don’t know how many types of documents you might have?*

Let’s come back to our document labeling example. Let’s say you have a new stream of documents [maybe a new meme is circulating or something] and you want to add this class to your document “label space,” i.e. the set of document types your model can label. In a traditional machine learning framework you would need to gather enough samples of this new document type, label each of them, add the samples to your training data, and retrain your model. But what about all the samples you’ve already used to train your model? Shouldn’t the **task** of document labeling transfer to these new labels, too? If your document labeling model were a human being who had learned how to label other documents, you would be able to simply describe the new document class, give a few examples, and then the human would be able to do it. In a tradition machine learning framework, the transfer of this knowledge isn’t so simple.

# The Solution: Prototypical Networks

Enter protoype learning and prototypical networks. Introduced in NeurIPS conference in 2017, [prototypical networks](https://proceedings.neurips.cc/paper_files/paper/2017/file/cb8da6767461f2812ae4290eac7cbc42-Paper.pdf) gives a new input-output paradigm for machine learning. The goal of this model training framework is simple: the model should be able to label a new sample given only a handful of examples.

