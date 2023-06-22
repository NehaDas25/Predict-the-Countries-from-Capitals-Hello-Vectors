# Work Report

## Information

- Name: <ins> DAS, NEHA </ins>
- CIN: <ins> 401457144 </ins>
- GitHub: <ins> NehaDas25 </ins>
- Email: <ins> ndas@calstatela.edu </ins>


## Features

- Not Implemented:
  - PART - 5: ERROR ANALYSIS
    - There were some model mis-classifications.
    - These mis-classifications happened because of Assumptions made by Naive Bayes Model.
  - PART - 6: PREDICT WITH OWN TWEET
    - Provided own custom tweet = "Another major improvement in timeline refresh speed just released – now 10X faster than a few months ago".
    - Using naives_bayes_predict, got the probability.


<br><br>

- Implemented:

  - PART - 1: PROCESS THE DATA
    - This involves removing the noise, removing punctuation and keep track of variation of words in the tweet.
    - 1.1 - Implementing the helper functions
        - In the count_tweets function, the parameters passed are a dictionary _result_, _tweetlist_ and _label_ . 
        - Since the size of tweet list and label is same, so we iterate them adjacently in form of zips(), and extract the _pair_ for each (word and label) which becomes the key of the dictionary _result_.
        - Now if the _pair_ is entered for the first time into the _result_ dictionary, then it is assigned a value = 1, else if it is found inside the dictionary, then its value for the same key is incremented by 1.
        - This passed all the unit-test cases as well.

  - PART - 2: TRAIN THE MODEL USING NAIVE BAYES
    - To implement the model, we need to pass the training set inside the count_tweets function for data pre-processing.
    - This pre-processing will return a dictionary by passing an empty dictionary, train_X and train_Y inside the count_tweets function.
    - Now we implemented the train_naive_bayes function, where the freqs dictionary obtained from count_tweets function, train_X and train_Y parameters are passed.
    - The goal of the train_naive_bayes function is to calculate the _logprior_ and _loglikelihood_ from the input parameters.
    - There is an empty variable set to 0 for _logprior_ and empty dictionary _loglikelihood_ .
    - Start counting the unique words from freqs dictionary by using _set_ function. And store it inside _vocab_. Calculate _V_ which is the length of the _vocab_ .
    - We need to calculate N_pos and N_neg, so set them to 0.
    - Now iterate through each of the freqs.keys(), which is nothing but the pair of (word, label). For each pair extracted from the freqs.keys(), if their label value is > 0, increment N_pos by the value of freqs[pair] else increment N_neg by the value of freqs[pair].
    - Since the size of train_X and train_Y is similar, we need to find of the length of documents which in our case is _tweets_, so we assign D = length (train_Y).
    - We need to calculate D_pos, D_neg and D_prior, where D_pos is sum of all labels where label = 1 and D_neg is sum of all labels where label = 0. Now we can calculate D_prior by using the log(D_pos/D_neg).
    - Upon testing with _EXPECTED_ _OUTPUT_ we found the calculated value of _logprior_ is same as expected, but for _loglikelihood_ its 9162 wheres expected is 9165.
    - But when testing with unit_test assigned, it fails because of code errors in unit_test which is mentioned in BUGS section.

  - PART - 3: TEST YOUR NAIVE BAYES
    - To test naives bayes, we need to test it by finding the probability of logprior and loglikelihood.
    - Implemented the naive_bayes_predict function, by providing the tweet, logprior and loglikelihood parameters as input.
    - Set probability parameter (p) = 0.
    - Add the logprior to the probability.
    - Using the process_tweet function we get the list of words by providing the tweet.
    - Iterate through the word_list, if the word extracted through iteration exists in the loglikelihood dictionary, add the value of the loglikelihood[word] to the probability.
    Return probability.
    - This gives output as expected.
    - This passes all test cases.

    - Implemented test_naive_bayes function by providing the test_X, test_Y, logprior, loglikelihood and naive_bayes_predict function as input parameters.
    - Need to find accuracy. 
    - Iterate through test_X, extract each tweet and pass it inside naive_bayes_predict, which will give the probability of prediction.
    - If the probability is > 0, then we define y_hat_i = 1, else it is 0. The y_hat_i is appended to a list called y_hat[].
    - Find error which is average of absolute value of differences of y_hats and test_y, since y_hats and test_y are of same size, so they can be iterated as a zip.
    - Find accuracy which is 1-error and return it.
    - This gives the output which matches the expected accuracy, but fails all test cases as mentioned in unit_test, where its mentioned in BUGS section.

  - PART - 4: FILTER WORDS BY RATIO OF POSITIVE AND NEGATIVE COUNTS
    - Implement get_ratio function by passing freqs dictionary and word.
    - Initialize a dictionary called pos_neg_ratoio, with positive, negative and ratio set to 0.
    - For all positive counts in freqs dictionary with label "1", we set the pos_neg_ration["positive"] as positive count and similarily for the nagtive counts. Counts for posituve and negative is implemented by using lookup().
    - For the ratio, we use the equation pos_neg_ratio = pos_neg_ratio["positive"]+1 / pos_neg_ratio["negative"]+1. 
    - This has passed all unit-test cases.

    - Implement get_words_by_threshold by passing freqs, label and threshold as input parameters.
    - Initialize an empty dictionary called word_list.
    - Iterate through the keys of the freqs dictionary.
    - Use the get_ratio function and pass the freqs and word, which will give the pos_neg_ratio.
    - If the label is 1 and the pos_neg_ratio["ratio"] > threshold value and if the label is 0 and the pos_neg_ratio["ratio"] < threshold value, then add the word to the word_list.
    - This doesn't pass all unit-test functions has some BUGS mentined in BUGS section.
<br><br>

- Partly implemented:
  - what features have not been implemented

<br><br>

- Bugs
  - PART-2: 
    - train_naive_bayes - Expected output doesn't match the regular output.
  
      ![image](https://user-images.githubusercontent.com/100334984/216846973-ac68eea3-85ea-4129-9b26-81b41171e176.png)
    - unittest.train_naive_bayes - KeyError: 'े' is obtained.
      ![image](https://user-images.githubusercontent.com/100334984/216847125-3c23de47-9463-4685-9717-9f97af47764b.png)
    - Error could be result2 is not loading the correct dictionary, which is done in line-309 of w2_unittest.py
      ![image](https://user-images.githubusercontent.com/100334984/216847217-b67d7aba-365d-4638-a039-0b27be0f328b.png)
    - Also opening the pkl file inside the supportedfiles directory, there appears to be a mismatch in the dictionary that we use and the values in the pre-loaded files inside supported files.

  - PART-3:
    - w2_unittest.unittest_test_naive_bayes - No test cases pass, possible reason of failure opening the pkl file inside the supportedfiles directory, there appears to be a mismatch in the dictionary that we use and the values in the pre-loaded files inside supported files.
    ![image](https://user-images.githubusercontent.com/100334984/216847405-61259eac-bd98-4594-91b6-323d29d4a0a5.png)
    
- PART-3:
  - w2_unittest.test_get_words_by_threshold - Few test cases failed, but 148 test cases passed and 4 test cases failed.
  ![image](https://user-images.githubusercontent.com/100334984/216847511-764874d2-1470-4f6d-8a0b-a1fef79598b3.png)

<br><br>


## Reflections

- Assignment is very good. Gives a thorough understanding of the basis of Logistic Regression and twitter sentiment analysis.
- Could be more better with test_cases failure handle scenarios.

## Output

### output:

<pre>
<br/><br/>
    Out[1] - True
    Out[4] - ['hello', 'great', 'day', ':)', 'good', 'morn']

    Out[6] - {('happi', 1): 1, ('trick', 0): 1, ('sad', 0): 1, ('tire', 0): 2}
    Expected Output: {('happi', 1): 1, ('trick', 0): 1, ('sad', 0): 1, ('tire', 0): 2}

    Out[7] - All tests passed

    Out[10] - 0.0
            9162
    Expected Output:
            0.0
            9165
    Out[11] - KeyError: 'े'

    Out[13] - The expected output is 1.5574658811595445
    Expected Output:
                    The expected output is around 1.55
                    The sentiment is positive.
    
    Out[14] - All tests passed

    Out[16] - Naive Bayes accuracy = 0.9955
    Expected Accuracy:
                        Naive Bayes accuracy = 0.9955
    
    Out[17] - I am happy -> 2.14
            I am bad -> -1.31
            this movie should have been great. -> 2.12
            great -> 2.13
            great great -> 4.26
            great great great -> 6.39
            great great great great -> 8.52
    Expected Output:
            I am happy -> 2.14
            I am bad -> -1.31
            this movie should have been great. -> 2.12
            great -> 2.13
            great great -> 4.26
            great great great -> 6.39
            great great great great -> 8.52
    
    Out[20] - -8.838016360554494

    Out[21] -
        Wrong output value for accuracy.
            Expected: 0.9955.
            Got: 0.973.
        Wrong output value for accuracy.
            Expected: 0.995.
            Got: 0.97.
        Wrong output value for accuracy.
            Expected: 0.995.
            Got: 0.975.
        Wrong output value for accuracy.
            Expected: 0.996.
            Got: 0.968.
        Wrong output value for accuracy.
            Expected: 0.996.
            Got: 0.976.
        0  Tests passed
        5  Tests failed
    
    Out[23] - {'positive': 162, 'negative': 18, 'ratio': 8.578947368421053}

    Out[24] - All tests passed

    Out[26] - 
    {':(': {'positive': 1, 'negative': 3675, 'ratio': 0.000544069640914037},
    ':-(': {'positive': 0, 'negative': 386, 'ratio': 0.002583979328165375},
    'zayniscomingbackonjuli': {'positive': 0, 'negative': 19, 'ratio': 0.05},
    '26': {'positive': 0, 'negative': 20, 'ratio': 0.047619047619047616},
    '>:(': {'positive': 0, 'negative': 43, 'ratio': 0.022727272727272728},
    'lost': {'positive': 0, 'negative': 19, 'ratio': 0.05},
    '♛': {'positive': 0, 'negative': 210, 'ratio': 0.004739336492890996},
    '》': {'positive': 0, 'negative': 210, 'ratio': 0.004739336492890996},
    'beli̇ev': {'positive': 0, 'negative': 35, 'ratio': 0.027777777777777776},
    'wi̇ll': {'positive': 0, 'negative': 35, 'ratio': 0.027777777777777776},
    'justi̇n': {'positive': 0, 'negative': 35, 'ratio': 0.027777777777777776},
    'ｓｅｅ': {'positive': 0, 'negative': 35, 'ratio': 0.027777777777777776},
    'ｍｅ': {'positive': 0, 'negative': 35, 'ratio': 0.027777777777777776}}

    Out[27] - 
    {'followfriday': {'positive': 23, 'negative': 0, 'ratio': 24.0},
    'commun': {'positive': 27, 'negative': 1, 'ratio': 14.0},
    ':)': {'positive': 2960, 'negative': 2, 'ratio': 987.0},
    'flipkartfashionfriday': {'positive': 16, 'negative': 0, 'ratio': 17.0},
    ':d': {'positive': 523, 'negative': 0, 'ratio': 524.0},
    ':p': {'positive': 105, 'negative': 0, 'ratio': 106.0},
    'influenc': {'positive': 16, 'negative': 0, 'ratio': 17.0},
    ':-)': {'positive': 552, 'negative': 0, 'ratio': 553.0},
    "here'": {'positive': 20, 'negative': 0, 'ratio': 21.0},
    'youth': {'positive': 14, 'negative': 0, 'ratio': 15.0},
    'bam': {'positive': 44, 'negative': 0, 'ratio': 45.0},
    'warsaw': {'positive': 44, 'negative': 0, 'ratio': 45.0},
    'shout': {'positive': 11, 'negative': 0, 'ratio': 12.0},
    ';)': {'positive': 22, 'negative': 0, 'ratio': 23.0},
    'stat': {'positive': 51, 'negative': 0, 'ratio': 52.0},
    'arriv': {'positive': 57, 'negative': 4, 'ratio': 11.6},
    'glad': {'positive': 41, 'negative': 2, 'ratio': 14.0},
    'blog': {'positive': 27, 'negative': 0, 'ratio': 28.0},
    'fav': {'positive': 11, 'negative': 0, 'ratio': 12.0},
    'fantast': {'positive': 9, 'negative': 0, 'ratio': 10.0},
    'fback': {'positive': 26, 'negative': 0, 'ratio': 27.0},
    'pleasur': {'positive': 10, 'negative': 0, 'ratio': 11.0},
    '←': {'positive': 9, 'negative': 0, 'ratio': 10.0},
    'aqui': {'positive': 9, 'negative': 0, 'ratio': 10.0}}

    Out[28] - 
        Wrong output values.
            Expected: {':p': {'positive': 104}}.
            Got: {':p': 105}.
        Wrong output values.
            Expected: {':p': {'ratio': 105.0}}.
            Got: {':p': 106.0}.
        Wrong output values.
            Expected: {':p': {'positive': 104}}.
            Got: {':p': 105}.
        Wrong output values.
            Expected: {':p': {'ratio': 105.0}}.
            Got: {':p': 106.0}.
        148  Tests passed
        4  Tests failed

    Out[29] - 
        Truth Predicted Tweet
        1	0.00	b'truli later move know queen bee upward bound movingonup'
        1	0.00	b'new report talk burn calori cold work harder warm feel better weather :p'
        1	0.00	b'harri niall 94 harri born ik stupid wanna chang :d'
        1	0.00	b'park get sunlight'
        1	0.00	b'uff itna miss karhi thi ap :p'
        0	1.00	b'hello info possibl interest jonatha close join beti :( great'
        0	1.00	b'u prob fun david'
        0	1.00	b'pat jay'
        0	1.00	b'sr financi analyst expedia inc bellevu wa financ expediajob job job hire'
    
    Input[30]:
        my_tweet = 'Another major improvement in timeline refresh speed just released – now 10X faster than a few months ago'
    Out[30] - 1.7894030910063101

<br/><br/>
</pre>
