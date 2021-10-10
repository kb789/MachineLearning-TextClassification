# Text Classification and Topic Modeling of the DBpedia Classes dataset
## Project Overview

The purpose of this project is build a machine learning model that will have the ability to classify the main topic of textual data. It will do this by “learning from” the training portion of a large dataset of articles that have been assigned main topics by humans. How effective this learning has been will be assessed when the model is given the opportunity to apply labels to the test portion of the dataset. The labels applied by the machine will be compared with the labels applied by humans, and the accuracy will be determined.

The model will learn from both the raw data itself—after it has been transformed into numerical data understandable by machines—and from the main topics that has been assigned by 3 additional algorithms. These algorithms do not learn from human-assigned labels; instead, they detect the main topics in a given corpus and then indicate how strongly or weakly each document in the corpus represents each of the main topics that had been detected in the corpus.

## Datasets

The [Kaggle dataset](https://www.kaggle.com/danofer/dbpedia-classes?select=DBP_wiki_data.csv) used in this project is an excerpt from data in DBPedia, which includes 342,782 wikipedia articles. Each article in this dataset is labeled with 3 hierarchical levels of categories. The first level is 1 of 9 categories, the second is 1 of 70 and the third is 1 of 219. This project uses the 219 categories in the third level as human applied labels for the articles. Because this dataset covers a vast, encyclopedic breadth of topics, it seems possible that a model that is trained by it could also successfully classify non-Wikipedia, non-DBpedia text. This theory will be tested by giving the model the chance to predict some text from outside the dataset.

## Problem Statement

This project is attempting to solve the problem of successfully classifying a large prelabeled dataset using a supervised learning technique. It is also trying to answer the question of whether topics detected by unsupervised learning techniques can be used as features to make the supervised learning technique more effective

## Implementation

The expected solution to the problem is as follows:

1.	Preprocess the text of the DBPedia articles and lemmatize it using the NLTK library

2.	Use three topic modeling algorithms—TruncatedSVD, Non-negative matrix factorization, and LatentDirichletAllocation—to find the main topics of the documents. Include these main topics as features, along with the preprocessed text, to train a Random Forest Classifier.

3.	Evaluate the efficacy of the model using the testing data. Tune the hyperparameters of both the Random Forest Classifier and the three topic modeling algorithms as needed.

4.	Test the final model on some text that is not part of the training/testing dataset


## Results and Assessment

The assessment of the model's results is twofold: first, the increase in accuracy from the benchmark model to the model with the features from the 3 topic modeling algorithms. The accuracy did improve, from 47% to 55%. The improvement caused by cleaning the data was negligible, so this 8% improvement can be attributed to the addition of the topic weights added by SVD, NMF, and LDA to the dataset. Second, the final accuracy of the model was 84%, an improvement of 36% in comparison with the benchmark model.

To further assess the robustness of the model, it was used to predict the classification labels of 4 documents that are not part of the dataset, DBPedia, or Wikipedia. To give the model a chance to work, documents were chosen that the dataset did have appropriate labels for. Overall, the classifier performed well. It  assigned the topic “Album” to [this excerpt](https://www.cnbc.com/2019/10/26/the-beatles-remain-a-pop-culture-phenomenon-even-among-gen-z-fans.html) from an CNBC article about Beatles’ albums still having strong sales among younger generations. It assigned the label “River” to an excerpt from [this Encyclopedia Britannica article](https://www.britannica.com/place/Nile-River) about the Nile River. It assigned “Golf Player” to this portion of the [biography on Tiger Woods’ website](https://tigerwoods.com/biography/). Finally it assigned “Planet” to a part of [this article](https://solarsystem.nasa.gov/planets/saturn/in-depth/) about Saturn on NASA’s website. Admittedly, the articles were somewhat “easy” in that they were pretty encyclopedic and had fairly clear, unambiguous topics. Still, the fact that they were from outside the dataset proves that this model does have some robustness.
