[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

>> It appears that exercise 2 is actually about confidence intervals and the impact the number of samples/iterations have on mean standard error and 90% confidence intervals (exponential distribution).

n = 10, iter = 1000

standard error 0.8913667060665624
confidence interval (1.3148711397797974, 3.8276580815898713)

n = 100, iter = 1000
standard error 0.21899890704411185
confidence interval (1.708245777096404, 2.3965912978228725)

n = 1000, iter = 1000
standard error 0.06278566176393083
confidence interval (1.8984605761473898, 2.1016869027154934)

As n increases we see a decrease in standard error and a tightening of the 90% confidence interval around 2 aka lambda aka expected mean


If the question is actually about goal scoring one 8-3... then below if the code, I ended up having to have a peak at the solution.  My RSME was roughly 1.4 with a 2 lambda and regardless of the number of iterations performed (i.e. 1000 to 100000).  Although mean error does decrease with more iterations it was darn near zero throughout indicating that this technique is roughly unbiased.

As for sampling error, as lambda increases so does the standard error. 


def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
    
 def Estimate6(lam=2, m=100000):

    estimates = []
    for i in range(m):
        L = SimulateGame(lam)
        estimates.append(L)

    print('Experiment 4')
    print('rmse L', RMSE(estimates, lam))
    print('mean error L', MeanError(estimates, lam))
    
    pmf = thinkstats2.Pmf(estimates)
    thinkplot.Hist(pmf)
    thinkplot.Config(xlabel='Goals scored', ylabel='PMF')
    
Estimate6()
