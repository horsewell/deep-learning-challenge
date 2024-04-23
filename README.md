# deep-learning-challenge
 Challenge 21

## Background

The nonprofit foundation Alphabet Soup wants a tool that can help it select the applicants for funding with the best chance of success in their ventures. With your knowledge of machine learning and neural networks, you’ll use the features in the provided dataset to create a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup.

From Alphabet Soup’s business team, you have received a CSV containing more than 34,000 organisations that have received funding from Alphabet Soup over the years. Within this dataset are a number of columns that capture metadata about each organisation, such as:

* **EIN** and **NAME**—Identification columns
* **APPLICATION_TYPE**—Alphabet Soup application type
* **AFFILIATION**—Affiliated sector of industry
* **CLASSIFICATION**—Government organisation classification
* **USE_CASE**—Use case for funding
* **ORGANIZATION**—Organisation type
* **STATUS**—Active status
* **INCOME_AMT**—Income classification
* **SPECIAL_CONSIDERATIONS**—Special considerations for application
* **ASK_AMT**—Funding amount requested
* **IS_SUCCESSFUL**—Was the money used effectively

## Process

Step 1: Preprocess the Data
Step 2: Compile, Train, and Evaluate the Model
Step 3: Optimise the Model
Step 4: Write a Report on the Neural Network Model

## Output

The following files:

* [Alphabet Soup Charity](AlphabetSoupCharity.ipynb) - The main file with following the process to create a neural network.
* [Alphabet Soup Charity Optimisations](AlphabetSoupCharity_Optimisation.ipynb) - 5 variations to try and optimise for better results.

Five models were saved (one for each model) and can be found in the `models/` directory.

# Report on the Neural Network Mobels
## Overview

The purpose of this analysis was to create a neural network to classify applicants seeking funding from a nonprofit foundation as likely to be successful or not. The goal is to be able to predict with a 75% accuracy.

I decided to do 5 experiments with the optimisation phase seeing if any of the changes would be able to get accuracy of 75% or more. Each of these build a model that is saved into the models directory.

## Results:
### Data Preprocessing
- The target for the model is the `IS_SUCCESSFUL` column of the data.
- The variables for the model are the remaining 11 columns in the data.
- Two variables were removed from the input data.
    - The `EIN` column is a unique identifier for every row
    - The `SPECIAL_CONSIDERATIONS` column was removed because less than 0.1% of applicants have this as True, these would probably be processed individually.
    - NOTE: The original model removed the `NAME` column, the best optimized model kept it, (though only the top 30 Names remained after binning).

### Compiling, Training, Evaluating
- The best optimised model had 4 total layers
    - The input and first hidden layer had twice the number of features as neurons and used the `relu` activation function
        - 2x the number of features was chosen as the standard amount of neurons if 2-3 times the number of features
    - The third layer had the same number of neurons as features and used the `relu` activation function
        - 1x the number of features was chosen for this layer to help speed up training
    - The output layer had 1 neuron with a `sigmoid` activation function because the output was a binary 0 or 1

- The target performance was 75.6% with the 5th model, all other models and the original had an accuracy of around 72.5%.
- To get this accuracy, I kept the `NAME` column as described above as well as added an extra layer to the model. Binning the `INCOME_AMT` and `AFFILIATION` columns to reduce some of their smallest categories into a single group.


### Summary
Overall, the model was able to reach a target accuracy of 75%. Improvements to this model could be done with `keras-tuner` hyperparameter optimisation and/or by better cleaning of the data. Different combinations of layers and neurons, adding more binned features, as well as using `keras-tuner` did not meaningfully improve the model as show with Attempts 1-4.

There may also be a different type of model or activation function that I am not currently aware of that may be better suited for this problem.

