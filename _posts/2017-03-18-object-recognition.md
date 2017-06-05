---
layout: inner
title: 'Object Recognition with Baxter'
date: 2017-03-18 03:30:00
categories: python scitkit-learn ros
tags: machine-learning
video_format: vimeo
featured_video_id: 218413450
lead_text: 'Winter Project for Northwestern MSR Program'
---

Implementation of the Bag of Words method for object recognition.

<!-- featured_image: '/assets/object_recognition.gif'
featured_image_alternate: '/assets/hand_points.jpg' -->

Final GitHub Repo: [object-recognition](https://github.com/apollack11/object-recognition)  

### The Goal
I hadn’t gotten a chance to explore machine learning yet at Northwestern, so I decided to center my winter project around the topic. Exploring object recognition seemed like a straightforward yet interesting way to do so. I set out to learn the basics of machine learning and to create a fully-functioning object classifier which could be used on the Baxter robot in our lab to locate and pick up objects.  

### Methodology  

#### Bag of Words
The video above this post shows the results of a trained classifier using the bag of words method. Bag of words is a four step process which consists of the following<sup>[1]</sup>:

**STEP 1:** Extract Features  
This step aims to simplify images into a set of smaller features so the classifier doesn’t need to train on every pixel of every image. These features should be unique and should not depend on orientation or scaling. For this step I used the scale-invariant feature transform (SIFT) algorithm implemented through OpenCV. SIFT features are invariant to orientation and uniform scaling and are partially invariant to illumination changes and affine distortion<sup>[2]</sup>. Due to their robustness, SIFT features seemed ideal for a project which will be demonstrated in a variety of locations with varying lighting conditions and cameras.

**STEP 2:** Learn Visual Vocabulary  
The next step is to learn visual vocabulary from the features extracted in Step 1. To do this, the features are put into clusters using unsupervised learning. Specifically, this step with use K-Means Clustering to determine features which are related to each other. I used K-Means Clustering from the Scikit Learn Python package to do this.

**STEP 3:** Quantize Features using Visual Vocabulary  
Created a histogram of all the features  

**STEP 4:** Train Classifier  
Implemented a Support Vector Machine (SVM) through Scikit Learn which was trained on the extracted features.  

#### Baxter Implementation  
After completing a working version of a three object classifier, I began work on enabling Baxter to recognize and pick up objects from the table in front of him. To interface with Baxter, I used the Robot Operating System (ROS) in multiple python scripts. One script activated the camera in Baxter's hand performed object recognition on each of the three sections of the image and published the location and name of each object as a message. Then a second script sends a desired object message which is read by a third script which moves Baxter's arm to the location of the object and picks it up. For more specifics of this system, please look at the [README](https://github.com/apollack11/object-recognition) for the repo.

#### Results  
The results of training on the Final Dataset are shown in the video above.

Final Dataset  
- Contains images taken from Baxter’s hand camera of an eraser, marker, and screwdriver
- Training set
    - 171 images of each (85.07% of data)
- Test set
    - 30 images of each (14.93% of data)
- Accuracy: 0.96667 &rarr; 96.67%

<!-- #### Tensorflow  
Relevant GitHub Repo:
[learning-tensorflow](https://github.com/apollack11/learning-tensorflow)

I also started looking into object recognition through Tensorflow. I started by completing the tutorials on Tensorflow found [here](https://www.tensorflow.org/tutorials/deep_cnn). One of the tutorials focused on recognizing handwritten digits using data from the MNIST dataset. This problem used a convolutional neural network to train a classifier to recognize handwritten digits. I extended the original solution to save the variables that defined the convolutional neural network so the model could be trained and then used to predict based on individual images. I was able to draw handwritten digits in GIMP and predict the number in the image based on the network. <!-- Below is an example image with prediction. -->   -->

### Future Work  
I would like to take the knowledge I learned while working on my final project for EECS349 Machine Learning and train a CNN on the ImageNet dataset for three different objects. I believe this would greatly improve the robustness of the system.


**References**  
[1] Kitani, Kris. "Bag-of-Visual-Words." _Carnegie Mellon University_. Web. <http://www.cs.cmu.edu/~16385/lectures/Lecture12.pdf>.
[2] Lowe, David G. "Object Recognition from Local Scale-Invariant Features." _Proceedings of the Seventh IEEE International Conference on Computer Vision_ (1999): n. pag. Web.
