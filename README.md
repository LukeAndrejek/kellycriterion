<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Understanding the Kelly Criterion</title>
  <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
  <script id="MathJax-script" async
          src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
  </script>
</head>
<body>
  <p>
    When I first heard about the Kelly criterion, my impression was that it provided a mathematically optimal way to determine what percentage of your available funds to wager on a bet depending on the distribution of outcomes of the wager. When reading summaries of the Kelly criterion, I tend to see statements like the following quote from Wikipedia: "The Kelly bet size is found by maximizing the expected value of the logarithm of wealth, which is equivalent to maximizing the expected geometric growth rate." After deriving the Kelly criterion myself, descriptions like this seem misleading. Let's derive the Kelly Criterion to assess this description.
  </p>
  <p>
    Suppose your friend offers to make a bet with you. You can wager any amount of money. If you win, your friend will pay you the amount you wagered times \(w\), but if you lose, you have to pay your friend the amount you wagered times \(l\). You know that your probability of winning is \(p\), and your probability of losing is \(q=1-p\). Your friend will make this bet with you as many times as you want. Suppose you have a certain amount of money, \(m_{0}\), that you can wager. What should you do?
  </p>
  <p>
    Let's first determine your expected outcome. If you win, then you keep your initial \(m_{0}\) and get an additional \(wm_{0}\). If you lose, then you start with your initial \(m_{0}\) but lose \(lm_{0}\). Thus the expected outcome of the first bet is
    \[
    E_{1}=\left(m_{0}+wm_{0}\right)p + \left(m_{0}-m_{0}l\right)q
    .\]
  You should only take the bet if you expect to gain more than you started with. That is,
    \[
    \left(m_{0}+wm_{0}\right)p + \left(m_{0}-lm_{0}\right)q > m_{0}
    .\]
  We can simplify and use \(q=1-p\) to obtain
    \[\left(1+w\right)p + \left(1-l\right)q > 1,\]
    \[p+wp+q-lq>1,\]
    \[1+wp-lq>1,\]
    \[wp>lq.\]
  So as long as \(wp>lq\), you should bet. The question is how much to bet.
  </p>
  <p>
    For simplicity, let's assume that each time you make a bet, you wager some fraction \(f\) of your remaining funds. Then each time you win, you multiply your funds by a factor of \(1+fw\), and each time you lose, you multiply your funds by a factor of \(1-fl\). Therefore, your bankroll after \(n\) bets is
    \[
    m_{n}=m_{0}\left(1+fw\right)^{k}\left(1-fl\right)^{n-k}
    \]
  where \(k\) is the number of wins and thus \(n-k\) is the number of losses. Each outcome involving \(k\) wins occurs with probability \(p^{k}q^{n-k}\), and there are \(C\left(n,k\right)\) ways of ordering the \(k\) wins and \(n-k\) losses among the \(n\) bets, where
    \[
    C\left(n,k\right)=\frac{n!}{k!\left(n-k\right)!}
    .
    \]
  Thus the probability of observing \(k\) wins, which we will define as \(p_{n}\left(k\right)\), is \(C\left(n,k\right)p^{k}q^{n-k}\). (Note that these probabilities follow a binomial distribution.)
  </p>
  <p>
    Since you can control \(f\), you want to choose a value of \(f\) which maximizes your wealth. One strategy would be to maximize the expected value of \(m_{n}\). We can use the binomial theorem to compute
    \[E_{n}=\sum_{k=0}^{n}m_{n}p_{n}\]
    \[=\sum_{k=0}^{n}m_{0}\left(1+fw\right)^{k}\left(1-fl\right)^{n-k}C\left(n,k\right)p^{k}q^{n-k}\]
    \[=\sum_{k=0}^{n}m_{0}\left[\left(1+fw\right)p\right]^{k}\left[\left(1-fl\right)q\right]^{n-k}\]
    \[=\left[\left(1+fw\right)p+\left(1-fl\right)q\right]^{n}.\]
  Thus you should choose \(f\) which maximizes
    \[
    \left(1+fw\right)p+\left(1-fl\right)q
    =p+fwp+q-flq
    =f\left(wp-lq\right)+1
    .\]
  Therefore, if your expected return on each bet is negative, i.e. \(E_{1}<m_{0}\), i.e. \(wp<lq\), i.e. \(wp-lq<0\), then the coefficient of \(f\) above is negative, and so you should choose the smallest possible value of \(f\), which is \(f=0\). That is, you should not take the bet. This is consistent with our previous findings. However, if your expected return on each bet is positive, i.e. \(E_{1}>m_{0}\), i.e. \(wp-lq>0\), then you should choose the largest possible value of \(f\), which is \(f=1\). That is, you should always wager your entire bankroll.
  </p>
  <p>
    Great, so have we answered the question? Well, let's think about how this strategy plays out. Suppose \(wp>lq\), and so you choose \(f=1\), and suppose \(l=1\), meaning that when you lose, you lose the entire amount wagered. Then your bankroll after \(n\) bets is \(m_{n}=m_{0}\left(1+w\right)^{k}0^{n-k}\). This means that if you lose any bet, i.e. if \(k<n\), then \(m_{n}=0\), which means that you are broke. Since the probability of losing at least one of \(n\) bets is \(1-p^{n}\), which converges to \(1\) as \(n\to\infty\), you will go broke at some point with probability \(1\). So choosing \(l=1\) simultaneously maximizes your expected bankroll and guarantees that your bankroll will eventually diverge from this expected bankroll.
  </p>
  <p>
    The problem with this strategy is that, counterintuitively, maximizing your expected bankroll does not maximize the bankroll that you are likely to observe. So let's instead try to maximize the most likely outcome. Since the probability of winning each bet is \(p\), then after \(n\) bets, you should expect the number of wins to be an integer \(k_{n}\) such that \(k_{n}/n\) is approximately \(p\). Furthermore, \(k_{n}/n\to p\) as \(n\to\infty\), and so the most likely bankroll after \(n\) bets converges to \(L_{n}=m_{0}\left(1+fw\right)^{pn}\left(1-fl\right)^{qn}\). In fact, since the probabilities \(p_{n}\left(k\right)\) follow a binomial distribution, one can show that \(p_{n}\) is maximized for any integers \(k\in\left[\left(n+1\right)p-1,\left(n+1\right)p\right]\), which is an interval containing \(pn\).
  </p>
  <p>
    We now need to maximize \(L_{n}\). This is a difficult formula to work with. Let's derive a helpful trick. Suppose we are trying to find the critical points of a function \(g\). Let \(h\) be is a strictly monotonic continuous function. Then \(h^{\prime}\) is never zero. Therefore, \(g^{\prime}\left(x\right)=0\) iff
    \[
    \left(h\circ g\right)^{\prime}\left(x\right)
    =h^{\prime}\left(g\left(x\right)\right)g^{\prime}\left(x\right)
    =0
    .\]
  Furthermore, if \(x\) is a critical point of \(g\), then
    \[
    \left(h\circ g\right)^{\prime\prime}\left(x\right)
    =\left[h^{\prime}\left(g\left(x\right)\right)g^{\prime}\left(x\right)\right]^{\prime}
    \]
    \[=h^{\prime}\left(g\left(x\right)\right)g^{\prime\prime}\left(x\right)+h^{\prime\prime}\left(g\left(x\right)\right)\left[g^{\prime}\left(x\right)\right]^{2}\]
    \[=h^{\prime}\left(g\left(x\right)\right)g^{\prime\prime}\left(x\right).\]
  Thus \(g^{\prime\prime}\left(x\right)\) and \(\left(h\circ g\right)^{\prime\prime}\left(x\right)\) have the same sign if \(h^{\prime}\left(g\left(x\right)\right)>0\), which is true if \(h\) is increasing, but they have different signs if \(h^{\prime}\left(g\left(x\right)\right)<0\), which is true if \(h\) is decreasing.
  </p>
  <p>
  Returning to \(L_{n}\), note that \(\log\) is a strictly monotonic continuous function, and so the critical points of \(L_{n}\) are also critical points of
    \[\log\left(L_{n}\right)=\log\left(m_{0}\left(1+fw\right)^{pn}\left(1-fl\right)^{qn}\right)\]
    \[=\log\left(m_{0}\right)+pn\log\left(1+fw\right)+qn\log\left(1-fl\right).\]
  Thus any critical point \(f^{*}\) of \(L_{n}\) will satisfy
    \[0=\frac{d}{df}\log\left(L_{n}\right)\big|_{f^{*}}=\frac{pnw}{1+f^{*}w}-\frac{qnl}{1-f^{*}l},\]
    \[\frac{pw}{1+f^{*}w}=\frac{ql}{1-f^{*}l},\]
    \[pw-pwf^{*}l=ql+qlf^{*}w,\]
    \[qlf^{*}w+pwf^{*}l=pw-ql,\]
  and since \(q+p=1\),
    \[f^{*}=\frac{pw-ql}{qlw+pwl}=\frac{pw-ql}{\left(q+p\right)wl}=\frac{pw-ql}{lw}=\frac{p}{l}-\frac{q}{w}.\]
  We also need to check that \(f^{*}\) is indeed a global maximum. Since \(\log\) is increasing, we know from earlier that \(L_{n}^{\prime\prime}\) has the same sign as \(\left[\log\left(L_{n}\right)\right]^{\prime\prime}\). We compute
    \[
    \left[\log\left(L_{n}\right)\right]^{\prime\prime}
    =\frac{d}{df}\left(pnw\left(1+fw\right)^{-1}-qnl\left(1-fl\right)^{-1}\right)
    \]
    \[=-\left(\frac{pnw^{2}}{\left(1+fw\right)^{2}}+\frac{qnl^{2}}{\left(1-fl\right)^{2}}\right),\]
  and since both fractions above are positive, the entire formula is negative. So \(L_{n}\) is concave down everywhere. Thus \(f^{*}\) is indeed a global maximum of \(L_{n}\), which establishes that selecting \(f=f^{*}\) indeed maximizes the most likely outcome. This choice of \(f\) is referred to as the Kelly criterion.
  </p>
  <p>
    The key feature of the Kelly criterion is that it maximizies the most likely outcome rather than the expected outcome. I am puzzled that this is not clearly stated in many summaries of the Kelly criterion. Furthermore, common descriptions of the Kelly criterion can be misleading. When Wikipedia says that the goal is to maximize "the expected value of the logarithm of wealth," it sounds as though the key insight of the Kelly criterion lies in applying the logarithm. Instead, the key insight lies in how you measure wealth. Since logarithms do not alter critical points,
  </p>
</body>
</html>
