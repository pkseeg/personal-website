---
title: Wilcoxon Rank Sum Testing Explained
subtitle:

# Summary for listings and search engines
summary: A brief overview of the Wilcoxon Rank Sum test and why it's useful

# Link this post with a project
projects: []

# Date published
date: "2023-12-12T00:00:00Z"

# Date updated
lastmod: "2023-12-12T00:00:00Z"

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
- statistics

categories:
- blog
---

I recently returned from EMNLP 2023 in Singapore, where I presented my work on developing a [Statistical Depth for Ranking and Characterizing Transformer-based Text Embeddings](https://pkseeg.com/publication/depth/). Part of that work was adopting a statistical test for determining whether two sets of texts, embedded using a transformer-based embedding model like [S-BERT](https://www.sbert.net/), differ significantly in embedding space. This test is a multivariate extension of the Wilcoxon rank sum test, and it was first developed by Regina Y. Liu and Kesar Singh in the 1993 paper ["A Quality Index Based on Data Depth and Multivariate Rank Tests"](https://www.tandfonline.com/doi/abs/10.1080/01621459.1993.10594317?casa_token=1YOxo9do0F8AAAAA:tsOCxHuiS6xnyyrTQHICqvoAOPdUXof503HbqqigixNUk9R_oisPm1cESOvVnJxqAhpcjQn4BOP-c9k).

At EMNLP 2023, a handful of times I found myself explaining how this test works to other NLP researchers. I figured it might be useful to be able to point them to a short introduction, like this one, so they can get the general gist of the test without reading the whole paper. However, I still recommend reading the whole paper if you want all the context, including how the test works for transformer-based text embeddings specifically and demonstrations of its use in testing for distributional differences between human-written and synthetic texts. 

In this short blog post I will explain how the multivariate Wilcoxon rank sum test works. I'll introduce the idea of ranking objects with respect to how well they represent a set (i.e. statistical depth). Then I'll explain the intuition behind the Q parameter, which measures how outlying one set of objects is with respect to another. Then I'll briefly show how the Q parameter can be used for statistical significance testing. 

# Part 1: Ranking Objects by the Representative Property

Say you have a set of objects, let's call it F. 

(image goes here)

Let's say we have some single object, x, of the same shape as the objects in F. If the objects in F only vary across a single dimension, it's really easy to score x by how **representative** it is of F. You can simply get an idea of the center of F (mean, median, mode, etc.), then score x according to how close it is to the center of F. If x is close to the center of F, it will receive a high score, e.g. it is representative of F.

(image goes here)

This gets more complicated as you increase the dimensionality of x and the objects in F. (Think: How well does (a,b) represent the set {(a, c), (c, b), (d, f)}?) However, the idea of representation remains the same. We want to get some idea of the center of F, which we'll call the median of F, then we can score some object x with respect to how close it is to this median. 

If we have many such objects to compare, X = {x0, x1, ... }, we can assign each object a representation score with respect to F, and then rank them according to this **representation score**.

(image goes here).

# Part 2: The Q Parameter

Let's now assume we have two sets of objects, F and G, instead of just one. We are going to assign each object in each set (F and G) a representation score, indicating how representative of F that object is. We'll get into why we want to do this a bit later, but for now we can see that there are generally two kinds of outcomes for this scoring.

## Outcome A

(image of the A outcome, interleaved ranks)

If the representation scores of objects in F and G are similar, this means G is generally representative of F. This is the same as saying that F and G do not differ very much, because objects in G and objects in F are equally as likely to be representative of F.

## Outcome B

(image of the B outcome, outlying ranks)

On the other hand, if the representation scores of objects in G are lower than those of objects in F, this indicates that G is not very representative of F. This is the same as saying that G differs from F, because objects in G are not as likely to be representative of F.

The Q parameter introduced by [Liu and Singh (1993)]((https://www.tandfonline.com/doi/abs/10.1080/01621459.1993.10594317?casa_token=1YOxo9do0F8AAAAA:tsOCxHuiS6xnyyrTQHICqvoAOPdUXof503HbqqigixNUk9R_oisPm1cESOvVnJxqAhpcjQn4BOP-c9k)) formalizes outcomes A and B by considering the probability of the representation scoring. The **Q parameter** is, essentially, the probability that a randomly selected object in F will receive a lower representation score than a randomly selected object in G. If this probability is around 50%, it indicates that objects from F and G are equally likely to represent F (as in outcome A). If this probability is lower than 50%, it indicates that objects from F are  unlikely to receive lower representation scores than objects from G, meaning objects from G do not represent F well generally (as in outcome B).

Generally speaking, if Q is around 50% it means F and G are equally good representations of F, thus they likely follow the same distribution. If Q is less than 50%, it means G is not a good representation of F, thus it is unlikely that they follow the same distribution.

# Significance Testing

We can use this intuition, involving F and G and representation scores with respect to F, to develop a statistical significance test associated with the Q parameter. To do so we assume a null hypthoses that F and G are equally representative of F, thus Q = 50%. We test against the null hypothesis that G is not representative of F generally, thus Q < 50%. By sampling m objects from F n objects from G, we can 