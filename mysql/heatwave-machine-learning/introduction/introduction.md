# Introduction

This workshop is based on [MySQL HeatWave User Guide: Iris Data Set Machine Learning Quickstart](https://dev.mysql.com/doc/heatwave/en/mys-hwaml-iris-quickstart.html)

HeatWave is a massively parallel, high-performance, in-memory query accelerator that accelerates MySQL performance by orders of magnitude for analytics workloads, mixed workloads, and machine learning. A HeatWave Cluster consists of a MySQL DB System and HeatWave nodes that store data in memory and process analytics and machine learning queries.

## About this Workshop

In this workshop, you will use the capabilities of HeatWave Machine Learning (ML) to implement a project which classifies species of Iris flowers. This project is also known as the Hello World version of Machine Learning. You will create and use a predictive machine learning model to step through preparing data, using the ML\_TRAIN routine to train a model, and using ML\_PREDICT\_ and ML\_EXPLAIN\_ routines to generate predictions and explanations. Finally, you will assess the quality of a model using the ML_SCORE routine and how to view a model explanation to understand how your model works.

The workshop uses the publicly available [Iris Data Set] (https://archive.ics.uci.edu/ml/datasets/Iris)  from the UCI Machine Learning Repository.

The Iris Data Set has the following data, where the sepal and petal features are used to predict the class label, which is

**type of Iris plant:**

- sepal length (cm)
- sepal width (cm)
- petal length (cm)
- petal width (cm)

**class of possible values:**

- Iris Setosa
- Iris Versicolour
- Iris Virginica

![three Iris flowers species](./images/iris-flowers.png "iris-flowers")

The sepal is the part that encases and protects the flower when it is in the bud stage. A petal is a leaflike part that is often colorful.

_Estimated Time:_ 2 hours

### About Product/Technology

HeatWave ML makes it easy to use machine learning, whether you are a novice user or an experienced ML practitioner. You provide the data, and HeatWave ML analyzes the characteristics of the data and creates an optimized machine learning model that you can use to generate predictions and explanations. An ML model makes predictions by identifying patterns in your data and applying those patterns to unseen data. HeatWave ML explanations help you understand how predictions are made, such as which features of a dataset contribute most to a prediction.

  ![Machine learning is easier with MySQL HeatWave](./images/heatwave-ml-easy.png "heatwave-ml-easy")

### Objectives

In this lab, you will be guided through the following steps:

- Get HeatWave MySQL environment details
- Connect to DB System using MySQL Workbench 
- Prepare and load training and test data
- Train the machine learning model
- Make predictions with test data using a trained model
- Run explanations on test data using a trained model
- Score your machine learning model to assess its reliability
- View a model explanation to understand how the model makes predictions

### Prerequisites

- Some Experience with MySQL Workbench - [MySQL Workbench] (https://www.mysql.com/products/workbench/)


## Acknowledgements

- **Author** - Anand Prabhu, Principal Member of Technical Staff, MySQL
- **Last Updated By/Date** - Anand Prabhu, Principal Member of Technical Staff, MySQL, August 2024
