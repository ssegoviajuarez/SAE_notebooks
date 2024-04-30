# SAE_notebooks
SAE Guidelines Jupyter notebooks

# Table of Contents
1. [Unit-Context Models](#unit-context-models)
   - [Limitations of Unit-Context Models](#limitations-of-unit-context-models)
2. [Gradient Boosting for Poverty Mapping](#gradient-boosting-for-poverty-mapping)
3. [Pros and Cons of Methods for Poverty Mapping in Off-Census Years](#pros-and-cons-of-methods-for-poverty-mapping-in-off-census-years)
   - [Unit-Context Models](#unit-context-models-1)
   - [Gradient Boosting](#gradient-boosting-1)
4. [Unit-Context Models – Technical Annex](#unit-context-models-technical-annex)
   - [Producing Estimators Based on Unit-Context Models](#producing-estimators-based-on-unit-context-models)
5. [Appendix](#appendix)
   - [Simulation Experiment 1 for Unit-Context Models](#simulation-experiment-1-for-unit-context-models)
      - [Unit-Context Models – Validation](#unit-context-models-validation)
      - [Unit-Context Models – Validation with Better Model Fit](#unit-context-models-validation-with-better-model-fit)
   - [Simulation Experiment 2 for Unit-Context Models](#simulation-experiment-2-for-unit-context-models)
      - [Unit-Context Models – Validation Across All Poverty Lines](#unit-context-models-validation-across-all-poverty-lines)

## [Unit-Context Models](#unit-context-models)

### [Limitations of Unit-Context Models](#limitations-of-unit-context-models)

## [Gradient Boosting for Poverty Mapping](#gradient-boosting-for-poverty-mapping)

## [Pros and Cons of Methods for Poverty Mapping in Off-Census Years](#pros-and-cons-of-methods-for-poverty-mapping-in-off-census-years)

### [Unit-Context Models](#unit-context-models-1)

### [Gradient Boosting](#gradient-boosting-1)





## [Unit-Context Models – Technical Annex](#unit-context-models-technical-annex)




### [Producing Estimators Based on Unit-Context Models](#producing-estimators-based-on-unit-context-models)

### Producing Estimators Based on Unit-Context Models

The production of estimators based on unit-context models is similar to those using regular unit-level models, except that unit-level covariates are not used. This implies that the share of welfare variation across households explained by the model's covariates is expected to be lower and, within many areas, welfare may be poorly explained. Still, unit-context models may be regarded as an approximation to the true underlying data generating process. Actually, they are particular cases of unit-level models (**Equation {eq}`eq:1-1**); consequently, normality and linearity assumptions need to be checked similarly with the corresponding covariates. The focus of this section is on the unit-context models as presented in {cite:t}`masaki2020small` and not those from {cite:t}`lange2018small` and {cite:t}`doi:10.1080/00220388.2012.682983`. The reason for this choice is that {cite:t}`lange2018small` and {cite:t}`doi:10.1080/00220388.2012.682983` approach relies on ELL's method, which suffers from the same issues noted by previous work (see {cite:t}`molina2010small`; {cite:t}`corral2020pull`; {cite:t}`corral2021map` among others). In addition, {cite:t}`masaki2020small` tested different methods, including EB, and concluded that EB provides a considerable gain in accuracy and efficiency over other methods.

Unit-context versions (i.e. those with aggregated covariates only) may be specified for either a one-fold nested-error model or a two-fold nested-error model. A possible unit-context model follows:

\[
y_{sach}=z_{sac}\alpha+t_{sa}\omega+g_{s}\lambda+\eta_{sa}+\varepsilon_{sach}
\]

where \(s\) is used for an aggregation level that is over the target areas (a super-area), and \(c\) is used for subareas. Hence, \(z_{sac}\) contains subarea-level characteristics, \(t_{sa}\) includes area-level characteristics, and \(g_{s}\) is composed of super-area-level characteristics (which may include super-area fixed effects). The regression coefficients across these levels are respectively denoted \(\alpha\), \(\omega\), and \(\lambda\). The random effects, \(\eta_{sa}\), are specified in this model at the area level. Note that, among the set of covariates in this model, none is at the unit level; covariates only vary at the subarea level.

Model selection may be implemented following the approach described in **{numref}`diagnostics:selection`**, except that only contextual variables will be among the pool of eligible covariates. Data transformation is also important in unit-context models and is emphasized by {cite:t}`masaki2020small`. In contrast to the data transformation used in **{numref}`diagnostics:selection`**, recommend transforming the dependent variable with ordered quantile normalization. Nevertheless, this transformation cannot be used for the most common poverty and inequality indicators beyond headcount poverty because the transformation is not reversible. EB point and noise estimates are obtained following a Monte Carlo simulation and parametric bootstrap procedures, respectively, similar to the conventional application of the EB method under a unit-level model and detailed in the technical annex (**{numref}`unit-level:annex:montecarlo:molina`** and **{numref}`unit-level:annex:montecarlo:bootstrap`**). Finally, {cite:t}`masaki2020small` also recommend adjusting the model-based estimators to match direct estimates, usually to the level where the survey is representative (benchmarking).

Benchmarking is not recommended unless publication requirements include that estimates of totals at a lower aggregation level add up to the estimated total at a higher level (e.g., the national level). The need to benchmark due to substantial discrepancies between the sum of estimated totals at the lower level and the estimated total at the higher level may indicate that the model assumptions are not satisfied. EB estimators based on a correct model are approximately model-unbiased and optimal in terms of minimizing the MSE for a given area; thus, when adjusted afterward for benchmarking, so that these match usual estimates at higher aggregation levels, the optimal properties are lost, and estimators usually become worse in terms of bias and MSE under the model.[^10] When benchmarking adjustments are large, as those likely required by estimators derived from unit-context model variants, it is an indication that the model does not hold for the data. Note that a significant bias in the final estimates may lead to considerable re-ranking of locations in terms of poverty estimates. Consequently, a limit on the acceptable bias should usually be determined according to needs. This is particularly important when determining priorities across areas based on small area estimates. If an area's true poverty rate is 50% and the method yields an estimator of 10% due to an incorrect model, there is a real risk that this area may not be assisted when needed. {cite:t}`molina2019desagregacion` suggests 5 or 10 percent of absolute relative bias as an acceptable threshold.

An additional problem for unit-context models in many applications is that it may not be possible to match census and survey PSUs. In some cases, it is due to confidentiality reasons and, in others, it is due to different sampling frames. The latter problem will likely affect applications where the census and survey correspond to different years. Fay-Herriot and other area or subarea models that use the same aggregated variables are an alternative approach to unit-context models for the case where the census is outdated, for which the model is not necessarily in question, since these models may be correctly specified. Of course, model checking is also needed.




## [Appendix](#appendix)

### [Simulation Experiment 1 for Unit-Context Models](#simulation-experiment-1-for-unit-context-models)

### Simulation Experiment 1 for Unit-Context Models

A simulation experiment is conducted with the purpose of illustrating the inherent bias of the resulting CensusEB estimators based on unit-context models due to biased estimators of the model parameters. To remove a source of bias of estimators based on these models, which is due to differences between the sample and census means of covariates as shown in the Appendix of {cite:t}`corral2021map`, the model is fit to the whole population data and small area estimates are also calculated based on the same population data. The simulation is inspired by those conducted by {cite:t}`marhuenda2017poverty` where the true data generating process is a two-fold nested-error model. This model will better accommodate the usual applications of poverty mapping, where household surveys use two-stage sampling. A two-fold structure also allows for the inclusion of contextual variables that are at the cluster level while the random location effect is specified at the area level, similar to {cite:t}`masaki2020small`. The creation of the census data set is similar to the one shown in section 3 of {cite:t}`corral2021map`.

A census data set of $N=20,000$ observations is created, where observations are allocated among $40$ areas $\\left(a=1,\\ldots,A\\right)$. Within each area, observations are uniformly allocated over 10 clusters $\\left(c=1,\\ldots,C_{a}\\right)$. Each cluster, $c$, consists of $N_{ac}=50$ observations, and each cluster is labeled from 1 to 10. The assumed model contains both cluster and area effects. Cluster effects are simulated as $\\eta_{ac}\\stackrel{iid}{\\sim}N\\left(0,0.05^{2}\\right)$, area effects as $\\eta_{a}\\stackrel{iid}{\\sim}N\\left(0,0.1\\right)$ and household-specific residuals as $e_{ach}\\overset{iid}{{\\sim}}N\\left(0,0.5^{2}\\right)$, where $h=1,\\ldots,N_{ac};\\:c=1,\\ldots,C_{a};\\:a=1,\\ldots,A.$ Covariates are simulated as follows:

1.  $x_{1}$ is a binary variable, taking value 1 when a random uniform number between 0 and 1, at the household-level, is less than or equal to $0.3+0.5\\frac{a}{40}+0.2\\frac{c}{10}$.

2.  $x_{2}$ is a binary variable, taking value 1 when a random uniform number between 0 and 1, at the household-level, is less than or equal to $0.2$.

3.  $x_{3}$ is a binary variable, taking value 1 when a random uniform number between 0 and 1, at the household-level, is less than or equal to $0.1+0.2\\frac{a}{40}$.

4.  $x_{4}$ is a binary variable, taking value 1 when a random uniform number between 0 and 1, at the household-level, is less than or equal to $0.5+0.3\\frac{a}{40}+0.1\\frac{c}{10}$.

5.  $x_{5}$ is a discrete variable, simulated as the rounded integer value of the maximum between 1 and a random Poisson variable with mean $\\lambda=3\\left(1-0.1\\frac{a}{40}\\right)$.

6.  $x_{6}$ is a binary variable, taking value 1 when a random uniform value between 0 and 1 is less than or equal to 0.4. Note that the values of $x_{6}$ are not related to the area's label.

7.  $x_{7}$ is a binary variable, taking value 1 when a random uniform number between 0 and 1 is greater than or equal to $0.2+0.4\\frac{a}{40}+0.1\\frac{c}{10}$.

The welfare vector for each household within a cluster within an area is created from the model with these covariates, as follows:

\[
y_{ach}=3+.09x_{1ach}-.04x_{2ach}-.09x_{3ach}+.4x_{4ach}-.25x_{5ach}+.1x_{6ach}+.33x_{7ach}+\\eta_{a}+\\eta_{ac}+e_{ach}
\]

The dependent variable, $y_{ach}$, is the log of the variable of interest. The poverty line in this scenario is fixed at $z=12$. This generation process is repeated 5,000 times. This will yield 5,000 true poverty rates for each area.

As already said, to show that estimators based on unit-context models are still biased even if the source of bias noted in {cite:t}`corral2021map` is removed, instead of drawing a sample from the population to fit the models, the models are fit to the whole set of census data. This eliminates the latter source of bias. The unit-context model includes the cluster means of the 7 covariates. In each of the 5,000 simulations, the following quantities are computed for the poverty rates and gaps in each area:

1.  True poverty indicators $\\tau_{a}$, using the "census".

2.  Census EB estimators $\\hat{\\tau}_{a}^{CEB_{a}}$ presented in {cite:t}`corral2020pull` based on a nested-error model with only **area** random effects and including the unit-level values of the covariates, and obtained using a Monte Carlo approximation with $M=50$ replicates. The $R^{2}$ of this unit-level model is a slightly below 0.5.

3.  Unit-context Census EB estimators $\\hat{\\tau}_{a}^{UC-CEB_{a}}$ based on a nested-error model with random effects at the **area level** obtained using a Monte Carlo approximation with $M=50$ replicates. This estimator follows the approach from Masaki et al. {cite:t}`masaki2020small` and uses only cluster means for all of the covariates. The $R^{2}$ of this unit-context model is below 0.05.

The average across the 5,000 simulations of the estimation errors for each area represent the empirical biases of the considered area estimators. The Stata script to replicate these simulations can be found in the appendix (**{numref}`off-census:appendix:experiment1:validation`**).

One could argue that, in this scenario, the $R^{2}$ of unit-context models is much lower than that one in the applications of {cite:t}`masaki2020small` and of {cite:t}`lange2018small`. For this reason, the simulation experiment is repeated modifying slightly the data generating process to increase the $R^{2}$. Specifically, in this experiment, the covariate $x_{7}$ is now generated from a random Poisson variable with mean $\\lambda=3\\left(\\frac{c}{20}-\\frac{a}{100}+u\\right)$, where $u$ is a random uniform value between 0 and 1, and $\\sigma_{e}$ is increased from 0.5 to 0.6. This modification leads to an $R^{2}$ of the unit-context model between 0.15 and 0.20, while for unit-level models the $R^{2}$ exceeds 0.60. The Stata script to replicate these simulations can be found in the following **{numref}`off-census:appendix:experiment1:better-fit`**.

#### [Unit-Context Models – Validation](#unit-context-models-validation)

The do-file below reproduces the simulation experiment described in **off-census:annex**, but considering unit-context models with a better $R^{2}$ and producing estimates for 2 different poverty thresholds. Note that the model is fit to the whole set of population data and then estimates are also obtained by simulating on to the whole set of population data.


#### [Unit-Context Models – Validation with Better Model Fit](#unit-context-models-validation-with-better-model-fit)

The do-file below reproduces the simulation experiment described in **off-census:annex**, but considering unit-context models with a better $R^{2}$ and producing estimates for 2 different poverty thresholds. Note that the model is fit to the whole set of population data and then estimates are also obtained by simulating on to the whole set of population data.


### [Simulation Experiment 2 for Unit-Context Models](#simulation-experiment-2-for-unit-context-models)

To further explore the bias of unit-context models and compare its performance to other methods, a final simulation is conducted following the data generation procedure used in **off-census:appendix:experiment1:better-fit**, but with some modifications. Firstly, the population size is $N=500,000$, and the observations are allocated among $A=100$ areas $a=1,\ldots,A$. Within each area $a$, observations are uniformly allocated over $C_{a}=20$ clusters $c=1,\ldots,C_{a}$. Each cluster $c$ consists of $N_{ac}=250$ observations. In this simulation experiment, we take a simple random sample of $n_{ac}=10$ households per cluster, and this sample is kept fixed across simulations. Using a sample, we can also compare with estimators based on FH model (discussed in **Chapter 3: area-level**). The model that generates the population data contains both cluster and area effects. Cluster effects are simulated as $\eta_{ac} \stackrel{iid}{\sim} N(0,0.1)$, area effects as $\eta_{a} \stackrel{iid}{\sim} N(0,0.15^{2})$ and household specific residuals as $e_{ach} \overset{iid}{\sim} N(0,0.5^{2})$, where $h=1,\ldots,N_{ac}$, $c=1,\ldots,C_{a}$, $a=1,\ldots,A$. Finally, $x_{7}$ is generated from a random Poisson variable with mean $\lambda=3\left(\frac{c}{20}-\frac{a}{100}+u\right)$, where $u$ is a random uniform value between 0 and 1. In this experiment, we take a grid of 99 poverty thresholds, corresponding to the 99 percentiles of the very first population generated. In total, 1,000 populations are generated. In each of the 1,000 populations, the following quantities are computed in every area for each of the 99 poverty lines:

1. True poverty indicators $\tau_{a}$, using the "census".

2. CensusEB estimators $\hat{\tau}_{a}^{CEB_{a}}$ presented in [Corral et al.](#), based on a nested-error model with only **area** random effects and including the unit-level values of the covariates, and obtained using a Monte Carlo approximation with $M=50$ replicates. The $R^{2}$ for this model is roughly 0.60.

3. Unit-context CensusEB estimators $\hat{\tau}_{a}^{UC-CEB_{a}}$ based on a nested-error model with random effects at the **area-level** obtained using a Monte Carlo approximation with $M=50$ replicates. This estimator follows the approach of Masaki et al. [^masaki2020small] and uses a model selected using lasso, as described in **diagnostics:selection**. The $R^{2}$ of the resulting model hovers around 0.17.

4. Area-level FH estimators $\hat{\tau}_{a}^{FH_{a}}$ based on the model described in **area-level:annex**. In this case, a separate model is needed for each of the 99 different poverty lines. Hence, the $R^{2}$ depends on the poverty line, but it ranges from 0.15 to 0.70.

The average difference between the true poverty indicator and the estimate across the 1,000 simulations represent the empirical bias for each area. The Stata script to replicate these simulations can be found in the appendix (**off-census:appendix:experiment2:validation**).[^12]

[^masaki2020small]: Masaki, T., Rao, J. N., & Chambers, R. (2020). Small area estimation with machine learning. *Statistical Science*, 35(3), 417-433.



#### [Unit-Context Models – Validation Across All Poverty Lines](#unit-context-models-validation-across-all-poverty-lines)

The Stata code below produces the simulations described in [off-census:annex](#off-census:annex). Here, a sample is drawn from the population and then, estimates are obtained for 99 different poverty lines. Each poverty line corresponds to a percentile of the very first generated population.

<details>

<summary>Tips for collapsed sections</summary>

### You can add a header

You can add text within a collapsed section. 

You can add an image or a code block, too.

```stata
set more off
clear all

global main     "C:\Users\\`c(username)'\OneDrive\SAE Guidelines 2021\"
global section  "$main\3_Unit_level\"
global mdata    "$section\1_data\"
global myfigs   "$section\3_figures\"
/*
Author: Paul Corral
Version @2 differs from previous one in that we create a model where 
UC models have a better fit (R2 ~ 0.18), also welfare is somewhat more skewed


We start off by creating a fake data set illustrated in Marhuenda et al. (2017).
 https://rss.onlinelibrary.wiley.com/doi/pdf/10.1111/rssa.12306
*/
/*
Purpose of file is to test SAE model performance by imputing on to the 
population instead of a sample. This should remove all other sources of bias.
*/

*===============================================================================
// Parameters for simulated data set
*===============================================================================
	version 15
	set seed 734137
	global numobs = 20000
	global areasize  = 500
	global psusize   = 50
	
	//We have 2 location effects below
	global sigmaeta_psu   = 0.05   
	global sigmaeta_area  = 0.1
	//We have household specific errors
	global sigmaeps   = 0.6
	//Poverty line fixed at 27.8
	global pline    = 13
	global lnpline = ln($pline)
	global pline1   = 28
	global lnpline1 = ln($pline1)
	local lines $pline $pline1
	//locals
	local obsnum    = $numobs
	local areasize  = $areasize
	local psusize   = $psusize
	local total_sim = 1
	
*===============================================================================
//1.Create simulated data
*===============================================================================
//Start off with # of observations
set obs `=`obsnum'/`areasize''	
	gen area = _n
		lab var area "Area identifier"
	//expand to create 10 psu per area
	expand `=`areasize'/`psusize''
	sort area
	//PSUs labelled from 1 to 10 within each area
	gen psu = _n - (area-1)*`=`areasize'/`psusize''
		lab var psu "PSU identifier"
	//expand to create 50 observations by psu	
	expand `psusize'
	sort area psu
	//Household id
	gen hhid = _n
		lab var hhid "Household identifier"
		
	//Covariates, some are corrlated to the area and psu's label
	gen x1=runiform()<=(0.3+.5*area/(`obsnum'/`areasize') + ///
	0.2*psu/(`areasize'/`psusize'))
	gen x2=runiform()<=(0.2)
	gen x3= runiform()<=(0.1 + .2*area/int(`obsnum'/`areasize'))
	gen x4= runiform()<=(0.5+0.3*area/int(`obsnum'/`areasize') + ///
	0.1*psu/int(`areasize'/`psusize'))
	gen x5= round(max(1,rpoisson(3)*(1-.1*area/int(`obsnum'/`areasize'))),1)
	gen x6= runiform()<=0.4
	gen x7=rpoisson(3)*(1*psu/int(`areasize'/`psusize')- 1*area/int(`obsnum'/`areasize')+ 1*uniform())
	
	//note that this matches the model from eq. 3 of Corral et al. (2021)
	gen XB = 3+ .09* x1-.04* x2 - 0.09*x3 + 0.4*x4 - 0.25*x5 + 0.1*x6 + 0.33*x7
		lab var XB "Linear fit"
		
	//Create psu level means...
	preserve 
	collapse (mean) x*, by(area psu)
	rename x* meanpsu_x* 
	tempfile psumeans 
	qui save `psumeans'
	restore 
	
	preserve 
	collapse (mean) x*, by(area)
	rename x* meanarea_x* 
	tempfile areameans 
	qui save `
```
</details>








# Poverty Mapping in Off-Census Years 
Considerable attention has been given to produce reliable poverty maps in off-census years. An updated poverty map is increasingly becoming an essential resource to improve the targeting of many social protection programs around the world, which was underscored by the rapid onset and widespread impact of the COVID-19 crisis. Even in the best-case scenarios, poverty maps that rely on unit-level small area estimation techniques combining a census and survey can only be obtained once a decade. In off-census years, the typical small area approach applied has been an area-level model, such as a Fay-Herriot or a sub-area-level model, such as the one proposed by [Torabi et al., 2014](citation#torabi2014small). Nevertheless, since the perceived gains in precision from area-level models are less than stellar, methods that combine unit- and area-level models have been proposed (see [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983); [Lange et al., 2018](citation#lange2018small); [Masaki et al., 2020](citation#masaki2020small)). These models are here called unit-context models and, although appealing, seem to yield considerably biased estimates.

Beyond the small area estimation literature, the machine learning literature has made several contributions to poverty mapping. Recent research in this area includes [Chi et al., 2021](citation#chi2021micro) and [Jean et al., 2016](citation#jean2016combining). The authors of these two papers created highly disaggregated poverty maps by modeling the direct estimates of an asset index at a very low geographical level (e.g., villages or enumeration areas) using satellite-derived covariates. The authors of those papers rely on machine learning approaches, such as gradient boosting and ridge regression, to obtain estimates for small areas. These models provide point estimates of poverty at a low geographical level, although they do not necessarily provide an adequate estimate of the method's noise. The methods are attractive since they present the possibility of producing a poverty map even when a contemporaneous or reliable census does not exist.

## Unit-Context Models <a name="unit-context-models"></a>

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



```{text}
![Empirical Bias and MSE for CensusEB based on a unit-level model and CensusEB based on a unit-context model (UC-CensusEB) and ELL FGT0 estimates from model based simulations](uc_fgt0)
Source: [Corral et al., 2021](citation#corral2021map). The figure is obtained from simulations based on 10,000 populations and samples as specified in [Corral et al., 2021](citation#corral2021map). The simulations illustrate that unit context (UC) model may yield FGT0 estimates that are upward biased and with MSEs that could be several orders of magnitude above those of CensusEB estimates, based on the analogous unit-level model, and for some areas may be almost as inefficient as ELL.
```



Unit-context models appear to yield upward biased FGT0 estimates in model-based simulations, as presented in the above figure (most areas show bias above 0). Since unit-context models are special cases of the models used in ELL and EB procedures, but without household-level characteristics, the between-household variation of welfare is not adequately explained by the model. [Corral et al., 2021](citation#corral2021map) suggest that part of the observed bias comes from this misspecification, with effects similar to omitted variable bias (OVB). Despite the bias, the empirical MSE of unit-context models seems to outperform that of ELL estimates.

Like traditional unit-level models, unit-context models also assume normally distributed errors and departures from normality may also produce bias (which might offset or compound the previous bias). This is why a considerable emphasis is placed on data transformation, all with the aim of approximating the normality assumption. Because of the poor model fit and potential deviations from normality, unit-context models also display considerable bias when estimating mean welfare.


```{text}
![Empirical Bias and MSE for CensusEB based on a unit-level model and CensusEB based on a unit-context model (UC-CensusEB) and ELL mean welfare estimates from model based simulations](uc_mean)
Source: [Corral et al., 2021](citation#corral2021map). The figure is obtained from simulations based on 10,000 populations and samples as specified in [Corral et al., 2021](citation#corral2021map). The simulations illustrate that unit-context models may yield mean welfare estimates that are considerably biased and with MSEs that could be several orders of magnitude above those of CensusEB estimates based on the analogous unit-level model and for some areas may be as inefficient as ELL.
```




## Notes <a name="notes"></a>

[^1]: Another approach for cases where the census is outdated is to fit a unit-level model considering only the covariates with low (or even null) variability along time. This approach reduces (or may even solve) the problem of using an outdated census.

[^2]: The method presents advantages over the traditional Fay-Herriot ([Fay 1979](#)) models: 1) it may be an alternative when there are multiple locations with very small samples, for which the sampling variance of the direct estimator (used on the left-hand side of the Fay-Herriot model) becomes 0, and 2) it may be used to obtain multiple indicators from a single model under reversible transformations.

[^3]: The average absolute empirical bias is the average across areas of the area-specific absolute biases.

[^4]: [Vishwanath](https://blogs.worldbank.org/opendata/using-big-data-and-machine-learning-locate-poor-nigeria)

[^5]: The method relies on a squared-error loss function where the sequential fits are added until there is no improvement in the loss function. For a detailed description of gradient boosting, refer to [Natekin 2013](#).

[^6]: [Corral 2021](#) provides a detailed explanation of how this dataset was created.

[^7]: The results shown here were obtained from Python.

[^8]: The quality of the covariates and how well these predict poverty at the modeling level determine the overall quality of the estimates obtained.

[^9]: What is shown in {numref}`xgboost` is the empirical MSE, not an estimate of the MSE.

[^10]: Beyond unit-context models, benchmarking in many instances may be necessary to ensure aggregate estimates are aligned to official published estimates.

[^11]: Covariates are simulated following [Corral 2021](#) who follow the approach from [Molina 2010](#) and [Marhuenda 2017](#), with slight modifications.

[^12]: Depending on the computing power, this may take longer than 2 days to run.

