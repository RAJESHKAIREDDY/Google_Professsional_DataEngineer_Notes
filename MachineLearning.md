# Types of MachineLearning

## Supervised ML:-
- It is used to make predictions.It learn from labelled data.
- ML model is used to predict a discrete value-->**Classification Model**.
- Eg:-Support Vector Machine(SVM),Decision Tree,Logistic Regression
- ML model is used to predict a continuous value-->**Regression Model**.
- Eg:- Linear Regression,Lasso & Ridge Regression,Random Forest Regression, Gradient Boost Regression(XGBoost)

## Unsupervised Learning:- 
- These algorithms learn by starting with unlabeled data and then identifying salient features, such as groups or clusters, and anomalies in a data stream.
- Eg:- K-means Clusering,K-Nearest Neighbour,Principal Component Analysis,Anomaly Detection Algorithms
    - **Clustering**: It is the process of grouping instances together based on common features. 
    - **Anomaly Detection**: It is a process of identifying unexpected patterns ins data.
    - **Collaborative Filtering**: It is widely used in recommendation systems such as netflix,google to provide personalized recommendations to users based on their past behavior and preferences.

## Reinforcement Learning:-
- It trains a model by interacting with it's environment & receiving feedback on the decision that it makes.
- It is especially useful in robotics and game playing.
- Eg:- Q-Learning,Monte Carlo Tree Search

## Deep Learning:
- It is not a kind of problem but a way to solve ML problems. It can be used with any of the three types of ML problems.

## ML Glossary

- The function that maps from inputs to outputs is known as an **activation function**
- eg:- Rectified Linear Unit(RELU),hyperbolic tangent function,Sigmoid Function.

 **Feature engineering** is the process of identifying which features are useful for building models. It also includes adding new features derived from existing features.
  - One Hot Encoding


- An **epoch** is the term used to describe one full pass over a training dataset by the training algorithm.

 **Learning rate**:- It is a hyperparameter that controls how much weights of a neural network are adjusted with each iteration during training.

 **Note**:-
1. Smaller learning rate can lead to longer training times.
2. learning rate that are too large can ignore optimal weights.

 **Bias** is the difference between the average prediction of a model and the correct prediction of a model.Models with high bias tend to have oversimplified representations of the process that generates the training data; this is underfitting the model

 **Variance** is the variability in model predictions. It helps to understand how model prediction differs across multiple training datasets.Models 
with high variance tend to overfit training data.

- models should have both **low bias and low variance**, and this is achieved by **lowering the mean squared error (MSE)** of the model by working through multiple training datasets.

 **Underfitting** creates a model that is not able to predict values of training data correctly or new data that was not used during training.
 - Underfitting would have resulted in poor performance with training data.  
 - Insufficiently complex models can lead to underfitting.
 - Underfitting occurs when a model does not capture relationships.

 **Overfitting** occurs when an ML model is trained too well on a particulart dataset & unable to generalize new data.This happens when 
there is noise in the data and the model fits the noise as well as the correct data points.To solve the overfitting problem in the scenario, you need to:
  -  Increase the training set.
  -  Decrease features parameters.
  -  Increase regularization.


 **Regularization**:- It is used to prevent overfitting & improve the generalization performance of a model. It helps to reduce the complexity of model, preventing overfitting which will improve accuracy & robustness of ML models.

  - **L1 regularization** calculates a penalty based on the absolute value of the weights.L1 regularization should be used when you want less relevant features to have weights close to zero.

  - **L2 regularization** calculates a penalty based on the sum-of-the-squares of the weights. L2 regularization should 
be used when you want outlier instances to have weights close to zero, which is especially useful when working with linear models.

  - **Dropout Regularization**: It is a regularization method to remove a random selection of the fixed number of units in a neural network layer. More units dropped out, the stronger the regularization.

 **Gradient Descent**: It is an optimization algorithm that helps us find the best parameters for our model by iteratively adjusting them in the direction that reduces the prediction errors, ultimately leading to better and more accurate predictions.
 -  Gradient descent is used to find the minimal RMSE or cost function.
 - **Batch Gradient Descent**: The **entire training dataset** is used to compute the gradients of the cost function with respect to the model parameters in each iteration.Also known as **vanilla gradient descent**.

 - **Stochastic Gradient Descent**: It is a variant of gradient descent that updates the model parameters for **each training example in the dataset**.
 
 - **Mini-batch Gradient Descent**: the gradients are computed on a **small random subset of the training dataset**, typically between 10 and 1000 examples

 **Backpropagation** is an algorithm used to train neural networks that calculates the **gradient of loss with respect to each weight** in the network using chain rule, propagating these gradients **backwards** from the output layer to update weights and minimize loss.

 **Cost Function** : It measures the error between predicted output of the model and the actual output.
 -   Cost Function & Loss Function are often interchangeable terms in ML.
 -   Cost Function more commonly used in ML.
 -   Loss Function more commonly used in Deep Learning.
 
## Neural Networks and its types

- **Artificial Neural Network(ANN)**  is one of the simplest variants of neural networks. They pass information in one direction, through various input nodes, until it makes it to the output node.
- Commonly used for regression and classification tasks.

-  **Recurrent Neural Networks (RNNs)** may not be suitable for **image classification tasks**, as they are more suitable for **sequential data or time series data** , such as **natural language processing**. 

- **Convolutional Neural Networks(CNN)** is designed for computer vision tasks, leveraging convolution operations to extract meaningful features from grid-like data, especially images.

## Evaluation models:-

- **Accuracy**:It tells you how often a classification model makes correct predictions. It measures the overall correctness of the model's predictions.
  - Accuracy = (TP + TN) / (TP + TN + FP + FN)

- **Precision**:It focuses on the accuracy of positive predictions made by the model. It measures how often the model correctly predicts positive instances out of all the instances it predicted as positive.
	- Precision = TP / (TP + FP)

- **Recall**: It is a measure of how many actual positive predictions are identified.Recall is also known as sensitivity.
  - Recall = TP / (TP + FN)

- **F1 Score**: It is harmonic mean of precision & recall.F1 scores are useful when you want to optimize a model to have balanced precision and 
recall.
-  It is also a good metric to use when evaluating models built with **imbalanced training sets**.
	- F1 Score = 2 * [(Precision * Recall) / (Precision + Recall)]

- data that is used for *evaluating hyperparameter choices* is known as **validation data**. 
- validation data set is used to tune hyperparameters.
-  **Test data**is **not used** for either **training or hyperparameter tuning**.

## Online vs Batch Prediction
![Alt text](image-3.png)



**Graphics Processing Units(GPU)**:- They  are accelerators that have multiple arithmetic logic units (ALUs), which implement adders and multipliers
- It is well suited to workloads that benefit from **massive parallelization**, such as **training deep learning models**.
- GPUs have high-bandwidth memory and typically outperform CPUs on fl oating-point operations.

**Tensor Processing Units**:- They are specialized accelerators based on ASICs and created by Google to improve the training of deep neural networks.
- TPUs perform **low-precision computation** with as little as 8-bit precision. Using low-precision computation allows for **high throughput**.
- TPUs can be used with **Compute Engine, Kubernetes Engine, and AI Engine**.
-  TPUs are **not recommended** for workloads that require **high-precision arithmetic**. 
- TensorFlow Lite, which is a framework for running machine learning models on mobile and IoT devices. 
- **1 TPU was 27 times faster at training than 8 GPUs**.

**Edge Computing**:- is the practice of moving compute and storage resources closer to the location at which it is needed.
- Edge computing is used when low-latency data processing is needed.





## ML API's

 **Vision**:- Allows you to derive insights from static images in the cloud or at edge,

**Cloud Vision API**: Cloud Vision API provides powerful image analysis capabilities, including Optical Character Recognition (OCR) technology, which can **extract text from images** of scanned documents, receipts, and other types of images.
- Vision AI API also provides for **batch processing**.

- **Cloud Video Intelligence API**: It provides models that can extract metadata; identify key persons, places, and things; and annotate video content. This service has pretrained models that automatically recognize objects in videos.

**Translation**:-
- Cloud Translation API
- Cloud Natural Language API

**Conversation**:-
- Cloud Text-to-Speech API
- Speech-to-text
- Dialogflow:- is used for chatbots, interactive voice response (IVR), and other dialogue based interactions with human speech. To understand intents behind customer commands and integrate with backend systems.
- Dialogflow is accessible through REST, gRPC, and client libraries. Client libraries are available for C#, Go, Java, Node.js, PHP, Python, and Ruby.

**Speech-to-Text** can be used to convert short duration audio in **synchronous** calls. As well as it is recommended **not to re-sample** the data, if it is coming at a lower sampling rate from the source.
- To process a speech recognition request for *long audio*, use **Asynchronous** Speech Recognition.

## GCP Options for Deploying ML Pipeline:
-  Cloud Auto ML
-  BigQuery ML 
-  Kubeflow 
- Spark ML

**Cloud Auto ML** :- It is a machine learning service designed for developers who want to incorporate machine learning in their applications without having to learn many of the details of ML. 
- It is  good to use when pre-trained API models are not sufficient for the task and need to train a model for a specific problem.

 **Several ML products**:-

 **AutoML Vision** :This service enables users to train their own machine learning models to classify images.

 **AutoML Video Intelligence**:It can be used to train machine learning models to classify segments of video using a custom set of labels.It can detect and track multiple objects through video segments.

 **AutoML Natural Language**: It enables developers to deploy machine learning applications that can analyze documents and classify them, identify entities in the text, and determine sentiment or attitudes from text.

 **AutoML Translation**:It is used to create custom tranlsation models.

 **AutoML Tables**: It builds machine learning models based on structured data.provide info on missing data,correlation,cardinalities.

 **BigQuery ML** enables users of the analytical database to build machine learning models using SQL and data in BigQuery datasets.
- It can be accesssed through BigQuery webUI,REST API,bq command-tool, External tools including Jupyter Notebooks
- It supports ML algorithms including **Linear regression,Binary logistic regression,K-means clustering, TensorFlow, Multiclass logistic regression for classification, DeepNeuralNetwork(DNN),MatrixFactorization(recommendation Systems) and PCA**

 **Note**:-
- AutoML Tables is a suitable choice when you want to optimize your model without extensive experimentation by automating feature engineering tasks and testing various algorithms.
- If minimizing model generation time is a priority, BigQueryML is a better option as it provides faster results by focusing on utilizing BigQuery's capabilities.

 **Kubeflow** is an open source project for developing, orchestrating, and deploying scalable and portable machine learning workloads.Kubeflow is designed for the Kubernetes platform.
- Kubeflow originally began life as a tool to help run TensorFlow jobs on Kubernetes, but it expanded to a multicloud framework for running ML pipelines. 
- Kubeflow can be used to run machine learning workloads in multiple clouds or in a hybrid cloud environment.

**Note**:- 
- Kubeflow is an ideal option for running machine learning workloads if you are familiar with Kubernetes Engine and have prior experience in building machine learning models.
- While Kubeflow enables scalable usage of machine learning models, it does not offer the same level of features as AutoML or the simplicity of BigQuery ML.

 **Spark MLib** is a comprehensive set of machine learning tools that can be used when deploying Cloud Dataproc clusters.

 **Note**:-
- Cloud AutoML is designed for developers who want to build on existing machine learning models and tools that automate some machine learning tasks, like feature engineering.
- BigQuery ML allows SQL users to build models within BigQuery and avoid having to export data and develop models using Python or Java.
- Kubeflow supports deploying scalable ML pipelines in Kubernetes.
- If you need an algorithm not available in other GCP machine learning services, consider using Spark MLib.
- Cloud Vision offers both pretrained models via an API and the ability to build custom models using AutoML Vision to provide flexibility depending on your use case.
- Cloud ML Engine is used to deploy models. It does not help to build the models.
- Deep and wide models are ideal for a recommendation application.**Wide models** are used for memorization. **Deep models** are for generalization.
- **TensorFlow Hub** is a repository of **reusable machine learning models** that have been **pre-trained** on large datasets and can be easily integrated into new applications with minimal effort.
-  TensorFlow Hub provides a wide range of models for various tasks such as **natural language processing, image recognition, and object detection**.
- Cloud Vertex AI is a **fully-managed machine learning platform** provided by Google Cloud that provides tools for building and deploying **custom ML models**. 
