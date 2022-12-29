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
  Let's first determine your expected outcome. If you win, then you keep your initial \(m_{0}\) and get an additional \(wm_{0}\). If you lose, then you start with your initial \(m_{0}\) but lose \(lm_{0}\). Thus the expected outcome of the first bet is \(E_{1}=\left(m_{0}+wm_{0}\right)p+\left(m_{0}-m_{0}l\right)q\).
</p>
</body>
</html>
