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

Signals are waves that carry information. Anything that accepts a signal as input and gives an output signal is a system. Systems process and transform the information as a signal passes through them. Let's consider the following scenario-- when two people talk, the person speaking generates an input voice signal, and the air channel b/w the two participants act as a system. 

<figure align="center">
<img src="/blog/assets/conversation2.gif" width="220" height="250" alt="converation">
<figcaption align="center" style="font-size:15px" ><em><b>Fig 1:</b> An exemplary conversation </em></figcaption>
</figure>

The voice signal flows through the air channel producing an output voice signal, received by the listener. The air channel alters the voice signal by adding distortions and noise.

<figure align="center">
<img src="/blog/assets/system.png" width="650" height="150" alt="signal System">
<figcaption align="center" style="font-size:15px" ><em><b>Fig 2:</b> System input output </em></figcaption>
</figure>


It is often desired to model and understand the behavior of these systems. If we can somehow determine the equation governing the system, it would allow us to evaluate the behavior of the system for more types of signals. We can evaluate the effect of the channel on say, on WiFi signals, or blue-tooth signals.

---

## Impulse response to Convolution

Interestingly, it turns out that a system provided with impulse function as input produces its equation as an output. This response(or output) of the system, measured using an impulse signal, is known as the ***Impulse response*** of the system. 

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

<figure align="center">
<img src="/blog/assets/impulse_response.jpg" width="800" height="300" alt="impulse response">
<figcaption align="center"  style="font-size:15px" ><em><b>Fig 3:</b> Convolution of an impulse with a system </em></figcaption>
</figure>


Here, the output of the system is given as convolution of input signal $$h(t)$$ with system equation. The convolution of signal $$x(t)$$ with system $$h(t)$$ is defined as:

$$
\begin{align*}
  & \phi(t) =  x(t) \ast h(t)\\
  & \phi(t) =  \int_{-\infty}^\infty x(\tau) h(t-\tau)d\tau \\
\end{align*}
$$ 

Under the hood, the operation simply means flipping one of the signals and sweeping it across the entire range, evaluating the area of the overlapping region. It has two fundamental operations, shifting and adding. These two fundamental operations remain same across different applications such as image processing and audio signal processing. This is shown in the following animation from [Wikipedia](https://en.wikipedia.org/wiki/Convolution).

<figure align="center">
<p> 
<img src="/blog/assets/Convolution_of_box_signal_with_itself2.gif" width="580" height="160" alt="convolution">
</p> 
<img src="/blog/assets/Convolution_of_spiky_function_with_box2.gif" width="580" height="160" alt="convolution">

<figcaption align="center"  style="font-size:15px" ><em><b>Fig 4:</b> Convolution operation of two signals </em></figcaption>
</figure>

Notice, how one signal changes and tries to capture some of the features of the another. The convolution operation is all about capturing the behavior of the system and applying them to input signals. The output is signal is derived using the characteristics of the input signal as well as the system.

---

## Practical aspects of Convolution

Convolution is an essential operation in audio signal processing where the process is used to generate different sound effects in the multimedia industry. Here are two examples from [CKSDE](http://www.cksde.com/) which allows you to listen to the convolution of two different audio samples.

### Example 1:

In this example, voice of a man is fed as an input to a system that produces a metallic delay effect. 

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316686&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316698&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>
  
<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826316689&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

### Example 2:

In this example, audio of a snare drum is fed as an input to a system that produces a decaying white noise.

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332850&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332844&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

<iframe width="30%" height="100" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/826332838&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>


Apart from this, convolutions also work with images and have immense applications in image recognition, filtering, etc. These are some interesting topics, which I would cover separately in my future posts.

### Example 3:

In image processing, slightly different terminologies are used. Instead of having a signal/system, here we have an input image(signal) and an image kernel (system). As images are nothing but matrices, the kernel (also known as filters) is a matrix (usually smaller than your image) used to apply effects on an image such as blurring, sharpening, outlining etc.

The convolution operation here as well, involves shifting and adding. The kernel slides over the image. As the kernel slides, an element-wise multiplication is performed with the pixels of the image. The sum of these multiplications becomes a pixel of the output/filtered image.

Given below is an example of convolution operation between two matrices:

$$
\begin{align*}
  & \left( \begin{array}{ccc}
      3 & 3 & 2 & 1 & 0 \\
      0 & 0 & 1 & 3 & 1 \\ 
      3 & 1 & 2 & 2 & 3 \\ 
      2 & 0 & 0 & 2 & 2 \\ 
      2 & 0 & 0 & 0 & 1
    \end{array} \right)
     \ast
  \left( \begin{array}{c}
      0 & 1 & 2 \\ 
      2 & 2 & 0 \\ 
      0 & 1 & 2 
    \end{array} \right)
  =
    \left( \begin{array}{c}
      12 & 12 & 17 \\ 
      10 & 17 & 19 \\ 
      9 & 6 & 14 
    \end{array} \right)
\end{align*}
$$

<figure align="center">
<p> 
<img src="/blog/assets/conv.gif" width="535" height="299" alt="convolution">
</p> 
<figcaption align="center"  style="font-size:15px" ><em><b>Fig 5:</b> Convolution operation of two matrices <a href="https://arxiv.org/abs/1603.07285">[Source]</a></em>
</figcaption>
</figure>

This same techniques can be applied to images as follows in python:

```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import cv2
import numpy as np

# Read in the image
image = mpimg.imread('cameraman-grayscale.png')

# Outline filter
outline= np.array([[-1,-1,-1],
                 [-1,8,-1],
                 [-1,-1,-1]])

# applying filter to the image
filtered_image = cv2.filter2D(image, -1, outline)
plt.imshow(image)
plt.imshow(filtered_image, cmap='gray')

```
Here, we convolved the image with an outline filter: $$\begin{pmatrix}-1 & -1 & -1 \\ -1 & 8 & -1 \\-1 & -1 & -1 \end{pmatrix}$$. 

The output shall generate two following images:

<figure class="half" style="display:flex">
    <img style="width:300px" src="/blog/assets/cameraman-grayscale.png">
    <img style="width:600px" src="/blog/assets/cameraman_oultine.png">
</figure>
<figcaption align ='center' style="font-size:15px"> <em><b>Fig 6:</b> <b>Left</b>: Input image. <b>Right</b>: Filtered image  </em>
</figcaption>

Most recent and also the most exciting application of convolution is in building deep learning models to classify images and identify objects. This class of deep learning models known as Convolutional Neural Networks (or [CNN](https://en.wikipedia.org/wiki/Convolutional_neural_network)) find application in face recognition, medical imaging, self driving cars etc. 
<figure align="center">
<p> 
<img src="/blog/assets/tesla.gif" width="535" height="299" alt="convolution">
</p> 
<figcaption align="center"  style="font-size:15px" ><em><b>Fig 7:</b> Self driving technology <a href="https://electrek.co/2017/03/13/tesla-vision-autopilot-chip-intel-mobileye/">[Source]</a></em>
</figcaption>
</figure>

---

## Further Reading


1. [Setosa.io](https://setosa.io/ev/image-kernels/) provides interactive introduction to experiment with image kernels.
2. You can listen more to examples of convolution at [CKSDE](http://www.cksde.com/p_6_250.htm). 
3. This [video](https://ocw.mit.edu/resources/res-6-007-signals-and-systems-spring-2011/video-lectures/lecture-4-convolution/) at MIT opencourseware by Prof. Alan V. Oppenheim provides in-depth explanation of convolution in the light of signal theory.
4. [CS231n](https://cs231n.github.io/convolutional-networks/) is a popular course to learn and experiment with CNN. 


---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/oldMagnum) or connect with me on [LinkedIn](https://www.linkedin.com/in/ankitk50/).
