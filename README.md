# Neural Network Charity Analysis
## Overview
In this project we use [charity_data.csv](Resources/charity_data.csv) to create a neural net to predict the likelihood that charitable organization will succeed when given financial support.

## Results
### Data Preprocessing
- The `IS_SUCCESSFUL` feature is the target variable of the analysis
- The following are the input features of the model (this will be altered in the optimization section):
    
    - `APPLICATION_TYPE`
    - `AFFILIATION`
    - `CLASSIFICATION`
    - `USE_CASE`
    - `ORGANIZATION`
    - `STATUS`
    - `INCOME_AMT`
    - `SPECIAL_CONSIDERATIONS`
    - `ASK_AMT`
- `EIN` and `NAME` are neither targets nor features and are removed from the analysis all together.
### Compiling, Training, and Evaluating the Model
- The architecture of the neural net is as follows:
    - 9 input neurons (due to the size of the data)
    - 1st Hidden Layer: 7 neurons, using ReLU activation function
    - 2nd Hidden Layer: 3 neurons, using ReLU activation function
    - Output layer: 1 neuron, using Sigmoid activation function
    
    The choice of this architecture was somewhat random in choice simply to see how the model would perform. However the Sigmoid activation function in the output layer was used to make use of its range of [0,1] because this is a classification task.
- With the above initial architecture, the was a test accuracy of 73.10% which is below the 75% target.

## Optimization
Three attempts were made to improve the model. The following are the changes for those attempts and the results:
- Attempt 1: 
    - The `STATUS` and `SPECIAL_CONSIDERATIONS` features were dropped from the analyis because the data is divided between them 34,294 to 5 and 34272 to 27 respectively. The data is more or less even divided between being the target variable, so these imbalanced features are only adding unnecessary noise.
    - The number of epochs is reduced to 50 due to the training converging quickly in the initial training above.
    - `APPLICATION_TYPE` bins are reduced from 9 to 6
    - `CLASSIFICATION` bins are reduced from 6 to 4
    - Results:
        - Test accuracy: 72.69%
- Attempt 2:
    - `INCOME_AMT` is binned into those that have income and those that do not. 24,388 charities have no income, 9911 have some.
    - Results:
        - Test accuracy: 72.29%
- Attempt 3:
    - Only the model architecture was changed for this attempt, otherwise keeping all changed from attempt 2:
        - 7 input neurons (due to size of data)
        - 1st Hidden Layer: 19 neurons, using ReLU activation function
        - 2nd Hidden Layer: 7 neurons, using ReLU activation function
        - 3rd Hidden Layer: 3 neurons, using ReLU activation function
        - Output Layer: 1 neuron, using Sigmoid activation function
    - Results:
        - Test accuracy: 72.57%

## Summary
Overall, even with optimization the above did not reach the target goal 75% accuracy. I suspect that an optimal number of layers and neuron would be able to learn this task. Further attempts at optimization would primarily involce altering this