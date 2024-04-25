---
title: "Attack based on data: a novel perspective to attack sensitive points directly"
authors:
- Yuyao Ge
- Zhongguo Yang
- Lizhe Chen
- Yiming Wang
- Chengyang Li
# author_notes:
# - "Equal contribution"
# - "Equal contribution"
# date: "2023-05-01T00:00:00Z"
# doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2023-05-01T00:00:00Z"

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
# publication_types: ["article-journal"]

# Publication name and optional abbreviated publication name.
publication: "Cybersecurity "
# publication_short: ""

abstract: Adversarial attack for time-series classification model is widely explored and many attack methods are proposed. But there is not a method of attack based on the data itself. In this paper, we innovatively proposed a black-box sparse attack method based on data location. Our method directly attack the sensitive points in the time-series data according to statistical features extract from the dataset. At first, we have validated the transferability of sensitive points among DNNs with different structures. Secondly, we use the statistical features extract from the dataset and the sensitive rate of each point as the training set to train the predictive model. Then, predicting the sensitive rate of test set by predictive model. Finally, perturbing according to the sensitive rate. The attack is limited by constraining the L0 norm to achieve one-point attack. We conduct experiments on several datasets to validate the effectiveness of this method.

# # Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

# tags:
# - Source Themes
# featured: false

# links:
# - name: ""
# #   url: ""
url_pdf: uploads/attact_based_on_data.pdf
# url_code: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_dataset: ''
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: ''
# url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/jdD8gXaTZsc)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---
<!-- 
{{% callout note %}}
Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Add the publication's **full text** or **supplementary notes** here. You can use rich formatting such as including [code, math, and images](https://docs.hugoblox.com/content/writing-markdown-latex/). -->
