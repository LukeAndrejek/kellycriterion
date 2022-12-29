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
  When I first heard about the Kelly Criterion, my impression was that it provided a mathematically optimal way to determine what percentage of your available funds to wager on a bet depending on the distribution of outcomes of the wager. Let's dig into the Kelly Criterion and see if it accomplishes this goal.
</p>
<p>
  Suppose your friend offers to make a bet with you. You can wager any amount of money. If you win, your friend will pay you the amount you wagered times \(w\), but if you lose, you have to pay your friend the amount you wagered times \(l\). You know that your probability of winning is \(p\), and your probability of losing is \(q=1-p\). Your friend will make this bet with you as many times as you want. Suppose you have a certain amount of money, \(m_{0}\), that you can wager. What should you do?
</p>
<p>
  Let's first determine your expected outcome. If you win, then you keep your initial \(m_{0}\) and get an additional \(wm_{0}\). If you lose, then you start with your initial \(m_{0}\) but lose \(lm_{0}\). Thus the expected outcome of the first bet is
  \[E_{1}=\left(m_{0}+wm_{0}\right)p + \left(m_{0}-m_{0}l\right)q.\]
You should only take the bet if you expect to gain more than you started with. That is,
  \[\left(m_{0}+wm_{0}\right)p + \left(m_{0}-lm_{0}\right)q > m_{0}.\]
We can simplify and use \(q=1-p\) to obtain
  \[\left(1+w\right)p + \left(1-l\right)q > 1,\]
  \[p+wp+q-lq>1,\]
  \[1+wp-lq>1,\]
  \[wp>lq.\]
So as long as \(wp>lq\), you should bet. The question is how much to bet.
</p>
<p>
  For simplicity, let's assume that each time you make a bet, you wager some fraction \(f\) of your remaining funds. Then each time you win, you multiply your funds by a factor of \(1+fw\), and each time you lose, you multiply your funds by a factor of \(1-fl\). Therefore, your bankroll after \(n\) bets is \(m_{0}\left(1+fw\right)^{n_{w}}\left(1-fl\right)^{n_{l}}\) where \(n_{w}\) is the number of wins and \(n_{l}\) is the number of losses. Each outcome involving \(n_{w}\) wins and \(n_{l}\) losses occurs with probability \(p^{n_{w}}q^{n_{l}}\), and there are \(C\left(n,n_{w}\right)\) ways of ordering the (n_{w}\) wins and \(n_{l}\) losses, where
  \[C\left(n,k\right)={n! \over k!\left(n-k\right!\right)}.\]
Thus the probability of observing \(n_{w}\) wins and \(n_{l}\) losses is \(C\left(n,n_{w}\right)p^{n_{w}}q^{n_{l}}\).
</p>
</body>
</html>
