---
layout: inner
title: 'Exploring Methods for Object Recognition'
date: 2017-03-18 03:30:00
categories: Python ScikitLearn Tensorflow
tags: Machine Learning
featured_image: '/assets/object_recognition.gif'
lead_text: 'Winter Project for Northwestern MSR Program'
---

Implementation of the Bag of Words method for object recognition.

Final GitHub Repo: [object-recognition](https://github.com/apollack11/object-recognition)  

### The Goal
I hadn’t gotten a chance to explore machine learning yet at Northwestern, so I decided to center my winter project around the topic. Exploring object recognition seemed like a straightforward yet interesting way to do so. I set out to learn the basics of machine learning and to create a fully-functioning object classifier.  

### Methodology  

#### Bag of Words
The gif above this post shows the results of a trained classifier using the bag of words method. Bag of words is a four step process which consists of the following<sup>[1]</sup>:

**STEP 1:** Extract Features  
This step aims to simplify images into a set of smaller features so the classifier doesn’t need to train on every pixel of every image. These features should be unique and should not depend on orientation or scaling. For this step I used the scale-invariant feature transform (SIFT) algorithm implemented through OpenCV. SIFT features are invariant to orientation and uniform scaling and are partially invariant to illumination changes and affine distortion<sup>[2]</sup>. Due to their robustness, SIFT features seemed ideal for a project which will be demonstrated in a variety of locations with varying lighting conditions and cameras.

**STEP 2:** Learn Visual Vocabulary  
The next step is to learn visual vocabulary from the features extracted in Step 1. To do this, the features are put into clusters using unsupervised learning. Specifically, this step with use K-Means Clustering to determine features which are related to each other. I used K-Means Clustering from the Scikit Learn Python package to do this.

**STEP 3:** Quantize Features using Visual Vocabulary  
Created a histogram of all the features  

**STEP 4:** Train Classifier  
Implemented a Support Vector Machine (SVM) through Scikit Learn which was trained on the extracted features.

#### Results  
The results of training on Dataset #2 are shown in the gif above. The details surrounding each dataset are below.    

Dataset #1
    - Contains images taken from phone of soda can and screwdriver
    - Training set
        - 51 images of soda can, 35 of screwdriver
    - Test set
        - 5 images of each
    - Accuracy: 0.859375 —> 85.94%

Dataset #2
    - Contains images taken from webcam of soda can and screwdriver
    - Training set
        - 193 images of each (85.78% of data)
    - Test set
        - 32 images of each (14.22% of data)
    - Accuracy: 0.953125 —> 95.31%

#### Tensorflow  
Relevant GitHub Repo:
[learning-tensorflow](https://github.com/apollack11/learning-tensorflow)

I also started looking into object recognition through Tensorflow. I started by completing the tutorials on Tensorflow found [here](https://www.tensorflow.org/tutorials/deep_cnn). One of the tutorials focused on recognizing handwritten digits using data from the MNIST dataset. This problem used a convolutional neural network to train a classifier to recognize handwritten digits. I extended the original solution to save the variables that defined the convolutional neural network so the model could be trained and then used to predict based on individual images. I was able to draw handwritten digits in GIMP and predict the number in the image based on the network. <!-- Below is an example image with prediction. -->  

### Future Work  
- Write custom SVM to train object recognition
- Improve robustness by collecting a wider variety of images
- Implement object recognition with the Baxter robot in our lab

**References**  
[1] Kitani, Kris. "Bag-of-Visual-Words." _Carnegie Mellon University_. Web. <http://www.cs.cmu.edu/~16385/lectures/Lecture12.pdf>.

[2] Lowe, David G. "Object Recognition from Local Scale-Invariant Features." _Proceedings of the Seventh IEEE International Conference on Computer Vision_ (1999): n. pag. Web.
