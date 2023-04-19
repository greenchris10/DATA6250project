# DATA6250project

For my project, I will be utilizing a dataset from kaggle. It has information about 55 thousand uber and lyft rides throughout different areas in Boston. The dataset contains 57 columns mostly composed of categorical features. Prior to performing the experiments I spent a lot of time dropping irrelavant columns so that the data would be eaiser to work with.

<img width="1095" alt="Untitled" src="https://user-images.githubusercontent.com/120329214/232910479-69b027ad-8da7-4ae9-9d0d-d7400cbe664b.png">

<img width="430" alt="Screenshot 2023-04-18 at 6 35 01 PM" src="https://user-images.githubusercontent.com/120329214/232919771-d40fa350-0e6a-4a2a-8a10-249ab2991c87.png">

<img width="1073" alt="Screenshot 2023-04-18 at 5 36 45 PM" src="https://user-images.githubusercontent.com/120329214/232910750-4fb67d1b-e75a-4158-b11e-484025f1188f.png">

<img width="1088" alt="Screenshot 2023-04-18 at 5 37 54 PM" src="https://user-images.githubusercontent.com/120329214/232910918-44b113d5-2ef0-4af9-9366-e805238e4c8b.png">

<img width="1079" alt="Screenshot 2023-04-18 at 5 41 47 PM" src="https://user-images.githubusercontent.com/120329214/232911605-c1a07824-c544-4077-86a3-82199dadd3f2.png">

Price has a strong positive correlation with distance and surge_multiplier. There is a very weak correlation with precipIntesity so I will drop that column. Latitude and longitude might be redundent columns since we have source and destination columns. Since we have the icon column that gives us a good description of the weather and time-of-day, I think we can drop the weather, and time/day columns. Product_id is also an irrelavant column I can drop.

<img width="787" alt="Screenshot 2023-04-18 at 5 42 56 PM" src="https://user-images.githubusercontent.com/120329214/232911813-81264daa-6960-4737-927e-0c44953be024.png">

<img width="1018" alt="Screenshot 2023-04-18 at 5 44 28 PM" src="https://user-images.githubusercontent.com/120329214/232912043-ef178313-8913-47b1-80b9-ddec342b44dd.png">

<img width="1181" alt="Screenshot 2023-04-18 at 5 26 05 PM" src="https://user-images.githubusercontent.com/120329214/232908801-7a82c12c-adf3-41f3-91da-5c1121c72e83.png">

Baseline:

The models I decided to use in my experiments were ridge regression, decision tree regressor, and a linear SVR. I performed grid search cv to find the best parameters for each model, but I ran into some difficulties along the way. The first problem was the duration of time it took to run, specifically with the SVR model. The way I worked around this was to import LinearSVR instead of using SVR with the kernel set to linear. SVMs scale pretty badly when it comes to large datasets, so it is more efficient to use the specific linear SVR. The decision tree regressor took a good bit of time to fit when using grid search CV, so I reduced the number of parameters I would test for. As a result, the highest performing parameters always overfit the data. When I would try a different combination of parameter choices, it would still overfit. The ridge model also suffered similar problems. With gridsearch CV, when I would test out different alphas with different solvers, the model would never converge and would take hours to run. I had to reduce the type of parameters I tested by a lot.

The way I chose to evaluate the performance of each model was to use mean squared error on both the test and training data. the MSE will tell us the average squared difference between the true and predicted y values. I also used the r2 score to evaluate performance. The r2 score will tell us how well the model predicts the outcome of the dependent variable. R-Squared values range from 0 to 1. An R-Squared value of 0 means that the model explains or predicts 0% of the relationship between the dependent and independent variables. A value of 1 indicates that the model predicts 100% of the relationship, and a value of 0.5 indicates that the model predicts 50%, and so on

Experiment 1:

This experiment was really middle of the pack performance wise. The decision tree had one of its best trials, but since the model is overfitting, I wouldn’t give it much consideration. The linear SVR’s result didn’t make sense. I only applied the feature pattern to the numerical features since the categorical ones were all one hot encoded. I removed the original numerical feature columns after applying the patterns, but I feel like the models would have performed better if the original columns were left in.

Experiment 2:

Surprisingly, this was the best performing experiment for all the different models. I expected it to be one of the worst. I’m interested in seeing how the performance would change if I added in more of the original features that I removed at the start. I think it would be beneficial to create a correlation matrix with the created features to see which ones had the strongest correlations with the price of the trip. The 

Experiment 3:

I applied PCA to two of the numerical columns of my feature matrix. I didn’t think it made sense to apply it to the whole matrix since the majority of features are categorical and would be one hot encoded. Honestly, performing any type of dimensionality reduction on the current feature matrix doesn’t make too much sense considering I manually reduced most of the columns already. If I wanted to reduce the categorical features, I think I could have used a technique called Multiple Correspondence Analysis. This was by far the worst performing experiment. The mse and r2 score were lower than the majority of all the other experiments that I’ve done. I think this is due to my earlier explanation. The features had already been reduced prior to running PCA on them.

Experiment 4:

I only applied the standard scaler transformation to the two numerical columns in my matrix. The other columns were one hot encoded so I didn't think there was much value in applying the transformation on that portion of the matrix.The decision tree performed worse than the first two experiments, but the r2 score remained pretty much the same. The ridge regression model performed very similarly to experiment 1 as the mse and r2 score basically match up. The linear SVR model took a few minutes to run and failed to converge without adding more iterations. 

Experiment 5:

When trying to determine the most important features, I had difficultiy interpreting the importance scores for my categorical columns. Since they were one hot encoded, I was unable to figure out which score corresponded with each feature prior to one hot encoding. I was able to see that surge multiplier was more important than distance which I found surprising. There were some categorical features that had the highest importance scores. I believe they corresponded to the source and destination features but I wasn't able to completely confirm that. The performance of the models in this experiment wasn't great at all. The only model that performed ok (with respect to the other experiments) was the decision tree. Prior to training the model, I applied the standard scalar transformation to the random columns that got added. Since the random columns had values between 100 and 200, but my other numerical columns were single digits, I believed applying this transformation was necessary. 

Conclusion:

Based on the 5 experiments I ran, I'd have to reccomend the ridge-regression model used in experiment 2. Adding the polynomial features to my feature matrix resulted in the best MSE and r2 score.

