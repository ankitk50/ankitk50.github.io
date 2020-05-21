---
layout: post
title: Convolution in all its glory
comment: true
---
<p align="center"> 
<img src="/blog/assets/fourier_cummaltive.gif" width="480" height="360" alt="fourier_gif">
</p>
<!--<img src="/blog/assets/jfourier.jpg" width="120" height="150" alt="fourier_gif"> -->

> “There cannot be a language more universal and more simple, more free from errors and obscurities … Mathematical analysis is as extensive as nature itself, and it defines all perceptible relations.” ―**Joseph Fourier**, The Analytical Theory of Heat

The following post is an effort to provide an intuitive understanding into one of the most popular expansions in mathematics known as the *Fourier series.* 

## History

Baron Jean-Baptiste Joseph Fourier (1768−1830) was a French mathematician, known for his contributions in the field of heat transfer and study of vibrations. He also helped develop many mathematical tools with profound application in today's world. 

He famously pointed out that every periodic function can be made using a combination of sines and cosines. This idea of representation of signals as superposition of basic waves, is known as the *Fourier series*. The idea led to a development of a new branch of mathematics known as the [harmonic analysis](https://en.wikipedia.org/wiki/Harmonic_analysis). 


---
## Definition

Before jumping right on to the mathematical expression of Fourier series, it's worth spending some time pondering upon - a series being a combination of sines and cosines. We know that, $$sin(nx)$$ and $$cos(nx)$$ are periodic functions of period $$\frac{2\pi}{n}$$. This implies that period of these functions can vary for different values of 'n'. 

These sine and cosine functions with different values of 'n' are often termed as harmonics of the function. For e.g. $$sin(x)$$, $$sin(2x)$$, $$sin(3x)$$..., are different harmonics of a sine wave. 

<p align="center"> 
<img src="/blog/assets/sine_harmonics.gif" width="480" height="360" alt="fourier_gif">
</p> 
Analytically, Fourier series of a periodic function $$\phi(x)$$ with period T is defined as the sum of different harmonics of sines and cosines:

$$
\begin{align*}
  & \phi(x) = a_0+ \sum_{i=1}^\infty a_ncos(nx) + \sum_{i=1}^\infty b_nsin(nx) \\
 where,\\
  &  a_0= \frac{1}{T}\int_0^T\phi(x)dx; \\
  & a_n = \frac{2}{T}\int_0^T\phi(x)cos(nx) dx; \\
  & b_n = \frac{2}{T}\int_0^T\phi(x)sin(nx) dx; \\
\end{align*}
$$

---
## Analysis

So far, we have looked at the definition of the Fourier series, now it's time to get visual intuition using python. It's normal to have a counter-intuitive feeling about Fourier series. Especially, it is difficult to visualize a square wave (non-continuous function) being synthesized using sine and cosines(continuous functions). In the following section we'll try to visualize the same.


[Fourier series for a square wave](https://mathworld.wolfram.com/FourierSeriesSquareWave.html) $$\beta(x)$$ with period T is given as:

$$
\begin{align*}
\beta(x) = \frac{4}{\pi} \sum_{n=1,3,5...}^\infty \frac{1}{n}sin(\frac{n\pi x}{T})
\end{align*}
$$

Here, we implement a function to generate Fourier series of a square wave using the expression above. The function returns takes number of terms to generate as an input.


```python
from scipy import signal
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure
import numpy as np

def plot_square_wave(): #plot a square wave
    t= np.arange(0,100,1) #x-axis range
    plt.plot(t, 1*signal.square(.02 * np.pi  * t))

#sythesis a square wave using fourier series
def fourier_series(N): 
    x= np.arange(0,10,.1)
    series=0 
    resolution=0.2
    plot_square_wave()
    for n in range(1,N):
        harmonic=((4/(2*n-1)*np.pi)*np.sin(resolution*(2*n-1)*np.pi*x)/N) 
        series+=harmonic #synthesis equation
    return series 

array=fourier_series(10) #plotting the function
plt.plot(array)
```
The output should look like this:
<p align="center"> 
<img src="/blog/assets/square_wave_approximation.png" width="480" height="360" alt="fourier_gif">
</p> 
Below is an animated version showing a square function being synthesized by combination of sine waves. The graph on the left, plots each term of the series individually. While the one on the right gives a remarkable view of how the components add up. 

<figure class="half" style="display:flex">
    <img style="width:400px" src="/blog/assets/fourier_waves_superpose.gif">
    <img style="width:400px" src="/blog/assets/fourier_waves_sum.gif">
</figure>

Here, we notice that the approximation overshoots the desired value at the edges of the square wave. This peculiar behavior of Fourier series is known as the [Gibbs phenomenon](https://en.wikipedia.org/wiki/Gibbs_phenomenon). Informally, the Gibbs phenomenon reflects the difficulty inherent in approximating a discontinuous function by a finite series of continuous sine and cosine waves.

---

## Applications

So, why study Fourier series? Apart from it's analytical rigor and visual beauty, does it add something more to this world? 
As much of our knowledge of the world is contained in functions, it becomes inevitable that we understand them. The voltage produced by a microphone, as a function of time, represents music that can then be encoded digitally and stored on a compact disc. The position of a planet, as a function of time, represents an orbit.

Functions are everywhere. They are also extremely complex objects. As the case with the square wave as a function of sine and cosine, any sufficiently complex object is too difficult to comprehend in one glance, for our minds are limited. We therefore study functions from many vantage points and use multiple representations and transforms, such as Fourier series, to generate alternative representations of functions.

Although, the original motivation of the Fourier series was to solve heat equations, today, Fourier series has many similar applications in electrical engineering, vibration analysis, acoustics, optics, signal processing, image processing etc.


---

## Further exploration

Interested in exploring Fourier series? Check out [this video](https://www.youtube.com/watch?v=r6sGWTCMz2k) by 3B1B. A detailed analytical introduction to the topic can be studied at [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-signals/ee-fourier-series/v/ee-fourier-series-intro).

---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/oldMagnum) or connect with me on [LinkedIn](https://www.linkedin.com/in/ankitk50/).