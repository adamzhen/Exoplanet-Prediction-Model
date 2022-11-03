# Exoplanet Prediction Model
*To preface, this program was created by and large as a way for me to practice using machine learning models in Python (pandas, scikit-learn, etc); it was not intended for scientific purposes.*

Now, essentially what I did was I used [NASA Exoplanet Archive's data on Kepler Objects of Interest (KOIs)](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=cumulative) in order to train models that could attempt to classify objects as exoplanet or not (CONFIRMED or FALSE POSITIVE). The 13 features that I trained the models on were:
1. Orbital Period (days)
2. Transit Epoch (BJD - 2,454,833.0)
3. Impact Parameter
4. Transit Duration (hours)
5. Transit Depth (parts per million)
6. Planetary Radius (Earth radii)
7. Equilibrium Temperature (Kelvin)
8. Transit Signal-to-Noise
9. Stellar Effective Temperature (Kelvin)
10. Stellar Radius (solar radii)
11. Right Ascension (deg)
12. Declination (deg)
13. Kepler-band (mag)

These features are simply the ones from the KOI dataset that I found to be at least potentially relevant; it should be noted that exoplanet prediction models in actual scientific literature tend to (from what I've seen) extract features directly from the measured light curves, which is probably a better method than what I did. 

As for the data samples, I used 9200 of the 9564 objects listed in the KOI dataset (removing the ones that had null values for any of the features). Of those 9200, only 7250 were already listed as CONFIRMED or FALSE POSITIVE (the other 1950 were still candidates, which I later used my model to generate predictions for). So I split those 7250 into training (60%), validation (20%), and test (20%) sets. Then, I trained 4 models (Logistic Regression, Multilayer Perceptron, Random Forest, & Gradient Boosted Trees), with GridSearchCV to identify the best parameters for each model. In the end, the gradient boosting model proved to be the highest-performing model, with an accuracy of 91.52%, precision of 88.67%, and recall of 88.83% (predict time was 49.531 ms, but that was not a very important factor) when tested on the test set. I then used this model to make predictions for the 1950 KOI candidates, and exported them as a [CSV file](https://github.com/adz888/Exoplanet-Prediction-Model/blob/main/koi_candidate_predictions.csv) and an [Excel sheet](https://github.com/adz888/Exoplanet-Prediction-Model/blob/main/koi_candidate_predictions.xlsx), which are available on this repository. 

I also created a exoplanet predictor program, with 3 options for entering input:
1. Enter a KOI Name for a KOI candidate that the model has already predicted (should work for almost all KOI candidates)
2. Make predictions using your own CSV file with data values
3. Manually enter data values for each of your entries
