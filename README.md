# SAE_notebooks
SAE Guidelines Jupyter notebooks


# SAE_notebooks

## Table of Contents
1. [Poverty Mapping in Off-Census Years](#poverty-mapping-in-off-census-years)
2. [Unit-Context Models](#unit-context-models)
3. [Limitations of Unit-Context Models](#limitations-of-unit-context-models)
4. [Notes](#notes)

## Poverty Mapping in Off-Census Years <a name="poverty-mapping-in-off-census-years"></a>
Considerable attention has been given to produce reliable poverty maps in off-census years. An updated poverty map is increasingly becoming an essential resource to improve the targeting of many social protection programs around the world, which was underscored by the rapid onset and widespread impact of the COVID-19 crisis. Even in the best-case scenarios, poverty maps that rely on unit-level small area estimation techniques combining a census and survey can only be obtained once a decade. In off-census years, the typical small area approach applied has been an area-level model, such as a Fay-Herriot or a sub-area-level model, such as the one proposed by [Torabi et al., 2014](citation#torabi2014small). Nevertheless, since the perceived gains in precision from area-level models are less than stellar, methods that combine unit- and area-level models have been proposed (see [DOI:10.1080/00220388.2012.682983](citation#doi:10.1080/00220388.2012.682983); [Lange et al., 2018](citation#lange2018small); [Masaki et al., 2020](citation#masaki2020small)). These models are here called unit-context models and, although appealing, seem to yield considerably biased estimates.

Beyond the small area estimation literature, the machine learning literature has made several contributions to poverty mapping. Recent research in this area includes [Chi et al., 2021](citation#chi2021micro) and [Jean et al., 2016](citation#jean2016combining). The authors of these two papers created highly disaggregated poverty maps by modeling the direct estimates of an asset index at a very low geographical level (e.g., villages or enumeration areas) using satellite-derived covariates. The authors of those papers rely on machine learning approaches, such as gradient boosting and ridge regression, to obtain estimates for small areas. These models provide point estimates of poverty at a low geographical level, although they do not necessarily provide an adequate estimate of the method's noise. The methods are attractive since they present the possibility of producing a poverty map even when a contemporaneous or reliable census does not exist.

## Unit-Context Models <a name="unit-context-models"></a>
Unit-context models attempt to model the population's welfare distribution using only area-level covariates. More specifically, unit-context models combine unit and area-level information to model the transformed household-level welfare (unit) using only area-level covariates (context). Since unit-context models do not require census microdata, they have been proposed as an alternative approach for the case when the available census microdata is too outdated to be considered for use under the conventional model-based methods that include unit-level covariates.[^1]

...

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




## Poverty Mapping in Off-Census Years

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





## Notes

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

