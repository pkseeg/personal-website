---
title: "The Scope of In-Context Learning for the Extraction of Medical Temporal Constraints"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- Parker Seegmiller
- Joseph Gatto 
- Madhusudan Basak
- Diane Cook
- Hassan Ghasemzadeh
- John Stankovic
- Sarah Masud Preum


# Author notes (optional)
#author_notes:
#- "Equal contribution"
#- "Equal contribution"

date: "2023-06-27T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2022-01-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: 2023 IEEE International Conference on Healthcare Informatics
publication_short: IEEE ICHI 2023

#abstract: Medications often impose temporal constraints on everyday patient activity. Violations of such medical temporal constraints (MTCs) lead to a lack of treatment adherence, in addition to poor health outcomes and increased healthcare expenses. These MTCs are found in drug usage guidelines (DUGs) in both patient education materials and clinical texts. Computationally representing MTCs in DUGs will advance patient-centric healthcare applications by helping to define safe patient activity patterns. We define a novel taxonomy of MTCs found in DUGs and develop a novel context-free grammar (CFG) to computationally represent MTCs from unstructured DUGs. Additionally, we release three new datasets with a combined total of N=836 DUGs labeled with normalized MTCs. We develop an in-context learning (ICL) solution for automatically extracting and normalizing MTCs found in DUGs, achieving an average F1 score of 0.62 across all datasets. Finally, we rigorously investigate ICL model performance against a baseline model, across datasets and MTC types, and through in-depth error analysis.

# Summary. An optional shortened abstract.
#summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://arxiv.org/pdf/2303.09366.pdf'
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ''
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---

# Medical Temporal Constraints

*Large Language Models can Extraction Medical Temporal Constraints from Drug Usage Guidelines*

# What Are Medical Temporal Constraints?

Medications usually come with specific instructions about when and how to take them. These instructions, which we call medical temporal constraints (MTCs), are very important for the treatment to work effectively and to ensure patient safety. If patients don't follow these guidelines, it can lead to health problems and higher healthcare costs. These MTCs are usually found in drug usage guidelines (DUGs), which are included in materials given to patients by doctors, and in other patient-centric education materials like those found on sites like WebMD. In this work, we created a structure to represent these MTCs as they appear in free-formatted patient health texts, and we explore the automatic extraction of these structured outputs using large language models (LLMs). This work can help outline safe patterns of activity for patients and improve healthcare applications that are focused on patient needs. 

{{< figure src="mtc_table1.png" title="Example of Medical Temporal Constraints" >}}

# What is In-Context Learning?

In-context learning (ICL) is a recent approach in language modeling where a LLM is given a task to perform after being provided with a prompt and several examples. In-context learning is different from traditional machine learning because the weights of the LLM are frozen (i.e. no backpropogation occurs); all of the task-specific knowledge is "learned" in context through the prompt and given examples. ICL is like teaching a model to perform a task by showing it only a few examples, and since the model has been trained to do a bunch of other language tasks it can reliably perform your specialized task as well. There has been a bunch of interesting investigation into why ICL works. However, in this work we focus only on how well ICL works for our patient-centric task. In related work, ICL has been found to be effective in extracting structured information from text, including scientific and medical structured information.

We used ICL with the GPT-3 model from OpenAI to extract MTCs from unstructured DUGs. We chose GPT-3 because it has been shown to be effective in extracting this type of information using ICL strategies, especially when the dataset is relatively small and training a new model is infeasible.

We designed three types of prompts to guide the model in extracting MTCs from unstructured text data. The first is a simple prompt that serves as a baseline for ICL. The second is a guided prompt, which is longer and includes elements of the labeling guide given to human annotators. The third is a specialized prompt, which is customized for each type of MTC and includes a basic description and a heuristic for formatting the MTC correctly.

{{< figure src="featured.png" title="Overview of MTC Extraction Pipeline" >}}

# What Did We Learn?

The specialized ICL prompt achieved an average F1 score of 0.62 across all datasets, demonstrating its relative effectiveness in extracting and normalizing MTCs from DUGs. We found 2 main sources of error in the GPT-3 output, hallucination and nonvalidity, which we describe below. 

Hallucinations are the most common error type, accounting for 43% of all labeled errors. Hallucination occurs when the model outputs an MTC or a list of MTCs that are valid but not found in the text sample (i.e. the model "hallucinates" information that was never seen in the sample context). This error type is particularly common in consistency and time-of-day MTCs. 

Nonvalidity is another common error, accounting for 15% of the errors. This happens when the model output cannot be parsed according to the context-free grammar (CFG) after minimal post-processing. 

{{< figure src="mtc_table7.png" title="Distribution of In-Context Learning Errors" >}}

These errors affect the model's performance in extracting MTCs, with hallucinations being a primary reason for poor performance. Reducing these errors is an active area of research that could lead to better results in MTC extraction tasks.

# What's Next?

Our research has shown that it is possible to computationally represent MTCs in DUGs using a CFG-based model and an ICL solution. This approach can help improve patient adherence to medication guidelines and ultimately lead to better health outcomes. However, there is still room for improvement, particularly in the extraction and normalization of certain types of MTCs. Future research could focus on refining the ICL model and exploring other methods for MTC extraction.