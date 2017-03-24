# muti

`muti` is an `R` package that computes the mutual information (MI) between two discrete random variables _X_ and _Y_.

You can install the development version with

```
if(!require("devtools")) {
  install.packages("devtools")
  library("devtools")
}
devtools::install_github("mdscheuerell/muti")
```

***

## Background

MI is the amount of information about one variable contained in the other; it can be thought of as a nonparametric measure of the covariance between the two variables. MI is a function of entropy, which is the expected amount of information contained in a variable. If _P_(_X_) is the probability mass function of _X_, then the entropy of _X_ is

_H_(_X_) = E[-ln(P(X))].

The MI between _X_ and _Y_ is then

MI(_X_,_Y_) = _H_(_X_) + _H_(_Y_) - _H_(_X_,_Y_)

where _H_(_X_,_Y_) is the joint entropy between _X_ and _Y_.

## Data discretization

`muti` computes MI based on 1 of 2 possible discretizations of the data:

1. __Symbolic__. In this case the _i_-th datum is converted to 1 of 5 symbolic representations (_i.e._, "peak", "decrease", "same", "trough", "increase") based on its value relative to the _i_-1 and _i_+1 values (see [Cazelles 2004](https://doi.org/10.1111/j.1461-0248.2004.00629.x) for details). Thus, the resulting symbolic vector is 2 values shorter than its original vector. For example, if the original vector was `c(1.2,2.1,3.3,1.1,3.1,2.2)`, then its symbolic vector for values 2-5 would be `c("increase","peak","trough","peak")`.

2. __Binned__. In this case each datum is placed into 1 of _n_ equally spaced bins. If the number of bins is not specified, then it is calculated according to Rice's Rule whereby `n = ceiling(2*length(x)^(1/3))`.

