---
title: "NeuSmoke: Efficient Smoke Reconstruction and View Synthesis with Neural Transportation Fields"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- Jiaxiong Qiu
- admin
- Zhong Li
- Han Yan
- Ming-Ming Cheng
- Bo Ren

# Author notes (optional)
# author_notes:
# - "Equal contribution"
# - "Equal contribution"

date: "2024-09-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2024-09-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *Siggraph Asia, 2024 (Conference Track)*
publication_short: ''

abstract: Novel view synthesis of smoke scenes presents a challenging problem. Previous neural approaches have suffered from inadequate quality and inefficient training. We introduce NeuSmoke, an efficient framework for dynamic smoke reconstruction using neural transportation fields, enabling high-quality density reconstruction and novel-view synthesis from multi-view videos. Our framework consists of two stages. In the first stage, we design a novel neural fluid field representation, integrating the transport equation with neural transportation fields. This includes adaptive embedding of multiple time stamps to enhance the spatial-temporal consistency of the reconstructed smoke. In the second stage, we combine novel-view color and depth information, employing convolutional neural networks (CNNs) to refine the smoke reconstruction. Our model achieves over 10 times faster than previous physics informed approaches. Extensive experiments demonstrate that our method surpasses existing techniques in novel view synthesis and volume density estimation in real-world and synthetic datasets.

# Summary. An optional shortened abstract.
summary: We introduce an efficient framework for dynamic smoke reconstruction using neural transportation fields.

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