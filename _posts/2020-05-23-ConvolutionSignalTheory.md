---
layout: post
title: Signal theory and Convolution
comment: true
---
<p align="center"> 
<img src="/blog/assets/CLT1.gif" width="800" height="300" alt="Central limit theorem">
</p>
<!--<img src="/blog/assets/jfourier.jpg" width="120" height="150" alt="fourier_gif"> -->



Convolution is a key to deciphering various aspects of signal theory. This concept is often left to its theoretical analysis and analytical perplexity. This is an attempt to illuminate this beautiful concept with some intuitive examples and explanations. 

## Introduction

Signals are waves that carry information. Anything that accepts a signal as input and gives an output signal is a system. Systems process and transform the information as a signal passes through them. Let's consider the following scenario-- when two people talk, the person speaking generates a input voice signal and the air channel b/w the two participants acts as a system. The voice signal flows through the air channel producing an output voice signal, received by the listener. 

<p align="center"> 
<img src="/blog/assets/conversation.gif" width="400" height="150" alt="converation">
</p>
<p align="center"> 
<img src="/blog/assets/system.png" width="650" height="150" alt="signal System">
</p>

The air channel alters the voice signal by adding distortions and noise. It is often desired to model and understand behavior of these systems. If we can somehow determine the equation governing the system, it would allows us to evaluate the behavior of the system for more types of signals. We can evaluate the effect of the channel on say, on WiFi signals or blue-tooth signals.

---

## Impulse response to Convolution

Interestingly, it turns out that a system provided with impulse function as an input, produces it's own equation as an output. This response(or output) of the system, measured using an impulse signal, is known as the ***Impulse response*** of the system. 

$$
\begin{align*}
  & h(t) =  x(t) \ast h(t)\\
  where, \\
  & x(t)=\delta(t) \\
\end{align*}
$$ 

The $$\ast$$ operator is used to denote convolution operation. Hence, convolution of impulse signal $$\delta(t)$$ with system $$h(t)$$ is known as the impulse response. We can think impulse function as an arrow to capture the characteristics of a system, which is otherwise not known. 

We can verify this fact in few lines of python code:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

imp = signal.unit_impulse(100, 'mid') #impulse signal
sig = np.repeat([0., 1., 0.], 100) #system function

#plot layout
fig = plt.figure(figsize=(15,5))
ax1 = fig.add_subplot(1,3,1)
ax2 = fig.add_subplot(1,3,2)
ax3 = fig.add_subplot(1,3,3)
ax1.set_title('Input')
ax2.set_title('System')
ax3.set_title('Response')

#output= imp * sig
response = signal.convolve(sig, imp, mode='same') / sum(sig) 

#plot
ax1.plot(imp,'orange')
ax2.plot(sig,'blue')
ax3.plot(response,'green')

```
The output looks like this: 
<p align="center"> 
<img src="/blog/assets/impulse_response.jpg" width="800" height="300" alt="impulse response">
</p> 


Here, the output of system is given as convolution of input signal $$h(t)$$ with system equation. The convolution of signal $$x(t)$$ with system $$h(t)$$ is defined as:

$$
\begin{align*}
  & \phi(t) =  x(t) \ast h(t)\\
  & \phi(t) =  \int_{-\infty}^\infty x(\tau) h(t-\tau)d\tau \\
\end{align*}
$$ 

Under the hood, the operation simply means flipping one of the signals and sweeping it across the entire range, evaluating area of the overlapping region. This is shown in the following animation from [wikipedia](https://en.wikipedia.org/wiki/Convolution).

<p align="center"> 
<img src="/blog/assets/Convolution_of_box_signal_with_itself2.gif" width="580" height="160" alt="convolution">
</p> 

<p align="center"> 
<img src="/blog/assets/Convolution_of_spiky_function_with_box2.gif" width="580" height="160" alt="convolution">
</p> 

Notice, how one signal changes and tries to capture some of the features of the another. Convolution operation is all about capturing the behavior of the system and applying them to input signals. The output is signal is derived using the characteristics of input signal as well as the system.

---

## Practical aspects of Convolution

Convolution is an essential operation in audio signal processing where the process is used to generate different sound effects in the multimedia industry. Here are two examples from [CKSDE](http://www.cksde.com/) which allows you to listen to convolution of two different audio samples.

### Example 1:

In this example, voice of a man is fed as an input to a system that produces metallic delay effect. 

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316686&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316698&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>
  
<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316689&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

### Example 2:

In this example, audio of a snare drum is fed as an input to a system that produces decaying white noise.

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332850&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332844&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332838&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>


Apart from this, convolutions also work with images and have immense applications in image recognition, filtering etc. These are some interesting topics, which I would cover separately in my future posts.

---

## Further exploration
Listen more to examples of convolution at [CKSDE](http://www.cksde.com/p_6_250.htm). This [video](https://ocw.mit.edu/resources/res-6-007-signals-and-systems-spring-2011/video-lectures/lecture-4-convolution/) at MIT opencourseware by Prof. Alan V. Oppenheim provides in-depth explanation of convolution in the light of signal theory.


---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/oldMagnum) or connect with me on [LinkedIn](https://www.linkedin.com/in/ankitk50/).
