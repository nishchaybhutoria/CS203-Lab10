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

There is a statistically significant difference in click-through rates between the two ad positions.

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

| Feature            | KS Statistic (test1)  | P-value (test1)  | KS Statistic (test2)  | P-value (test2)  |
|--------------------|-----------------------|------------------|-----------------------|------------------|
| PT08.S1(CO)        | 0.032813              | 0.490012         | 0.127500              | 1.65e-09         |
| NMHC(GT)           | 0.012812              | 0.999921         | 0.227187              | 1.98e-29         |
| C6H6(GT)           | 0.020938              | 0.938445         | 0.142500              | 8.89e-12         |
| PT08.S2(NMHC)      | 0.021562              | 0.923540         | 0.141875              | 1.12e-11         |
| NOx(GT)            | 0.017500              | 0.988482         | 0.524062              | 4.13e-162        |
| PT08.S3(NOx)       | 0.034375              | 0.430351         | 0.322813              | 1.43e-59         |
| NO2(GT)            | 0.019062              | 0.972194         | 0.407500              | 7.20e-96         |
| PT08.S4(NO2)       | 0.020000              | 0.957373         | 0.597187              | 1.35e-214        |
| PT08.S5(O3)        | 0.028125              | 0.685568         | 0.136563              | 7.54e-11         |

Kolmogorov-Smirnov (KS) tests indicate a significant covariate shift between the training data and test2, but not test1. Most features in test2 showed high KS statistics and p-values < 0.05 compared to the training set.

The NO2(GT) feature highlights this difference. The comparison between train and test2 showed a significant distributional divergence (KS=0.3689, p=0), while the comparison between train and test1 indicated high similarity (KS=0.0171, p=0.9971).
