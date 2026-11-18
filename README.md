# Capstone project: Black Box Optimisation for Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

## Section 1: Project overview

Imperial college ML course capstone project

We need to optimise the performance of 8 of "black box" functions F1 to F8. There is some information in the specification of the real world objectives of the function such as "it is for a recipe contest" and "the function is noisy".

We have initially been provided with 10 or more parameterised calls to each function and the value returned. 

Our goal is to MAXIMISE the value for each function by making a guess every week for 13 weeks through a portal for which the functions will be evaluated and returned in an email.

Each input is in the bounds [0,1] This is not stated in the Capstone but confirmed by staff independently.
  
This is adapted from a public competition in 2020 in a machine learning challenge event.

The goal is to produce a documented process as to how we attempted the Optimisation so it may be reviewed by potential employers.
In the final weeks we will be competing against eachother on a "Friendly Basis" and it will be revealed what professional teams with much greater resources can achieve.

The Optimisation of systems is a common problem. For examples neural nets and LLMs have a large number of Hyperparameters chosen by the developer. We can't check all combinations and given a set of results we should like to be able to find the optimum.

Hyperparameters are chosen by minimizing the loss (or maximizing some metric) on a separate validation set — data the model never trains on directly. 

It is hoped potential employers or academic staff could use my GitHub to assess my level of ML/AI skills together with Python skills on a proven project. 

## Section 2: Data

Initially the model receives inputs and outputs by files initial_inputs.npy and intitial_outputs.npy which are NumPy values that can be loaded into Python. 

The generated inputs are put into a portal (assessible to students only so no URL given) and these are submitted to a system which will generate outputs by return email. Results are contained in an email body and also in 2 attached
files which are not in the original .npy format. The results are cumulative so you receive the past inputs and outputs and not just the current week.

I transform these to npy arrays within the files and include them in my main capstone program as documentation of each week's work. 

The inputs have to follow a format of zero fronted by 6 decimal places delimited by a dash.

0.562189-0.356654-1.000000-1.000000 Example for a 4 dimensional input 

## Section 3: challenge objectives

I have created a dashboard to show my progress against the original maxima. My goal is to beat all originals

fn  original best 	my best
1.  7.71087511e-16  6.25449708e-05
2.  6.11205216e-01  6.44501013e-01
3. -3.48353134e-02 -3.48328477e-02
4. -4.02554228e+00  6.12529679e-01
5.  1.08885962e+03  7.56593488e+03
6. -7.14264948e-01 -3.01723506e-01
7.  1.36496830e+00  2.28758587e+00
8.  9.59848200e+00  9.97488500e+00


All functions are to be maximised.

What constraints or limitations must you consider 
(e.g. number of queries, response delay and unknown function structure)?

The functions are not known and we have 13 weeks to optimise (you can fall behind and catch up). For what 
should be an automated system the response can seem very slow at 4 or 5 days but I believe this has been 
corrected.



## Section 4: Model and Technical Approach

The strategies used were 
1. Baysian optimisation (BO) with UCB acquisition function (the simplest form). Visualisations were applied to low dimensional cases to ensure that the optimisation formula used was realistic and then we could have faith it translated to higher dimensions.
2. Baysian optimisation (BO) with EI acquisition function. 
3. Baysian optimisation (BO) with UCB acquisition function, but with added information showing the percentage 
attributed to the standard deviation component. 

I graph the lower dimensional functions. We use logs of F1 and assume the negatives are noise.

Bayesian optimisation by default models the function with mean and standard deviations.

Would you consider using SVMs, regressions or Bayesian techniques? 

Modelling in anything that is not Bayesian based is difficult in that you only have a snapshot based on very few values in a sparse high dimensional space. I may move from simpler BO to 
A linear model has no interior maximum, so the maximum can only sit on the edge of the allowed input region. 
That is the main difficulty with this approach.

The EI is considered a good balance between exploration and exploitation. UCB has kappa which is the number of 
standard deviations on top of the mean to consider.

## Section 5: HYPERPARAMETER OPTIMSATION
Description of which hyperparameters you have and how you chose to optimise them. 

## Section 6: RESULTS
I have created a dashboard to show my progress against the original maxima. My goal was to beat all originals

fn  original best 	my best
1.  7.71087511e-16  6.25449708e-05
2.  6.11205216e-01  6.44501013e-01
3. -3.48353134e-02 -3.48328477e-02
4. -4.02554228e+00  6.12529679e-01
5.  1.08885962e+03  7.56593488e+03
6. -7.14264948e-01 -3.01723506e-01
7.  1.36496830e+00  2.28758587e+00
8.  9.59848200e+00  9.97488500e+00


## (OPTIONAL: CONTACT DETAILS)