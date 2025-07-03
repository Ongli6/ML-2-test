# Hyperparameter Log

**PRE BASELINE NOTES**
- Consider dropping RAG rating from baseline, not really sure how good the human input is.

## Experiment 001 - Baseline
**Date:** 2025-07-03
**Model:**
- n_estimators=500,
- max_depth=30,
- min_samples_split=5,
- min_samples_leaf=2,
- max_features='sqrt',
- class_weight='balanced',
- verbose=1,
- random_state=42,
- n_jobs=-1


**Preprocessing:**  
- TF-IDF (max_features=100)  
- StandardScaler  
- SimpleImputer (mean)  

**Engineered Features**
- attendance_converted(int)
- Attendance_mising(int)
- Credit Ratio(int)
- Current Missing(int)
- Target Mising(int)
- last_online_missing(int)
- days_since_last_online(int)

**Results:**  
=== Classification Report ===
 
                          | precision | recall | f1-score | support | 
                          | ---------- | ------ | -------- | ------ |
    |  Break in Learning  |     0.44   |  0.46  |   0.45   |   81   |
    |Completed: Achieved  |     0.99   |  0.95  |   0.97   |  110   | 
    |         Continuing  |     0.95   |  0.93  |   0.94   |  629   |       
    |          Withdrawn  |     0.88   |  0.91  |   0.90   |  393   |         


           accuracy                           0.90      1213
          macro avg       0.82      0.81      0.81      1213
       weighted avg       0.90      0.90      0.90      1213


=== Confusion Matrix ===

     [ 37   1  19  24]
     [  2 105   2   1]
     [ 21   0 585  23]
     [ 24   0  10 359]

=== Summary Scores ===
Accuracy:      0.8953
F1 Score:      0.8145
Precision:     0.8157
Recall:        0.8137
Log Loss:      0.3338
ROC AUC (OVR): 0.9603

**Notes:**  
Baseline shows EXTREMELY high numbers. Feature importance graph (001_ATHGP_feature_importance) reveals that credit ratio is more then TWICE as good at prediciting withdraw then the next feature. Really gotta drop this to see how big the stat drop is as i think a 0 credit ratio may unintentionally be marking it as withdrawn. 




## Experiment 002 - All the homies hate Credit Ratio
**Date:** 2025-07-03
**Model:**
- n_estimators=500,
- max_depth=30,
- min_samples_split=5,
- min_samples_leaf=2,
- max_features='sqrt',
- class_weight='balanced',
- verbose=1,
- random_state=42,
- n_jobs=-1


**Preprocessing:**  
- TF-IDF (max_features=100)  
- StandardScaler  
- SimpleImputer (mean)  

**Engineered Features**
- attendance_converted(int)
- Attendance_mising(int)
- Current Missing(int)
- Target Mising(int)
- last_online_missing(int)
- days_since_last_online(int)

**Results:**  
=== Classification Report ===
                     precision    recall  f1-score   support

  Break in Learning       0.43      0.49      0.46        81
Completed: Achieved       0.92      0.96      0.94       110
         Continuing       0.94      0.92      0.93       629
          Withdrawn       0.89      0.88      0.89       393

           accuracy                           0.88      1213
          macro avg       0.80      0.81      0.80      1213
       weighted avg       0.89      0.88      0.88      1213


=== Confusion Matrix ===
[[ 40   2  18  21]
 [  2 106   1   1]
 [ 23   7 578  21]
 [ 27   0  19 347]]

=== Summary Scores ===
Accuracy:      0.8829
F1 Score:      0.8049
Precision:     0.7961
Recall:        0.8148
Log Loss:      0.3621
ROC AUC (OVR): 0.9572

**Notes:**  
ok seems like it didnt make that much difference after all! i thought credit ratio might be tipping it off but model seems really solid without it?? confusion matrix reveals that "break in learning" is a little tougher to identify but thats to be expected as its just withdrawn but temporary. 
