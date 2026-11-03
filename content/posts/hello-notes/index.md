---
title: "Notes on Adam: From SGD to Adaptive Moments"
date: 2026-11-03
draft: true   # template note; visible only with `hugo server -D`
tags: [optimization, deep-learning]
summary: "A template note showing math, code, tables, and footnotes. Copy this folder to start a new note."
---

This is a **sample note**. It shows the features you can use in the learning log:
a table of contents, LaTeX math, code blocks, tables, footnotes, and images.

## Stochastic Gradient Descent

Given a loss $\mathcal{L}(\theta)$ and a minibatch gradient $g_t = \nabla_\theta \mathcal{L}_t(\theta_{t-1})$,
SGD updates

$$
\theta_t = \theta_{t-1} - \eta\, g_t .
$$

## Adam

Adam keeps exponential moving averages of the first and second moments[^adam]:

$$
\begin{aligned}
m_t &= \beta_1 m_{t-1} + (1-\beta_1)\, g_t \\
v_t &= \beta_2 v_{t-1} + (1-\beta_2)\, g_t^2 \\
\hat m_t &= \frac{m_t}{1-\beta_1^t}, \qquad \hat v_t = \frac{v_t}{1-\beta_2^t} \\
\theta_t &= \theta_{t-1} - \eta \,\frac{\hat m_t}{\sqrt{\hat v_t} + \epsilon}
\end{aligned}
$$

### In code

```python
def adam_step(theta, g, m, v, t, lr=1e-3, b1=0.9, b2=0.999, eps=1e-8):
    m = b1 * m + (1 - b1) * g
    v = b2 * v + (1 - b2) * g**2
    m_hat = m / (1 - b1**t)
    v_hat = v / (1 - b2**t)
    return theta - lr * m_hat / (v_hat**0.5 + eps), m, v
```

## Comparison

| Optimizer | State per param | Adaptive? |
|-----------|-----------------|-----------|
| SGD       | 0               | No        |
| Momentum  | 1               | No        |
| Adam      | 2               | Yes       |

> **Tip:** put images next to this file (same folder) and reference them as `![caption](figure.png)`.

## References

[^adam]: Kingma & Ba. [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980). ICLR 2015.
