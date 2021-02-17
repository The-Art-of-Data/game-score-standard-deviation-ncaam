# game-score-standard-deviation-ncaam
Fits a Game Score Standard Deviation model to the home team margin of victory.
Uses the method described in Statistical Sports Models in Excel (Mack, 2019).
Inputs are 2 separate lists of strings for away and home team names,
and 2 separate lists of integers for away and home team scores.

Briefly, 4 statistics are calculated for each team:
(average points for home, average points against home, 
average points for away, average points against away)
Then an Ordinary Least Squares minimization is used to calculate the coefficients.
The points stats are stored in .points_df, and the optimized coefficients stored as
.opt_intercept, .opt_pfh, .opt_pah, .opt_pfa, .opt_paa.

Based on those stats and coefficients, the model predicts a home margin of victory with .predict_raw()
The next steps described in SSME are 
i: run a linear regression to map the model predictions to actual mov, .predict_mov()
ii: input the regression estimated spread into the cumulative density function of the 
    normal distribution to get the estimated home team win percentage, .predict_proba_()
Both these steps are performed inside this module, but it is recommended that you use the 
.predict_raw() method to get the GSSD model's pure prediction, and then run your own linear
regression on that to see a full regression summary output, as well as for use in an ensemble.
