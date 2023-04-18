# DATA6250project

Baseline:

The models I decided to use in my experiments were ridge regression, decision tree regressor, and a linear SVR. I performed grid search cv to find the best parameters for each model, but I ran into some difficulties along the way. The first problem was the duration of time it took to run, specifically with the SVR model. The way I worked around this was to import LinearSVR instead of using SVR with the kernel set to linear. SVMs scale pretty badly when it comes to large datasets, so it is more efficient to use the specific linear SVR. The decision tree regressor took a good bit of time to fit when using grid search CV, so I reduced the number of parameters I would test for. As a result, the highest performing parameters always overfit the data. When I would try a different combination of parameter choices, it would still overfit. The ridge model also suffered similar problems. With gridsearch CV, when I would test out different alphas with different solvers, the model would never converge and would take hours to run. I had to reduce the type of parameters I tested by a lot.

Experiment 1:

This experiment was really middle of the pack performance wise. The decision tree had one of its best trials, but since the model is overfitting, I wouldn’t give it much consideration. The linear SVR’s result didn’t make sense. I only applied the feature pattern to the numerical features since the categorical ones were all one hot encoded. I removed the original numerical feature columns after applying the patterns, but I feel like the models would have performed better if the original columns were left in.

Experiment 2:

Surprisingly, this was the best performing experiment for all the different models. I expected it to be one of the worst. I’m interested in seeing how the performance would change if I added in more of the original features that I removed at the start. I think it would be beneficial to create a correlation matrix with the created features to see which ones had the strongest correlations with the price of the trip. The 

Experiment 3:

I applied PCA to two of the numerical columns of my feature matrix. I didn’t think it made sense to apply it to the whole matrix since the majority of features are categorical and would be one hot encoded. Honestly, performing any type of dimensionality reduction on the current feature matrix doesn’t make too much sense considering I manually reduced most of the columns already. If I wanted to reduce the categorical features, I think I could have used a technique called Multiple Correspondence Analysis. This was by far the worst performing experiment. The mse and r2 score were lower than the majority of all the other experiments that I’ve done. I think this is due to my earlier explanation. The features had already been reduced prior to running PCA on them.

Experiment 4:

I only applied the standard scaler transformation to the two numerical columns in my matrix. The other columns were one hot encoded so I didn't think there was much value in applying the transformation on that portion of the matrix.The decision tree performed worse than the first two experiments, but the r2 score remained pretty much the same. The ridge regression model performed very similarly to experiment 1 as the mse and r2 score basically match up. The linear SVR model took a few minutes to run and failed to converge without adding more iterations. 

Experiment 5:
