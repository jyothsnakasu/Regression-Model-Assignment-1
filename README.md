# Regression-Model-Assignment-1

Data Analysis
library(ggplot2)
data(mtcars)
attach(mtcars)
## The following object is masked from package:ggplot2:
## 
##     mpg
This first look at the data shows us that HP and MpG are inversely related and manual transmission cars are generally more fuel efficient.

mtcars$amf[am==0]='AUT'
mtcars$amf[am==1]='MAN'
print(qplot(x=wt, y=mpg, colour=am, facets=.~amf, data=mtcars,main="MpG vs. Weight/Gearing"))


Looking further we see that manual transmission cars tend to have smaller weight and use less fuel.

Making our model
We will perform linear regression with all variables, and then perfom stepwise model selection to select the best predictors. cyl, am, hp and wt will be included in the final model.

fit<-glm(mpg~as.factor(cyl) + as.factor(vs) + as.factor(am) + as.factor(gear) + as.factor(carb) + disp + hp + drat + wt + qsec, data=mtcars)
library(MASS)
step <- stepAIC(fit, direction="both")
step$anova
Conclussions
Based on the final model fitting results, we can conclude that:

As wt increases per 1000lb (0.5 tons), the mpg will decrease by 2.5.
MpG will decrease very slighly with HP increase.
cyl increases from 4 to 6 to 8, will cause MpG to decrease by 3 and 2 times respectively.
Automatic gearing has higher MpG compared to manual gearing.
Appendix
Initial Explorations
plot(hp, mpg, pch=am,col=259,bg=7,
  xlab="Horsepower", cex=1.2,
  ylab="Miles per gallon", main="MpG vs. HP /Gearing")
legend("topright", c("AUT","MAN"), pch=c(0,1))


Final model
fit2<-glm(mpg ~ as.factor(cyl) + as.factor(am) + hp + wt, data=mtcars)
layout(matrix(c(1,2,3,4),2,2)) 
plot(fit2)

