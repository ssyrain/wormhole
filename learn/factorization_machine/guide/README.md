
## Factorization Machine

For a *p* dimension example *x*, the factorization machine models the data by

![hat_y](hat_y.png)

where *w_i* denotes by the i-th element of the *p*-length vector *w*, and *v_i*
denotes by the i-th row of *p*-by-*k* matrix *V*.

Given training data pairs *(x,y)*, the factorization machine learns the model
*w* and *V* by solving the following objective:

<!-- \left[\sum_{(x,y)} \ell(\hat y(x,w,V), y)\right] + \lambda_1 |w|_1 + \frac{1}{2} \lambda_2
\|w\|_2^2 + \frac{1}{2} \mu_2 \|V\|_F^2 -->

![obj](obj.png)

The right choice of the embedding dimension *k* varies for different data, and
even for different features in the same dataset. We can specify *k* by the
rules:

```
if feature i appears more than 1024 times
    then use a 512 embedding size
else if feature i appears more than 256 times
    then use a 64 embedding
else
    no embedding
```

The according configuration is

```proto
embedding {
dim = 512
threshold = 1024
}
embedding {
dim = 64
threshold = 256
}
```