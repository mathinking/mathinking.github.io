---
layout: single
title: "Part 3. Need functionality in Python only available in MATLAB (e.g. Simulink)"
excerpt: "From the series: <br>*A trick you don't know about Python: MATLAB*"
date:  2021-07-20 12:15:00 +0100
categories: [en]
tags: [python, matlab, a trick you dont know about python - matlab]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header: 
  teaser: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-functionality.jpg
  overlay_color: "#000"
  overlay_filter: "0"
  overlay_image: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-functionality.jpg
  caption: "Photo credit: [Silas Köhler](https://unsplash.com/@silas_crioco?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
---

This post is the third post on the series [A trick you don't know about Python: MATLAB](../../../blog/en/a-trick-you-dont-know-about-python-matlab).

One apparent and yet frequent reason for calling MATLAB from Python is when you need to use a specific functionality not available in Python. Such a scenario might involve using Simulink, code generation functionality, or the use of particular engineering libraries (i.e., wireless communications, controls, aerospace, biology, etc.).

For this post, I'd like to showcase the workflow of using Python and Simulink together. As I already showed with [part 1](../../../blog/en/a-trick-you-dont-know-about-python-matlab-integrate) and [part 2](../../../blog/en/a-trick-you-dont-know-about-python-matlab-facilitate-workflows), it all begins with starting the MATLAB Engine:

```python
import matlab.engine
eng = matlab.engine.start_matlab('-desktop')
```

The MATLAB Engine API for Python provides not only access to MATLAB functions but also Simulink models:

```python
modelName = "simulatePID"
eng.open_system(ModelName, nargout=0)
```

![Simulink Model opened from Python](/assets/images/2021/a-trick-you-dont-know-about-python-matlab/simulink.jpg)

Once the model is loaded, we can send data back and forth using the `eng` object:

```python
# Put variables into the workspace for the model to use
eng.workspace['Kp'] = 1.0
eng.workspace['Ki'] = 1.0
eng.workspace['Kd'] = 0.0
```

Running the model through the MATLAB Engine is as simple as calling the MATLAB `sim` function. However, I have written a function to run the model and write back the data to a Parquet file (this is another convenient way to exchange data between MATLAB and Python):

![Simulate Model and write results to a Parquet file](/assets/images/2021/a-trick-you-dont-know-about-python-matlab/simulate-write-parquet.jpg)


```python
outputFileName = "controllerResponse.parquet"
eng.simAndWriteToParquet(ModelName, outputFileName)
```

You can then read the results from the simulation using `pyarrow`:

```python
import pandas as pd
# Read as a dataframe and display
df = pd.read_parquet(outputFileName)
print(df)
```

```
     Time  Plant Response  Setpoint
0     0.0        0.000000         0
1     0.2        0.000000         0
2     0.4        0.000000         0
3     0.6        0.000000         0
4     0.8        0.000000         0
..    ...             ...       ...
248  49.2        0.999999         1
249  49.4        0.999999         1
250  49.6        0.999999         1
251  49.8        1.000000         1
252  50.0        1.000000         1

[253 rows x 3 columns]
```

Finally, we plot the simulation results:
```python
pd.options.plotting.backend = "plotly"
fig = df.plot(df["Time"], [df["Plant Response"],df["Setpoint"]])
fig.show()
```
<div>
  <div style="position:relative;padding-top:56.25%;">
    <iframe src="/assets/images/2021/a-trick-you-dont-know-about-python-matlab/simulink-results.html" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen
      style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
  </div>
</div>
We can continue exploring different parameters to develop a suitable PID controller or use optimization techniques to facilitate the process and obtain an optimal set of parameters.

Once we finish, we exit the MATLAB Engine.

```python
eng.exit()
```