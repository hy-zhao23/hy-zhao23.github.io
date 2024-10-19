---
layout: project
title: Beyond Single Concept Vector
subtitle: Modeling Concept Subspace in LLMs with Gaussian Distribution
authors:
  - name: Haiyan Zhao
  - name: Heng Zhao
  - name: Bo Shen
  - name: Ali Payani
  - name: Fan Yang
  - name: Mengnan Du
description: A description of my project
image_base_url: /assets/projects/img/gcs/
links:
  - title: arXiv
    url: https://arxiv.org/abs/2410.00153
  # - title: Slides
  #   url: https://arxiv.org/abs/2402.09647
  # - title: Code
  #   url: https://github.com/
  - title: Citation
    url: "#citation"
citation_key: gcs
---


## Abstract
Probing learned concepts in large language models (LLMs) is crucial for understanding how semantic knowledge is encoded internally. Training linear classifiers on probing tasks is a principle approach to denote the vector of a certain concept in the representation space. However, the single vector identified for a concept varies with both data and training, making it less robust and weakening its effectiveness in real-world applications. To address this challenge, we propose an approach to approximate the subspace representing a specific concept. Built on linear probing classifiers, we extend the concept vectors into Gaussian Concept Subspace (GCS). We demonstrate GCS's effectiveness through measuring its faithfulness and plausibility across multiple LLMs with different sizes and architectures. Additionally, we use representation intervention tasks to showcase its efficacy in real-world applications such as emotion steering. Experimental results indicate that GCS concept vectors have the potential to balance steering performance and maintaining the fluency in natural language generation tasks.

## GCS Framework

{% assign carousel_images = "" | split: "" %}
{% assign image1 = page.image_base_url | append: "framework/1.png" | split: "|" %}
{% assign carousel_images = carousel_images | concat: image1 %}
{% assign image2 = page.image_base_url | append: "framework/2.png" | split: "|" %}
{% assign carousel_images = carousel_images | concat: image2 %}
{% assign image3 = page.image_base_url | append: "framework/3.png" | split: "|" %}
{% assign carousel_images = carousel_images | concat: image3 %}

{% include image_carousel.html images=carousel_images %}

## Evaluation
### <strong>RQ1</strong>: How faithfully do GCS-sampled concept vectors represent the original concepts?(Faithfulness)
- Experiment 1

<div style="display: flex; justify-content: center;">
  <table style="width: 90%;">
    <tr>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/l7-hist-Bird-30.png' | relative_url }}" alt="Llama-2-7B, layer 30" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/g7-hist-Bird-26.png' | relative_url }}" alt="Gemma-7B, layer 26" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/l13-hist-Bird-38.png' | relative_url }}" alt="Llama-2-13B, layer 38" style="width: 100%; max-width: 300px;"></td>
    </tr>
    <tr>
      <th style="text-align: center;">Llama-2-7B, layer 30</th>
      <th style="text-align: center;">Gemma-2-7B, layer 26</th>
      <th style="text-align: center;">Llama-2-13B, layer 38</th>
    </tr>
  </table>
</div>
<p style="text-align: center;"><em>Figure: Histogram of cosine similarity within observed concept vectors, sampled concept vectors,
and between both sets for concept "Bird".</em></p>

<div style="display: flex; justify-content: center;">
  <table style="width: 90%;">
    <tr>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/l7-Averaged-similarities-Bird-o-s-1000.png' | relative_url }}" alt="Llama-2-7B, layer 30" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/g7-Averaged-similarities-Bird-o-s-1000.png' | relative_url }}" alt="Gemma-7B, layer 26" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/hist/l13-Averaged-similarities-Bird-o-s-1000.png' | relative_url }}" alt="Llama-2-13B, layer 38" style="width: 100%; max-width: 300px;"></td>
    </tr>
    <tr>
      <th style="text-align: center;">Llama-2-7B</th>
      <th style="text-align: center;">Gemma-2-7B</th>
      <th style="text-align: center;">Llama-2-13B</th>
    </tr>
  </table>
</div>
<p style="text-align: center;"><em>Figure: Layer-wise average cosine similarity from the second layer to the penultimate layer of observed concept vectors, sampled concept vectors, and between both sets for concept "Bird".</em></p>

- Experiment 2
<div style="display: flex; justify-content: center;">
  <table style="width: 90%;">
    <tr>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/acc/l7-Averaged-accuracy-Bird-o-s-1000.png' | relative_url }}" alt="Llama-2-7B, layer 30" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/acc/g7-Averaged-accuracy-Bird-o-s-1000.png' | relative_url }}" alt="Gemma-7B, layer 26" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/acc/l13-Averaged-accuracy-Bird-o-s-1000.png' | relative_url }}" alt="Llama-2-13B, layer 38" style="width: 100%; max-width: 300px;"></td>
    </tr>
    <tr>
      <th style="text-align: center;">Llama-2-7B</th>
      <th style="text-align: center;">Gemma-2-7B</th>
      <th style="text-align: center;">Llama-2-13B</th>
    </tr>
  </table>
</div>
<p style="text-align: center;"><em>Figure: Accuracy of observed and sampled concept vectors aross varying models.</em></p>

- Conclusion
  - Observed concept vectors are similar to sampled concept vectors in representation space.
  - GCS-sampled concept vectors are more general and robust on classifying concept-related data.

### <strong>RQ2</strong>: To what extent do explanations derived from GCS-sampled concept vectors align with human expectations about the hierarchies among model's learned knowledge?(Plausibility)
- Experiment 1
<div style="display: flex; justify-content: center;">
  <table style="width: 90%;">
    <tr>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/heatmap/l7-sim-mat-s-30.png' | relative_url }}" alt="Llama-2-7B, layer 30" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/heatmap/g7-sim-mat-s-26.png' | relative_url }}" alt="Gemma-7B, layer 26" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/heatmap/l13-sim-mat-s-38.png' | relative_url }}" alt="Llama-2-13B, layer 38" style="width: 100%; max-width: 300px;"></td>
    </tr>
    <tr>
      <th style="text-align: center;">Llama-2-7B</th>
      <th style="text-align: center;">Gemma-2-7B</th>
      <th style="text-align: center;">Llama-2-13B</th>
    </tr>
  </table>
</div>
<p style="text-align: center;"><em>Figure: Heatmap of concept average cosine similarity of 16 concepts across Llama-2-7B, Gemma-7B, and Llama-2-13B. The 16 low-level concepts are grouped into four high-level categories: the first 4 rows/columns represent sports events, the next 4 represent populated places, followed by 4 for animals, and the last 4 for movie genres.</em></p>

- Experiment 2
<div style="display: flex; justify-content: center;">
  <table style="width: 90%;">
    <tr>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/pca/l7-pca_sampled_layer_30.png' | relative_url }}" alt="Llama-2-7B, layer 30" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/pca/g7-pca_sampled_layer_27.png' | relative_url }}" alt="Gemma-7B, layer 26" style="width: 100%; max-width: 300px;"></td>
      <td style="text-align: center;"><img src="{{ '/assets/projects/img/gcs/fig/pca/l13-pca_sampled_layer_38.png' | relative_url }}" alt="Llama-2-13B, layer 38" style="width: 100%; max-width: 300px;"></td>
    </tr>
    <tr>
      <th style="text-align: center;">Llama-2-7B</th>
      <th style="text-align: center;">Gemma-2-7B</th>
      <th style="text-align: center;">Llama-2-13B</th>
    </tr>
  </table>
</div>
<p style="text-align: center;"><em>Figure: PCA visualization of 16 concepts across Llama-2-7B, Gemma-7B, and Llama-2-13B.
Low-level concepts belonging to the same high-level concept category share the same color.</em></p>

- Conclusion
  - Low-level concepts within the same high-level category typically exhibit higher similarity scores.
  - Some high-level categories, such as "Sports Event", shows very high internal similarity across all models, suggesting these concepts are closely related in the models' representations.
  - Some high-level categories, such as "Populated Place" and "Animal", show stronger correlation, align with human intuition about real-world relationships between these concepts.

### <strong>RQ3</strong>: Can the proposed GCS method effectively mitigate unwanted behaviors in LLMs?(Effectiveness on emotion steering)
<div style="display: flex; justify-content: center;">
  <img src="{{ '/assets/projects/img/gcs/fig/intervention.png' | relative_url }}" style="width: 90%; max-width: 800px;">
</div>
<p style="text-align: center;"><em>Figure: An illustration of inference-time intervention with a LLM.</em></p>

<div style="display: flex; justify-content: center;">
  <img src="{{ '/assets/projects/img/gcs/fig/intervention_exp.png' | relative_url }}" style="width: 90%; max-width: 800px;">
</div>
<p style="text-align: center;"><em>Figure: Comparison of generated texts with and without intervention.</em></p>

<div style="display: flex; justify-content: center;">
<table border="1" style="width: 90%; border-collapse: collapse; margin-bottom: 20px; text-align: center;">
  <caption><strong>Table 1: Evaluation of generated text after adding steering vectors.</strong></caption>
  <thead>
    <tr>
      <th rowspan="2" style="text-align: center; vertical-align: middle;">Steering Method</th>
      <th colspan="10" style="text-align: center;">Strength</th>
    </tr>
    <tr>
      <th style="text-align: center;"></th>
      <th style="text-align: center;">0.038</th>
      <th style="text-align: center;">0.043</th>
      <th style="text-align: center;">0.048</th>
      <th style="text-align: center;">0.053</th>
      <th style="text-align: center;">0.059</th>
      <th style="text-align: center;">0.064</th>
      <th style="text-align: center;">0.069</th>
      <th style="text-align: center;">0.074</th>
      <th style="text-align: center;">0.080</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Mean Difference</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>1.020</td><td>0.860</td><td>1.220</td><td>1.100</td><td>1.653</td><td>1.245</td><td><strong>1.800</strong></td><td>1.780</td><td>1.260</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>3.857</td><td>5.460</td><td>5.740</td><td>5.420</td><td>5.571</td><td>6.306</td><td><strong>5.440</strong></td><td>4.420</td><td>3.420</td>
    </tr>
    <tr>
      <td rowspan="2">1 sigma</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>1.000</td><td>0.800</td><td>1.260</td><td>1.490</td><td>2.120</td><td><strong>2.980</strong></td><td>2.280</td><td>1.776</td><td>2.160</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>4.780</td><td>3.680</td><td>4.040</td><td>3.531</td><td>4.860</td><td><strong>4.857</strong></td><td>6.480</td><td>5.347</td><td>5.800</td>
    </tr>
    <tr>
      <td rowspan="2">2 sigma</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>0.840</td><td>1.520</td><td>1.143</td><td>1.878</td><td><strong>2.625</strong></td><td>2.458</td><td>2.520</td><td>2.340</td><td>1.960</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>4.420</td><td>3.680</td><td>3.857</td><td>4.061</td><td><strong>5.854</strong></td><td>6.688</td><td>6.460</td><td>6.360</td><td>6.520</td>
    </tr>
    <tr>
      <td rowspan="2">3 sigma</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>0.820</td><td>1.220</td><td>1.220</td><td>1.837</td><td>2.460</td><td><strong>2.571</strong></td><td>2.388</td><td>2.510</td><td>1.854</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>3.920</td><td>4.180</td><td>3.580</td><td>3.449</td><td>5.120</td><td><strong>5.633</strong></td><td>6.204</td><td>6.633</td><td>5.542</td>
    </tr>
    <tr>
      <td rowspan="2">4 sigma</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>0.840</td><td>0.755</td><td>1.380</td><td>1.960</td><td><strong>2.280</strong></td><td>2.224</td><td>2.612</td><td>2.720</td><td>1.520</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>3.600</td><td>3.837</td><td>4.400</td><td>3.560</td><td><strong>4.720</strong></td><td>5.878</td><td>6.653</td><td>6.800</td><td>4.200</td>
    </tr>
    <tr>
      <td rowspan="2">5 sigma</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>0.580</td><td>0.640</td><td>1.429</td><td>1.640</td><td><strong>2.458</strong></td><td>1.680</td><td>2.333</td><td>2.224</td><td>2.220</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>3.440</td><td>4.040</td><td>5.347</td><td>3.480</td><td><strong>4.771</strong></td><td>5.900</td><td>5.625</td><td>5.694</td><td>4.980</td>
    </tr>
    <tr>
      <td rowspan="2">One linear</td>
      <td>Joyfulness (Avg) ↑</td>
      <td>0.840</td><td>1.245</td><td>1.520</td><td>2.000</td><td>2.292</td><td>2.580</td><td><strong>3.020</strong></td><td>2.480</td><td>2.080</td>
    </tr>
    <tr>
      <td>Coherence (Avg) ↓</td>
      <td>4.360</td><td>3.347</td><td>4.380</td><td>4.640</td><td>5.208</td><td>6.020</td><td><strong>5.918</strong></td><td>6.780</td><td>6.340</td>
    </tr>
    <tr>
      <td colspan="11" style="border: none; text-align: left;">
        <p>Note: A higher joyfulness score indicates a better steering effect. Coherence measures the repetitiveness and chaos in the generated sentences, with lower values being preferable. The best performance for each method is highlighted in bold within the table.</p>
      </td>
    </tr>
  </tbody>
</table>
</div>


- Conclusion
  - GCS-sampled concept vectors can better balance steering performance and maintaining the fluency in natural language generation tasks.


{% include citation.html %}


