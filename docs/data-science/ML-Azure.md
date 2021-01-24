[TOC]

# Azure Machine Learning

#### Sources
https://github.com/MicrosoftLearning/Data-Science-and-ML-Essentials/tree/master/Labs

#### Requirement
1. Anaconda

OR

1. Spyder (or IPython console)
2. scikit-learn
3. matplotlib
4. numpy

## Module 1: Intro to Data Science

#### Introduction
* Evolving subject, no single definition
* Requires a range of skills

Exploration and quantitative analysis of all available structured or unstructured data to develop understanding, extract knowledge, and formulate actionable results.

Data --> Decisions --> Actions

##### Data ---> What happened? -->  Why did it happen? --> What will happen? ---> Decision
Accidents like plane crashes etc

Areas of interest: Automatic Trading, Bidding

#### Steps

* Finding data sources
* Acquiring data
* Cleaning and transforming data, Reshaping (99% work)
* Relationship finding
* Decision

#### Types of Analytics

* Retrospective
* Real-time
* Predictive (Most ML falls under)
* Prescriptive
* Intelligent Saas apps (Cortana, ..)

##### Predictive vs Prescriptive

* Predictive analysis calibrated on past data, tells us what to expect
* Prescriptive analysis tells what actions to take

#### Historical Notes

* Big Data by astronomers Cox & Ellsworth in 1997
* By CCC in 2012
* By KDD in 1996

#### Big Data Process

##### CCC

* A

##### KDD

* A



# Module 1

## Chapter 4: Regression

#### Intro

#### Simple Linear Regression

#### Ridge Regression

#### Support Vector Machine Regression (SVM)

#### Cross-Validation

#### Nested Cross-Validation

* Popular evalution technique in ML
* Divide data set into 10 folds, pich one for test, reserve 1 for validation, and rest 8 as test data.



## Chapter 5: Classification

#### Intro
* Prediction of labels/predictable data - **X** (true/false or 1/-1) using independent variable/Feature/ - **Y**..

#### Decision Boundary 

#### Classification Error

#### Loss Functions

### Different ML Techniques & LFs

#### Logistic Regression

#### SVM Regression

#### AdaBoost Regression

#### Decision Tree

#### Boosted Decision Tree

#### Imbalanced Dataset

#### Minority Class Data (Excess amount, Weight)

#### ROC (Receiver Operating Characteristic) Curve

#### FPR & TPR (False Positive Rate & True Positive Rate)



## Chapter 6: Clustering

#### Intro
* Unsuperwised label prediction

#### Unsuperwised Learning
* Means training data has **no ground truth labels** to learn from 

### K- Means Clustering
* Input K = number of clusterss
* Randomly initialize centers
* Assign all the points to the closest centers 
* Repeat till convergence 

### Hierarchical Agglomerative Clustering
* Start with each point in its own cluster
* Repeatedly merge the clusters of the closest two points

#### Distance metrics are important
* Large impact on the solution
* Some algos uses "Adaptive" distance measures


## Chapter 7: Recommender Systems & Matrix Factorization

#### Intro
$$
\left(\begin{array}{cc} 
5 & * & 1 & 1\\
5 & * & 1 & 1
\end{array}\right)
$$ 

#### Example: 
Netflix contest

#### Options
* User-Based Collaborative Filtering
* Item-Based Collaborative Filtering

#### Matrix-Factorization

$$
Carmen_1 \left (\begin{array}{cc}
5 & 1
\end{array}\right)
$$

## Chapter 8: Intro to Data Science Technologies

#### Why Azure ML?
* Easy to deploy services on production

#### Supports?
* Sql
* R
* Python

#### Cortana Analytics Suite
* https://www.microsoft.com/cortanaanalytics
* Preconfigures Solutions
* Dashboard & Visualization
* Machine Learning & Analytics
* Azure Bigdata (Hadoop Implementation)
* Information Management

#### Azure ML Studio
* https://account.azure.com
* Experiments contain workflow
* Experiments constructed of modules
* Modules:
    * Transform Data
    * Compute Models
    * Score Models
    * Evaluate Models
* Create custom modules with SQL, R & Python

# Module 2: Working with Data

## Chapter 9
## Chapter 10
## Chapter 11: Data Sampling and Quantization
#### Azure ML Table Data Types:
* Numeric: Integer, Floating points
* Boolean
* String
* Date time
* Time span
* Categorial
* Image

#### Continuous Vs Catergorial Variables
Continuous: Countable, e.g. Time, Temperature, Counts*
Categorial: Classifiable, e.g. Gender, Type, City

$*$ descrete continuous

### Quantization
A range with sampled data.

#### What?
Continuous variables must be sampled

#### Sampling?
Digitizing the domain.
* Time stamped
* Precision

#### Example
* Temperature every minute
* Count over 1 hour

#### Quantization of Continuous Variable
Convert continuous variables into categorial using binning/categorizing.

Binning: Allocating each value into one category/bin.

Example:
* Small, Medium & Large

Module to use: Quantize Module

#### Extra

Metadata Editor

## Chapter 12: Data Cleansing and Transformation
(Data Munging)

* Deals with
    * Missing & repeated values
    * Outliers and errors
    * Scaling 
    * Filtering with custom code
* Iterative process
* Example: Forest-Fire Data

### Missing & Repeated Values
* are common
* many ML algos don't deal with missing values 
* repeated values bias results, so
    * search for them
    * make estimation
    * treat them

#### Clean Missing & Repeated values 
* remove rows
* substitute a specific value
* Interpolate values - Linear/polynomial on the basis of growth/trend of the data
* forward/backword fill
* With Azure ML Module: Clean Missing Data, Remove Duplicate Rows
* With R
    * Missing data: is.na()
    * Repeated data: duplicated()
* With Python
    * Missing data: pandas.isnull()
    * Repeated data: DataFrame.drop_duplicates()


### Errors & Outliers
* can bias model training, so
    * search for them
    * validate
    * treat them

#### Visualizing Outliers
* Scatter plot matrix
    * R - pairs plot
    * Python - pandas.tools.plotting.scatter_matrix
* Bar chart or graph 
* histogram

#### Clean Errors & Outliers
* Error treatment
    * Censor: remove entire row
    * Trim: trim the value inbetween a range
    * Interpolate: Linear or polynomial on the basis of growth/trend of the data
    * Substitute
* With Azure ML Module: Clip values (select column--> set lower/upper threshold)
* With R
    * data.frame = data.fram[filter.expression,]
* With Python
    * frame1 = frame1[(frame1["col1"] > 40.0) & (frame1["col2"] < 30.0) & (frame1["col3"] < 23.0)]
    

### Scaling Data
(aka Normalization, Transformation)
* Why:
    * to put all the numerical data into same range line -1 to 1 or 0 to 10 other than a:0-1, b:0-100, c:500:1000
    * not doing so:
        * will make adverse effect on training model
        * will get biased training model

* What:
    * looking at numerical features/columns
    * numerical features/variable/columns needs similar scale
    * Scaling methods:
        * zero mean & unit variance
        * min-max: all numeric values in range 0 to 1
        * logrithmic: does distributional changes (good for classification)
        * LogNormal: 
        * Hyperbolic tangent scaling: distribution transformation
    * ordered data like time-series may need to de-trend
    * scale after treating outliers
* How:
    * Azure ML Module: Normalize Data
    * R: 
    * Python:
* Doubts:
    * How to make such transformations?
    
# Module 3: Visualizing Data & EXploring Models

## Chapter 13: Data Exploration & Visualization

### Exploratory Data Analysis
* What:
    * Explore the data with visualization
    * Understand the relationships in the data
* How:
    * Create multiple views of data
    * Data conditioning: Poweful plotting method to project multiple dimension on two dimension page/screen
    
#### View of data
* Relationships in data can be complex
* Data exploration requires multiple views
* Conditioned (aka faceted, trellis, lattice) plots are ideal
    * project multiple dimension onto two
    * plots of subsets (group by)
    
#### Types of plots
* Scatter and line plots
* Bar: 
    * like histogram but
    * Used for categorical & factor data like disease, blood grp
    * Types: ordered, un-ordered
* Histogram:
    * used for continuos variable like time, temp
    * density or count are plotted on vertical axis
    * widely used
* Violin
* Q-Q
* Box: 
    * Shows 4 quartiles, i.e. 
        * a box divided in two half (by median), 
        * one upper vertical line, one lower and 
        * dot as outliers
* Line: connecting dot--> Polynomial regression--> curve




```python

```


```python

```
