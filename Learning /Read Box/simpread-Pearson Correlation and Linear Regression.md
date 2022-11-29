> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [sites.utexas.edu](http://sites.utexas.edu/sos/guided/inferential/numeric/bivariate/cor/)

> A correlation or simple linear regression analysis can determine if two numeric variables are signifi......

A correlation or simple linear regression analysis can determine if two [numeric variables](http://sites.utexas.edu/sos/variables/) are significantly linearly related. A correlation analysis provides information on the **strength** and **direction** of the linear relationship between two variables, while a simple linear regression analysis estimates parameters in a linear equation that can be used to **predict** values of one variable based on the other.

**Correlation**

The Pearson correlation coefficient, _r_, can take on values between -1 and 1.  The further away _r_ is from zero, the stronger the linear relationship between the two variables.  The sign of _r_ corresponds to the direction of the relationship.  If _r_ is positive, then as one variable increases, the other tends to increase.  If _r_ is negative, then as one variable increases, the other tends to decrease.  A perfect linear relationship (_r=_-1 or _r=_1) means that one of the variables can be perfectly explained by a linear function of the other.

Examples:

[![](http://sites.utexas.edu/sos/files/2015/07/Scatter_vipers-300x273.png)](http://sites.utexas.edu/sos/files/2015/07/Scatter_vipers.png) [![](http://sites.utexas.edu/sos/files/2015/07/Scatter_temp-300x273.png)](http://sites.utexas.edu/sos/files/2015/07/Scatter_temp.png)

**Linear Regression**

A linear regression analysis produces estimates for the **slope** and **intercept** of the linear equation predicting an outcome variable, _Y_, based on values of a predictor variable, _X._  A general form of this equation is shown below:

[![](http://sites.utexas.edu/sos/files/2015/07/regression-equation-300x57.png)](http://sites.utexas.edu/sos/files/2015/07/regression-equation.png)

The intercept, _b_0,  is the predicted value of _Y_ when _X_=0.  The slope, _b_1, is the average change in _Y_ for every one unit increase in _X_.  Beyond giving you the strength and direction of the linear relationship between _X_ and _Y_, the slope estimate allows an interpretation for how _Y_ changes when _X_ increases. This equation can also be used to predict values of _Y_ for a value of _X_.

Examples:

[![](http://sites.utexas.edu/sos/files/2015/07/Scatter_line_vipers-300x273.png)](http://sites.utexas.edu/sos/files/2015/07/Scatter_line_vipers.png)        [![](http://sites.utexas.edu/sos/files/2015/07/Scatter_line_temp-300x273.png)](http://sites.utexas.edu/sos/files/2015/07/Scatter_line_temp.png)

**Inference**

Inferential tests can be run on both the correlation and slope estimates calculated from a random sample from a population. Both analyses are _t_-tests run on the null hypothesis that the two variables are not linearly related. If run on the same data, a correlation test and slope test provide the same test statistic and _p_-value.

**Assumptions:**

*   [Random samples](http://sites.utexas.edu/sos/random/)
*   [Independent observations](http://sites.utexas.edu/sos/indobs/)
*   The predictor variable and outcome variable are linearly related (assessed by visually checking a scatterplot).
*   The population of values for the outcome are normally distributed for each value of the predictor (assessed by confirming the [normality](http://sites.utexas.edu/sos/normal/) of the residuals).
*   The variance of the distribution of the outcome is the same for all values of the predictor (assessed by visually checking a residual plot for a funneling pattern).

**Hypotheses:**

_Ho_: The two variables are not linearly related.  
_Ha_: The two variables are linearly related.

**Relevant Equations:**

[Degrees of freedom](http://sites.utexas.edu/sos/degreesfreedom/): _df_ = _n_-2

[![](http://sites.utexas.edu/sos/files/2015/07/correlation-300x160.png)](http://sites.utexas.edu/sos/files/2015/07/correlation.png)

[![](http://sites.utexas.edu/sos/files/2015/07/slope-300x164.png)](http://sites.utexas.edu/sos/files/2015/07/slope.png)

[![](http://sites.utexas.edu/sos/files/2015/07/yint-300x61.png)](http://sites.utexas.edu/sos/files/2015/07/yint.png)

**Example 1: Hand calculation**

These videos investigate the linear relationship between people’s heights and arm span measurements.

Correlation:  
[](https://www.youtube.com/watch?v=WFfv6JrasKg&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/WFfv6JrasKg/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=WFfv6JrasKg&rel=0&width=640&height=480)

Regression:  
[](https://www.youtube.com/watch?v=XExSeTuQzlc&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/XExSeTuQzlc/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=XExSeTuQzlc&rel=0&width=640&height=480)

Sample conclusion: Investigating the relationship between armspan and height, we find a large positive correlation (_r_=.95), indicating a strong positive linear relationship between the two variables. We calculated the equation for the line of best fit as _Armspan_=-1.27+1.01_(Height)_. This indicates that for a person who is zero inches tall, their predicted armspan would be -1.27 inches. This is not a possible value as the range of our data will fall much higher. For every 1 inch increase in height, armspan is predicted to increase by 1.01 inches.

**Example 2: Performing analysis in Excel 2016 on  
**Some of this analysis requires you to have the add-in [Data Analysis ToolPak](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcOHdBek9qOG9WUWM) in Excel enabled.

[Dataset used in videos](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcWklySjhQbmNONlE)

Correlation matrix and _p_-value:  
[PDF directions corresponding to video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FceGhXam5MMWpMZlE)  
[](https://www.youtube.com/watch?v=7yW61Tk5Kh0&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/7yW61Tk5Kh0/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=7yW61Tk5Kh0&rel=0&width=640&height=480)

Creating scatterplots:  
[PDF directions corresponding to video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcNlhKbnpyaFBhNFE)  
[](https://www.youtube.com/watch?v=k8AQ-5_OL-8&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/k8AQ-5_OL-8/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=k8AQ-5_OL-8&rel=0&width=640&height=480)

Linear model (first half of tutorial):  
[PDF directions corresponding to video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcbEVnb3BWNmhhYm8)  
[](https://www.youtube.com/watch?v=86Li1BEepvE&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/86Li1BEepvE/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=86Li1BEepvE&rel=0&width=640&height=480)

Creating residual plots:  
[PDF directions corresponding to video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcNktqdjVUSWhCVzg)  
[](https://www.youtube.com/watch?v=3RGWK9R68lw&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/3RGWK9R68lw/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=3RGWK9R68lw&rel=0&width=640&height=480)

Sample conclusion: In evaluating the relationship between how happy someone is and how funny others rated them, the scatterplot indicates that there appears to be a moderately strong positive linear relationship between the two variables, which is supported by the correlation coefficient (_r_ = .65). A check of the assumptions using the residual plot did not indicate any problems with the data. The linear equation for predicting happy from funny was _Happy_=.04+0.46_(Funny)._ The y-intercept indicates that for a person whose funny rating was zero, their happiness is predicted to be .04. Funny rating does significantly predict happiness such that for every 1 point increase in funny rating the males are predicted to increase by .46 in happiness (_t_ = 3.70, _p_ = .002).

**Example 3: Performing analysis in R**

The following videos investigate the relationship between BMI and blood pressure for a sample of medical patients.

[Dataset used in videos](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FccHFjekxVZ3U0bHM)

Correlation:  
[R script file used in video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcZW5FSTBqYlpFdDQ)  
[](https://www.youtube.com/watch?v=VT2yDF0nUSw&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/VT2yDF0nUSw/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=VT2yDF0nUSw&rel=0&width=640&height=480)

Regression:  
[R script file used in video](https://drive.google.com/uc?export=download&id=0B9b4o4b_Q7FcYmJqZzJBeU1MdjQ)  
[](https://www.youtube.com/watch?v=NsZ9PFWFabA&rel=0&width=640&height=480)

[![](https://img.youtube.com/vi/NsZ9PFWFabA/0.jpg)

![](http://sites.utexas.edu/sos/wp-content/plugins/wp-video-lightbox/images/play.png)

](https://www.youtube.com/watch?v=NsZ9PFWFabA&rel=0&width=640&height=480)