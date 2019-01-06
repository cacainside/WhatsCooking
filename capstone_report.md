# Machine Learning Engineer Nanodegree
## Capstone Project
Man-Fong Cheng  
January 6th, 2019

## I. Definition
_(approx. 1-2 pages)_

### Project Overview

This project is about Kaggle's What's Cooking[3], which is a interesting topic to use recipe ingredients to categorize the cuisine. I choose this topic because I love eating cuisine from different countries, so I would be extremely happy to work with data with recipe information.

### Problem Statement
It is a supervised multi-class classification problem because the result should categorize the recipe into cuisine type, such as Chinese cuisine, Japanese cuisine or Italian cuisine, etc. The input data is list of ingredients for making cuisine,  which is non-structured text format. However, the ingredients are not sentences and steps, they are just word, which make it easier to pre-process. For the solution algorithm, I choose XGBoost [1].

### Metrics
I would use accuracy to evaluate the model.


## II. Analysis
_(approx. 2-4 pages)_

### Data Exploration

-  There are train data-set and test data-set. And it is JSON format. 
-  Data  includes **39774 recipes ids** with list of ingredients and type of cuisine, and I use train_test_split, split 20% as testing data. Because there's no label at test data from Kaggle, That's why I chose to split train data to test data.
-  Here are an example of train data.
e.g. 
 {  
 "**id**": 24717,  
 "**cuisine**": "indian",  
 "**ingredients**": [  
     "tumeric",  
     "vegetable stock",  
     "tomatoes",  
     "garam masala",  
     "naan",  
     "red lentils",  
     "red chili peppers",  
     "onions",  
     "spinach",  
     "sweet potatoes"  
 ]  
 },
 
The input features include cuisine, id and ingredients. Let's discuss them below:
- id: It's discrete integer, and it is meaningless to our project.
- cuisine: There are **20 unique types of cuisines** in the data set, which means we are going to have 20 classes. There's no missing cuisine in this dataset. The highest frequncy cuisine in our dataset is italian, which includes 7838 cuisine. And we need to do one hot encoding to make cuisine appear in 0 and 1 in each type.
- Ingredients: There are ** 39774 cuisines**, and each of them have their own ingredients. There are some ingredients of cuisine are not unique. For 39774 cuisines we got 39674 unique ingredients. However, I don't think it matters, so cuisine use have same ingredients, but with different process step and ingredient's quatity make them different food. So I will not deal with the uniqueness of ingredients. There's no missing ingredients in this dataset, every cuisine has its own ingredients. However, as above mentioned in cuisine feature, ingredients also need to use one hot encoding to transfer data into 0 and 1 for further process.


### Exploratory Visualization
As below, we can see each cuisine count from dataset. The highest frequncy cuisine in our dataset is italian, which includes 7838 cuisine. And we need to do one hot encoding to make cuisine appear in 0 and 1 in each type.
![Alt text](https://github.com/cacainside/WhatsCooking/blob/master/2019-01-06%2021.59.22.png "Cuisine ")


### Algorithms and Techniques
I am going to use XGBoost as my algorithm, I will input ingredients as data, and cuisine as target. XGBoost has hyperparameterm and I will use grid search to pick a better one. And all the input data need to transfer by one hot encoding.

### Benchmark
SVM is my benchmark, I use my preprocess data and run SVM, with parameter C: 0.5, and tolerance :1e-3. And I got 0.9611 accuracy from test data, which is very high.

## III. Methodology
_(approx. 3-5 pages)_

### Data Preprocessing
In data preprocessing part, I first check top 10 ingredients in each cuisine, and we can see many similar ingredients, based on my google result, I list this can be seens as the same, and I will assign it as same while data preprocessing
scallions = Green Onions [1]
black pepper = pepper [2]
eggs = large eggs [4]
extra-virgin olive oil = olive oil [5]
garlic = garlic cloves

And then stemming [2] (potatoes and potato should be the same ingredients), also I do capitalize. And one hot encoding.

### Implementation

- Data exploration: Explore the whole data, and make sure there's no missing data.
- Data pre-processing: 
  - combine into same ingredient (As above mention)
  - stemming (porterStemmer)
  - capitalize
  - One Hot encoding (CountVectorizer, LabelEncoder, label_binarize)
- Training:XGBoost, and using grid search (learning_rate:  0.01, 0.1, max_depth: 3, 6)
- Testing: I am going to test my model from previous training result.

There's no any complications with the original metrics or techniques that required changing prior to acquiring a solution.



### Refinement
These no refinement in this report, initial solution and final solution is the same.


## IV. Results
_(approx. 2-3 pages)_

### Model Evaluation and Validation

- _Is the final model reasonable and aligning with solution expectations? Are the final parameters of the model appropriate?_
- _Has the final model been tested with various inputs to evaluate whether the model generalizes well to unseen data?_
- _Is the model robust enough for the problem? Do small perturbations (changes) in training data or the input space greatly affect the results?_
- _Can results found from the model be trusted?_

### Justification
In this section, your model’s final solution and its results should be compared to the benchmark you established earlier in the project using some type of statistical analysis. You should also justify whether these results and the solution are significant enough to have solved the problem posed in the project. Questions to ask yourself when writing this section:
- _Are the final results found stronger than the benchmark result reported earlier?_
- _Have you thoroughly analyzed and discussed the final solution?_
- _Is the final solution significant enough to have solved the problem?_


## V. Conclusion
_(approx. 1-2 pages)_

### Free-Form Visualization
In this section, you will need to provide some form of visualization that emphasizes an important quality about the project. It is much more free-form, but should reasonably support a significant result or characteristic about the problem that you want to discuss. Questions to ask yourself when writing this section:
- _Have you visualized a relevant or important quality about the problem, dataset, input data, or results?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Reflection
In this section, you will summarize the entire end-to-end problem solution and discuss one or two particular aspects of the project you found interesting or difficult. You are expected to reflect on the project as a whole to show that you have a firm understanding of the entire process employed in your work. Questions to ask yourself when writing this section:
- _Have you thoroughly summarized the entire process you used for this project?_
- _Were there any interesting aspects of the project?_
- _Were there any difficult aspects of the project?_
- _Does the final model and solution fit your expectations for the problem, and should it be used in a general setting to solve these types of problems?_

### Improvement
In this section, you will need to provide discussion as to how one aspect of the implementation you designed could be improved. As an example, consider ways your implementation can be made more general, and what would need to be modified. You do not need to make this improvement, but the potential solutions resulting from these changes are considered and compared/contrasted to your current solution. Questions to ask yourself when writing this section:
- _Are there further improvements that could be made on the algorithms or techniques you used in this project?_
- _Were there algorithms or techniques you researched that you did not know how to implement, but would consider using if you knew how?_
- _If you used your final solution as the new benchmark, do you think an even better solution exists?_

-----------
[1] https://www.thekitchn.com/whats-the-difference-between-spring-onions-scallions-and-green-onions-word-of-mouth-217111 
[2] https://www.chefsteps.com/ingredients/black-pepper 
[3] https://www.kaggle.com/c/whats-cooking
[4] https://www.thespruceeats.com/egg-size-conversions-1328750
[5] https://www.thekitchn.com/whats-the-difference-between-olive-oil-and-extra-virgin-olive-oil-word-of-mouth-218767

**Before submitting, ask yourself. . .**

- Does the project report you’ve written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Analysis** and **Methodology**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your analysis, methods, and results?
- Have you properly proof-read your project report to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
- Is the code that implements your solution easily readable and properly commented?
- Does the code execute without error and produce results similar to those reported?
