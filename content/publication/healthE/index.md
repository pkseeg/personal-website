---
title: "HealthE: Recognizing Health Advice & Entities in Online Health Communities"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- Parker Seegmiller
- Joseph Gatto 
- Garrett Johnston
- Madhusudan Basak
- Sarah Masud Preum


# Author notes (optional)
#author_notes:
#- "Equal contribution"
#- "Equal contribution"

date: "2023-06-06T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2022-01-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: 2023 Proceedings of the International AAAI Conference on Web and Social Media
publication_short: ICWSM

abstract: The task of extracting and classifying entities is at the coreof important Health-NLP systems such as misinformation de-tection, medical dialogue modeling, and patient-centric infor-mation tools. Granular knowledge of textual entities allowsthese systems to utilize knowledge bases, retrieve relevant in-formation, and build graphical representations of texts. Un-fortunately, most existing works on health entity recognitionare trained onclinical notes, which are both lexically and se-mantically different from public health information found inonline health resources or social media. In other words, ex-isting health entity recognizers vastly under-represent the en-tities relevant topublic health data, such as those providedby  sites  like  WebMD.  It  is  crucial  that  future  Health-NLPsystems  be  able  to  model  such  information,  as  people  relyon online health advice for personal health management andclinically relevant decision making.In this work, we release a new annotated dataset,HealthE,which  facilitates  the  large-scale  analysis  of  online  textualhealth advice. HealthE consists of 3,400 health advice state-ments with token-level entity annotations. Additionally, werelease 2,256 health statements which arenothealth adviceto facilitate health advice mining. HealthE is the first datasetwith  anentity-recognition  label  space  designed  for  themodeling of online health advice. We motivate the need forHealthE by demonstrating the limitations of five widely-usedhealth entity recognizers on HealthE, such as those offered byGoogle and Amazon. We additionally benchmark three pre-trained language models on our dataset as reference for futureresearch. All data is made publicly available.

# Summary. An optional shortened abstract.
#summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: ''
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
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
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

Find the paper [here](https://ojs.aaai.org/index.php/ICWSM/article/view/22210/21989).
