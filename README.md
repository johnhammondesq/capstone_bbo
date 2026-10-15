Section 1: project overview
Briefly describe the BBO capstone project and its purpose.

Imperial college ML course capstone project

Capstone project: Black Box Optimisation for Imperial College Professional Certificate in Machine Learning 
and Artificial Intelligence.

We need to optimise the performance of 8 of "black box" functions F1 to F8. There is some information in the 
specification of the real world objectives of the function such as "it is for a recipe contest" and 
"the function is noisy".
We have initially been provided with 10 or more 
parameterised calls to each function and the value returned. 

Our goal is to MAXIMISE the value for each function by making a guess every week for 13 weeks through a portal 
for which the functions will be evaluated and returned in an email.

Each input is in the bounds [0,1] This is not stated in the Capstone but confirmed by staff independently.
  
This is adapted from a public competition in 2020 in a machine learning challenge event.

What is the overall goal of the BBO capstone project? 

The goal is to produce a documented process as to how we attempted the Optimisation so it may be reviewed by 
potential employers.
In the final weeks we will be competing against eachother on a "Friendly Basis" and it will be revealed what 
professional teams with much greater resources can achieve.

Why is it relevant in real-world ML? 

The Optimisation of systems is a common problem. For examples neural nets and LLMs have a large number 
of Hyperparameters chosen by the developer. We can't check all combinations and given a set of results we 
should like to be able to find the optimum.
Hyperparameters are chosen by minimizing the loss (or maximizing some metric) on a separate validation set — 
data the model never trains on directly. This distinction matters enormously, and is the whole reason a 
validation set exists as a concept separate from the training set. 

What’s the high-level idea?


How would this BBO capstone project support you in your current or future career?

It is hoped potential employers or academic staff could use my GitHub to assess my level of ML/AI skills 
together with Python skills on a proven project. 

Section 2: inputs and outputs
Clearly state what your model receives and returns.

Initially the model receives inputs and outputs by files initial_inputs.npy and intitial_outputs.npy which are 
NumPy values that can be loaded into Python. 

What are the inputs (query format, dimensions, constraints, etc.)? 

The generated inputs are put into a portal (assessible to students only so no URL given) and these are submitted
to a system which will generate outputs by return email. Results are contained in an email body and also in 2 attached
files which are not in the original .npy format. The results are cumulative so you receive the past inputs and outputs
and not just the current week.


I transform these to npy arrays within the files and include them in my main capstone program as documentation of 
each week's work. 

What is the expected output (response value, performance signal, etc.)? 
Include example formats, if possible.

The inputs have to follow a format of zero fronted by 6 decimal places delimited by a dash.

0.562189-0.356654-1.000000-1.000000 Example for a 4 dimensional input 

Section 3: challenge objectives
Outline what you are trying to achieve within the BBO capstone project.

I have created a dashboard to show my progress against the original maxima. My goal is to beat all originals

 Fn  Original Max    My new maxima
  1  7.71087511e-16            -inf
  2  6.11205216e-01  6.44501013e-01
  3 -3.48353134e-02            -inf
  4 -4.02554228e+00  6.12529679e-01
  5  1.08885962e+03  4.44052250e+03
  6 -7.14264948e-01            -inf
  7  1.36496830e+00  1.67764724e+00
  8  9.59848200e+00  9.97410000e+00


Is the goal to minimise or maximise the function(s)? 

All functions are to be maximised.

What constraints or limitations must you consider 
(e.g. number of queries, response delay and unknown function structure)?

The functions are not known and we have 13 weeks to optimise (you can fall behind and catch up). For what 
should be an automated system the response can seem very slow at 4 or 5 days but I believe this has been 
corrected.


Section 4: technical approach
Describe the strategies you used across your first three query submissions. 

The strategies used were 
1. Baysian optimisation (BO) with UCB acquisition function (the simplest form). Visualisations applied to 
low dimensional cases to ensure that the optimisation formula used was realistic and then faith it translated to 
higher dimensions.

You’re encouraged to treat this section as a living record – 
continue updating it as your approach evolves throughout the BBO capstone project.
What ML methods or heuristics do you use? 
Will you model the unknown function? 
Would you consider using SVMs, regressions or Bayesian techniques? 
How do you balance exploration and exploitation? 
What makes your approach thoughtful or unique?