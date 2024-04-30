# SAE_notebooks
SAE Guidelines Jupyter notebooks

Considerable attention has been given to produce reliable poverty maps in off-census years. An updated poverty map is increasingly becoming an essential resource to improve the targeting of many social protection programs around the world, which was underscored by the rapid onset and widespread impact of the COVID-19 crisis. Even in the best-case scenarios, poverty maps that rely on unit-level small area estimation techniques combining a census and survey can only be obtained once a decade. In off-census years, the typical small area approach applied has been an area-level model, such as a Fay-Herriot or a sub-area-level model, such as the one proposed by [Torabi et al., 2014](citation#torabi2014small). Nevertheless, since the perceived gains in precision from area-level models are less than stellar, methods that combine unit- and area-level models have been proposed (see [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983); [Lange et al., 2018](citation#lange2018small); [Masaki et al., 2020](citation#masaki2020small)). These models are here called unit-context models and, although appealing, seem to yield considerably biased estimates.

Beyond the small area estimation literature, the machine learning literature has made several contributions to poverty mapping. Recent research in this area includes [Chi et al., 2021](citation#chi2021micro) and [Jean et al., 2016](citation#jean2016combining). The authors of these two papers created highly disaggregated poverty maps by modeling the direct estimates of an asset index at a very low geographical level (e.g., villages or enumeration areas) using satellite-derived covariates. The authors of those papers rely on machine learning approaches, such as gradient boosting and ridge regression, to obtain estimates for small areas. These models provide point estimates of poverty at a low geographical level, although they do not necessarily provide an adequate estimate of the method's noise. The methods are attractive since they present the possibility of producing a poverty map even when a contemporaneous or reliable census does not exist.

## Unit-Context Models

Unit-context models attempt to model the population's welfare distribution using only area-level covariates. More specifically, unit-context models combine unit and area-level information to model the transformed household-level welfare (unit) using only area-level covariates (context). Since unit-context models do not require census microdata, they have been proposed as an alternative approach for the case when the available census microdata is too outdated to be considered for use under the conventional model-based methods that include unit-level covariates.[^1]

Previous applications of unit-context models for small area estimation were proposed by [Arora et al., 1997](citation#arora1997empirical), who studied the number of trips home students have taken, and by [Efron et al., 1975](citation#efron1975data), who looked at batting averages and toxoplasmosis cases. In these applications, the method appears to work well, although in both studies, the model with aggregate covariates is used to produce estimates of the area means of the dependent variable in the model (no transformation is considered). In the context of poverty, the target poverty indicators are typically complex nonlinear functions of the dependent variables in the model. Hence, properly replicating the full welfare distribution is essential as noted in [Chapter 4: Unit-Level Models](ref#unit-level). At the area level, this is complicated since household characteristics are not used in the model. Thus very little, if any, of the variation in welfare across households in the area is explained. If simple area means of the welfare variable of interest are the target, then, due to the assumptions embedded into the nested-error models used in Chapter 4: [Unit-Level Models](ref#unit-level), a transformation (such as log or log-shift) of the welfare variable is used as the dependent variable in the model. Consequently, the area means of the untransformed welfare variable are desired, which are then means of exponentials of the dependent variable. As is illustrated in the next section, when estimating indicators that are nonlinear functions of the dependent variables in the model, unit-context models will likely produce small area estimators of poverty with substantial bias.

[DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983) first considered unit-context models for poverty estimation in an application for Vietnam. In this application, the dependent variable was the household-level logarithm of per capita expenditure from the Vietnam Household Living Standard Survey from 2006, whereas all covariates are commune-level means obtained from a dated (1999) census. [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983) obtains ELL estimates of poverty for small areas under that model and compares the performance with typical ELL poverty estimates obtained using unit-level covariates from the Vietnam Household Living Standard Survey from 2006 and the 2006 Rural Agriculture and Fishery Census. The author finds that provinces and districts hovering around the middle of the distribution suffered considerable re-rankings across methods. However, those at the top and the bottom were relatively stable.

A similar approach to the one from [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983) was presented by [Lange et al., 2018](citation#lange2018small) as an alternative in cases when census and survey data are not from similar periods. However, the same inefficiency issues noted in Chapter 4: [Unit-Level Models](ref#unit-level) regarding ELL estimates would likely persist when considering a model using only area-level covariates. Improvements to the approach were seemingly made by [Masaki et al., 2020](citation#masaki2020small) by taking measures to address some of the shortcomings of a standard ELL approach and to obtain EB estimators from [Molina et al., 2010](citation#molina2010small). The authors conduct a design-based validation study using census data for Sri Lanka and Tanzania for a wealth index constructed by principal component analysis and suggest that the use of EB improves precision over ELL when implementing unit-context models.

Although the unit-context approach is attractive in that it does not require a contemporaneous census and can readily accommodate variables extracted from the emerging fields related to geospatial analysis, there are serious concerns about bias in unit-context estimators, as noted in [Corral et al., 2021](citation#corral2021map) as well as the concerns raised in the following section. The MSE from unit-context models is also likely to be incorrectly estimated since the required parametric bootstrap procedure assumes the underlying model using only area-level characteristics to be correct. In other words, the unit-context model's assumptions require household-level welfare to not depend on household-specific characteristics, which is unlikely to be the case. Incorrect MSE estimates risk presenting a map with considerable bias as being overly precise. Therefore, based on the currently available evidence, area-level models, like Fay-Herriot (Chapter 3: [Area-Level Models](ref#area-level)), are generally preferred over unit-context models (see the following section for more details).

In cases where neither area- nor unit-level models are advised due to data limitations, no clear consensus has emerged on the best path forward or if one even exists. In evaluating alternatives, practitioners should choose methods which rely on assumptions that are realistic to the circumstances in which the model will be employed, which are approximately unbiased (or its bias does not exceed a certain limit), and for which an accurate method exists to measure the small area estimators' MSE. In cases where the MSE cannot be adequately estimated, then at least it should be known in which (realistic) scenarios the approach has limited bias. If these conditions cannot be reasonably met, it is preferable to not produce a map than to produce one with potentially biased estimates, or one in which precision is overestimated, or most worrisome, both. In the next section, the limitations of unit-context models are discussed.


## Limitations of Unit-Context Models

Based on results from a validation study using model- and design-based simulations, [Corral et al., 2021](citation#corral2021map) conclude unit-context models, like those presented in [Masaki et al., 2020](citation#masaki2020small), [Lange et al., 2018](citation#lange2018small), and [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983), are not recommended except under exceptional cases due to the high likelihood of bias in estimates.[^2]

[DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983) application of a unit-context model to estimate poverty in small areas in Vietnam already hints toward potential problems of the unit-context approach. The author compares the results from unit-context models to those obtained via a standard unit-level method, ELL, and finds considerable changes in rankings. [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983) finds that differences in rankings are largest for locations around the middle of the distribution.

Despite the use of EB, the unit-context application by [Masaki et al., 2020](citation#masaki2020small), also provides hints of potential methodological problems with the approach. A ratio procedure was used to benchmark the values to ensure alignment between direct estimates at the level of representativeness and the estimates obtained by the approach. The need to benchmark indicates considerable discrepancies between the sum of estimated totals at the lower level and the estimated total at the higher level. The need to benchmark also suggests that the model's assumptions are not satisfied.

![Empirical Bias and MSE for CensusEB based on a unit-level model and CensusEB based on a unit-context model (UC-CensusEB) and ELL FGT0 estimates from model based simulations](uc_fgt0)
Source: [Corral et al., 2021](citation#corral2021map). The figure is obtained from simulations based on 10,000 populations and samples as specified in [Corral et al., 2021](citation#corral2021map). The simulations illustrate that unit context (UC) model may yield FGT0 estimates that are upward biased and with MSEs that could be several orders of magnitude above those of CensusEB estimates, based on the analogous unit-level model, and for some areas may be almost as inefficient as ELL.

Unit-context models appear to yield upward biased FGT0 estimates in model-based simulations, as presented in the above figure (most areas show bias above 0). Since unit-context models are special cases of the models used in ELL and EB procedures, but without household-level characteristics, the between-household variation of welfare is not adequately explained by the model. [Corral et al., 2021](citation#corral2021map) suggest that part of the observed bias comes from this misspecification, with effects similar to omitted variable bias (OVB). Despite the bias, the empirical MSE of unit-context models seems to outperform that of ELL estimates.

Like traditional unit-level models, unit-context models also assume normally distributed errors and departures from normality may also produce bias (which might offset or compound the previous bias). This is why a considerable emphasis is placed on data transformation, all with the aim of approximating the normality assumption. Because of the poor model fit and potential deviations from normality, unit-context models also display considerable bias when estimating mean welfare.

![Empirical Bias and MSE for CensusEB based on a unit-level model and CensusEB based on a unit-context model (UC-CensusEB) and ELL mean welfare estimates from model based simulations](uc_mean)
Source: [Corral et al., 2021](citation#corral2021map). The figure is obtained from simulations based on 10,000 populations and samples as specified in [Corral et al., 2021](citation#corral2021map). The simulations illustrate that unit-context models may yield mean welfare estimates that are considerably biased and with MSEs that could be several orders of magnitude above those of CensusEB estimates based on the analogous unit-level model and for some areas may be as inefficient as ELL.



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
