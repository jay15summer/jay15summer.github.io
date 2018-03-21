---
layout: post
title:  "Dealing with categorical variables in regression"
categories: blog 
tags: regression
---
## 1. Brief introduction

Under most situations, categorical variables cannot be entered directly into a regression model and be meaningfully interpreted. As a result, a common method dealing with categorical variables in regression is **Dummy Coding**. Dummy coding refers to the process of coding categorical variables into dichotomous variables ([Wikiversity](https://en.wikiversity.org/wiki/Dummy_variable_(statistics))).

For example, given a categorical variable having three classes: “faculty”, “staff”, and “student”. Dummy variables are created as follows:

|         | dv_1 | dv_2 | dv_3 |
|:-------:|:----:|:----:|:----:|
| faculty |   1  |   0  |   0  |
|  staff  |   0  |   1  |   0  |
| student |   0  |   0  |   1  |

The categorical variable is dummy coded as three dummy variables: dv_1, dv_2, and dv_3.

Usually, people will select a category as the reference category in the regression process to avoid rank deficiency. For example, if “faculty” is chosen as the reference category, the new dummy coded variables become: 

|         | dv_1 | dv_2 |
|---------|------|------|
| faculty | 0    | 0    |
| staff   | 1    | 0    |
| student | 0    | 1    |

## 2. Dummy coding in Python using `pandas`

```python
# Create dataframe with categorical variable: [“status”: faculty, staff, student] 
import pandas as pd
data = pd.DataFrame({'status':['faculty','staff','student']})
dv1 = pd.get_dummies(data)
print(dv1)
# if having another categorical variable: [“gender”: M, F]
data = pd.DataFrame({'gender':['M','F', 'M'], 'status':['faculty','staff','student']})
dv2 = pd.get_dummies(data)
print(dv2)
```
<br>
<table style="border-collapse:collapse;border-spacing:0"><tr><th style="font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center" colspan="3">Output:</th></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center" colspan="3">dv1</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">status_faculty</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">status_staff</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">status_student</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">1</td></tr></table>

<table style="border-collapse:collapse;border-spacing:0"><tr><th style="font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center" colspan="5">dv2</th></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">gender_F</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">gender_M</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">status_faculty</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">status_staff</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">status_student</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td></tr><tr><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">1</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">0</td><td style="font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;text-align:center;vertical-align:top">1</td></tr></table>

## 3. Dummy coding in Matlab

```matlab
% create categorical variable: ["status": faculty, staff, student]
status = categorical({'faculty'; 'staff'; 'student'});
dv_status = dummyvar(status)
% if having another categorical variable: ["gender": M, F]
gender = categorical({'M'; 'F'; 'M'});
dv_gender_status = [dummyvar(gender) dummyvar(status)]
```
<br>
<pre class="codeoutput">
dv_status =

     1     0     0
     0     1     0
     0     0     1


dv_gender_status =

     0     1     1     0     0
     1     0     0     1     0
     0     1     0     0     1
</pre>

## 4. An example of using dummy coding for categorical regression

Categorical regression using dummy coding can be done either manually or automatically in Matlab.
The codes are shown respectively as follows which generate the same fitting results. 

```matlab
% 4.A Manually dummy coding
load('carsmall')
cars = table(MPG, Weight, Model_Year);
cars.Model_Year = nominal(cars.Model_Year);
dv = dummyvar(cars.Model_Year);
Model_Year1 = dv(:, 1); Model_Year2 = dv(:, 2); Model_Year3 = dv(:, 3);
cars = table(MPG, Weight, Model_Year2, Model_Year3);
fit = fitlm(cars, 'MPG~Weight*Model_Year2 + Weight*Model_Year3')
```
<br>
<pre class="codeputput">
fit = 

Linear regression model:
    MPG ~ 1 + Weight*Model_Year2 + Weight*Model_Year3

Estimated Coefficients:
                           Estimate          SE         tStat        pValue  
                          ___________    __________    ________    __________

    (Intercept)                37.399        2.1466      17.423    2.8607e-30
    Weight                 -0.0058437    0.00061765     -9.4612    4.6077e-15
    Model_Year2                4.6903        2.8538      1.6435       0.10384
    Model_Year3                21.051         4.157      5.0641    2.2364e-06
    Weight:Model_Year2    -0.00082009    0.00085468    -0.95953       0.33992
    Weight:Model_Year3     -0.0050551     0.0015636     -3.2329     0.0017256
</pre>
<br>
```matlab
% 4.B Automatic dummy coding via built-in matlab function
load('carsmall')
cars = table(MPG, Weight, Model_Year);
cars.Model_Year = nominal(cars.Model_Year);
fit = fitlm(cars, 'MPG~Weight*Model_Year')
```
<br>
<pre class="codeputput">
fit = 

Linear regression model:
    MPG ~ 1 + Weight*Model_Year

Estimated Coefficients:
                             Estimate          SE         tStat        pValue  
                            ___________    __________    ________    __________

    (Intercept)                  37.399        2.1466      17.423    2.8607e-30
    Weight                   -0.0058437    0.00061765     -9.4612    4.6077e-15
    Model_Year_76                4.6903        2.8538      1.6435       0.10384
    Model_Year_82                21.051         4.157      5.0641    2.2364e-06
    Weight:Model_Year_76    -0.00082009    0.00085468    -0.95953       0.33992
    Weight:Model_Year_82     -0.0050551     0.0015636     -3.2329     0.0017256
</pre>


