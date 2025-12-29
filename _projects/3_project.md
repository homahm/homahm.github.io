---
layout: page
title: Open-World Detection and Inference at Scale
description: Detection and prediction methods for large-scale real-world data under minimal supervision
img: assets/img/ML_models.png
importance: 3
category: computational-methods
---

This project develops machine learning methods for detecting and predicting diverse phenomena in large-scale real-world data under minimal supervision. We focus on open-world settings where training data is limited, noisy, and highly imbalanced—conditions typical of sociotechnical systems research.

<div class="caption">
    Our methods enable inference across diverse content types from multimodal data in complex online environments where traditional supervised learning approaches fail due to data scarcity and label noise.
</div>

Key methodological contributions include:

- **Weakly supervised learning** frameworks for content detection with limited labeled data
- **Multi-task learning** architectures that leverage shared representations across related detection tasks
- **Imbalanced learning techniques** for identifying rare but important content (e.g., hate speech, misinformation)
- **Open-world classification** methods that can detect novel content categories not seen during training
- **Multimodal fusion** approaches combining text, images, video, and network structure

These computational methods underpin our empirical studies of online platforms, enabling large-scale measurement and analysis of phenomena that would be impossible to manually annotate. Our frameworks are designed for robustness to the inherent noise and evolving nature of real-world social media data.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/schematics_v3.pdf" title="Detection framework schematic" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Architecture for open-world detection in complex sociotechnical systems.
</div>




