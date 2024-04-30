# SAE_notebooks
SAE Guidelines Jupyter notebooks

# Introduction

__Small area methods__ attempt to solve low representativeness of surveys within areas, or the lack of data for specific areas/subpopulations by incorporating information from outside sources (target datasets). 

__Target datasets:__ population census, large scale administrative records from tax administrations, or geospatial information produced using remote sensing. 

The strength of these target datasets is their granularity on the subpopulations of
interest.


# Model-based estimation

* Direct estimators are not efficient estimates for areas that
have not been included in the sample.

* Model-based estimation relies on a parametric model. Borrows strength 
by using a model.

* The domains are assumed to be part of a superpopulation whose
characteristics are estimated by the models.

* Estimation using frequentist or Bayesian approaches.

* Inference is under model conditional on the selected sample.

* Rao and Molina (2015) - the availability of these auxiliary data as well 
as a valid model are essential for obtaining successful small area estimates.

* Poverty is a nonlinear function of welfare, therefore sae methods of linear characteristics are invalid (Molina and Rao, 2010).A proposed solution to this problem is to use Monte Carlo simulation to obtain multiple vectors of
the measure of interest (Elbers, Lanjouw, and Lanjouw, 2003).


## Unit level models

A basis unit level population model assumes that the unit
$y$-values $y_{ch}$, associated with the units $h$ in the areas $c$, are
related to auxiliary variables $x_{ch}$ through a one-way nested
error regression model:

$$\[
\ln(y_{ch})= x_{ch}'\beta + u_{ch} \\
\ln(y_{ch})= x_{ch}\beta +\eta_{c} + e_{ch}
\]$$

where,

$$\[
h=1,...,N_{c} \\
c=1,...,C \\
\eta_{c}\sim\text{iid}N(0, \sigma_{\eta}^2) \\
e_{ch}\sim\text{iid}N(0, \sigma_{e}^2) \\
\]$$



  * Choose households (h) randomly from a cluster (c).
  * $\eta_c$ is the cluster-specific random effect: the difference between
  average consumption/income $y$ at cluster $c$ and the average consumption/income
  $y$ of all the country/sample.
  * $e_{ch}$ is the household-specific random effect: the deviation of the $h-th$
  household consumption/income $y$ from the averages of the $c-th$ cluster.
  * where $\eta_c$ and $e_{ch}$, are assumed to be independent from each other with different data generating processes.
  * Households within a cluster are usually not independent from one another, to allow for the clustering of households and their interrelatedness: $u_{ch} =\eta_c + e_{ch}$.
  *Note that the interrelatedness of $\eta_c$ across observations (households) is already a violation of OLS assumptions.
  
  Therefore the resulting model we wish to estimate is a linear mixed model ( contains both fixed and random effects).

To achieve valid small area estimates it is necessary that the set of explanatory variables, X, used in the first stage model can also be found in the census data. It is important that the variables are compared beforehand to verify that not only their definitions are in agreement, but also their distributions
  
### The ELL methodology

Elbers, Lanjouw, and Lanjouw (2003, henceforth ELL).

ELL focuses on welfare imputation methodology, nevertheless it can be
applied for other continuous measures aside from welfare.

ELL methodology for decomposing the first stage residuals's variance parameters.

Therefore the resulting model we wish to estimate is a linear mixed model ( contains both fixed and random effects).

The second stage consists in utilizing the parameter estimates from the
first stage and applying these to census data to obtain small area poverty and inequality measures.

The unit level model in equation (1) is fit by FGLS. This implies that, initially, 
the residuals are assumed to not be nested as in equation (1) and thus the model
is fit using ordinary least squares (OLS), after which the appropriate 
covariance matrix is estimated.

<br>

__Step 1.__ Fit the nested error model (1) to the survey data. This yields the set of the 
initial parameter estimates from the sampled data:

$$\hat{\theta}_0=( \hat{\beta}_0,\hat{\sigma}_{\eta0}^2,\hat{\sigma}_{e0}^2)$$

where the $0$ subscript is used hereafter to indicate that the estimates come from the original household survey. In the implemented version, the model is fit via FGLS as specified in Nguyen et al. (2018).

<br>
<details>
  <summary>__Click to see answer__</summary>
 <style>
  div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
  </style>
<div class = "blue">

  1. Estimating distribution of $\hat{\sigma}_{e0}^2$ (the Alpha model). 
  
  Parametric form of heteroskedasticity: $$\sigma_{e0}^2 = \frac{Aexp(Z'_{bh}\alpha) + B}{1 + exp(Z'_{bh}\alpha)}$$
  In In ELL (2003) this is simplified by setting $B = 0$ and $A = 1.05max(\hat{e}_{ch}^2)$, and thus the simpler form is estimated via OLS (This is the actual model used by PovMap, which we also implement):
  
  $$ln\frac{e_{ch}^2}{(A-e_{ch}^2)}= Z'_{bh}\alpha + r_{ch}$$
  This approach resembles that of Harvey (1976), nevertheless the prediction is bounded.
  By defining  $exp(Z'_{bh}\alpha)=D$ and using the delta method, the household specific        conditional variance estimator for $e_{ch}$ is:
  $$\hat{\sigma}_{e0}^2 \approx \frac{AD }{1 + D} + \frac{1}{2}\hat{var}(r) \frac{AD(1+D)}{(1 + D)^3}$$
  where $\hat{var}(r)$ is the estimated variance from the residuals of the model above.
  
  2. Estimating distribution of $\hat{\sigma}_{\eta0}^2$.
  
  ELL (2002) proposes 2 methods to obtain the variace of $\hat{\sigma}_{\eta0}^2$.
  
    1.1 By simulation
      
    
    1.2 By formula
    
    The `sae' command only allows for this using the ELL methodology.
    
  
  
  3. ELL's GLS estimator \hat{\beta}_0.
  Once with $\hat{\sigma}_{e,ch}^2$ and $\hat{\sigma}_{\eta}^2$, we can construct
  the covariance matrix of the error vector $u_{ch}=\eta_c + e_{ch}$ $\hat{\Omega}$ of   dimension $N\times N$. The estimates for the GLS are:

```math
  \[
  \hat{\beta}_0 = (X'W\Omega^{-1}X)^{-1}X'W\Omega^{-1}Y
  \]
  and
  \[
  Var(\hat{\beta}_0) = (X'W\Omega^{-1}X)^{-1}(X'W\Omega^{-1}WX)(X'W\Omega^{-1}X)^{-1}
  \]
```

  where $W$ is a $N\times N$ diagonal matrix of sampling weights. Beause $W\Omega^{-1}$
  is __usually not symmetric__ due to the difference in sampling weights between observations, the covariance matrix must be adjusted by obtaining the average of the 
  covariance matrix and its transpose. Check (Haslett et al., 2010). 
 
 </div>
</details>

  <br>

__Step 2.__ Draw new model parameters  $\theta^*=(\beta^*,\sigma_{\eta}^{2*},\sigma_{e}^{2*})$. Using the former obtained parameters (subscript 0) estimates as true parameters values to  draw from their respective asymptotic distributions as follows:

  2.1 First, regression coefficients are drawn from
  
  \[
  \beta^{*}\sim MVN(\hat{\beta}_0,\hat{vcov}(\hat{\beta}_0)) 
  \]
  
  2.2 The variance of the cluster effects is drawn, according to Demombynes (2008) and   Demombynes et al. (2002), from
  
  \[
  \sigma_{\eta}^{2*}\sim Gamma (\hat{\sigma}_{\eta0}^{2}, \hat{var}(\hat{\sigma}_{\eta0}^{2}))
  \]
  
  2.3 The variance of the household-level errors is drawn, according to Gelman 
  et al. (2004, pp. 364-365), from
  
  \[
  \sigma_{e}^{2*}\sim\hat{\sigma}_{e0}^{2}\frac{n-K}{\chi_{n-K}^{2*}}
  \]
  
  where $\chi_{n-K}^{2*}$ denotes a random number from a chi-squared distribution with   $n-K$ degrees of freedom. Here, $n$ is the number of observations in the survey     data used to fit the model and $K$ is the number of correlates used in the model.

<details>
  <summary>__Click to see answer__</summary>
  <p style="color:red">
  Aqui pongo el model fit via FGLS
  </p>
</details>

  <br>
  
__Step 3.__ Using the simulated model parameters in step 2, calculate the welfare for every household in the census $y_{ch}^*$ from the model as
\[
\ln(y_{ch}^*)= x_{ch}\beta^* +\eta_{c}^* + e_{ch}^*
\]

where the household-specific errors are generated as
\[
e_{ch}^*\sim\text{iid}N(0, \sigma_{e}^2*)\\
\]

and the location effects are generated as
\[
\eta_{c}^*\sim\text{iid}N(0, \sigma_{\eta}^2*)\\
\]

The vector of simulated welfares $y_{c}^*=(y_{c1}^*,y_{c2}^*,...,y_{cN_{c}}^*)'$
for every household within location $c$ will be of size $N_{c}$, the number of 
census housholds in the location.

<br>

__Step 4.__ Repeat steps $2$ and $3$ $M$ times. The standard value has been so far 
$M = 100$, although in practice a larger number of simulations is required to
approximate well the distributions and so a larger number should be executed.

<br>


__Step 5.__ With all vectors $y_{c}$ , $c = 1,...,C$ of simulated welfare in hand, 
indicators can be produced. Definebthe indicator of interest for a given 
simulated vector in location $c$ as $\tau_{C}^{ELL*}=f(y_{c}^*)$.

<br>


## Area level models


# Design-based estimation

Design-based (Model-assisted) methods

Definition (Rao, 2003): In the context of sample surveys, we refer to a domain
estimator as *direct* if it is based only on the domain-specic sample data.
(...)
Design based estimators make use of survey weights, and the
associated inferences are based on the robability distribution
induced by the sampling design with the population values held fix (...).


* Direct estimation
* Can allow for use of models (model-assisted)
* Inference is under the randomization distribution
