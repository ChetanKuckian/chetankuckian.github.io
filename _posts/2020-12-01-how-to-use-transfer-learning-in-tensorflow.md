---
title: "How to use Transfer Learning in TensorFlow"
categories: "Data Science"

excerpt: "How to use TensorFlow to apply transfer learning to a real life data set."

header:
    teaser: "./assets/images/posts/how-to-use-transfer-learning-in-tensorflow/teaser.jpg"
    caption: "Model Output"
---


Transfer Learning is a brilliant feature provided by TensorFlow. It helps to train new models by taking help from already trained models. Consider that you want to train a model for predicting number of certain objects in an image but do not have enough images to train with, we can then leverage the already trained models to our advantage and tweak them to get our result without training the model for a huge dataset and spend a lot of time and computation on training.

In this I will explain how to leverage transfer learning for a Face Counting Challenge dataset from Analytics Vidhya.

Link to the Dataset:*[Face Counting](https://datahack.analyticsvidhya.com/contest/vista-codefest-computer-vision-1/)
*

First we would need to read the images and the target values into an numpy array. I have shared the link to the notebook where the entire code is present.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/loading_data_into_numpy_arrays.jpg" alt="continous integration diagram">
    <figcaption>Loading data into numpy arrays</figcaption>
</figure>

Now we load our base model into a variable. Here MobileNetV2 model which is present in TensorFlow is used. We provide the input shape of the image and load the weights using ‘imagenet’. This means that the base model was trained on the imagenet dataset. We set the base model’s training to False so that we do not go through the whole process of training those layers again.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/loading_base_model.jpg" alt="continous integration diagram">
    <figcaption>Loading Base Model</figcaption>
</figure>

Now we can see the base model’s layer by printing the model summary to check if the model is loaded properly.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/model_summary_1.jpeg" alt="continous integration diagram">
    <figcaption>Model Summary</figcaption>
</figure>

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/model_summary_2.jpeg" alt="continous integration diagram">
    <figcaption>Model Summary</figcaption>
</figure>

From the summary we can see that the base model has been loaded successfully. The base model takes the input of shape (224,224,3) and the last layer of the model is of (7,7,1280). Now we build our model on top of this model.

First we get the last layer of the output and also create a input layer which gives the data according to the base models requirement eg: the model may require data normalized between [-1,1] or [0,1] depending on how it was trained.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/setting_the_preprocess_input_layer.jpeg" alt="continous integration diagram">
    <figcaption>Setting the preprocess input layer and the last layer from the base model</figcaption>
</figure>

Now we can Flatten the last layer and add a few Dense layers according to our need or add a few more Convolutions and create the model according to our requirement.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/building_own_model.jpeg" alt="continous integration diagram">
    <figcaption>Building our own model on top of base model</figcaption>
</figure>

Once the model is built we can then compile the model, here we have kept the last layer without any activation because we are trying to predict the number of human faces in the image.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/compiling_the_model.jpeg" alt="continous integration diagram">
    <figcaption>Compiling the model
</figcaption>
</figure>

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/training_the_model.jpeg" alt="continous integration diagram">
    <figcaption>Training the model</figcaption>
</figure>

We can then plot the model’s history to see the loss in training and validation. Here we can see that the training curve is quite smoothly decreasing showing that the model’s training was stable.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/training_and_validation_loss.jpeg" alt="continous integration diagram">
    <figcaption>Training and Validation loss of the Model</figcaption>
</figure>

When we submit the prediction of test data we get an RMSE of 1.86 which comes in the top 100 of the predicted scores.

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/prediction_outcome.jpeg" alt="continous integration diagram">
    <figcaption>Prediction Outcome</figcaption>
</figure>

The entire code for this is present here:https://colab.research.google.com/drive/1wWRScvK2B6ACi6eusuvEiBtBGwJyOAve?usp=sharing

Please checkout the code which uses multiple transfer learning models to predict the output for this dataset which gave an RMSE of 1.68 and the rank of 82 at the moment this story is being written:https://github.com/LosingCoder/MachineLearning/tree/master/Face%20Counting%20Challenge

<figure>
    <img src="/assets/images/posts/how-to-use-transfer-learning-in-tensorflow/rank.jpeg" alt="continous integration diagram">
    <figcaption>Rank</figcaption>
</figure>
