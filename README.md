# Capstone project: Black Box Optimisation for Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

## Project overview

Imperial college ML course capstone project

We need to optimise the performance of 8 of "black box" functions F1 to F8. There is some information in the specification of the real world objectives of the function such as "it is for a recipe contest" and "the function is noisy".

We have initially been provided with 10 or more parameterised calls to each function and the value returned. 

Our goal is to MAXIMISE the value for each function by making a guess of inputs every week for 13 weeks through a portal for which the functions will be evaluated and returned in an email. This simulates the expensive nature of the real function evaluation.

Each input is between 0 and 1. This is not stated in the Capstone but confirmed by staff independently.
  
This is adapted from a public competition in 2020 in a machine learning challenge event. In the final weeks we will be competing against eachother on a "Friendly Basis" and it will be revealed what professional teams with much greater resources can achieve.

The Optimisation of systems is a common problem. For examples neural nets and LLMs have a large number of Hyperparameters chosen by the developer. We can't check all combinations and given a set of results we should like to be able to find the optimum.

It is hoped potential employers or academic staff could use my GitHub to assess my level of ML/AI skills together with Python skills on a proven project. 

## Data

[Component Datasheet](datasheet.md)

Initially the model receives inputs and outputs by files emailed by the university initial_inputs.npy and intitial_outputs.npy which are NumPy values that can be loaded into Python. 

The generated inputs are put into a portal (assessible to students only so no URL given) and these are submitted to a system which will generate outputs by return email. Results are contained in an email body and also in 2 attached
files which are not in the original .npy format. The results are cumulative so you receive the past inputs and outputs and not just the current week.

I transform these to npy arrays within the files and include them in my main capstone program as documentation of each week's work. 

The inputs have to follow a format of zero fronted by 6 decimal places delimited by a dash.

0.562189-0.356654-1.000000-1.000000 Example for a 4 dimensional input 

## Challenge Objectives

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



## Model and Technical Approach

The initial codebase was built from code in an example provided by the course. I wrote an ETL section to load the original .npy files  that contained the original readings into a Data Structure that contained the entire project information in one place. 
As discussed earlier the effort was focused first on F1 and F2 with 2 dimensional inputs because these were the only functions that could be visualised in the surrogate function by brute iteration through a grid of values. 
At the same time I built a maximisation function to maximise the value of the acquisition function for UCB only since the formula was very simple (mean plus a multiple of standard deviation). This allowed me to verify the formula maximum against the colour plots of the 2D inputs. Because of the vast differences in scale in F1, I did this using F2. 
This led to some modifications in that the search pattern was refined to use the SOBOL method where  I used the well-spread starting points via Sobol sequence which scales far better  than uniform random for covering a d-dimensional cube evenly.
The number of restarts on the optimisation was upped to 20 as I got different results each time until I did this as the maximiser got stuck in local maximums.
The Gaussian process had the single, simplest Kernel, rcb and isotropic and this also required that the number of restarts was upped to 100 to ensure repeatability without the code taking too long to run on my modest laptop.
A cell of code was written for challenge functions F3 to F8 where the input dimensions ranged from 3 to 8 using the previously verified optimisation for F1 and F2. 
There was also a print out that allowed me to review all the data in one cell. 
A results section took the predictions and rewrote them in the format required for input into the Capstone Portal.

As each week’s results arrived I wrote a new cell to incorporate that into the data structure. The results from the input.txt and output.txt was just incorporated into code as the simplest and clearest way to load the data, though I could have loaded the files directly that would have been more error prone.
Very early on I included the EI ( Expected Improvement ) acquisition function to my very simple UCB. This was far more complex being based on Normal and Cumulative Normal distributions, but is regarded as an excellent blend of exploration and exploitation though it is not tuneable like the UCB. It used the optimisation function verified earlier for UCB and was seen to generate improvements.
One of the weekly tasks asked for components of exploration vs exploitation. I was only able to give this for UCB as the upper bounds of the Gaussian process depended on the number of standard deviations added to the mean for a degree of exploitation. So I rewrote the process to list the percentage of the total prediction that was generated by the standard  deviation.
The primary modification of the Kernels was to introduce different length scales for each input variable. This gave an idea of the relative effect on the output of each input.
Inclusion of the Matern Kernel as this was popular in the literature. Inclusion of white noise was tried but didn’t seem to produce any results.
Introduction of a Logarithmic transform for F1 because of the difference in scale with the negative values being treated as noise didn’t improve things so I started to manually probe in directions around the highest output of the original data and found success going south west but as I got to the end I started to gamble and overshot into a negative area. 
I improved the analysis of the initial values by sorting them in order
I created a Dashboard of Results vs the best predictions from the original readings given for the functions.
Facilities to output readings to .csv spreadsheets for Excel analysis. Excel analysis was very convenient.
I computed the input correlations and a Principal Component Analysis of results which was not really useful because of the lack of correlation.




## HYPERPARAMETER OPTIMSATION

Looking at others' results I should have looped through the possible combinations as Bayesian Optimisation is very lightweight to run. I had to start simple to confirm I was doing the basics correctly.

Optimisation Function: Number of restarts=Random|Normal 
GP  Kernel: = rbf| matern with optional white noise 
Acquisition Function:  
Ucb: beta=no of sds., 
EI: xi = minimum improvement


## RESULTS
I have created a dashboard to show my progress against the original maxima. My goal was to beat all originals which was achieved

fn  original best 	my best
1.  7.71087511e-16  6.25449708e-05
2.  6.11205216e-01  6.44501013e-01
3. -3.48353134e-02 -3.48328477e-02
4. -4.02554228e+00  6.12529679e-01
5.  1.08885962e+03  7.56593488e+03
6. -7.14264948e-01 -3.01723506e-01
7.  1.36496830e+00  2.28758587e+00
8.  9.59848200e+00  9.97488500e+00

| Fn | d | Best in supplied data | Best found |
|---|---|---|---|
| F1 | 2 | 7.71087511e-16 | **6.25449708e-05** | 
| F2 | 2 | 0.611 | **0.645** | 
| F3 | 3 | −0.034835 | **−0.034832** | 
| F4 | 4 | −4.03 | **0.612** | 
| F5 | 4 | 1,089 | **7,566** | 
| F6 | 5 | −0.714 | **−0.302** | 
| F7 | 6 | 1.365 | **2.287** | 
| F8 | 8 | 9.598 | **9.975** | 




## Repository layout
```text
├── .gitignore                                # don't load these files to git
├── LICENSE.txt                               # MIT standard licence
├── README.md                                 # this file
├── capstone.xlsm                             # all inputs and outputs for each function on eight sheets in the workbook
├── datasheet.md                              # a description of the data used for capstone
├── model_card.md                             # how the model works and its purpose
├── requirements.txt                          # versions of software required to replicate this process
├── initial_data/                             # initial function evaluations for functions 1 to 8
│   └── function_n/                           # sample function directory
│       ├── initial_inputs.npy                # inputs defined as saved numpy arrays
│       └── initial_outputs.npy               # outputs defined as saved numpy arrays
├── CAP01_MOD12/ ... CAP13_MOD24/             # set of directories detailing work for 13 Capstone stages for modules 12 to 24
│   └── CAP05_MOD16/                          # directory of capstone stage 05 for course module 16
│       ├── Module16answer.docx               # downloadable word file with course answers
│       ├── Module16answer2.docx              # a second set of course answers
│       ├── capstone 16.ipynb                 # the version of the program at the capstone stage
│       ├── inputs.txt                        # the inputs file returned by email from the portal - history of this and previous weeks edited into array definition
│       └── outputs.txt                       # the outputs file returned by email from the portal
├── CAPSTONE_CONCLUSION/                      # directory containing the Capstone Conclusions
└── src/                                      # capstone source directory
    ├── capstone.ipynb                        # main working version of the capstone jupyter notebook
    └── plotting_utils.py                     # plotting of grid estimations for low dimension functions

```
## CONTACT DETAILS
John Hammond — email johnhammondesq@yahoo.co.uk Questions and suggestions are welcome as GitHub issues on this repository.

## Licence

Code and documentation: MIT licence (see [LICENSE](license.txt)). The challenge functions and initial data belong to the Imperial College PCMLAI programme and are included for educational use only.