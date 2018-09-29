# SCU-alumni-donation-prediction
Alumni gifting prediction and segmentation.

### SUMMARY
SCU’s development team is interested in increasing the number of alumni that donate to SCU during their reunion year. Despite the various engagement efforts put in by SCU, only a minority of alumni give back to SCU during their reunion year.
Based on the data provided, we are required to help SCU in prioritizing prospects that would be most likely to give back to SCU during reunion.

### Tech Stack
The following packages are used for the analysis:
rms, data.table, ggplot, MASS.

### Analysis method
1. Read dataset and transform variables such as FamilyAlum, State, GradSince, WERating etc.
2. Run Ordinal Logit models to predict missing WERating values.
3. Run Binary Logit models to get propensity scores.
4. Segment sample based on propensity scores and other characteristics.

### Summary stats - Plots

![alt text][logo]

[logo]: https://github.com/VNair88/SCU_Alumni-Prediction-and-Segmention/blob/master/Plots/RYCohort_sum.JPG  "Plot1"


![alt text][logo1]

[logo]: https://github.com/VNair88/SCU_Alumni-Prediction-and-Segmention/blob/master/Plots/WERating_sum.JPG  "Plot2"

### Ordinal Logit model
#### Prediction of missing wealth enginge rating values (WERating).
Break dataset into 2: subset that contains WealthEngineRating values & subset that doesn't contain WealthEngineRating values. <br>
Run ordinal logit model on subset 1. Dependent var - WealthEngineRating. <br>
Start with the initial model. Drop variables in subsequent iterations based on significance. <br>
Compare models on AIC scores and out of sample prediction. <br> 
Final model - WealthEngineRating ~ RYCohort + BetweenRY + ActionNote + SportsAlum + UGAlumAwards + OtherUGAct + EverAssigned + BoardMember + GradDegree + TotalReunions + NetEvents + OnePlusEvents + TotalActions + NeverGiven + Gave + FamilyAlum <br>
Predict values for WealthEngineRating using the final model on subset 2. <br>
Combine subsets 1 and 2.

### Binary Logit model
#### Prediction regarding whether a gift was given in 2009.
Check correlations among numeric variables of the dataset. <br>
Run a binary logit model on a training dataset (70% of the original dataset). <br>
Dependent var - Gave2009. <br>
Check correlations among numeric variables of the dataset. <br>
Start by running an initial model. <br>
Drop variables on subsequent iterations based on significance. <br> 
Compare models on AIC scores and out of sample prediction. <br>
Final model - Gave2009 ~ Gave2004 + Gave1999 + BetweenRY + Attended09 + Attended04 + Attended99 + YearsLapsed_factor + NetEvents + TotalActions <br>
Predict and retrieve propensity scores.

### Segmentation based on propensity scores
Based on propensity scores, individuals in three segments
1. Individuals with propensity scores greater than 80%
2. Individuals with propensity scores between 60% & 80%
3. Individuals with propensity scores between 40% & 60%

How the segments differ - 

![alt text][logo2]

[logo2]: https://github.com/VNair88/SCU_Alumni-Prediction-and-Segmention/blob/master/Plots/Cat_Attended.JPG  "Plot3" 

![alt text][logo3]

[logo3]: https://github.com/VNair88/SCU_Alumni-Prediction-and-Segmention/blob/master/Plots/Cat_Board.JPG  "Plot4"

![alt text][logo4]

[logo4]: https://github.com/VNair88/SCU_Alumni-Prediction-and-Segmention/blob/master/Plots/Cat_Gradsince.JPG  "Plot5"


