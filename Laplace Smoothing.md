# Laplace Smoothing

In Statistics, Laplace Smoothing is a technique to smooth categorical data. Laplace Smoothing is introduced to solve the problem of zero probability. By applying this method, prior probablity and conditional probability can be written as:
{{$
p_l(C_k) = p_l(Y = C_k) = (\Sigma^N_{i=1} I(y_i = C_k) + l ) / N +Kl
}}$

{{$
p(x_1 = a_j|y = C_k) = (\Sigma^N_{i=1} I(x_{1_i} = a_j,y_i = C_k) + l) / (\Sigma^N_{i=1} I(y_i = C_k) + Al )
}}$
, where *K* denotes the number of different values in *y* and *A* denotes the number of different values in *a*,,j,,. Usually *l* in the formula equals to 1. 
