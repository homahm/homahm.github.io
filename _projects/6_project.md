---
layout: page
title: Statistical Inference on Networks
description: Developing robust measurement frameworks for online discourse
img: assets/img/networks.png
importance: 2
category: computational-methods
related_publications: ghasemian2020stacking, ghasemian2019evaluating
publications_list:
  - title: "Stacking models for nearly optimal link prediction in complex networks"
    authors: "Ghasemian, A., Hosseinmardi, H., Galstyan, A., Airoldi, E. M., & Clauset, A."
    year: 2020
    venue: "Proceedings of the National Academy of Sciences, 117(38)"
  - title: "Evaluating overfit and underfit in models of network community structure"
    authors: "Ghasemian, A., Hosseinmardi, H., & Clauset, A."
    year: 2019
    venue: "IEEE Transactions on Knowledge and Data Engineering, 32(9)"
---

This project develops rigorous statistical frameworks for analyzing network structures and relationships in online social systems. We advance fundamental methods for link prediction, community detection, and structural inference while addressing key challenges of model selection, overfitting, and generalization in network analysis.

<div class="caption">
    Our work establishes principled approaches to network inference that achieve near-optimal prediction while avoiding common pitfalls of overfitting and model mis-specification.
</div>

Key methodological contributions include:

- **Ensemble link prediction** combining multiple network models through stacking to achieve near-optimal performance
- **Model selection frameworks** for community detection that properly balance fit and complexity
- **Overfitting and underfitting detection** methods that identify when network models fail to generalize
- **Cross-validation techniques** adapted for network data with dependencies between observations
- **Benchmark evaluation protocols** establishing rigorous standards for comparing network inference methods

Our statistical methods have broad applications across computational social science, enabling more reliable inference about relationship formation, group structure, and information diffusion in complex online networks. This work provides the methodological foundation for empirical studies of platform dynamics and social behavior.

## Featured Research

**[Stacking models for nearly optimal link prediction in complex networks](https://www.pnas.org/doi/10.1073/pnas.2006806117)**
*Ghasemian, A., Hosseinmardi, H., Galstyan, A., Airoldi, E. M., & Clauset, A. (2020). Proceedings of the National Academy of Sciences, 117(38).*

Link prediction is a fundamental problem in network analysis with applications ranging from recommender systems to identifying missing interactions in biological networks. This work develops a stacking ensemble approach that systematically combines diverse network models—including graph embeddings, similarity indices, and probabilistic models—to achieve near-optimal link prediction performance across a wide range of network types. Our framework demonstrates that no single method dominates across all networks, but principled ensemble methods can consistently approach optimal performance.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/schematics_v3.pdf" title="Network inference framework" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Statistical inference framework for analyzing network structures in online social systems.
</div>




