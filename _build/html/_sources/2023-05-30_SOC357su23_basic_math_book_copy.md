---
title: Some advanced arithmetic useful for the social sciences
author: McCarthy Bur, G
date: 2023-06-04
---

# Some basic operators

1. The summation operator tells us to sum from the observation denoted at the bottom of the capital greek letter $\Sigma$ ("sigma", which makes the "s" sound, as in **s**um) and go up until the observation denoted on top of the $\Sigma$. For us, the bottom item will almost always be individual (denoted *i*) equal to one, going up until individual equal to *n*, where *n* is the sample size. Examine this simple example data-set: 

    $\begin{array}{|c|c|}
    \hline
    i & y  \\ \hline
    1 & 3  \\ \hline
    2 & 10  \\ \hline
    3 & 2  \\ \hline
    4 & 4.5  \\ \hline
    \end{array}$

    Now, try to carry out the arithmetic operation indicated by the following notation: $\sum_{i=1}^n y_i$. 

    The numbering of individuals is, for our purposes, basically always arbitrary, and summation is 
    commutative anyways (the order of the items summed, or the *summands*, does not matter), so sometimes you 
    will see the sub- and superscripts omitted. 

    Let's suppose that we are interested in someone's highest year of education achieved and we have 
    observations on *n* = 10 individuals. Let their scores on the education variable be represented by the 
    vector $\vec{y} = [10, 12, 16, 12, 18, 10, 20, 18, 9, 10]^t$. All that the little "t" represents here is 
    that this is the transpose of the actual vector, which would be a column in the standard way of 
    representing data in matrices (rows are individuals, columns are variables). As you can see above, it 
    would waste a lot of space to represent column vectors the correct way in text documents, you will see 
    this convention very often. The idea is that we are making clear that this is a list of different 
    individuals and *not* the scores for one individual on ten different variables (if we wanted that, we'd 
    just omit the "t"). 
    
    Now, try to sum up these individuals' scores. The order here is arbitrary, but you might as well 
    conceptualize those scores above as being a specific case of the following 
    vector: $\vec{y} = [y_1, y_2, ... y_n]^t$. The last piece of notation is that we we will represent random 
    variables in their most
    abstract form with capital Roman letters; their sample equivalents have lowercase Roman letters. Unlike
    in most statistics books, I will consistently use Greek letters without hats to denote true population 
    parameters (most books usually, but not always, do this) and Greek letters with carets or "hats". Greek
    letters will be used in the conventional way: the sound they make indicates the parameter. Here, $\tau$
    ("tau") stands in for the total. Note that the notation means that to find the sample estimate of the 
    total of the random variable *Y*, we sum up the observed values in the sample, $y_i$.
    
    \begin{align*}
    \widehat{\tau}_Y &= \sum_{i=1}^n y_i
    \end{align*}

2. The mean is a measure of central tendency&mdash;something like the "characteristic value of a distribution", which the mean, median and mode all get at. **"Mean" is simply the formal term for the arithmetic average.** We'll focus on the simple case where possible outcomes are discrete, meaning that they are finite in number or **countably** infinite; most real-world data-sets involve discrete outcomes (but sometimes it is theoretically important to consider infinite outcomes; more on this later). 

    For example, if we record someone's income to the cent, while they could in theory tell us that they have 
    any number up to infinity, this is *countably* infinite; setting aside the formal definition, this means 
    basically that we'll never need to use a number whose distance to another number in the set of outcomes is 
    <0.01.
    
    **The mean is sometimes referred to as the expected value or expectation.** When we write the mean as an 
    expected value or expectation, we conceptualize it as a population level property; it is the weighted sum 
    of all possible values of the variable. So, we are summing over the possible outcomes of the variable when 
    we write the mean as an expectation&mdash;we are **not** summing over any observed individuals. 
    Many textbooks and internet sources do not change their notation here, which confuses new students, so I 
    will now re-index the sum. Let *o* index an outcome of the random variable *Y* (i.e., "*o*=5" would mean 
    the fifth possible outcome, where order again typically does not matter) and let *O* indicate the number 
    of possible outcomes. Then, for a discrete random variable:  
    
    \begin{align*}
    \mathbb{E}[Y] &= \sum_{o=1}^O y_o * \mathbb{P}(Y=y_o)
    \end{align*}

    This says that we look at each possible outcome *o*, starting with *o* = 1, and multiple the value of that 
    outcome $y_o$ by its probability of occurring, $\mathbb{P}(Y=y_o)$. 

    The exception for our notation is that I will consistently use $\widehat{\mu}_Y$ to indicate the sample 
    estimate of the population mean. Most textbooks use the notation $\bar{y}$. The problem with this notation 
    is that it breaks the general rule about Greek and Roman letters mentioned above and requires you to 
    memorize a new relationship. Just remember that $\widehat{\mu}_Y$ and $\bar{y}$ both indicate the sample 
    estimate of the mean (my notation here is increasingly common in data science and machine learning 
    contexts, e.g. Shalizi 2020, but it is still uncommon in social science). 
    
3. The variance is a measure of spread or dispersion. You can think about it as the expected difference between a randomly-selected observation and the mean. We define it formally as the expectation of the difference between the random variable *Y* and its mean $\mu_Y: \mathbb{V}[Y] = \mathbb{E}[(Y - \mu)^2]$. You may wonder why we square the difference. There is a very good reason for this that leads us to the proof of a useful fact about the mean, which is that it is the value for a given set about which all deviations are not just minimized but also zero!

    \begin{align*}
            &1. \mathbb{E}[Y - \mu_Y] = \mathbb{E}[Y] - \mathbb{E}[\mu_Y] 
                && \text{expectation operator is linear} \cr
            &2. \mathbb{E}[Y] = \mu_Y && \text{by definition} \cr
            &3. \mathbb{E}[\mu_Y] = \mu_Y && \text{expectation of a constant is just that constant} \cr
            &4. \mathbb{E}[Y - \mu_Y] = \mu_Y - \mu_Y = 0  && \text{arithmetic}
        \end{align*}   

   An extremely useful trick is to rewrite the variance as follows: 

    \begin{align*}
            &1. \mathbb{V}[Y] = \mathbb{E}[(Y - \mu_Y)^2] && \text{definition} \cr
            &2. = \mathbb{E}[Y^2 - 2*\mu_Y*Y + \mu_Y^2] && \text{binomial expansion AKA "FOILing"} \cr
            &3. = \mathbb{E}[Y^2] - \mathbb{E}[2*\mu_Y*Y] + \mathbb{E}[\mu_Y^2] 
                && \text{expectation operator is linear} \cr
            &4. = \mathbb{E}[Y^2] - 2*\mu_Y*\mathbb{E}[Y] + \mathbb{E}[\mu_Y^2]
                && \text{constants can be factored out} \cr
            &5. = \mathbb{E}[Y^2] - 2*\mu_Y*\mu_Y + \mathbb{E}[\mu_Y^2]
                && \text{definition of expectation} \cr
            &6. = \mathbb{E}[Y^2] - 2*\mu_Y^2 + \mu_Y^2
                && \text{expectation of a constant is just that constant, definition of square} \cr
            &7. = \mathbb{E}[Y^2] - \mu_Y^2
                && \text{arithmetic} \cr
            &8. \mathbb{V}[Y] = \mathbb{E}[Y^2] - \mathbb{E}[Y]^2
                && \text{definition of expectation} \cr
        \end{align*}

# Bivariate analysis: tests for a difference in means

Suppose that we are interested in determining whether two groups differ on some key outcome variable, such as their level of education or income. Let's be clear and formalistic about what we are after: we want to know whether or not, say, $\mu_{income | white}  = \mu_{income | black}$ or $\mu_{education | male}  = \mu_{education | female}$, where, to avoid the confusion caused by double subscripts, I've used the standard notation of a vertical bar to indicate "given that one is...". 

An obvious move here is just to replace these with their sample equivalents. So, using the older (if more confusing) notation for a sample mean, we might check whether $\overline{educ}_{male} = \overline{educ}_{female}$. And, in fact, this is exactly the right idea. The question now, however, is whether or not this difference is liable to have arisen by chance. 

You should stop and really consider this for a moment because this is the entire idea behind *inferential* statistics, as opposed to simply descriptive statistics (recall: descriptive statistics are just ways of summarizing the data we have, whether these are population-level or sample-level, without reference to whether these represent some other group). Why can't I trust, say, an observed difference of a year between a group of men and women? 

One intuitive reason not to trust this, and this is what you'll almost always hear in internet arguments about this sort of thing from people who are a little learnèd (if not too learnèd), is that the sample size might be too small. It turns out that this is a little too conservative: we need to *adjust* for small sample sizes, but if we have a truly random sample, any data are better than no data, and we can just adjust for the small sample size. 

Another reason not to trust this is that we don't have access to the whole population. This is really just the same objection as above: the sample size is too small. But, there's a subtle difference here: in this case, the gripe cuts to the heart of the matter. We don't just have a "small" sample size, whatever that might mean. We have a *sample*, period: some group of people smaller than the population we care about. And samples are noisy processes; that's what makes them great, in fact&mdash;they differ from the population only by random error ("noise"). But, we do need to take account of the error. So, how do we do that? 

Let's actually start with an easier, if slightly less-interesting, question: how would we do this for just one group's mean? It turns out that to calculate the sampling noise, we need a little bit of theory. 

## The Central Limit Theorem (CLT)

To make a judgment call about whether or not a sample mean $\overline{Y}$ represents a population mean $\mu_Y$, we need to have some sense for how the sample mean behaves across many samples. In other words, we need to know the probability distribution (technically: the probability density function, or PDF) of sample means. 

### Histograms and probability distributions

I will presume here that you are at least loosely familiar generally with histograms, from which we'll build an intuition for the Normal PDF; in the class for which these notes are being prepared, I'll have slides that walk you through how those work. Histograms are basically sample approximations of PDFs. On the X-axis, we have the possible-outcomes[^fn] for a variable; on the Y-axis, we have some kind of indication of the frequency of observations. So, any individual bar tells us the frequency of observations taking on a certain possible-value. For example, in the histogram for education below, about five percent of observations took on the value 11, meaning that five percent of the sample had 11 years of education. 

[^fn]: There is, unfortunately, no single-word term for "possible outcomes", which is a strange oversight. 

![Simple histogram for education](./figures/hist_educ.png)

PDFs are just the equivalent of a histogram when 1) we know about the true population distribution and 2) we have a continuous random variable. Recall that all actual sample data are discrete: we stop measuring the digits at a certain point (e.g., we measure height only to the tenth of an inch in some data-sets). But, in principle, height could be measured infinitely more-precisely with better and better microscopes, so it is a continuous random variable. But, it is rare to really know the PDF of a real-world variable; height happens to be approximately Normal, which is why I picked it as an example, but this is still only an approximation. 

![Simple histogram for height](./figures/hist_height.png)

However, it turns out, quite impressively, that sample means are Normally-distributed across many samples: this is the Central Limit Theorem (CLT). In other words, if you had a population from which you could take an infinite number of samples (with replacement), the histogram of sample means would basically be indistinguishable from a smooth, Normal curve. We'll learn two useful techniques that use this fact in due time.  

If the population is sufficiently large relative to the the size of the sample, each individual observation can be treated as independent of the others and taken from the same distribution (so long as they are drawn at random): they are "independent, identically-distributed" (IID) random variables.

It is important to note that each observation of the sample, before they are actually observed, is a random variable: when some researcher plans to sample 500 people and ask them their income, and she has not actually selected any individuals for inclusion, the income of the *i*th person, $Y_i$ is still a random variable. So, when we talk abstractly about the variance of a sample mean across many samples, we need to treat these sample means themselves as random variables. This is a major source of confusion early on, so remain *en garde* here: each actual observation in the sample is the *realization* of a random variable. It is often helpful to consider the analogy to an experiment in which we flip coins: the concept of "the outcome of the 10th coin I flip" is more-obviously a random variable for most people because it hasn't yet happened. While the person whose income I ultimately observe in the sample has already *obtained* that income, there is a point at which I don't know *which* person I'll observe, and thus that "person's" income is rather like the outcome of the as-yet-unflipped coin. 

So, we are after the variance of a sum of IID random variables (divided by the constant *n*).  While the extremely useful general formula for the variance of a sum of random variables is slightly complex (see appendix), it is not just extremely useful but extremely simple for independent random variables: it is just the sum of their variances. Let $\overline{Y}$ represent the sample mean of a random variable comprised of *n* IID random variables $Y_1, Y_2, ... Y_n$; each variable comes from a population distribution with standard deviation $\sigma_Y$, which we'll simply refer to using $\sigma$ for simplicity.  

   \begin{align*}
    \mathbb{V}[\overline{Y}] = \sigma^2_{\overline{Y}} &= \sum_{i=1}^n \mathbb{V}[\frac{Y_i}{n}] \cr
    &= \sum_{i=1}^n \frac{1}{n^2} \mathbb{V}[Y_i] \cr
    &= \frac{1}{n^2} (\sigma^2_1 + \sigma^2_2 + ... + \sigma^2_n) \cr
    &= \frac{1}{n^2} n*\sigma^2 \cr
    &= \frac{\sigma^2}{n} \cr
    \sigma_{\overline{Y}} &= \frac{\sigma}{\sqrt{n}}
    \end{align*}
    
## The standard error (sampling noise) for a difference in means

It turns out that the difference in means, which we tend to conceive naturally as two things combined, can be thought of as simply the mean of a single "difference" variable. This variable turns out to have a slightly different *t* distribution, and the exact calculation of degrees of freedom becomes somewhat involved (in fact, degrees of freedom no longer have to be integers, which is quite an interesting fact), but these are details that aren't really essential to an understanding of the basic point: we have a nearly-Normal sampling distribution for this difference in means.

Fortunately, we have already learned the key rule for the standard error for a difference in means; if two random variables are independent, the variance of the variables' sum *or* difference is just the sum of the variances. So, the sampling variance here is simply $\sigma^2_{\overline{Y}_F} + \sigma^2_{\overline{Y}_M}$, and the standard error is the root thereof. 

# Analysis of variance (ANOVA)

Earlier, we discussed one horn of inferential statistics, that of checking whether an observed difference between two groups is statistically significant. But we can also ask other interesting questions that will be useful to us later, such as how well group-identification *explains* outcomes: how good is a model that says that $\textbf{education} = \beta_0 + \beta_1*\textbf{gender} + \boldsymbol{\epsilon}$. 

Fundamentally, regression is a means of explaining variance, which is simply a deflated sum of squares. 
\begin{align*}
&\text{total sum of squares = TSS = } \sum_{i=1}^n (y_i - \bar{y})^2 \cr
&\text{sample variance = TSS/degrees of freedom =} \frac{\text{TSS}}{n - 1} = 
    \frac{\sum_{i=1}^n (y_i - \bar{y})^2}{n-1}
\end{align*}

For example, the analysis of variance (ANOVA) decomposition asserts the following, 
where *a* is the number of levels of a qualitative predictor of interest *A*: 

\begin{align*}
& \text{TSS} = \sum_{j=1}^a \sum_{i=1}^n (y_{ij} - \bar{y})^2 \cr
&= \sum_{j=1}^a \sum_{i=1}^n (y_{ij} - (\mathbf{\bar{y}_j} - \mathbf{\bar{y}_j}) - \bar{y})^2 \cr
&= \sum_{j=1}^a \sum_{i=1}^n (y_{ij} - \mathbf{\bar{y}_j} + \mathbf{\bar{y}_j} - \bar{y})^2 \cr
&= \sum_{j=1}^a \sum_{i=1}^n (\text{within-group deviation} + \text{between-group deviation})^2 \cr
&= \sum_{j=1}^a \sum_{i=1}^n (\text{within deviation})^2 + 
    \sum_{j=1}^a \sum_{i=1}^n (\text{between deviation})^2 + 
    2*\sum_{j=1}^a \sum_{i=1}^n (\text{between deviation} * \text{within deviation}) \cr
& \text{Note that the sum of a set of individual deviations from a mean is necessarily zero. Then...} \cr
&= \sum_{j=1}^a \sum_{i=1}^n (y_{ij} - \bar{y}_j)^2 + (\bar{y}_j - \bar{y})^2 \cr
&= \underbrace{\sum_{j=1}^a \sum_{i=1}^n (y_{ij} - \bar{y}_j)^2}_\text{within-groups variation}  + 
    \underbrace{\sum_{j=1}^a \sum_{i=1}^n  (\bar{y}_j - \bar{y})^2 }_\text{between-groups variation} \cr
\end{align*}

If we translate this into a regression context, we have the familiar result that the model sum of squares plus
the residual sum of squares is equal to the total sum of squares since the group mean value $\bar{y}$ is also the predicted value $\widehat{y}$.

## Appendix

### The general formula for the variance of a sum of random variables. 

Let *Y* be the sum of random variables $Y_1, Y_2, ... Y_k$. Assume centered variables for the sake of step 5, where we will want to replace each variable's deviation from its mean with a single symbol to make the multinomial expansion easier. This can be, in principle, any symbol; it seems most natural to just use the variable itself, and we often assume centered variables anyways. Note that there is absolutely no difference if I had used, say, $\Delta_{Y_j}$ to represent the deviation of the *j*th variable from its mean. 

To get an intuition for the correct algorithm for multinomial expansion, draw a picture of rectangle with both unique side lengths partitioned into $Y_1, Y_2, ... Y_k$. Then, find the area of the rectangle, which is logically equal, of course, to finding $(Y_1 + Y_2 + ... Y_k)^2$. The rectangle is now comprised of smaller rectangles with areas $(Y_1*Y_1), (Y_2*Y_1) ... (Y_k*Y_1)$ going down the first column, $(Y_1*Y_2), (Y_2*Y_2) ... (Y_k*Y_2)$ going down the second, etc. We can thus visualize this as operation as follows: write out $(Y_1 + Y_2 + ... Y_k)^2$ as $(Y_1 + Y_2 + ... Y_k)*(Y_1 + Y_2 + ... Y_k)$. Starting with the first (or second; it doesn't matter) set of parentheses, take each term, multiply it by every term in the second set of parentheses, then add them up, and then do this for each term in the first set. Then, add up all the summed terms. This corresponds to summing up all of the items in the variance-covariance matrix. It was too time-consuming for me to draw a picture of all of this in Markdown, but DeVellis (2003) is a good, unintimidating visual representation of this sort of proof (which is really useful in general in the context of statistics). 

By the way, it may be useful to note that to sum all entries in a matrix, we can write it as a quadratic form. If we have centered variables, our covariance matrix $\boldsymbol{\Sigma}$ is simply $\frac{1}{n-1}\textbf{X}^t\textbf{X}$, where $\textbf{X}$ is the data matrix. Then, to sum all elements in that matrix, we write. $\vec{1}^t\boldsymbol{\Sigma}\vec{1}$. This proof won't use matrix properties, though. 

 \begin{align*}
            &1. \mathbb{V}[Y] = \mathbb{E}[(Y - \mu_Y)^2] && \text{definition of variance} \cr
            &2. = \mathbb{E}[([Y_1 + Y_2 + ... Y_k] - \mu_Y)^2] && \text{definition of variable Y} \cr
            &3. = \mathbb{E}[([Y_1 + Y_2 + ... Y_k] - [\mu_{Y_1} + \mu_{Y_2} + ... \mu_{Y_k}])^2] \
                && \text{expectation operator is linear} \cr
            &4. = \mathbb{E}[(Y_1 - \mu_{Y_1} + Y_2 - \mu_{Y_2} + ... Y_k - \mu_{Y_k})^2]
                && \text{commutativity of addition} \cr
            &5. = \mathbb{E}[(Y_1 + Y_2 + ... Y_k)^2]
                && \text{definition of centered variables} \cr
            &6. = \mathbb{E}[Y_1^2 + (Y_2 * Y_1) + ... (Y_k * Y_1) + (Y_1 * Y_2) + Y_2^2 + (Y_3 * Y_2) ... ]
                && \text{picture the rectangle as mentioned above} \cr
            &7. = \mathbb{E}[\sum_{j=1}^k\sum_{i=1}^k Y_i * Y_j]
                && \text{generalizing the pattern} \cr
            &8. = \sum_{j=1}^k\sum_{i=1}^k \sigma^2_{Y_i, Y_j}
                && \text{definition of(co)variances} \cr
            &9. = \sum_{j=1}^k \sigma^2_{Y_j} + 2\sum_{i>j}^k\sum_{j=1}^k \sigma^2_{Y_i, Y_j}
                && \text{covariance matrix is symmetric}
        \end{align*}

Of course, we often work with variables&mdash;such as the sample means of women's education and that of men, $\overline{Y}_F$ and $\overline{Y}_{M}$&mdash;whose population covariance $\sigma_{\overline{Y}_F, \overline{Y}_M}$ is equal to zero. Then, only the first term of line 9 above is relevant to the calculation of the variance of a random variable which is itself the summation or addition of other random variables. 

