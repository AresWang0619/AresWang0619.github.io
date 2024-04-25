---
title: 'Reasoning with Large Language Models on Graph Tasks: The Influence of Temperature'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - **Wang Yiming** 
  - Zhang Ziyang
  - Chen Hanwei
  - Shen Huayi

# Author notes (optional)
# author_notes:
#   - 'Equal contribution'
#   - 'Equal contribution'

date: '2024-04-09T00:00:00Z'
# doi: ''

# Schedule page publish date (NOT publication's date).
# publishDate: '2017-01-01T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
# publication_types: ['EI-conference']

# Publication name and optional abbreviated publication name.
# publication: In *Hugo Blox Builder Conference*
# publication_short: In *ICW*

abstract: Large language models (LLMs) have garnered significant attention due to their impressive performance across various fields. Consequently, numerous researchers are exploring the potential of applying these models to graph problems. However, the effect of the temperature coefficient on graph reasoning within large models remains underexplored. To this end, we investigate the effect of temperature by using NLGraph as a benchmark. We aim to explore the effect of varying the temperature parameter in the discrete range of 0 to 1 on the models’ inference performance. The experimental results show that the LLMs’ sensitivity to temperature varies across tasks at different difficulty levels. In most cases, the accuracy is higher at moderate temperatures and lower at extreme temperature settings, suggesting that proper temperature tuning can improve inference performance. In addition, the effect of temperature change on accuracy is more significant in the shortest path problem. As the temperature increases, the tendency of the model to explore different solutions increases and the creativity and disorder of the response increases, leading to a decrease in accuracy and causing an increase in the rate of change.

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

# tags: [LLMs]

# Display this page in the Featured widget?
# featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

# url_pdf: ''
# url_code: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_dataset: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_video: 'https://youtube.com'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects:
#   - example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

<!-- {{% callout note %}}
Click the _Cite_ button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the _Slides_ button to check out the example.
{{% /callout %}}

Add the publication's **full text** or **supplementary notes** here. You can use rich formatting such as including [code, math, and images](https://docs.hugoblox.com/content/writing-markdown-latex/). -->
