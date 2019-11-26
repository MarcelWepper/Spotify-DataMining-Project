# Spotify_DataMining_Projet

Based on to: https://github.com/mdeff/fma
Coded by: @stetzlaff, @l0wsk1ll3d, @MarcelWepper

# 1 Problem
In the modern society music is as present as ever, so economic interest is increasingas well.  From the business perspective, popular songs are evidently more desired than others.  Thus the question arises, wether these certain hit songs have some-thing in common, which makes them more popular than others.  Especially if this commonality can be measured, analyzed and predicted for new songs. This project work deals with the problem, if and how a songs popularity maybe predicted by its audio features.  Applied to machine learning, this task can be mapped to the area of classification.  In this context the class of interest contains the most popular songs.
# 2  Data
The dataset considered in this project consits of multiple parts. The first part of the data holds songs and their meta data as well as their sound features. The sound features  where  extracted  from  the  original  freely  available  audio  files  using  the python package librosa, by a research team of the MIT. In total the data offers 518 numerical attributes for over 100,000 songs. To predict the popularity of these songs, an estimation of popularity is required. Spotify, a commonly used music streaming service, provides meta data for eachsong available on their plattform. This metadata can be requested by users via the Spotify REST API and contains a measure of popularity on a scale from 1 to 100, 100 being most popular. For every track in the first part of the data set, the popularity score will be requested from the Spotify interface and serve as the target label for classification. Therefore only the tracks available on Spotify will be considered.
# 3  Approach
In this section, the proposed data mining approach will be explained in chronological order.
## 3.1  Preprocessing
Since the raw dataset will not proove any value for the proposed methods, it has to be preprocessed beforehand.
* The first step of preprocessing envolves checking the data for duplicates and missing values and handling them, in case there are any.
* Since classifiers usually struggle with a high number of classes and there are 100 popularity labels, it will proove beneficial to either bin them into groupsor transform them into binary classes.
* To enable classifiers, which depend on distance metrices as similarity measures,  the  numerical  attributes  will  be  standardized  to  a  mean  of  0  and  a standard deviation of 1.
* Depending on the size of the subset of songs available on Spotify, the dataset will be downsampled to reduce computational costs.
* Having a high number of attributes might on the one hand deplete available computational resources and on the other hand introduce unwanted noise. Thus feature selection will be applied to reduce the number of attributes.
* The dataset will be split in multiple training and test sets using Cross-Validation. This enables preformance evaluation of the classifiers.
* Depending on the class distribution in the training data, the amount of songs for each target label in the training set will be balanced using resampling methods like up- or downsampling.
## 3.2  Methods
After the dataset was adequatly prepared, following classifier algortihms will be applied to allow the popularity estimation of songs. Instead of applying higher complexity algorithms (e.g. neural nets) that require more time investment to function, this work will focus on a set of simpler algorithms. Since the implementation of these methods consumes fewer project resources, more of them can be tried outand later be evaluated against each other.
* K-nearest-neighbors (knn) is most likely the easiest of the available classifiers. Nevertheless it can be applied for most classification scenarios and will serve as an appropriate first estimator.
* Compared  to  the  prediction  focused  approach  of  knn,  desicion  trees  also allow to gain insights of the relation between the audio features and the popularity. Thus desicion trees will be the second applied algorithm.
* The  maximal  margin  classifier  is  a  simple  method,  which  assumes  linear boundaries between classes. This assumption makes it impractial for mostdatasets but provides the foundation for support vector classifiers (svc). Through the extension of the linear assumption in svc, they can be applied to a broader range of problems and will serve as the third algorithm for prediction. If the project ressources allow further implementations, other simple algorithms like Naive Bayes or stochastic gradient descent (sgd) will be added to this list.
## 3.3  Evaluation Methods
In the final phase of this project work the perfomance of the mentioned algorithms will be evaluated critically and compared.  Model accuracy will be predicted for every method through Cross-Validation.  Using the estimated confusion matrices Precision and Recall will be examined and combined into the F1 measure to quantize the estimated model perfomance. Also receiver operating characteristic (ROC) curves will be plotted for the mentioned methods and the respective areas undercurve (AUC) will be computed as well. This set of measures will allow a thorough examination of perfomance of each trained learning algorithm. In order to increase these perfomances, the hyperparameters of the algorithms will be tuned as well.
# 4  Expecations
Since the selection of algorithms focuses on easier implementable methods,  the danger of underfitting the problem is present. The application of these methods are simple because their model assumptions are simple. This poses the possible downside, that the simple assumptions might not be able to grasp the potentially high complexity of the relationship between a songs popularity and its sound features. Another difficulty lies within the dataset itself. Looking at the high numberof attributes leads to a potential problem with a phenomenon called the curse of dimensionality. In high dimensional space data becomes sparce and algorithms might struggle to identify patterns within the data. Thus it is to be expected that the methods perfomances exceed just slightly or not at all the baseline of naively progonosing the majority class.
