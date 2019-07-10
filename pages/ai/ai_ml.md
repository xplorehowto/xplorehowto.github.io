---
title: Machine Learning - Summary
keywords: ai, artificial intelligence, ml, machine learning, deep learning, models
tags: [ai, ml]
sidebar: ai_sidebar
permalink: /ai_ml
folder: ai
---

## Machine Learning Categories

Machine Learning (ML) use cases can be categorized into:
- Object Vision (detection, classification, segmentation, motion, etc. )
- Human Vision (face, pose, motion, etc.) 
- Speech (translation, speech-to-text-to-speech, etc.)
- Voice (identification, etc.)
- Document analysis (categorize, sentiment, insight, etc.)
- Recommendation
- Forecasting or Projection
- Domain specific

## Models Repository

### Tensorflow Models

Hosted at the [Github- TensorFlow Models](https://github.com/tensorflow/models)  
is recommended **START from here for learning**. The repository is grouped by: 
- Official models are a collection of example models that use TensorFlow's 
  high-level APIs. They are intended to be well-maintained, tested, and kept 
  up to date with the latest stable TensorFlow API. They should also be 
  reasonably optimized for fast performance while still being easy to read. 
  Recommend newer TensorFlow users to start here. 
  [[Further discussions](#tensorflow---official-models)]

- Research models are a large collection of models implemented in TensorFlow 
  by researchers. They are not officially supported or available in release 
  branches; it is up to the individual researchers to maintain the models 
  and/or provide support on issues and pull requests.
  [[Further discussions](#tensorflow---research-models)]

- Samples folder contains code snippets and smaller models that demonstrate 
  features of TensorFlow, including code presented in various blog posts.

- Tutorials folder is a collection of models described in the 
  [TensorFlow tutorials](https://www.tensorflow.org/tutorials/).
  
[*Source: Github - Tensorflow Models readme*]
  
#### Tensorflow - Official Models

Hosted in the [official folder](https://github.com/tensorflow/models/tree/master/official).  
There are not that many models from the official collections, and most of them
are not commonly used in the online blogging. For example, the popular 
**object detection** models are hosted at the "Research" model repo as 
discussed [here](#tensorflow---research-models).

Current available models are:
- bert: A powerful pre-trained language representation model: BERT, which 
  stands for Bidirectional Encoder Representations from Transformers.
- boosted_trees: A Gradient Boosted Trees model to classify higgs boson process 
  from HIGGS Data Set.
- mnist: A basic model to classify digits from the MNIST dataset.
- resnet: A deep residual network that can be used to classify both CIFAR-10 
  and ImageNet's dataset of 1000 classes.
- transformer: A transformer model to translate the WMT English to German 
  dataset.
- wide_deep: A model that combines a wide model and deep network to classify 
  census income data.

<div class="alert alert-success" role="alert">
  <i class="fa fa-check-square-o"></i> 
  <b>Note:</b>
  follow the instructions provided in the 
  <a href="https://github.com/tensorflow/models/tree/master/official#requirements">Requirements</a>
  for how-to setup the models.
</div>

#### Tensorflow - Research Models

Hosted in the [research folder](https://github.com/tensorflow/models/tree/master/research).  
There are at least 50 models in the 
[collections](https://github.com/tensorflow/models/tree/master/research#models) 
including the popular 
["object detection"](https://github.com/tensorflow/models/tree/master/research/object_detection) 
model found in the subfolder. 
  
An in-depth discussion about how-to navigate the model repo is provided below
for object detection; and for others in the future.

##### Object Detection

Hosted in the 
[object_detection folder](https://github.com/tensorflow/models/tree/master/research/object_detection).
The models are capable of localizing and identifying multiple objects in a 
single image, though it still remains a core challenge in computer vision. 
The TensorFlow Object Detection API is an open source framework built on top 
of TensorFlow that makes it easy to construct, train and deploy object 
detection models.
  
Follow the instructions below to navigate object detection repo:

- checkout [Table of Content](https://github.com/tensorflow/models/tree/master/research/object_detection#table-of-contents)

- Go to [g3doc documentation folder](https://github.com/tensorflow/models/tree/master/research/object_detection/g3doc);
  the TOC also links to this folder 
  
- **Must do**, get familiar with the [Installation](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md)

- **[Tensorflow detection model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)** 
  list all the different models, and provide links to download the models;
  this is where everyone download the models from.


## Inference Speed Benchmark

The inference speed is governed by image size, model, hardware and 
framework but perhaps to a lesser extend.

### Hardware benchmark

Alasdair Allan performed benchmarking for the following hardwares while keeping
the model and framework the same around 
[May 2019](https://medium.com/@aallan/benchmarking-edge-computing-ce3f13942245):

- **Coral Dev Board** (NXP i.MX 8M processor, Google Edge TPU, 
  [Setup](https://medium.com/@aallan/hands-on-with-the-coral-dev-board-adbcc317b6af),
  [Specs](https://coral.withgoogle.com/docs/dev-board/datasheet/))
- **NVIDIA Jetson Nano** (64-bit quad-core Arm Cortex-A57 CPU 1.43GHz, 
  NVIDIA Maxwell GPU with 128 CUDA cores capable of 472 GFLOPs (FP16), 
  4GB of 64-bit LPDDR4 RAM onboard, 16GB of eMMC storage,
  [Setup](https://blog.hackster.io/getting-started-with-the-nvidia-jetson-nano-developer-kit-43aa7c298797),
  [Spec](https://blog.hackster.io/introducing-the-nvidia-jetson-nano-aaa9738ef3ff))
- **Coral USB Accelerator with a Raspberry Pi** (
  [Setup](https://medium.com/@aallan/hands-on-with-the-coral-usb-accelerator-a37fcb323553)
  [Specs](https://coral.withgoogle.com/docs/))
- **The original Movidus Neural Compute Stick with a Raspberry Pi** () 
- **Second generation Intel Neural Compute Stick 2 with a Raspberry Pi** ()
- **Apple MacBook Pro 2016 model** [Quad-core 2.9 GHz Intel Core i7]
- **Vanilla Raspberry Pi 3, Model B+** without any acceleration

He compared two quite similar models pretrained by Google, both models use
Tensorflow framework: 
[Mobilenet v2 SSD trained with COCO dataset](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz) 
and 
[Mobilenet v1 SSD 0.75 depth trained also with COCO dataset](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_0.75_depth_300x300_coco14_sync_2018_07_03.tar.gz).
  
An single 3888×2916 pixel image was used which contained two recognizable 
objects, a banana and an apple. The image was resized down to 300×300 pixels 
before presenting it to the model, and each model was run 10,000 times before 
an average inferencing time was taken.

{% include image.html file="ai/aa_hw_benchmark_2019-05.png" url="#" 
  caption="Hardware benchmarking: inference time in ms; Source: 
  <a href='https://medium.com/@aallan/benchmarking-edge-computing-ce3f13942245'>
  Benchmarking Edge Computing
  </a>" 
  max-width=900 %}

{% include image.html file="ai/aa_hw_benchmark_table_2019-05.png" url="#" 
  caption="Hardware benchmarking: inference time in ms; Source: 
  <a href='https://medium.com/@aallan/benchmarking-edge-computing-ce3f13942245'>
  Benchmarking Edge Computing
  </a>" 
  max-width=700 %}

The inference time [reported by Google](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md#coco-trained-models)
is 31 ms and 26 ms, respectively, tested under the following conditions: 
600x600 pixel image, time includes all pre and post-processing, and 
performed on desktop using an Nvidia GeForce GTX TITAN X card.
They also advised that Mobilenet V2 is faster on mobile devices than 
Mobilenet V1, but is slightly slower on desktop GPU.
 

## Frameworks

List of machine learning frameworks, high level descriptions and links to
useful in-depth information.

### Tensorflow

Start from [Github Tensorflow repo](https://github.com/tensorflow/tensorflow) 
and follow through to the end of the for 
[links](https://github.com/tensorflow/tensorflow#for-more-information) 
to good information. 

#### Installation

Two very good sources, directly from Tensorfow, to start from: 
- [Github Tensorflow repo - Installation](https://github.com/tensorflow/tensorflow#installation)
  install using `pip` for both CPU and GPU, other hardware architectures 
  including Raspberry Pi, and nighly build
  
- [Tensorflow website](https://www.tensorflow.org/install)
  more detailed instructions; including; docker container, and Google Colab. 


## References

- [Google Python Style Guide](https://github.com/google/styleguide/blob/gh-pages/pyguide.md)