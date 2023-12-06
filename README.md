# Evaluating pricing options with A/B test and designing a high-level system to scale the testing    
This is a small practice of applying an A/B test to evaluate the results of two seperate pricing campaign based on the number of sales, revenue, payouts and earnings. In the second part, you can also find a brief design idea on how to automate A/B testing in large-scale environment.  

## Compare price options 
Although we don't see a significance difference(alpha being 0.05) in the number of sales between two price options, when we look at the earnings - which we may consider as the main metric for this study, we see a significant lift using the price option  [7951]  comparing the  [7952] . So based on this test, we can infer that  [7951]  will be a more profitable option.

Test Results for each metrics: 

**accept_status:** 
split_test_option | conversion_rate | std_deviation | std_error
--- | --- | --- | ---                                            
[7951] | 0.005702 | 0.075297 | 0.000796
[7952] | 0.007410 | 0.085764 | 0.001694
Z Statistic - -0.98
P-Value - 0.327
CI 95% for test1 group | [0.004, 0.007]
CI 95% for test2 group | [0.004, 0.011]


**revenue:**
split_test_option | conversion_rate | std_deviation | std_error
--- | --- | --- | ---                                          
[7951] | 0.100846 | 1.847446 | 0.019535
[7952] | 0.060920 | 1.100530 | 0.021734
Z Statistic - 6.17
P-Value - 0.000
CI 95% for test1 group | [0.095, 0.107]
CI 95% for test2 group | [0.052, 0.070]


**payout:**
split_test_option | conversion_rate | std_deviation | std_error
--- | --- | --- | ---                                            
[7951] | 0.077616 | 1.582461 | 0.016733
[7952] | 0.045593 | 0.931788 | 0.018402
Z Statistic - 5.59
P-Value - 0.000
CI 95% for test1 group | [0.072, 0.083]
CI 95% for test2 group | [0.038, 0.054]


**erns:**
split_test_option | conversion_rate | std_deviation | std_error
--- | --- | --- | ---                                           
[7951] | 0.023230 | 0.799415 | 0.008453
[7952] | 0.015328 | 0.581664 | 0.011487
Z Statistic - 2.43
P-Value - 0.015
CI 95% for test1 group | [0.020, 0.026]
CI 95% for test2 group | [0.011, 0.020]


## Design a system that would optimize hundreds of tests daily  
On the high level, there may be two different approaches to design an automated A/B testing environment: Real-time and batch. In theory, they will work pretty similar on how to carry out the tests, but the main difference will be one system works in real time employing real-time triggers while the other works in batch. Here, I'll touch upon on a real-time system design:    

For this system, employng a queue(e.g Kafka or Kineses) may be helpful. This queue may trigger a new test for every conversion(i.e. sales) happened along the pipeline. Here the two important factors to take into consideration would be:
- 1: Whether the test will have enough observations in it to make a sound hypothesis testing(this can be addressed by defining an if condition based on the predefined test power)
- 2: How to compare a new test with the existed tests results on the fly in an efficient way. There might be different approaches for this, but one way can be using a data structure like priority queue(e.g. heap) to keep the best test metrics in memory up-to-date in ordered way, and update these test results on the fly whenever a new conversion happens in any of them. To update this priortiy queue each tests may have their own microservices running based on the triggers and filters they're getting from Kafka service for example, and the priority queue would help us to store the best test results in an ordered way. This system can be horizontally scaled if we want to test different metrics at each time applying the same workflow for each of them.  