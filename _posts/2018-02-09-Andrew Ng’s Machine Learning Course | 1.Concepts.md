---
layout: post
title:  "Andrew Ng’s Machine Learning Course |1.Concepts"
date:   2018-02-09
excerpt: "What is machine learning? We will try to define what it is and also try to give you a sense of when you want to use machine learning. "
tag:
- Machine Learning 
comments: true
---

Even among the machine learning practitioners there isn't a well accepted definition of what it is and what it isn't machine learning. But many people have tried to defined them.

# Machine Learning definition
* Arthur Samuel(1959) : Field of study that gives computers the ability to learn without being explicitly programmed.
* Tom Mitchell (1998) : A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.  

A checkers learning problem: 
* Task T: playing checkers
* Performance measure P: percent of games won against opponents 
* Training experience E: playing practice games against itself
  
We can specify many learning problems in this fashion, such as learningto recognize handwritten words, or learning to drive a robotic automobile autonomously.


# Machine learning algorithms:
* Supervised learning
* Unsupervised learning  

Others : Reinforcement learning, recommender systems.

---
layout: post
title:  "Andrew Ng’s Machine Learning Course | 1-2 Supervised Learning"
date:   2018-02-09
excerpt: "We're going to define what is probably the most common type of machine learning problem, which is supervised learning."
tag:
- Machine Learning 
comments: true
---
# Definition
Let’s start by talking about a few examples of supervised learning problems.Suppose we have a dataset giving the living areas and prices of 47 housesfrom Portland, Oregon:  
  
|Living area(feet^2)|Price(1000$s)|  
|-|-|  
|2104|400|  
|1600|330|  
|1416|232|  
|3000|540|  
|...|...|  
  
We can plot this data:
![](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/2018-2-10-1.PNG)
  
Given data like this, how can we learn to predict the prices of other housesin Portland, as a function of the size of their living areas?

To establish notation for future use, we’ll use <img src="http://latex.codecogs.com/gif.latex?\inline&space;x^{(i)}" title="x^{(i)}" /> to denote the “input” variables (living area in this example), also called input features, and <img src="http://latex.codecogs.com/gif.latex?\inline&space;y^{(i)}" title="y^{(i)}" /> to denote the “output” or target variable that we are trying to predict(price). A pair <img src="http://latex.codecogs.com/gif.latex?\inline&space;(x^{(i)},&space;y^{(i)})" title="(x^{(i)}, y^{(i)})" /> is called a training example, and the dataset that we’ll be using to learn—a list of m training examples <img src="http://latex.codecogs.com/gif.latex?\inline&space;\{&space;(x^{(i)},y^{(i)};i=1,...,m\}" title="\{ (x^{(i)},y^{(i)};i=1,...,m\}" /> is called a training set. Note that the superscript “(i)” in thenotation is simply an index into the training set, and has nothing to do with exponentiation. We will also use X denote the space of input values, and Y the space of output values. In this example, X = Y = R.To describe the supervised learning problem slightly more formally, our goal is, given a training set, to learn a function h : X → Y so that h(x) is a “good” predictor for the corresponding value of y. For historical reasons, this function h is called a hypothesis. Seen pictorially, the process is therefore like this:  
![](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/2018-2-10-2.PNG)  
  
  
  

When the target variable that we’re trying to predict is continuous, such
as in our housing example, we call the learning problem a **regression problem**.
When y can take on only a small number of discrete values (such as
if, given the living area, we wanted to predict if a dwelling is a house or an
apartment, say), we call it a **classification problem**.
