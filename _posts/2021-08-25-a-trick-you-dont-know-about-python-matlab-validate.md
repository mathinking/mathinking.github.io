---
layout: single
title: "Part 4. Want to validate conclusions in Python by running equivalent MATLAB code"
excerpt: "From the series: <br>*A trick you don't know about Python: MATLAB*"
date:  2021-08-25 12:35:00 +0100
categories: [blog, en]
tags: [python, matlab, a trick you dont know about python - matlab]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header: 
  teaser: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-validate.jpg
  overlay_color: "#000"
  overlay_filter: "0.3"
  overlay_image: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-validate.jpg
---

This post is the fourth post on the series [A trick you don't know about Python: MATLAB](../../../blog/en/a-trick-you-dont-know-about-python-matlab).

For this example, I will be presenting an exciting benchmark initiated by my colleague [Mike Croucher](https://www.linkedin.com/in/mike-croucher-32336113/), a member of MathWorks' Customer Success Engineering team in the UK. He works with academics around the country on different aspects of their teaching and computational research. If you haven't already, you must visit his [blog](https://walkingrandomly.com/) - as soon as you finish reading this entry. ;)

When discussing with Mike why a Python user would use MATLAB, one frequent reason is validating your conclusions and results. Mike pointed me to this benchmark he had done in the past on using K-means and a talk he had given on [Reproducible ML](https://mikecroucher.github.io/reproducible_ML/). In this talk, given some data, he assigns you the following task:

> Use K-means in Python with 50 clusters and K-means++ initialization

Relatively simple, it shouldn't matter what implementation I use, right? I can give you back 50 centroids, and you are good to go. 

No. Absolutely not. 

In the code below, you will see a comparison between three K-means implementations, all using K-means++ initialization. Credit to Mike for this. I am just building on top of [his example](https://github.com/mikecroucher/reproducible_ML/blob/master/k_means_implementation.ipynb). 

We start by generating and visualizing random blobs of data:

```python
from sklearn.datasets import make_blobs
import numpy as np
import plotly.graph_objects as go
from plotly.subplots import make_subplots

nclust = 50
np.set_seed = 2
cmeans = np.random.rand(nclust,2)*100 - 50 # Initial starting guesses for the centres
num_samples = 10000
(points,ground_truth) = make_blobs(n_samples=num_samples, n_features=2, centers=nclust, 
    cluster_std=1.0, center_box=(-50.0, 50.0), shuffle=True, random_state=0)

datablobs = go.Scatter(x=points[:,0], y=points[:,1], mode="markers", 
    marker=dict(color='Black', size=3))
fig = go.Figure(data=datablobs, layout_title_text="Our dataset")
fig.update_xaxes(title_text="x")
fig.update_yaxes(title_text="y")
fig.update_layout(autosize=False, width=400, height=400, showlegend=False)
fig.show()
```

<div>
  <div style="position:relative;padding-top:55%;">
    <iframe src="/assets/images/2021/a-trick-you-dont-know-about-python-matlab/generate-data.html" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen
      style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
  </div>
</div>

What follows is a demonstration that **different implementations** of the **same algorithm** can lead to **different results**:

```python
# Starting MATLAB Engine and data preparation
import matlab.engine 
eng = matlab.engine.start_matlab()
points_ml = matlab.double(points.tolist())

# Using Scipy
import scipy.cluster
scipy_res = scipy.cluster.vq.kmeans2(points, k=nclust, minit='++')

# Using Scikit-learn
from sklearn.cluster import KMeans as scikit_kmeans
kmeans_scikit_result = scikit_kmeans(n_clusters=nclust,init='k-means++').fit(points)

# Using MATLAB - kmeans function uses kmeans++ initialization by default
result = eng.kmeans(points_ml, nclust, nargout=2) 
kmeans_matlab_centers = np.array(result[1])
```

Let's now visualize the results:

```python
# Comparing results
centroid_size=8
fig = make_subplots(rows=1, cols=3, subplot_titles=("Scikit learn", "Scipy", "MATLAB"))
scilearn = go.Scatter(x=kmeans_scikit_result.cluster_centers_[:,0], 
    y=kmeans_scikit_result.cluster_centers_[:,1], mode="markers", 
    marker=dict(color='Red', size=centroid_size))
scipy = go.Scatter(x=scipy_res[0][:,0], y=scipy_res[0][:,1], 
    mode="markers", marker=dict(color='Green', size=centroid_size))
matlab = go.Scatter(x=kmeans_matlab_centers[:,0], y=kmeans_matlab_centers[:,1], 
    mode="markers", marker=dict(color='Blue', size=centroid_size))

fig.add_trace(datablobs, row=1, col=1)
fig.add_trace(scilearn, row=1, col=1)

fig.add_trace(datablobs, row=1, col=2)
fig.add_trace(scipy, row=1, col=2)

fig.add_trace(datablobs, row=1, col=3)
fig.add_trace(matlab, row=1, col=3)

fig.update_layout(autosize=False, width=900, height=375, showlegend=False)
```

<div>
  <div style="position:relative;padding-top:42%;width:100%;">
    <iframe src="/assets/images/2021/a-trick-you-dont-know-about-python-matlab/benchmark.html" frameborder="0" autosize="true" webkitAllowFullScreen mozallowfullscreen allowFullScreen
      style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
  </div>
</div>

As you can see, there are minor differences as we compare results. So, which of the three implementations is the correct one? 

Well, they all are. How can this be possible? Simple. Each implementation is giving a local optima of the optimization problem through different initial points selected randomly.

What conclusions can we draw from this?

Firstly, as Mike states:

> Saying, "This is the result of applying K-means clustering using the Kmeans++ initialisation scheme" is not sufficient to allow someone to reproduce your work. 

And adds:

> Even an algorithm as simple as K-means can exhibit different behaviors across implementations. To enable reproducibility, we need to share the exact code and data used in our analysis.

Thus, **validate your conclusions as you do research or implement your product**.

With that, you should now proceed to visit Mike's blog, it won't dissapoint you: 

:point_right: [Walking Randomly](https://walkingrandomly.com/)