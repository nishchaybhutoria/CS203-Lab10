# CS203: Software Tools & Techniques for AI  

---

## Team Members (Team 17)
- Nishchay Bhutoria (23110222)  
- Srivaths P (23110321)

---

# Part 1: A/B Testing using Ad Click Prediction

### 1. Dataset Loading & Preprocessing

![image](https://github.com/user-attachments/assets/d117469c-f298-42c2-ba80-ced1c11e17df)
![image](https://github.com/user-attachments/assets/8c5eeaf6-83ad-4b29-8dd0-6b4d08da7674)

---

### 2. Group Definition
- Group A: Users with `ad_position = 2` (Top)  
- Group B: Users with `ad_position = 0` (Bottom)

---

### 3. Z-Test

![image](https://github.com/user-attachments/assets/3e723d97-18f3-4d35-9ab4-86a0d807f774)

---

### 4. Interpretation

Yes, there is a statistically significant difference in click-through rates between the two groups. The p-value of ~0.00005 is less than the significance level of 0.05, indicating that the observed difference in click-through rates is unlikely to have occurred by random chance. This suggests that the ad position has a significant impact on user engagement.

---

# Part 2: Covariate Shift Detection

### 1. Dataset Preparation
- Datasets: `train.csv`, `test1.csv`, `test2.csv`
- Decimal commas converted to floats

![image](https://github.com/user-attachments/assets/50b7e3e5-48ae-4933-8d7c-14a6f033f041)

---

### 2. KS Test on `NO2(GT)`

![image](https://github.com/user-attachments/assets/c1f6a98f-344d-470a-b5a4-7117c05f6f10)

Train vs Test1: There is no significant difference in the distribution of NO2(GT) values between the training and test1 datasets, as indicated by the high p-value (~0.9971).

Train vs Test2: There is a significant difference in the distribution of NO2(GT) values between the training and test2 datasets, as indicated by the low p-value (~0.0000).

---

### 3. KS Test for All Features

Kolmogorov-Smirnov (KS) tests indicate a significant covariate shift between the training data and test2, but not test1. Most features in test2 showed high KS statistics and p-values < 0.05 compared to the training set.

The NO2(GT) feature highlights this difference. The comparison between train and test2 showed a significant distributional divergence (KS=0.3689, p=0), while the comparison between train and test1 indicated high similarity (KS=0.0171, p=0.9971).
