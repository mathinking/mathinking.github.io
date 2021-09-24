---
layout: single
title: "My favorite features in MATLAB R2021a"
excerpt: Exploring some of the new features in yet another interesting software release
date:  2021-04-12 16:10:00 +0100
categories: [en]
tags: [matlab, machine learning, deep learning, computer vision, reinforcement learning, release]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header:
  teaser: /assets/images/2021/my-favorite-features-matlab-r2021a/class-diagram-viewer.jpg
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/2021/my-favorite-features-matlab-r2021a/class-diagram-viewer.jpg
---

MATLAB R2021a was released on March 10 with new products and major updates to several products. If you are looking for detailed release highlights, this post is probably not the right place to look. Instead, check MATLAB [release highlights](https://www.mathworks.com/products/new_products/latest_features.html?s_tid=hp_release_2021a) or [release notes](https://www.mathworks.com/help/relnotes/).

This post has the intention to cover my favorite MATLAB features in R2021a, features that either I have been waiting for or I intend to use going forward.

It has been a challenge to narrow the list down to just 10 features and taken me more time to sort them than actually writing this post. You might have chosen a different order or other new features. So please, enter your comments below!

Here we go.

# 10. bubblecloud
If you are working with data and have to provide your users with visualizations to correctly interpret that data, bubble charts can be a powerful way to do it. In this release, [bubblecloud]() allows to create a bubble cloud chart where a variable can specify the bubble sizes and you can illustrate the relationship between elements in the dataset by color. 

For example, ¿which countries have vaccinated(*) a higher percentage of their population against COVID-19 as of April 7th? 

_(*) at least one dose_
```
t = readtable('https://covid.ourworldindata.org/data/owid-covid-data.csv');
t2 = t(t.date == datetime('2021-Apr-07'),:);
t2.percentVaccinated = t2.people_vaccinated./t2.population;
t2(startsWith(t2.iso_code,"OWID"), :) = [];
bubblecloud(t2,'percentVaccinated','location','continent')
```
![Using bubble cloud](/assets/images/2021/my-favorite-features-matlab-r2021a/bubblecloud.jpg)

# 9. Custom experiments in Experiment Manager
Experiment Manager continues to get better and better. 

If you are working in the area of Deep Learning, one of the things you might be struggling with is to efficiently manage  variations of your network or hyperparameters to figure out which design performs best. [Experiment Manager App](https://www.mathworks.com/help/deeplearning/ref/experimentmanager-app.html) was introduced in R2020a to facilitate this process.

![Experiment Manager App](/assets/images/2021/my-favorite-features-matlab-r2021a/experiment-manager.png)

Here is an intro to the Experiment Manager App by the great Joe Hicklin: 
{% include video id="AnQYFZ62KWI" provider="youtube" %}

After including the possibility to run multiple trials of an experiment in parallel and Bayesian optimization (to determine the best combination of hyperparameters for an experiment) in R2020b, you can now include custom experiments in Experiment Manager. But what does this mean?

Up till now, experiments had to use the [trainNetwork](https://www.mathworks.com/help/deeplearning/ref/trainnetwork.html) function (built-in training loop), reducing the network architecture variations to using SeriesNetwork and DAG (Directed Acyclic Graph) based networks. With Custom training experiments, Experiment Manager supports workflows that use dlnetwork and a model function, where you may design your own training loop. This allows to design experiments for architectures such as Siamese Networks, GANs (Generative Adversarial Networks), Graph Conv Networks and others. Custom training experiments gives you full control over your network design variations, being able to a use custom learning schedule and any other _trick_ that would require using and controlling the training loop.

![Experiment Manager App](/assets/images/2021/my-favorite-features-matlab-r2021a/experiment-manager-custom.png)

# 8. TensorFlow Model Importer

Let's face it. Importing TensorFlow models in MATLAB has never been an easy task. Until now.

If you are working with R2017b through R2020b, you can use `importKerasNetwork` and `importKerasLayers` functions to import models in the HDF5 format. In some cases, the importer cannot deal with a specific layer and places a placeholder for you to finish the task. Alternatively, you could bring the TensorFlow to MATLAB via [ONNX](https://onnx.ai/), but the [tf2onnx](https://github.com/onnx/tensorflow-onnx) project, in active development, seems to still be missing a lot of needed functionality. 

Fortunately for the MATLAB user, the [Deep Learning Toolbox Converter for TensorFlow models](https://www.mathworks.com/matlabcentral/fileexchange/64649-deep-learning-toolbox-converter-for-tensorflow-models) facilitates now bringing TF2.0 models into MATLAB for prediction and transfer learning. 

# 7. Live Editor Controls

Ever since I started to use the [Live Editor](https://www.mathworks.com/products/matlab/live-editor.html) for demos, one of the missing features has been being able to refer to an existing workspace variable to dynamically control drop-down items. 

Now you can do this for drop-down values and bounds within a slider control. 
![Experiment Manager App](/assets/images/2021/my-favorite-features-matlab-r2021a/drop-down-control.png)


# 6. Prettyprint for JSON

This might seem a small thing to you, but does help a lot to me.

Reading this JSON output might not be so straight forward:

```
>> jsonencode(johnS)

ans =

    '{"firstName":"John","lastName":"Smith","isAlive":true,"age":27,"address":{"streetAddress":"21 2nd Street","city":"New York","state":"NY","postalCode":"10021-3100"},"children":[]}'
```

but MATLAB can now _prettify_ the output:

```
>> jsonencode(johnS,'PrettyPrint',true)

ans =

    '{
       "firstName": "John",
       "lastName": "Smith",
       "isAlive": true,
       "age": 27,
       "address": {
         "streetAddress": "21 2nd Street",
         "city": "New York",
         "state": "NY",
         "postalCode": "10021-3100"
       },
       "children": []
     }'
```

# 5. Labeling large images

The [Image Labeler app](https://www.mathworks.com/help/vision/ref/imagelabeler-app.html) enables you to label ground truth data in a collection of images, enabling Computer Vision and Deep Learning workflows. While the app does help tremendously in facilitating the labeling process, as images were getting bigger, such task became more tedious. There is an open-source contribution by my colleague [Brett Shoelson](https://www.mathworks.com/matlabcentral/profile/authors/845693), [labelBigImage](https://www.mathworks.com/matlabcentral/fileexchange/74382-label-images-too-big-to-fit-in-memory), which frankly works extremely well. And this might still be my preferred solution if you are working with releases between R2019b and R2020b. However, when loading images in R2021a with Image Labeler, if an image has a dimension larger than 8000 pixels or is a multiresolution image, the app offers you the option to convert the image into a blocked image:

![Label Large Images in Image Labeler](/assets/images/2021/my-favorite-features-matlab-r2021a/image-labeler-large.png)

See the [doc](https://www.mathworks.com/help/vision/ug/label-blocked-image-using-the-image-labeler.html) for additional details.

# 4. Reinforcement Learning Designer App

This one came to a surprise to me the first time I learnt about it. Why? Because v1.0 is already great! With [Reinforcement Learning Designer](https://www.mathworks.com/help/reinforcement-learning/ref/reinforcementlearningdesigner-app.html) you can easily cover a RL workflow to design, train and simulate agents with MATLAB and Simulink: 

![Reinforcement Learning Designer App](/assets/images/2021/my-favorite-features-matlab-r2021a/reinforcement-learning-app.png)

1. The app allows you to import an existing environment or use predefined environments in MATLAB and Simulink
2. Once the environment has been added to the app, you can automatically create or import an agent for that environment
3. You can then train and simulate the agent against the specified environment
4. After analyzing your results, you can iterate and tune your agent by modifying its parameters
4. Finally, you can export the agent results to the workspace for further analysis and deployment phases

# 3. Shallow nets in Classification Learner and Regression Learner

I stopped counting the times that users have asked me why shallow nets were not included in Classification Learner and Regression Learner apps. 

Deep Learning Toolbox, formerly known as Neural Network Toolbox, was first released in June 1992 and developed by Mark Hudson Beale, Martin T. Hagan and Howard B. Demuth. More than 10 years ago, I received the course Neural Network Design from [Howard B. Demuth](http://www.ee.uidaho.edu/ee/emeritus/hdemuth/hdemuth.html) and this was the spark that got me in pursuing a PhD in Neural Networks. I might dive deeper into this some other day...

By including shallow nets in Classification Learner and Regression Learner apps, together with other updates to the apps that coincidently happened also in this release (importing test data, sorting and deleting models, loading data from command line and others), I see these Machine Learning apps getting very close to feature complete.

![Shallow nets in Classification Learner and Regression Learner](/assets/images/2021/my-favorite-features-matlab-r2021a/regression-learner-nnet.jpg)

# 2. Class Diagram Viewer

One of my top wishes for Object-Oriented Programing in MATLAB has always been to easily inspect and view my MATLAB classes as I would do if using [UML](https://www.uml.org/). There are a [few contributions](https://www.mathworks.com/matlabcentral/fileexchange/59722-m2uml) from the community that aim to solve this challenge and, although these solve my requirements to some degree, I am still missing some key features. 

[Class Diagram Viewer](https://www.mathworks.com/help/matlab/ref/classdiagramviewer.html) allows you to create class diagrams showing implementation details and hierarchies. You may inspect the internal structure of the classes, properties, methods, understand hierarchy of classes, inheritance, etc.

![Class Diagram Viewer on ClassificationSVM](/assets/images/2021/my-favorite-features-matlab-r2021a/class-diagram-viewer.jpg)

# 1. Using name=value syntax for passing name-value argument pairs

I must admit. This one makes me happy, very happy. :smile:

Yes, Python and R, as well as other high-level programming languages support this syntax. In software development, when something improves your usability and user experience, it's wise to bring it on. This is a great idea!

As an example, the code snippet on [feature #6](#6-prettyprint-for-json) turns into:

```
>> jsonencode(johnS,PrettyPrint=true)
```

And those were my top :one::zero: features in MATLAB R2021a. What are [yours](https://www.mathworks.com/help/relnotes/)? 
