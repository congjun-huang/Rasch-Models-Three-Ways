# Rasch-Models-Three-Ways

This is a team project with members:
* Dahl, Nick - [nicholas.dahl@duke.edu](mailto:nicholas.dahl@duke.edu)
* Huang, Congjun - [congjun.huang@duke.edu](mailto:congjun.huang@duke.edu)
* Lu, Shiting - [shiting.lu@duke.edu](mailto:shiting.lu@duke.edu)
* Oblak, Christopher - [christopher.oblak@duke.edu](mailto:christopher.oblak@duke.edu)

## Background

A basic model for exploring logistic item response data is the Rasch
model where the goal is to model a subject’s performance on a task based
on a simple combination of their “ability” and the “difficulty” of the
question. Imagine we give an exam to
![J](https://latex.codecogs.com/svg.latex?J "J") subjects who then all
answer the same ![K](https://latex.codecogs.com/svg.latex?K "K")
questions, which are then marked correct
(![y\_{jk}=1](https://latex.codecogs.com/svg.latex?y_%7Bjk%7D%3D1 "y_{jk}=1"))
or
incorrect(![y\_{jk}=0](https://latex.codecogs.com/svg.latex?y_%7Bjk%7D%3D0 "y_{jk}=0")).
These data can then be modeled using,

![
\\text{Pr}(y\_{jk}=1) = \\text{logit}^{-1}(\\alpha_j - \\beta_k)
](https://latex.codecogs.com/svg.latex?%0A%5Ctext%7BPr%7D%28y_%7Bjk%7D%3D1%29%20%3D%20%5Ctext%7Blogit%7D%5E%7B-1%7D%28%5Calpha_j%20-%20%5Cbeta_k%29%0A "
\text{Pr}(y_{jk}=1) = \text{logit}^{-1}(\alpha_j - \beta_k)
")

where
![\\alpha_j](https://latex.codecogs.com/svg.latex?%5Calpha_j "\alpha_j")
is the *ability* of subject
![j](https://latex.codecogs.com/svg.latex?j "j") and
![\\beta_k](https://latex.codecogs.com/svg.latex?%5Cbeta_k "\beta_k") is
the *difficulty* of question
![k](https://latex.codecogs.com/svg.latex?k "k"). For our purposes we
will assume that all subjects completed all questions so that there is a
total of
![J \\times K](https://latex.codecogs.com/svg.latex?J%20%5Ctimes%20K "J \times K")
rows in our data. For a detailed review of Rasch models and some
considerations around identifiability see Section 14.3 Item-response and
ideal-point models from Data Analysis Using Regression and
Multilevel/Hierarchical Models (2006) by Gelman & Hill.

We have constructed a simulated data set of 200 students taking an exam
with 20 questions and the results are presented in `data/exam.csv`.
These data were simulated using the basic Rasch model described above,
so each student has a specific ability score and each question a
difficulty. For the sake of identifiability we will always assume that
the distributions of abilities have a mean of 0 while difficulties
do not.

## Step 1 - Data Cleaning

Starting from the given data, we will tidy it and construct any columns that are
necessary for the subsequent models in steps 2 - 5. All code for tidying
/ cleaning the data will occur in this section exclusively.

Once the tidying and cleaning is finished, we will construct a test / train
split of these data.

## Step 2 - Basic EDA

We will use these data (training split) to answer the following questions to the
best of our ability using summary statistics.

-   What is the average *difficulty* of the questions in these data?
    (Here and for all subsequent questions on difficulty we want to know
    the probability of getting an average question correct)
-   What was the hardest question based on these data?
-   Which student had the highest ability based on these data?

## Step 3 - Logistic Regression

We will use these data (training split) to fit a standard logistic regression
model using student id and question number as features. Once the model has been
fit we will answer the following questions based on our model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

## Step 4 - Mixed Effects

We will repeat the previous step but now fit a mixed effects model for these
data using statsmodels. We will make sure to justify our choice of what is
treated as a random effect and a fixed effect.

Once the model has been fit we will answer the following questions based on our
model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

## Step 5 - Bayesian Model

Finally, we will again fit these data (training split) but this time using a
Bayesian implementation of the Rasch model using PyMC3. As stated above
we will assume that ability has mean 0 and an unknown variance. For all
model parameters we will pick any reasonable weakly or non-informative prior and 
include at least some basic diagnostics showing that the model
converged.

Once the model has been fit we will answer the following questions based on our
model results:

-   What is the average *difficulty* of the questions according to this
    model?
-   What was the hardest question according to this model?
-   Which student had the highest ability according to this model?

## Step 6 - Comparison

We will summarize our findings from the previous 4 steps and discuss the
similarities and differences we have found between the models and EDA in
terms of the three questions. 

## Step 7 - Evaluation

We will compare the performance of the 3 models using out-of-sample data (test
split) by constructing and plotting ROC curves that also include the AUC
of each model. For the Bayesian model from step 5 we will use the posterior median or mean of the predicted
probabilities.
