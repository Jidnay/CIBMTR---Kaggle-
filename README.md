# CIBMTR - Kaggle

In the [CIBMTR Kaggle competition](https://www.kaggle.com/competitions/equity-post-HCT-survival-predictions/overview), the objective is to develop a model using survival data to predict the risk of an event occurring, such as a patient's death.

The provided dataset does not directly include the risk variable that competitors are required to predict. Instead, the dataset includes the variables efs (event-free survival, where 1 indicates an event occurred and 0 indicates censoring) and efs_time (the time at which the event occurred or the censoring took place). Consequently, competitors must employ creative "target engineering" techniques to derive a suitable target variable. One common method in the literature is the Kaplan-Meier estimator.

In my approach, I utilized the Weibull distribution, which closely resembles the Kaplan-Meier estimator. I adjusted the shape and scale parameters for each race class. Since the risk is constant at the start and end of the Weibull distribution, I incorporated a linear term to account for this behavior. The linear term is defined as the product of efs_time and a hyperparameter.

The final equation used to calculate the risk is as follows:

$$ y_ {risk} = \alpha \cdot weibull - \beta \cdot \text{efs_time_norm} + \theta $$

The final model is a emsemble of Xgboost and Catboost.
