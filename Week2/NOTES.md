# Week 2 Notes

## Steps for creating the Linear Regression model

- Get the dataset to be used for training the model
- Divide the dataset into training, validation and test datasets
    - Use 60%, 20%, 20% distribution for the training, validation and test datasets

    - Remove the NaN (null) values from the datasets either using 0 or mean of the particular feature
    
    - Get the feature to be predicted (y) from the datasets and store them separately to be used later for verification
    
    - Delete the 'y' variable from the divided datasets so that the model does not use them accidentally
- Create a method to use linear regression method to find the weights (w) using the available data in the training dataset
    - Linear Regression Equation: g(x) ≈ y ⇒ (X)w ≈ y ⇒ (X^-1)(X)(w) ≈ (X^-1)y ⇒ **w ≈ (X^-1)(y)**
    - The inverse is possible only for a square matrix and the feature matrix (X) does not necessarily is available in a square matrix form due to the difference in the number of features available and the records in the matrix.
    - To handle this, we find the inverse of the **Gram matrix (XTX i.e., product of X and its transpose, XT)** of the feature matrix (X) and use it to find the approximate value of the weights (w) to be used for prediction.
    - This model becomes Normal linear regression model.

        > - Simple Linear Regression Equation: *Xw = y*
        > - Multiplying by transpose of X, *XT* on both sides,
        >
        >   >    *XT.X.w = XT.y*
        > - Multiplying by the inverse of the Gram matrix (XTX) to get the the value of w, we get,
        >
        >   >    *(XTX)^-1.(XTX)w = (XTX)-1.(XT).y*
        > - Since *X.X^-1 = I*, we get,
        >
        >   >    *w = (XTX)^-1.(XT).y*

    - **Normal Linear Regression Model Equation:**

        > w = (XTX)^-1.(XT).y
        
- Create a method to measure the correctness of the predictions. E.g, **RMSE (Root Mean Squared Error)**
- Use the derived *weights (w)* from training the linear regression model to predict the price for the features in the validation dataset
- Calculate the RMSE score for the predictions by comparing it with the actual values of the validation dataset
- If the RMSE score is high (closer to 1), improve the model by including more features from the training dataset in the linear regression model
- If the RMSE score is very high (a lot higher than 1), then check for regularization issues like *linear combination* and improve the dataset using *regularized parameter (r)*
- Train the model again using *training + validation dataset* combined and get the improved weights
- And then test the returned weights (w) with the test dataset and check the RMSE scores
- If the RMSE scores are still low, improve the model dataset by including more features by changing the object based feature values into numerical based feature values 


## Categorical Data
- The Linear Regression model can only take into consideration the numerical values. The other data types i.e., strings are not relevant for the model as is. These string data types (object in DataFrame) are called Categorical Data.
-  To use these for training the model, these need to converted into some numerical data and then used in the model.
- Handling these categorical data and using them in training the model can improve its accuracy.

## Regularization
- In a matrix, there are chances where one column can be represented as a multiple of other column or the chances of linear combination. This can make the matrix irreversible and then the linear regression solution will not exist.  
- Regularization is the process of adding a small variable to the feature matrix, called *regularization parameter, 'r'* to remove these linear combination chances. 

## Using the model
- The data to be used for prediction will be given in a dictionary format by the users.
- To use the dictionary and predict the price:
    - Convert dict to DataFrame
    - Prepare X from the DataFrame
    - Use the X to calculate the predicted price using the 'w' values from the training data
    - Converted the calculated value to exponential form - 1 (to undo the log + 1 on the price for the training)
    - Return the calculated actual price
