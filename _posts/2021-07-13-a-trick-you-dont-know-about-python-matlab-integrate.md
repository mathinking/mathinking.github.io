---
layout: single
title: "Part 1. Integrate MATLAB code from a colleague into Python"
excerpt: "From the series: <br>*A trick you don't know about Python: MATLAB*"
date:  2021-07-13 09:00:00 +0100
categories: [blog, en]
tags: [python, matlab, a-trick-you-dont-know-about-python-matlab]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header: 
  teaser: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-integrate.jpg
  overlay_color: "#000"
  overlay_filter: "0.3"
  overlay_image: assets/images/2021/a-trick-you-dont-know-about-python-matlab/trick-integrate.jpg
  caption: "Photo credit: [Ryoji Iwata](ttps://unsplash.com/@ryoji__iwata?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
---

This post is the first post on the series [A trick you don't know about Python: MATLAB](../../../blog/en/a-trick-you-dont-know-about-python-matlab).

Simplifying integration between programming languages is critical to facilitate team collaboration and streamline product development. Frequently, I receive questions on how to integrate MATLAB with Python. 

The following example showcases two different integration scenarios: integrating MATLAB code with Python in a development phase and integrating MATLAB code with Python for production.

# Integrating MATLAB code with Python in Development
The key element in facilitating the call of MATLAB from Python is the [MATLAB Engine API for Python](https://www.mathworks.com/help/matlab/matlab_external/get-started-with-matlab-engine-for-python.html?lang=en). Once [installed](https://www.mathworks.com/help/matlab/matlab_external/install-the-matlab-engine-for-python.html), you may use it to call MATLAB functions and exchange data between Python and MATLAB by using the classes included in the `matlab` package.

We start by calling the `matlab.engine.start_matlab` function, which starts a new MATLAB process in the background:

```python
import matlab.engine
eng = matlab.engine.start_matlab()
```

The `eng` object now enables you to pass data and call functions executed by MATLAB:
```python
x = eng.sqrt(42.0)
print(x)
```
```
6.48074069840786
```
which tells MATLAB to compute the square root of 42.0 by calling `sqrt`.

You can then call your Python code:
```python
import weather
json_data = weather.get_current_weather("Boston","US",apikey)
data = weather.parse_current_json(json_data)
print(data)
```
```
{'temp': 45, 'feels_like': 38.91, 'temp_min': 41, 'temp_max': 48.99, 'pressure': 1010, 'humidity': 76, 'speed': 12.66, 'deg': 270, 'lon': -71.0598, 'lat': 42.3584, 'city': 'Boston', 'current_time': '2021-04-20 10:54:13.569727'}
```

and call any user-defined functions developed in MATLAB:
```python
aq = eng.predictAirQual(data)
print(aq)
```
```
Good
```
outputing a native `str` Python data type.

Finally, you can exit the engine using the `exit` function:
```python
eng.exit()
```

Enabling debugging workflows is vital to facilitate code integration. In this sense, the MATLAB Engine API provides various ways to start up the engine in desktop mode:
```python
eng = matlab.engine.start_matlab("-desktop")
```

or using [`matlab.engine.connect_matlab`](https://www.mathworks.com/help/matlab/apiref/matlab.engine.connect_matlab.html) to connect Python to a [previously](https://www.mathworks.com/help/matlab/ref/matlab.engine.shareengine.htm) shared MATLAB session:
```python
eng = matlab.engine.connect_matlab()
```

# Integrating MATLAB code with Python in Production

Another relevant use case of integrating MATLAB code with Python is when the Python user incorporates a MATLAB package created using [MATLAB Compiler SDK](https://www.mathworks.com/products/matlab-compiler-sdk.html). In this case, we are replacing MATLAB Engine for the MATLAB runtime so that you can call the MATLAB code without a MATLAB license. 

Assuming the user-defined function in MATLAB `predictAirQual` has been packaged into the `AirQual` python package, the code runs as follows:

```python
# Import the package created from MATLAB
import AirQual

# Initializing MATLAB runtime
aq = AirQual.initialize()

# Calling packaged MATLAB function
label = aq.predictAirQual(data)

# Terminating MATLAB runtime
aq.terminate()
```

Additionally, another very convenient mechanism aligned with scalable and secure architecture designs can be realized by using MATLAB Production Server. [MATLAB Production Server](https://www.mathworks.com/products/matlab-production-server.html) is an application server that allows us to operationalize your models or algorithms through APIs, integrating them with the IT and OT systems available in your organization. So, once the development is completed in MATLAB, we can take it to Production Server and simply access those algorithms and models in a _function-as-a-service_ manner, invoking functions via a RESTful API using JSON payloads for input and output:

```python
from urllib import request
import json

# Server address 
url = "http://localhost:9910/AirQualReport/CurrentAirQual"

# Prep json inputs to call MATLAB code 
headers = {"Content-Type": "application/json"}
body = json.dumps({"nargout": 2, "rhs" : "San Jose"})
# Convert to string and encode
body = str(body)
body= body.encode("utf-8")

# Post method
req = request.Request(url, data=body, headers=headers)
# Response
resp = request.urlopen(req)
result = json.loads(resp.read())
print(result)
```
```
{'lhs': [{'mwdata': ['Good'], 'mwsize': [1, 4], 'mwtype': 'char'}, {'mwdata': [55.76], 'mwsize': [1, 1], 'mwtype': 'double'}]}
```

What to learn more about how the integration can simplify some of your Python workflows? 

Stay tuned for **part 2**!