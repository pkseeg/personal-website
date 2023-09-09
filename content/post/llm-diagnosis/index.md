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

{{< youtube HluANRwPyNo >}}

{{< figure src="problem-description.png" title="Example problem description." >}}

