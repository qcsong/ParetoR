# ParetoR

Pareto-Optimization via Normal Boundary Intersection Method in Diversity Hiring <br />
Developer: Q. Chelsea Song <br />
Contact: qianqisong@gmail.com <br />
Last Update: 04/22/2017 

## Objective ##

The current R package provides a set of Pareto-optimal solutions that simultaneously optimize both diversity and criterion validity in a personnel selection scenario [see Song, Wee, & Newman (2017). The current package allows for implementation of (1) Pareto-optimal method that was adapted from De Corte, Lievens & Sackett (2007); (2) Pareto-optimal shrinkage formulae to estimate formula-adjusted shrunken Pareto-optimal solutions (see Study 2 of Song (2018; dissertation); (3) regularized Pareto-optimal method (see Study 3 of Song (2018; dissertation)). 

## Instructions ##

### Install and Load Package ###

1. Open an R console or RStudio window. (R can be downloaded for free from https://cran.r-project.org; RStudio can be downloaded for free from https://www.rstudio.com/)
2. Install R package "ParetoR" through Github by pasting and running the following commands in R console or RStudio:
   install.packages("devtools") <br />
   library("devtools") <br />
   install_github("Diversity-ParetoOptimal/ParetoR") <br />
   library("ParetoR") <br />

### Main Functions ###

**ParetoR function**  <br />
*Pareto-optimal method introduced by De Corte, Lievens & Sackett (2007)*  <br /> 

#### Example Implementation ####

1. Specify four inputs (example from DeCorte, Lievens & Sackett (2007) is given below): <br />
   &nbsp; # (1) Proportion of minority applicants (**prop**) = (# of minority applicants)/(total # of applicants) <br />
      &nbsp; ## *Example*: <br />
      &nbsp; &nbsp; &nbsp; &nbsp; prop <- 1/4 <br />
   &nbsp; # (2) Selection ratio (**sr**) = (# of selected applicants)/(total # of applicants) <br />
      &nbsp; ## *Example*: <br />
      &nbsp; &nbsp; &nbsp; &nbsp; sr <- 0.10 <br />
   &nbsp; # (3) Subgroup differences (**d**): standardized mean differences between minority and majority subgroups, on each predictor (in applicant pool) <br />
      &nbsp; ## *Example*: <br />
      &nbsp; &nbsp; &nbsp; &nbsp;  d <- c(1.00, 0.23, 0.09, 0.33) <br />
   &nbsp; # (4) Correlation matrix (**R**) = criterion & predictor inter-correlation matrix (in applicant pool) <br \>
      &nbsp; ## *Example*: <br />
      &nbsp; &nbsp; &nbsp; &nbsp; # Format: Predictor_1, ..., Predictor_n, Criterion <br />
&nbsp; &nbsp; &nbsp; &nbsp; R <- matrix(c(1, .24, .00, .19, .30, <br /> 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .24, 1, .12, .16, .30, <br /> 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .00, .12, 1, .51, .18, <br /> 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .19, .16, .51, 1, .28, <br /> 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .30, .30, .18, .28, 1), <br /> 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (length(d)+1),(length(d)+1)) <br /><br />
2. Paste and run the following command in R console or RStudio: <br \>
&nbsp; &nbsp; &nbsp; &nbsp; out = ParetoR(prop, sr, d, R)

#### Output Description ####

1. Pareto Optimal solutions (i.e., 21 equally-spaced solutions that characterize the Criterion validity – AI ratio tradeoff curve, and Predictor Weights at each point along tradeoff curve).
2. Plots (i.e., Criterion validity – AI ratio tradeoff curve, Predictor weights across trade-off points).

**ParetoShrinkage** function <br \>
*Estimate shrunken Pareto-optimal solution based on Pareto-optimal shrinkage formulae introduced in Study 2 of Song (2018; dissertation)* <br \>

#### Example Implementation ####

1. Specify inputs <br \>
 &nbsp; # (1) Calibration sample size  <br \>
 &nbsp; &nbsp; &nbsp; &nbsp; Ncal <- 100
 &nbsp; # (2) Number of predictors  <br \>
 &nbsp; &nbsp; &nbsp; &nbsp; numpred <- 4
 &nbsp; # (3) Number of Pareto-optimal points (i.e., number of sets of predictor weights)  <br \>
 &nbsp; &nbsp; &nbsp; &nbsp; p_pareto <- 21
 &nbsp; # (4) Vector of calibration sample job performance validity  <br \>
 &nbsp; &nbsp; &nbsp; &nbsp; load(R_perf_cal)
 &nbsp; # (5) Vector of calibration sample race bivariate correlation [i.e., correlation between race dummy variable (0-minority, 1-majority) and predictor composite score]  <br \>
 &nbsp; &nbsp; &nbsp; &nbsp; load(R_race_cal)

2. Paste and run the following command in R console or RStudio: <br \>
 &nbsp; # Estimate shrunken Pareto-optimal solution
 &nbsp; &nbsp; &nbsp; &nbsp; ParetoShrinkage(Ncal = Ncal, numpred = numpred, p_pareto = p_pareto, 
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; R_perf_cal = R_perf_cal, R_race_cal = R_race_cal, 
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; use = "Wherry)

#### Output Description ####

1. Formula-adjusted Pareto-optimal solution

#### Note ####

The program is modeled after DeCorte's (2006) TROFSS Fortran program and Zhou's (2006) NBI Matlab program (version 0.1.3).
The current version only supports scenarios where AI ratio and one other criterion are being optimized.

#### References ####

Song, Q. C., Wee, S., & Newman, D. (provisionally accepted). Diversity Shrinkage: Cross-Validating Pareto-Optimal Weights to  Enhance Diversity via Hiring Practices. *Journal of Applied Psychology*. <br />
Das, I., & Dennis, J. E. (1998). Normal-boundary intersection: A new method for generating the Pareto surface in nonlinear multicriteria optimization problems. *SIAM Journal on Optimization*, 8, 631-657. <br />
De Corte, W. (2006). *TROFSS User's Guide*. <br />
De Corte, W., Lievens, F., & Sackett, P. (2007). Combining predictors to achieve optimal trade-offs between selection quality and adverse impact. *Journal of Applied Psychology*, 92, 1380-1393. <br />
Wee, S., Newman, D. A., & Joseph, D. L. (2014). More than g: Selection quality and adverse impact implications of considering second-stratum cognitive abilities. *Journal of Applied Psychology*, 99, 547-563. <br />

#### Acknowledgements ####

Great appreciation to Dr. Serena Wee, Dr. Dan Newman and Dr. Wilfried De Corte for guidance and feedback on development of the program.

#### Web Application ####

We also developed a user-friendly web application to implement the Pareto-Optimal technique described in the current package (https://qchelseasong.shinyapps.io/ParetoR/). The web application (like the ParetoR package) uses only a correlation matrix, selection ratio, proportion of applicants from the minority group, and subgroup d values as input. It then provides a full set of Pareto solutions and their corresponding predictor weights.
