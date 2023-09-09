---
title: Vanilla LLMs Are Not Fit for Medical Diagnosis
subtitle:

# Summary for listings and search engines
summary: Large Language Models (LLMs) are unfit for the complex task of medical diagnosis.

# Link this post with a project
projects: []

# Date published
date: "2023-09-05T00:00:00Z"

# Date updated
lastmod: "2023-09-05T00:00:00Z"

# Is this an unpublished draft?
draft: false

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
- llms
- opinion

categories:
- blog
---

With language-based AI on the rise, many are projecting futures in which all sorts of fields are taken over by autonomous agents. Given the complexity and cost of healthcare in the U.S. specifically, it’s easy to hope for a future in which healthcare services are made more accessible and less expensive via an AI taskforce. While I agree with the sentiment that many healthcare tasks can be enhanced by modern language processing techniques (I’m betting my PhD on it), I worry that the magic of ChatGPT may have people convinced that “being a doctor” is a solvable task for existing generative language modeling tools. My worry is not unfounded, either; in April, the “infamous” Martin Shkreli released the world’s first AI doctor (or “virtual healthcare assistant,” for lack of a less legally-binding term). You can read all about that mess [here](https://www.thedailybeast.com/martin-shkrelis-dr-gupta-ai-chatbot-is-a-medical-and-legal-nightmare).

In this post I’m going to argue that medical diagnosis is *not* a task which should be entrusted to current language models, despite the simplicity of treating it as a language-to-language task. As someone who has worked in healthcare and studies/writes about language modeling, I’m hoping I have something to add.

(I should mention that my intended audience of this post includes medical professionals, NLP researchers, people in-between and anyone who is interested in the future of AI generally. I don’t assume you have too much of a technical background - hopefully if you have one you’ll forgive me, and find my overview insightful anyway.)

# Part 1: How We Got Here

Generative language modeling is a sequence-to-sequence task in which human language (e.g. a ”prompt”) is taken as input and human language (e.g. a “response”) is given as output. Programs that perform this task are called generative language models (LMs). Existing LMs range in complexity from very simple to very complex.

{{< figure src="model_comparison.png" title="Language models can be simple or complex!" >}}

In the last year, generative language modeling has received wide-spread attention in both [scientific literature](https://arxiv.org/pdf/2303.18223.pdf) and [popular media](https://www.newyorker.com/podcast/political-scene/the-creator-of-chatgpt-on-the-rise-of-artificial-intelligence), largely due to the release of ChatGPT, a chat-oriented anthropomorphic language model which has acheived some pretty stunning results. This model (and others like it) are trained on copious amounts of human-written language, taken from the internet, which is one of the many reasons they can provide human-like responses to various prompts.

The beauty of ChatGPT from a technical perspective is that many difficult tasks can be made easy by expressing them in “plain English.” There have been and will be many tasks in which large language models (LLMs) like ChatGPT acheive state-of-the-art performance, because there are a lot of reasoning tasks which can be easily formalized with human language inputs and human language outputs. These include some medical tasks, including responding to health questions on [social media](https://each.international/wp-content/uploads/2023/05/jamainternal_ayers_2023_oi_230030_1681999216.70842.pdf) and even obtaining a passing grade on a practice versions of the [United States Medical Licensing Examination](https://arxiv.org/pdf/2303.13375.pdf).



{{< youtube HluANRwPyNo >}}


