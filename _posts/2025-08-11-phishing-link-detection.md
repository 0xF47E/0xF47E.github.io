---
layout: post
title: How I Detect Phishing Links with ML
author: me
---

While studying for my bachelor degree, my interest in Machine Learning grew. When it was time to start the bachelor thesis, I had a hard time finding the right topic for me. I really wanted to try something practical. Fortunately I found some interesting research about the detection of phishing, which is an important task nowadays, regarding the high incident numbers.

I trained different ML models on a balanced dataset to see which would have the best performance. I also tried to implement my own feature extraction and tried different combinations with hashed feature extractions. 

In the end I had some valuable data and models with good performance in identifying phishing links.

![ROC-AUC for the different models](/images/phishing-link-detection/ROC-AUC.png)

In the future I would love to further research this topic and try to make more efficient, more light-weight, and more performant models in order to have an open-source solution for everyone.

Link to project: [phishing-link-detection](https://github.com/0xF47E/phishing-link-detection)

