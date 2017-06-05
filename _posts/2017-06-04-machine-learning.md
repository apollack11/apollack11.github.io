---
layout: inner
title: 'Predicting the Presence of Lung Cancer using a CNN'
date: 2017-06-04 16:30:00
categories: tensorflow python
tags: machine-learning
featured_image: '/assets/lung_flythrough.gif'
lead_text: 'Final project for EECS349: Machine Learning'
---

Exploring the parameters of convolutional neural networks to create an accurate image classifier.

Final GitHub Repo: [EECS349_Project](https://github.com/njkaiser/EECS349_Project)

Contributors: Adam Pollack, Chainatee Tanakulrungson, Nate Kaiser  

### Summary  
The objective of this project was to predict the presence of lung cancer given a 40×40 pixel image snippet extracted from the [LUNA2016 medical image database](https://luna16.grand-challenge.org/data/). This problem is unique and exciting in that it has impactful and direct implications for the future of healthcare, machine learning applications affecting personal decisions, and computer vision in general. The medical field is a likely place for machine learning to thrive, as medical regulations continue to allow increased sharing of anonymized data for the sake of better care. Not only that, but the field is still new enough that our project implements methods at the forefront of technology.  

### Approach  
Due to the complex nature of our task, most machine learning algorithms are not well-posed for this project. There are currently two prominent approaches for machine learning image data: either extract features using conventional computer vision techniques and learn the feature sets, or apply convolution directly using a CNN. In the past few years, however, CNNs have far outpaced traditional computer vision methods for difficult, enigmatic tasks such as cancer detection. We decided to implement a CNN in TensorFlow, Google's machine learning framework.  

<div style="text-align: center;">
  <img src="/assets/cancerous_images.png" alt="Cancerous Images" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>Figure 1: Examples of <i>cancerous</i> images</p>
</div>

<div style="text-align: center;">
  <img src="/assets/non_cancerous_images.png" alt="Non-cancerous Images" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>Figure 2: Examples of <i>non-cancerous</i> images</p>
</div>

Because we collectively had limited experience with convolutional neural networks, we decided to first explore the hyperparameters of a CNN. We did so by creating an experiment in which we varied the kernel size and number of filters of each convolutional layer and the dropout rate for a total of 108 models. For this study, we kept a constant network architecture.

<div class="container">
  <div class="panel panel-default">
    <div class="panel-heading" style="text-align: center">
      <b>Hyperparameter Permutations</b>
    </div>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Attribute</th>
          <th>Values Tested</th>
        </tr>
      </thead>
      <tbody>
        <tr style="text-align: left">
          <td>Kernel Size (Convolutional Layer 1)</td>
          <td>3x3, 5x5, 7x7</td>
        </tr>
        <tr style="text-align: left">
          <td>Kernel Size (Convolutional Layer 2)</td>
          <td>3x3, 5x5, 7x7</td>
        </tr>
        <tr style="text-align: left">
          <td>Number of Filters (Convolutional Layer 1)</td>
          <td>16, 32</td>
        </tr>
        <tr style="text-align: left">
          <td>Number of Filters (Convolutional Layer 2)</td>
          <td>32, 64</td>
        </tr>
        <tr style="text-align: left">
          <td>Dropout Rate</td>
          <td>0.1, 0.2, 0.3</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

Each model was trained on 2,064 images (batch size of 104), validation was run every 10 epochs on another 442 images, and a final test was run after 500 epochs on another 442 images.

### Results  
After determining the best set of hyperparameters based on average peak validation accuracy, we then tested six new architectures based on these hyperparameters. The structure of each of these architectures was decided based on the principles described in the Stanford CS231n course notes<sup>[[1]](http://cs231n.github.io/convolutional-networks/)</sup>. After running the final six architectures at 500 epochs, we found the inflection point of the loss to be around 250 epochs. We then ran each of the six architectures for 250 epochs and recorded the final test accuracy. The best network architecture of these six achieved a test accuracy of 96.38%.

<div class="panel panel-default">
  <div class="panel-heading">
    <b class="panel-title">Final Network Architecture</b>
  </div>
  <div class="panel-body">
    Input &rarr; [Conv Layer 1 &rarr; ReLU] &rarr; Max Pool Layer 1 &rarr; [Conv Layer 2 &rarr; ReLU] &rarr; Max Pool Layer 2 &rarr; [Conv Layer 3 &rarr; ReLU] &rarr; Max Pool Layer 3 &rarr; [Fully-Connected Layer 1 &rarr; Dropout] &rarr; Fully-Connected Layer 2 &rarr; Output Classes [0 or 1]
  </div>
</div>

<div style="text-align: center;">
  <img src="/assets/final_model_accuracy.png" alt="Final Model Accuracy Graph" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>Figure 3: Tensorboard Graph of Accuracy for Final Model at 500 epochs (Orange Line = Training Dataset, Blue Line = Validation Dataset)</p>
</div>

<div style="text-align: center;">
  <img src="/assets/final_model_loss.png" alt="Final Model Accuracy Graph" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>Figure 4: Tensorboard Graph of Loss for Final Model at 500 epochs (Orange Line = Training Dataset, Blue Line = Validation Dataset)</p>
</div>

### Conclusion  
After finding our best model, we ran further analysis to extract a confusion matrix and misclassified images of the final test results to determine why this number was not closer to 100%.

<div class="container">
  <div class="panel panel-default">
    <div class="panel-heading" style="text-align: center">
      <b>Confusion Matrix</b>
    </div>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th></th>
          <th>Predicted Positive</th>
          <th>Predicted Negative</th>
        </tr>
      </thead>
      <tbody>
        <tr style="text-align: left">
          <td><b>Actual Positive</b></td>
          <td>226</td>
          <td>12</td>
        </tr>
        <tr style="text-align: left">
          <td><b>Actual Negative</b></td>
          <td>4</td>
          <td>200</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<div style="text-align: center;">
  <img src="/assets/misclassified_images.png" alt="Misclassified Images" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>Figure 5: Examples of misclassified images from the test dataset</p>
</div>

Our model classified more examples as negative when they should have been positive than vice versa. We believe this is because of the nature of some of the positive examples. For example, the first four misclassified images above are all positive examples of cancer even though two of them have almost no distinct features. It is likely that it would be just as difficult for a human to classify those images as a doctor. We also can't guarantee that the data we used is completely correctly classified; it is possible there are some mislabeled images.  

### Future Work  
We plan to test our model on entire scans of a lung by extracting 40x40 images from each image slice of the lung. Sliding a window with a stride of around 20 would give us a large set of images to test for cancer but with a pre-trained model, this would be relatively easy to do. Our hope is that this method would allow us to determine whether or not cancer is present in an entire lung instead of a predetermined section. We would also like to try implementing one or more named convolutional neural networks such as AlexNet<sup>[[2]](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)</sup> or Inception<sup>[[3]](https://arxiv.org/abs/1409.4842)</sup>.

### Final Report  
If you are intersted in learning more about the details of this project, please read our
<a href="https://apollack11.github.io/EECS349_Report.pdf" target="_blank">report</a>.

### References  
[1] Stanford Course Notes on CNNs: <http://cs231n.github.io/convolutional-networks/>  
[2] AlexNet: <http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks>  
[3] Inception (by Google): <https://arxiv.org/abs/1409.4842>
