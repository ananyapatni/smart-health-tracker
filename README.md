# smart-health-tracker
This project combines statistical analysis and machine learning to enable data-informed health interventions.

## How to use:
Clone the repo: git clone https://github.com/yourusername/smart-health-tracker.git
Install dependencies: pip install -r requirements.txt
Run the notebook to see the full analysis pipeline.

## Dataset Description:
The data used has 11 columns, named in order, 
    Age
    Gender
    Daily Steps
    Resting Heart Rate
    Active Heart Rate
    Hours of Sleep
    Daily Calorie Intake
    Stress Level (0-10 scale)
    Sleep Quality (0-100 score)
    Daily Activity Type (categorical: sedentary, moderate, intense)
    Mood (multiclass: sad, neutral, happy)


## Analysis Pipeline

Step 1 was to categorized aforementioned 11 features into three "Health Pillars" to create a holistic view of user Illness:

    Physical: Daily Steps, Calorie Intake, Activity Type (Sedentary to Intense).

    Physiological: Age, Gender, Resting Heart Rate, Active Heart Rate.

    Psychological: Stress Level (0–10 scale), Mood (Sad, Neutral, Happy), Sleep Quality (0–100 score).

Then using correlation matrices, I uncovered how metrics correlate:

    Stress vs. Sleep Quality (r≈−0.4): The most significant negative correlation, which found that mental strain impacts the quality of sleep more severely than the total hours slept.

    Steps vs. Calories: While positively correlated, the relationship is non-linear, highlighting distinct groups of "Active Undereaters" and "Sedentary Overeaters."

    Physiological Strain: Higher Stress Levels were statistically linked to elevated Active Heart Rates during exercise, suggesting mental stress increases the physical "cost" of activity.


To move beyond simple correlation, I used Ordinary Least Squares (OLS) to test a hypotheses:

Hypothesis: Can Daily Steps and Stress predict Sleep Duration?
Result: Both features were statistically significant (p<0.05).
However, the low R2 score suggests that sleep is a "black box" influenced by latent variables (like caffeine or environment) not captured in traditional tracking.


I challenged three architectures to predict if a user is "Ill Rested" (7+ hours of sleep):
Model 1 used Logistic Regression with a	Linear Boundary. It showed a 50.4% result, which proves that	Health data is too non-linear for basic regression.
Model 2 used a Single Layer Perceptron (PyTorch). The output was 51.1% with high recall, but lacked "nuance" in prediction.
Finally Model 3 was a Deep Neural Network with	Multi-Layer ReLU	that performed with a 51.5% result, and could pick up subtle Stress/HR interactions.
To understand the phenomena better, I used SVM + PCA which helped visualize the decision boundaries, proving that health "states" (Rested vs. Tired) often overlap in a high-dimensional space.

Unsupervised insights from K-Means and DBSCAN helped build specific user archetypes, including 
"The High-Stress Athlete" : High steps, high heart rate, but critically low sleep quality.
"The Balanced Relaxer" : Moderate activity paired with low stress and high restorative sleep.

 Anomalies: DBSCAN isolated users with "Physiological Mismatches" (e.g., zero steps but high active heart rates), essential for data cleaning in real-world deployments.)

 
