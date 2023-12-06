# Evaluating pricing options with A/B test and designing a high-level system to scale the testing    
This is a small practice of applying an A/B test to evaluate the results of two seperate pricing campaign based on the number of sales, revenue, payouts and earnings. In the second part, you can also find a brief design idea on how to automate A/B testing in large-scale environment.  

## Compare price options 
Although we don't see a significance difference(alpha being 0.05) in the number of sales between two price options, when we look at the earnings - which we may consider as the main metric for this study, we see a significant lift using the price option  [7951]  comparing the  [7952] . So based on this test, we can infer that  [7951]  will be a more profitable option.

Test Results for each metrics: 

accept_status
                   conversion_rate  std_deviation  std_error
split_test_option                                           
[7951]                    0.005702       0.075297   0.000796
[7952]                    0.007410       0.085764   0.001694
Z Statistic - -0.98
P-Value - 0.327
CI 95% for test1 group - [0.004, 0.007]
CI 95% for test2 group - [0.004, 0.011]


revenue
                   conversion_rate  std_deviation  std_error
split_test_option                                           
[7951]                    0.100846       1.847446   0.019535
[7952]                    0.060920       1.100530   0.021734
Z Statistic - 6.17
P-Value - 0.000
CI 95% for test1 group - [0.095, 0.107]
CI 95% for test2 group - [0.052, 0.070]


payout
                   conversion_rate  std_deviation  std_error
split_test_option                                           
[7951]                    0.077616       1.582461   0.016733
[7952]                    0.045593       0.931788   0.018402
Z Statistic - 5.59
P-Value - 0.000
CI 95% for test1 group - [0.072, 0.083]
CI 95% for test2 group - [0.038, 0.054]


erns
                   conversion_rate  std_deviation  std_error
split_test_option                                           
[7951]                    0.023230       0.799415   0.008453
[7952]                    0.015328       0.581664   0.011487
Z Statistic - 2.43
P-Value - 0.015
CI 95% for test1 group - [0.020, 0.026]
CI 95% for test2 group - [0.011, 0.020]