# deep-learning-challenge⋅⋅

Module 21 Challenge for Vanderbilt Data Analytics February 2024⋅⋅

There are 5 files located in this repository, as follows:⋅⋅

This README file, AlphabetSoupCharity.ipynb, AlphabetSoupCharity.h5, AlphabetSoupCharity_Optimization.ipynb, and AlphabetSoupCharity_Optimization.h5.⋅⋅

Special Recognition: Ahmad Mousa is as passionate and caring as he is knowledgeable, and Joshua Steier never hesitates to help walk us through challenges.⋅⋅ 

I always do participate in office hours and study groups while working on projects with collaborators including but not necessarily limited to the following peers: Ilknur Sekmen, Justin Ibeh, Karson Kosek, Kiara Shannon, Luisa Dinwiddie, Margo Berry, Morgan Escue, Morgan Foge, Nathan Johnson, William Brewer, Andrew Clifft, Angela Reed, and Josh Gibson, and I did spend my time in stackoverflow.com, w3schools.com, geeksforgeeks.com, github.com, and bing's new copilot whom I currently consider > google ai; however, the bootcamp has added a new Xpert Learning Assistant, and my life is now complete. Thank you for this resource!⋅⋅

The Google Drive location for this file is as follows: https://drive.google.com/drive/folders/1AHr53s-y9UVh--CbluDeScYEORQ7PSOu?usp=sharing⋅⋅

# Overview 
  **The purpose of the analysis** is to study a database of grant applications to predict which ones might be successful.
# Results
  ## Data Preprocessing 
   **charity_data.csv** contains 34,299 records with 12 fields: EIN, NAME, APPLICATION_TYPE, AFFILIATION, CLASSIFICATION, USE_CASE, ORGANIZATION, STATUS, INCOME_AMT, SPECIAL_CONSIDERATIONS, ASK_AMT, and IS_SUCCESSFUL. 
   ### What variable(s) are the target(s) for your model? 
   The target column IS_SUCCESSFUL will be stripped from the X axis and moved to the y axis for training purpose. An IS_SUCCESSFUL "0" indicates an unsuccessful application (16,038 records) while "1" indicates a successful application (18,261 records).
   ### What variable(s) are the features for your model?
   EIN and NAME identify the applicant, APPLICATION_TYPE and CLASSFICATION are alphanumeric codes, AFFILIATION, USE_CASE, AND ORGANIZATION contain categorical data, STATUS is a boolean field with only 5 records containing a 0, SPECIAL_CONSIDERATIONS is a boolean field with only 27 records containing a Y, INCOME_AMT bins the results into 9 income ranges, and the vast majority (25,398) applicants chose the lowest ASK_AMT amount $5,000. 
   ### What variable(s) should be removed from the input data because they are neither targets nor features?
   The initial model removed EIN and NAME, but a corelation was later found between duplicate NAME values and IS_SUCCESSFUL while STATUS and SPECIAL_CONSIDERATIONS do not have a significant relationship with IS_SUCCESSFUL, so the optimized model retained NAME but dropped EIN, STATUS, and SPECIAL_CONSIDERATIONS.
 ## Compiling, Training, and Evaluating the Model
 I first mirrored the original model, but for the optimized model, I kept the NAME column and dropped STATUS and SPECIAL_CONSIDERATIONS, and I optimized the NAME by duplicates and ASK_AMT columns by the most common value. Special Note: I was able to achieve the desired result with the NAME cutoff at 2, meaning every NAME who was not a duplicate was changed to 'Other'. My goal was to focus on optimizing features so I could reduce the numbers of neurons, layers, and epochs, making the model run as lean as possible.
   ### How many neurons, layers, and activation functions did you select for your neural network model, and why?
   In the original model: the first hidden layer of 80 neurons used activation function tanh, the second hidden layer of 30 neurons used activation function relo, and the output layer used 1 neuron and a sigmoid function.  The optimized model was leaner, with the same 3 layers and activation functions but only 3, 2, and 1 neurons for a fast and efficient runtime.
   ### Were you able to achieve the target model performance?
   The original model took 3 minutes and 37 seconds but fell just shy of 75% accuracy with a final score rounded up to 73% while the optimized model succeeded with a complete runtime of only 50 seconds and a boosted 76% accuracy.
   ### What steps did you take in your attempts to increase model performance?
   Time and energy were not optimized in the first model for the following 3 reasons:  
   1) **Studied** STATUS and SPECIAL_CONSIDERATIONS for clues when they only offered significance for 35 fields total between them both.  
   2) **Ignored** one legitimate feature (NAME), not considering the impact duplicate names could have on an application's success.  
   3) **Failed** to optimize another (ASK_AMT). 23,917 of the 34,299 records asked for what is likely the base amount: 5,000. All other amount are marked "other".  
   + **Combining** these 3 observations, I dropped EIN, STATUS, and SPECIAL_CONSIDERATIONS, optimized NAME, APPLICATION_TYPE, CLASSIFICATION, INCOME_AMT, and ASK_AMT to increased accuracy while reducing the neurons, layers, and epochs to the lowest possible numbers for the leanest and most efficient successful result.
# Summary
  **When** results are only good 3 out of 4 times, we can safely suspect they have not been manipulated; however, we do want to draw out every byte of significance we can find in the data. A model should exist that loops through classification and numerical data to find corelations between our features and targets that our human eyes may have missed. Until then, a lasso regression might possibly have been able to do a better job of optimizing our data for analysis, but we would still have been relying on a black box algorithm. At the end of a study, we want to be able to understand our results even more than we believe them.  
  **No** results have meaning unless we can apply them somewhere. This model might in fact carry more significance for the Alphabet Soup underwriters; if any model can predict the outcome of a grant application through nothing but external factors, the application process itself likely needs a severe overhaul.

