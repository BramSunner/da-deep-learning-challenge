# Overview

This analysis is done for the non-profit organization 'AIphabet Soup' which wants to determine the applicants for funding with the best chance of success.  
The idea is to create a tool that the organization can use to determine if a new funding applicant would be successful with the funding they receive.  
To aid the creation of this tool, AIphabet Soup has provided a dataset containing records of 34,000 organizations that have received funding from them.  

This tool needs to have an prediction rate of 75% or higher in order for it to be used.

# Data Preprocessing

### What variable(s) are the target(s) for your model?

1. IS_SUCCESSFUL is the target for the model.

### What variable(s) are the features for your model?

1. STATUS
2. ASK_AMT
3. APPLICATION_TYPE_Other
4. APPLICATION_TYPE_T19
5. APPLICATION_TYPE_T3
6. APPLICATION_TYPE_T4
7. APPLICATION_TYPE_T5
8. APPLICATION_TYPE_T6
9. AFFILIATION_CompanySponsored
10. AFFILIATION_Family/Parent
11. AFFILIATION_Independent
12. AFFILIATION_National
13. AFFILIATION_Other
14. AFFILIATION_Regional
15. CLASSIFICATION_C1000
16. CLASSIFICATION_C1200
17. CLASSIFICATION_C2000
18. CLASSIFICATION_C2100
19. CLASSIFICATION_C3000
20. CLASSIFICATION_Other
21. USE_CASE_CommunityServ
22. USE_CASE_Heathcare
23. USE_CASE_Other
24. USE_CASE_Preservation
25. USE_CASE_ProductDev
26. ORGANIZATION_Association
27. ORGANIZATION_Co-operative
28. ORGANIZATION_Corporation
29. ORGANIZATION_Trust
30. INCOME_AMT_0
31. INCOME_AMT_1-9999
32. INCOME_AMT_10000-24999
33. INCOME_AMT_100000-499999
34. INCOME_AMT_10M-50M
35. INCOME_AMT_1M-5M
36. INCOME_AMT_25000-99999
37. INCOME_AMT_50M+
38. INCOME_AMT_5M-10M
39. SPECIAL_CONSIDERATIONS_N
40. SPECIAL_CONSIDERATIONS_Y

### What variable(s) should be removed from the input data because they are neither targets nor features?

1. EIN
2. NAME

# Compiling, Training, and Evaluating the Model

Creating the tool took a few stages and the target goal was not met but I will outline the process here.

### First Model

First, I tried a model with two layers.  

1. 7 neurons with a 'relu' activation.
2. 1 neuron with a 'sigmoid' activation.

I chose to do a simple model because I believed the problem at hand did not require a complex model.  
I was proven wrong, as the accuracy for this model missed the target by a large margin.  

### Second Model

After seeing the terrible model above, I decided to use more layers and neurons in the second model.
This model had 3 layers.

1. 5 neurons with a 'relu' activation.
2. 3 neurons with a 'relu' activation.
3. 1 neuron with a 'sigmoid' activation.

This model performed terrible as well. 

### Third Model

After another failure with adding more neurons, I decided that the activation function could make a difference.
I kept the amount of layers and neurons the same for the third model, but the activation function changed to 'tanh'.

1. 5 neurons with a 'tanh' activation.
2. 3 neurons with a 'tanh' activation.
3. 1 neuron with a 'sigmoid' activation.

This model performed under the target as well.

### Fourth Model

Since nothing had worked prior, I decided that perhaps the issue was still the amount of neurons.
Why not try to use a large amount of them?

1. 100 neurons with a 'tanh' activation.
2. 100 neurons with a 'tanh' activation.
3. 100 neurons with a 'tanh' activation.
4. 1 neuron with a 'sigmoid' activation.

Even with the large amount of neurons, the model still performed the same as the other models.

### Fifth Model

For the fifth model, I decided to use the keras hyperparameter tuner to assist in finding the optimal setup for the model.

Following is the parameters for the best model:
1. 'activation': 'sigmoid',
2. 'first_units': 7,
3. 'num_layers': 2,
4. 'units_0': 7,
5. 'units_1': 3,
6. 'units_2': 7,
7. 'units_3': 3,
8. 'units_4': 1,
9. 'units_5': 7,
10. 'tuner/epochs': 25,
11. 'tuner/initial_epoch': 0,
12. 'tuner/bracket': 0,
13. 'tuner/round': 0

This model did perform the best.  
It received a 73% accuracy score when tested.  
However, that does not meet the standards so it is also a failure.

# Summary

None of the models tried ended up hitting the target metric.  
Given that a range of activation functions, layers, and amounts of neurons were tried, I am led to believe that the input data could be the issue.  
It would be worthwhile to improve upon the preprocessing step and give the model a dataset tuned better to its success.  
However, this problem could also be solved using a supervised ML algorithm.  
It would also be worthwhile to run a full test of supervised ML algorithms for this problem.

I cannot recommend any of the models made in this test for the problem at hand because they do not perform well.



















