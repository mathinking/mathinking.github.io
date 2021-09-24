---
layout: single
title: "My favorite features in MATLAB R2021b"
excerpt: Exploring some of the new features in yet another interesting software release
date:  2021-09-24 14:10:00 +0100
categories: [en]
tags: [matlab, machine learning, deep learning, parallel computing, lidar, python, release, software development]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header:
  teaser: /assets/images/2021/my-favorite-features-matlab-r2021b/21b_door.jpg
  overlay_color: "#000"
  overlay_filter: "0.1"
  overlay_image: /assets/images/2021/my-favorite-features-matlab-r2021b/21b_door.jpg
---

It’s yet again that time of the year. A new MATLAB release just came out.

I know that there are plenty of great features that could have made it to the list, which doesn’t mean I don’t find them relevant or useful. These are the ones that I believe that will be more relevant to me in the coming months.

So let’s cut to the chase and visit my favorite new features in MATLAB R2021b:

# 10. Exporting Animations in the Live Editor
Exporting animations got easier with the Live Editor. You can export animations to movies or GIFs simply by using the new Export Animation button. 

[![Exporting Animations with Live Editor](/assets/images/2021/my-favorite-features-matlab-r2021b/exportinganimation.jpg)](/assets/images/2021/my-favorite-features-matlab-r2021b/exportinganimation.gif)

_Click the image to play the exported animation from MATLAB_

# 9. Test class template

Testing your code is an integral part of developing quality software. For me, testing is like breathing. If you don’t (adequately) test your code, it will eventually die. With the existing [testing frameworks in MATLAB](https://www.mathworks.com/help/matlab/matlab-unit-test-framework.html), you can write unit tests, performance tests, test your apps, or test a portion of your complete system in isolation using mock objects to replace the dependencies.

MATLAB R2021b includes a TestCase class template to speed up the creation of your tests. You need to go to New > Test Class in the Home, Editor, or Live Editor tabs:

![New Test Class](/assets/images/2021/my-favorite-features-matlab-r2021b/newtestclass.jpg)

This brings up the following template so that you can create the test more conveniently:

![New Test from Template](/assets/images/2021/my-favorite-features-matlab-r2021b/testclasstemplate.jpg)

Interestingly, the default test class coming out of the template fails right away, so that you start to implement your tests and your code. Moreover, it includes several method blocks (`TestClassSetup`, `TestMethodSetup`, and `Test`) to begin customizing your tests.

There is a **brilliant** presentation by my colleague [Heather Gorr, Ph.D.](https://twitter.com/heathergorr) where she covers test-driven development, among other topics:

:point_right: [Would you trust your model with your life? Research vs. reality in AI](https://www.youtube.com/watch?v=M75CSBqTeEU){:target="_blank"}

# 8. New live tasks

I must admit that I don’t use Live Tasks often. However, every time I do, my mind explodes. This new release brings [Compute by group](https://www.mathworks.com/help/matlab/ref/computebygroup.html) and [Normalize Data](https://www.mathworks.com/help/matlab/ref/normalizedata.html) live tasks to MATLAB, and the [Cluster Data](https://www.mathworks.com/help/stats/clusterdatatask.html) live task to Statistics and Machine Learning Toolbox. Of all, my favorite, maybe also due to the UX experience, is Compute by Group. Grouping data and computing statistics, transformations, or filtering operations on each group couldn’t be more effortless with this live task. Of course, the task automatically generates MATLAB code for you.

See it in action by yourself:

[![Compute by group live task](/assets/images/2021/my-favorite-features-matlab-r2021b/computebygroup_play.png)](/assets/images/2021/my-favorite-features-matlab-r2021b/computebygroup.gif)

# 7. Cuda optimized code for ROS Nodes
In the past, I have _deeply_ suffered the process of bringing CUDA code from a Deep Neural Network (generated from GPU Coder) to ROS nodes. It required having to manually integrate the generated library inside a handwritten C++ ROS node. 

In this release of ROS Toolbox, you can now generate and deploy CUDA-optimized code for ROS nodes directly from your Simulink model. Simply beautiful. 

![Export ML model](/assets/images/2021/my-favorite-features-matlab-r2021b/simulinkcudaros.png)

See it for yourself with this [Lane and Vehicle Detection example](https://www.mathworks.com/help/ros/ug/lane-and-vehicle-detection-in-ros-using-yolov2-deep-learning-algorithm.html).

# 6. backgroundPool
I have frequently received feedback from MATLAB users who wanted to run code asynchronously, forcing them to use Parallel Computing Toolbox. Usually, MATLAB suspends execution while running calculations. And if you are developing an app, for instance, this might affect its responsiveness.

I have frequently received feedback from MATLAB users that wanted to run code asynchrounously and that forced them to use Parallel Computing Toolbox. Usually, MATLAB suspends execution while running calculations. And if you are developing an app, for instance, this might affect its responsiveness.

It's worth noting that [Parallel Computing Toolbox](https://www.mathworks.com/products/parallel-computing.html) provides an API for a broad range of parallel programming paradigms, GPU computing, and an API to bring your processing to clusters and HPCs (including Big Data Frameworks like Hadoop or Spark). 

Although having access to Parallel Computing Toolbox will have added benefits (access to more threads basically), MATLAB users can now run a single worker as a thread in the main MATLAB process. This facilitates asynchronous workflows (using [`backgroundPool`](https://www.mathworks.com/help/matlab/ref/parallel.backgroundpool.html) to open the pool and [`parfeval`](https://www.mathworks.com/help/matlab/ref/parfeval.html) to run your functions in the background).

You can check [here](https://www.mathworks.com/help/matlab/matlab_prog/use-the-background-to-make-your-apps-more-responsive.html) an example of how your app can be more responsive with `backgroundPool`. 

# 5. PointNet++
PointNet and PointNet++ papers ([1](#pointnet), [2](#pointnetplusplus)) fall in this category of research papers that I have read thoroughly. I might post one day on these two papers and why PointNet++ is an excellent choice for segmenting point cloud data. 

![PointNet++](/assets/images/2021/my-favorite-features-matlab-r2021b/pointnetplusplus.png)

But for now, you no longer need to figure out how to create a PointNet++ network with the extended DL framework in MATLAB (as was the case in R2021a) and [`pointnetplusplusLayers`](https://www.mathworks.com/help/lidar/ref/pointnetpluslayers.html) does the job right away. For instance, you will be able to solve [semantic segmentation on point cloud data from aerial lidar](https://www.mathworks.com/help/lidar/ug/aerial-lidar-segmentation-using-pointnet-network.html):

![Semantic Segmentation using PointNet++](/assets/images/2021/my-favorite-features-matlab-r2021b/semanticsegmentation_lidar.png)

1. <a name="pointnet"></a>Charles R. Qi, Hao Su, Kaichun Mo and Leonidas J. Guibas, "PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation", 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2017 [https://arxiv.org/abs/1612.00593v2](https://arxiv.org/abs/1612.00593v2){:target="_blank"}
2. <a name="pointnetplusplus"></a>Charles R. Qi, Li Yi, Hao Su, and Leonidas J. Guibas. "PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space", ArXiv:1706.02413 [Cs], June 7, 2017. [https://arxiv.org/abs/1706.02413](https://arxiv.org/abs/1706.02413){:target="_blank"}

# 4. Your Machine Learning model to production is one click away
Once you have trained a Machine Learning model using Classification Learner or Regression Learner, bringing it to production is just one-click away. 

![Export ML model](/assets/images/2021/my-favorite-features-matlab-r2021b/exportmodel.jpg)

This will create a deployment project for MATLAB Production Server and autogenerate the required MATLAB code to serve your model in production. You can find examples for Classification Learner and Regression Learner apps [here](https://www.mathworks.com/help/stats/deploy-model-trained-in-classification-learner-to-mps.html) and [here](https://www.mathworks.com/help/stats/deploy-model-trained-in-regression-learner-to-mps.html). 

# 3. pyrun and pyrunfile
Ever since the first version of the Python interface was shipped in MATLAB R2014b, I have been a true and loyal fan. The interface not only does the job of calling Python from MATLAB, but I also believe that it is a beautiful implementation design. If you’d like to check the doc, you can certainly do so. However, I recommend you watch one of the multiple talks available online, where my colleagues [Heather](https://twitter.com/heathergorr) and [Yann](https://www.linkedin.com/in/yann-debray-70305026) discuss use cases, workflow, and tips on using the two languages together:

{% include video id="MzoFK0_UbOA" provider="youtube" %}

As incredible as the interface might seem to me or others, I understand it may not be practical for those who just need to run a snippet or script of Python code. With [`pyrun`](https://www.mathworks.com/help/matlab/ref/pyrun.html) and [`pyrunfile`](https://www.mathworks.com/help/matlab/ref/pyrunfile.html) you can now call Python commands and scripts from MATLAB:

```
>> pyrun("from __future__ import braces")
Python Error: SyntaxError: not a chance (<string>, line 1)
```

This is one of the funny easter eggs in CPython regarding having braces to control flow. You can do more meaningful stuff to exemplify your use case; indeed, I simply find this one quite funny.

# 2. Git workflow in MATLAB Online
In simple terms, [MATLAB Online](https://www.mathworks.com/products/matlab-online.html) is simply MATLAB on your web browser. No downloads. No installs. 

Git integration has been part of MATLAB for a long time now. Starting in R2021b, MATLAB Online provides support for basic Git workflows:

![New from Git](/assets/images/2021/my-favorite-features-matlab-r2021b/matlabonline_fromgit.jpg)

You can now clone, commit, pull, push and fetch files to and from your MATLAB Drive:

![Cloning a repo](/assets/images/2021/my-favorite-features-matlab-r2021b/matlabonline_clone.jpg)

# 1. Updates to the MATLAB Editor
If you got so far reading, my top pick has been the updates to the MATLAB Editor. This may not seem a fancy pick to you. For quite some time now, there were a considerable number of coding features that were available for Live Scripts but not for plain code (.m files to be clear). For those of us who still maintain a lot of code in plain code, it frequently came with a loss in productivity. :umbrella:

The MATLAB Editor now supports a rich set :sunny: of features for your MATLAB code (in .m files):
* Zooming in and out your code
* Tab completion
* Assistance with auto syntax completion 
* Smart parameter suggestion as you are filling in function calls
* Enhanced debugging
* Code refactoring 
* Code block selection
* Bookmarks
* Case-change of text 
* ...

My life just got a lot easier with R2021b. 

Check the [latest features](https://www.mathworks.com/help/matlab/release-notes.html) in the release notes, and feel free to share your favorites with me. 