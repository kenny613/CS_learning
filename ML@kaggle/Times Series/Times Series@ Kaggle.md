## Linear Regression
---
#### Time step features
- Linear regression with time dummy
```python
target = weight * time + bias # time = [0,1,...]
```

#### Lag features
- Linear Regression with lag feature
```python
target = weight * lag + bias
```
- With time dependence, we can include the information of pervious target 
- 1-step lag feature: Using `df['Lag'] = df['target'].shift(1)`
- |Hardcover|Lag_1|
|---|---|
|Date|||
|---|---|---|
|2000-04-01|139|NaN|
|2000-04-02|128|139.0|
|2000-04-03|172|128.0|
|2000-04-04|139|172.0|
|2000-04-05|191|139.0|
## Moving Average Plots
---
- Linear regression has **less lag** than the moving average and responds more quickly to changes in direction.

## Seasonality
---
#### One-hot encoding for <b>Seasonal indicators</b>
- One-hot encoding for days of weeks
	- |Date|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday|
	|---|---|---|---|---|---|---|
	|2016-01-04|0.0|0.0|0.0|0.0|0.0|0.0|
	|2016-01-05|1.0|0.0|0.0|0.0|0.0|0.0|
	|2016-01-06|0.0|1.0|0.0|0.0|0.0|0.0|
	|2016-01-07|0.0|0.0|1.0|0.0|0.0|0.0|
	|2016-01-08|0.0|0.0|0.0|1.0|0.0|0.0|
	|2016-01-09|0.0|0.0|0.0|0.0|1.0|0.0|
	|2016-01-10|0.0|0.0|0.0|0.0|0.0|1.0|
	|2016-01-11|0.0|0.0|0.0|0.0|0.0|0.0|
	- `n` variables, we only use `n-1` dummies (set all to `0` to indicate Monday)

--- 
## Fourier Features and the Periodogram

#### Autoregressive model

$$A \cos(2\pi \omega t + \phi) = \beta_1 \cos(2\pi \omega t) + \beta_2 \sin(2\pi \omega t),$$

with $𝛽_{1}=𝐴cos⁡(𝜙)$ and $𝛽_{2}=−𝐴sin⁡(𝜙)$
- We see time series as a sum of cosine waves with different amplitudes and frequencies
- $2\pi ft \rightarrow$ $f$ = 一秒行咗幾多fraction嘅wave, 乘以 $t$ 幾多秒
	- $ft = t$ 嘅時間總共咗幾多fraction嘅wave
## Periodogram
- Y-axis: $\left(a^{2}+b^{2}\right)/2$, which is
$$P\left(\frac{j}{n}\right) = \widehat{\beta}_1^2\left(\frac{j}{n}\right)+\widehat{\beta}_2^2\left(\frac{j}{n}\right)$$
- X-axis: frequency = $\frac{j}{n}$ 
- Obtain the dominating frequency by the how large is the value, we can conclude the periodicity of the data (weekly, quarterly, … frequency explain periodicity)
-
-

## Appendix
---
- Keywords: Spectral Analysis
- The context of the question is not entirely clear for me, however I'll try to answer from what I know. In the reverse order.

1. Isn't f*t = 1?  
- No. Here, t stands for the time (think of that as an offset from time t = 0). However, T is a period, and f = 1/T. Therefore, f*T = 1. When the value of t is an integral multiple of T, f*T is an integer, and the term sin(2πft)=sin(2πk)=0sin⁡(2𝜋𝑓𝑡)=sin⁡(2𝜋𝑘)=0.

2. Why do we multiply f*t?  
- Because sin function takes arguments which are angles, which are measured in degrees or radians. Also, it can be seen that ω=2πf𝜔=2𝜋𝑓, where ω𝜔 is angular velocity, measured in degrees or radians per unit time. If you multiply that by value of time, then the resulting unit is degree or radian, which can be fed to the sin function.

3. How does the term sin(2πft)sin⁡(2𝜋𝑓𝑡) come from?  
- It arises in describing waves, where the value sin(2πft)sin⁡(2𝜋𝑓𝑡) describes the time dependent magnitude of the wave. For a given t, it outputs the 'height' of the wave, which is sinusoidal. Since sin is a periodic function, the wave is periodic with period T = 1/f.
https://www.quora.com/How-does-the-term-sin-2*pi*f*t-come-from-I-know-that-sin-and-cosine-take-radians-as-arguments-which-will-be-pi-2-*-no-of-degrees-but-why-do-we-mulitply-f*t-Isnt-f*t-1
53.7K views

View 33 upvotes