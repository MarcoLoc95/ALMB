# What's Fourier got to do with it?
The example of the rolling hills in the introduction of this chapter might suggest a different way to look at images, but it is still not straightforward _why_ Fourier transforms are involved in optics and, ultimately, microscopy. Advanced optics books do not usually spend many words on it and directly dive into complex math, manipulating formulas until a Fourier transform appears. On the other side of the spectrum, biology-oriented books seldom mention spatial frequencies and explain every phenomenon in terms of diffraction and interference, sweeping many problems with this explanation under the carpet. The average biophysicist might get frustrated and confused with either treatment and wonder about the actual physical meaning. In this section we will try to approach this topic without taking any important step for granted.

As we have mentioned in Chapter 3, every object can be considered as a collection of individual point sources, each emitting spherical waves. All these waves travel a very large distance before reaching our eyes or our phone camera: the spherical curvature of the wavefronts gradually becomes flatter and flatter the farther we get from the source, until we can approximate it to a plane (_Fig. 1_). All these plane waves can be described each as a complex exponential $e^{iky}$, where $k$ is the wave number and $y$ is the vertical distance between the observation point and the source ($x$ is the same for all points in this example, so it is a common factor for all waves). All these plane waves mix at the observation point, interfering with each other. Thanks to the superposition principle, we can say that at the observation point we measure the sum of all these plane waves $\Sigma e^{iky}$. Because an object is made up of a huge amount of tiny point sources, we can write this as an integral $\int_0^h e^{iky} dy$, where $h$ is the height of the object. But this integral can be rewritten by using a function $f(y)$ such that $\int_{-\infty}^{+\infty} f(y) e^{iky} dy$ where $f(y)$ is 1 between 0 and $h$, and 0 elsewhere. This is where the Fourier transform emerges, at a fundamental level. 


IMG Inkscape

Plane waves and spherical waves
---
aa

Huygens-Fresnel principle
---
aa

Fraunhofer regime and Fourier transforms
---
aa

Two- and three-dimensional Fourier transforms
---
aa

Converging lenses as Fourier transformers
---
a
