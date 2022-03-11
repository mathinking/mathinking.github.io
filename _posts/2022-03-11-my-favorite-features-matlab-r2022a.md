---
layout: single
title: "My favorite features in MATLAB R2022a"
excerpt: Exploring some of the new features in yet another interesting software release
date:  2022-03-11 13:00:00 +0100
categories: [en]
tags: [matlab, machine learning, deep learning, python, release, software development, mlops]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header:
  teaser: /assets/images/2022/my-favorite-features-matlab-r2022a/MATLABOnlineFull.jpg
  overlay_color: "#000"
  overlay_filter: "0.1"
  overlay_image: /assets/images/2022/my-favorite-features-matlab-r2022a/MATLABOnlineFull.jpg
---

MATLAB R2022a was released this week and, as I have done for the previous two releases ([R2021a](/blog/en/my-favorite-features-matlab-r2021a), [R2021b](/blog/en/my-favorite-features-matlab-r2021b)), I would like to highlight the features that I am most excited about.

As usual, it has been hard to come up with this list. I have had to leave out many new features that I am truly eager about... Do not forget to check the [release highlights](https://www.mathworks.com/products/new_products/latest_features.html) with 5 new products and [release notes](https://www.mathworks.com/help/relnotes/) to learn about updates to your favorite products. 

# 10. pcode
For all my years at MathWorks, every once in a while, I have been approached by users regarding `pcode` obfuscation. Protecting IP has always been a topic of interest for MATLAB users. MATLAB R2022a now includes the option to create a P-code file using a more complex obfuscation algorithm. 

```
pcode myfunc -R2022a
```
Although this is extremely simple, consider combining several approaches to protect your code or data. Check these [Security considerations to protect your code](https://www.mathworks.com/help/matlab/matlab_prog/protect-your-source-code.html).

# 9. Taylor Pruning
Deploying Deep Neural Networks to embedded systems can become a challenging problem, especially if the network doesn't fit in your device. There are several model compression techniques that may be useful in this regard. Pruning allows to reduce the memory footprint of the network and thus increase inference speed, by removing whole filters in the network, making it less wide. 

![Comparing numbers of filters from original and pruned network](\assets\images\2022\my-favorite-features-matlab-r2022a\PruningUsingTaylorPrunableNetworkExample.png)
You may also compare the accuracy of the original and the pruned network:
![Confusion Chart - Original Network](\assets\images\2022\my-favorite-features-matlab-r2022a\ConfusionChart_OriginalNetwork.png) ![Confusion Chart - Pruned Network](\assets\images\2022\my-favorite-features-matlab-r2022a\ConfusionChart_PrunedNetwork.png)

Check [`taylorPrunableNetwork`](https://www.mathworks.com/help/deeplearning/ref/deep.prune.taylorprunablenetwork.html) for more details on how Taylor Pruning works or visit these examples ([1](https://www.mathworks.com/help/deeplearning/ug/prune-filters-in-a-detection-network-using-taylor-scores.html), [2](https://www.mathworks.com/help/deeplearning/ug/prune-filters-detection-network.html)) to learn more.
# 8. Updates to Machine Learning Apps
Classification and Regression Learner Apps, which I have highlighted in the past ([1](https://mathinking.github.io/blog/en/my-favorite-features-matlab-r2021a/#3-shallow-nets-in-classification-learner-and-regression-learner), [2](https://mathinking.github.io/blog/en/my-favorite-features-matlab-r2021b/#4-your-machine-learning-model-to-production-is-one-click-away)) have been profoundly updated in 2022a, including:
* Save current session and open a previously saved session
* Reserve a percentage of imported data for testing
* _Feature ranking algorithms to select predictors_
* Create several draft models
* Use model summary to change model options and view model results
* Train all draft models (including training in parallel)

Additionally, there are updates specific to Classification and Regression Learner. 

Out of all the previous Machine Learning Apps updates, my top choice is having the possibility to use feature ranking algorithms to select predictors. By using various feature ranking algorithms, you may rank features by importance scores and select features in auto/manual mode.
![Ranking Features in Classification Learner](\assets\images\2022\my-favorite-features-matlab-r2022a\ClassificationLearner_RankFeatures.png)

# 7. Publish a MATLAB function as a Docker container microservice
MATLAB Compiler SDK facilitates now the creation of a Microservice Docker Image using [`compiler.package.microserviceDockerImage`](https://www.mathworks.com/help/compiler_sdk/mps_dev_test/compiler.package.microservicedockerimage.html). After packaging your MATLAB function into a Microservice Docker Image, you can run the microservice `myfunc`:
```
docker run --rm -p 9900:9910 myfunc
```

and then test the running service using curl, Postman, [Thunder Client](/blog/en/when-matlab-production-server-met-thunder-client-vs-code/), etc.
```
curl -v -H Content-Type:application/json -d '{"nargout":1,"rhs":[4]}' http://hostname:9900/myfuncarchive/myfunc
```

[Learn more](https://www.mathworks.com/help/compiler_sdk/mps_dev_test/create-a-microservice-docker-image.html)

# 6. Training with heterogeneous multi-input networks
The trainNetwork function now supports layer graphs with mixtures of ImageInputLayer, Image3DInputLayer, SequenceInputLayer, and FeatureInputLayer layer objects. When using the trainNetwork function, the network must have at most one sequence input layer.

![Multi-input network](\assets\images\2022\my-favorite-features-matlab-r2022a\Multi-Input.png)

# 5. User-Authored Live Tasks
Live Editor tasks are simple point-and-click interfaces that can be added to a live script to perform a specific set of operations. MATLAB and different toolboxes include several of these tasks to facilitate and streamline development. 

Starting in MATLAB 2022a, you can [author your own Live Task](https://www.mathworks.com/help/matlab/creating_guis/live-task-development-overview.html). I have worked extensively with this new feature. I will likely share more about this in a future post.

# 4. Network Analyzer updates
This may seem like a very small update to some of you. I find this as one of those updates that deeply simplify your life (if working in Deep Learning). Network Analyzer allows you now to the activation dimension labels and the total number of learnable parameters of a network. 
Each activation dimension has one of the following labels:
* S — Spatial
* C — Channel
* B — Batch observations
* T — Time or sequence
* U — Unspecified

![Network Analyzer](\assets\images\2022\my-favorite-features-matlab-r2022a\NetworkAnalyzer.png)

# 3. Python syntax highlighting 
The MATLAB Editor has been updated to make viewing and editing Python files much easier. The Editor now displays Python files with syntax highlighting for keywords, strings, comments, and errors. In addition, the Editor auto-indents Python files and indicates matched and mismatched delimiters such as parentheses, brackets, and braces.

![Before and after](\assets\images\2022\my-favorite-features-matlab-r2022a\PythonSyntaxHighlighting.png)
_(MATLAB Editor before and after MATLAB R2022a)_

# 2. Dark theme in MATLAB Online
Oh yes! You can now change the colors of the MATLAB Desktop using themes. Go to Preferences > MATLAB > Appearance and set the theme to Dark
![MATLAB Online Preferences](\assets\images\2022\my-favorite-features-matlab-r2022a\MATLABOnlinePreferences.jpg)

You may now continue your development from the dark side.
![MATLAB Online Dark Theme](\assets\images\2022\my-favorite-features-matlab-r2022a\MATLABOnlineDark.jpg)

# 1. MATLAB Deep Learning Model Hub
You can find the latest pretrained MATLAB deep learning models in the new [MATLAB Deep Learning Model Hub](https://github.com/matlab-deep-learning/MATLAB-Deep-Learning-Model-Hub). Finally, a one-stop place to search for suitable models for a range of deep learning applications, including lidar point cloud processing, audio speech to text, pose estimation, etc. 

![MATLAB Deep Learning Model Hub](\assets\images\2022\my-favorite-features-matlab-r2022a\MATLAB_DeepLearningModelHub.jpg)