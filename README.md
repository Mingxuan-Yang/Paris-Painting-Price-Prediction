# Price Prediction of Paintings in the 18th Century Paris

## Introduction

This is a group project, where we take the role of a consultant hired by an Art historian to explore what factors drove the prices of paintings in 18th century Paris. Based on these factors, a prediction model will be built to identify possible overvalued and undervalued paintings.

## Datasets

The dataset we use to analyze is a series of auction transactions of the paintings in Paris, ranging from 1764 to 1780. This dataset mainly contains the following information:

- Sale data, which includes basic information about dealers, end buyers, transaction dates and prices  
- Characteristics of paintings, such as their painters, sizes, materials, number of figures and themes

The whole dataset is divided into three parts: a subset for training (`paintings_train.Rdata`), a subset for testing (`paintings_test.Rdata`), and a subset for validation (`paintings_validation.Rdata`). We should conduct data exploration and model construction based on `paintings_test.Rdata`. Then the model performance is tested on the `paintings_test.Rdata`, the result of which can be viewed through the scoreboard. After the project is turned in, the final score will be based on the predictions on `paintings_validation.Rdata`.

## Model

### Variable

According to variable definition as well as data exploration result, we decide to use the following variables:

- `year`: year of sale  
- `log_surface`: the logarithmic transformation of surface of paintings in squared inches  
- `dealer`: a categorical variable representing dealer initials with 4 unique dealers: J, L, P and R  
- `lrgfont`: indicates whether the dealer devotes an additional paragraph  
- `endbuyer`: a categorical variable indicating the type of end buyer, with B = buyer, C = collector, D = dealer, E = expert organizing the sale, X = identity unknown and blank = no information  
- `origin_author`:  origin of painting based on nationality of artist, with A = Austrian, D/FL = Dutch/Flemish, F = French, G = German, I = Italian, S = Spanish and X = Unknown  
- `winningbiddertype`: indicating the type of winning bidder wih B = buyer, C = collector, D = dealer, E = experts organization and n/a = no information  
- `finished`: indicating whether the painting is finished, with '1' indicating painting is finished  
- `type_intermed`: a categorical variable representing the type of intermediary with B = buyer, D = dealer and E = expert;  
- `diff_origin`: indicating whether variable `origin_author` is different from `origin_cat`; in other words, it means whether the origin of the paintings based on nationality and dealer's classification are the same or not, with 1 representing the same  
- `Fame`: indicating whether the author of the painting is famous, with '1' indicating that the author is famous  
- `paired`: indicating whether the painting is sold or suggested as a pairing for another, with '1' indicating it's sold as a pairing for another;  
- `mat`: representing the category of material, with 'al' = alabaster, 'ar' = slate, 'b' = wood,  'br' = bronze frames, 'c' = copper, 'ca' = cardboard, 'co' = cloth, 'g' = grissaille technique, 'h' = oil technique, 'm' = marble, 'mi' = miniature technique, 'o' = other, 'p' = paper, 'pa' = pastel, 't' = canvas, 'ta' = canvas, 'v' = glass and n/a = NA  
- `prevcoll`: indicating if the previous owner of the painting is mentioned, with '1' indicating yes  

The more detailed process of variable selection and construction can be accessed at the [final report](Part-II-Writeup.pdf).

### Model Construction

In this project, we have tested four kinds of models based on the variables selected in the previous section:

- Linear Regression Model  
- Random Forest  
- Bayesian Model Average  
- Generalized Additive Model

The model performance is evaluated through 5 indicators:

- *Bias*: Average Yhat-Y, where positive values indicate the model tends to overestimate price (on average) while negative values indicate the model tends to underestimate price.  
- *Maximum Deviation*: Maximum |Y-Yhat|, which identifies the worst prediction made in the validation data set.  
- *Mean Absolute Deviation*: Average |Y-Yhat|, which indicates the average error.  
- *Root Mean Square Error*: Sqrt Average (Y-Yhat)^2.  
- *Coverage*: Average lwr < Y < upr, the proportion of true prices falling between the predicted confidence interval.

After weighing these indicators, we find that Random Forest seems to have the best performance among those 4 models.

## Result

The result of the scoreboard is based on `paintings_validation.Rdata` and can be viewed [here](https://www2.stat.duke.edu/courses/Fall19/sta521/Final_Project_Scoring/display_leaderboard.html). As Team 3, we came ***second*** in this competition. The results of our Random Forest model are shown below.

|    |test data|validation data|
|:--:|:--:|:--:|
|*Bias*|153.389|216.605|
|*Coverage*|0.935|0.923|
|*Maximum Deviation*|8422.370|15553.292|
|*Mean Absolute Deviation*|313.295|357.611
|*RMSE*|886.098|1164.917|

## Authors

- Mingxuan Yang  
- Jiawei Chen
- Machao Deng
- Jishen Yin
