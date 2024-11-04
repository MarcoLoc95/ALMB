# What's Fourier got to do with it?
The example of the rolling hills in the introduction of this chapter might suggest a different way to look at images, but it is still not straightforward _why_ Fourier transforms are involved in optics and, ultimately, microscopy. Advanced optics books do not usually spend many words on it and directly dive into complex math, manipulating formulas until a Fourier transform appears. On the other side of the spectrum, biology-oriented books seldom mention spatial frequencies and explain every phenomenon in terms of diffraction and interference, sweeping many problems with this explanation under the carpet. The average biophysicist might get frustrated and confused with either treatment and wonder about the actual physical meaning. In this section we will try to approach this topic without taking any important step for granted.

As we have mentioned in Chapter 3, every object can be considered as a collection of individual point sources, each emitting spherical waves. All these waves travel a very large distance before reaching our eyes or our phone camera: the spherical curvature of the wavefronts gradually becomes flatter and flatter the farther we get from the source, until we can approximate it to a plane (_{numref}`Fig. {number} <fraunhofer>`_).

```{figure} ../figures/fraunhofer.png
---
height: 50%
name: fraunhofer
align: center
---
Spherical waves can be approximated as plane waves in the far field regime.
```

Plane waves can be described as a complex exponential $e^{iky}$, where $k$ is the wave number and $y$ is the vertical distance between the observation point and the source. All these plane waves mix at the observation point, interfering with each other. Thanks to the superposition principle, we can say that at the observation point we measure the sum of all these plane waves $\Sigma e^{iky}$. Because an object is made up of a huge amount of tiny point sources, we can write this as an integral $\int_0^h e^{iky} dy$, where $h$ is the height of the object. But this integral can be rewritten by using an auxiliary function $f(y)$ such that $\int_{-\infty}^{+\infty} f(y) e^{iky} dy$, where $f(y)$ is 1 between 0 and $h$, and 0 elsewhere. This is where Fourier transforms emerge. 


```{figure} ../figures/fraunhoferfourier.png
---
height: 50%
name: fraunhoferfourier
align: center
---
In the observation plane the Fourier transform of the object appears.
```

In the observation plane we do not see the image directly, but its Fourier transform  (_{numref}`Fig. {number} <fraunhoferfourier>`_). By placing a lens (our eye or a phone camera) in the observation plane, the diverging wavefronts will be bent to focus a real image on the screen (our retina or the image sensor). But you can very well imagine that the lens, due to its finite size, will collect only a portion of the waves close to the center. The higher spatial frequencies, far from the center, will not be collected, leading to a loss of information in the reconstruction of the object. This is the real reason behind the limit to resolution in microscopy.

Now that we have a more intuitive understanding of the phenomenon, let us treat it more quantitatively.

Plane waves and spherical waves
---

In this section we will disregard the temporal evolution of the electric field, as intensities are averaged over a period of time when measured, and the phase, assumed to be a constant for coherent light.

By definition, a **plane wave** is a wave where the wavefronts are flat and parallel to each other. The spatial component of the electric field of a plane wave travelling in the x-direction can be written as:

$$
E \propto e^{i kx}
$$

where $k=\frac{2\pi}{\lambda}$ is the wave number and $\lambda$ is the wavelength. 

More in general, given the wave vector $\vec k$ pointing at the direction of propagation of the wave, the electric field in position $\vec r=(x,y,z)$ more in general becomes:

$$
E \propto e^{i \vec k \cdot \vec r} \propto e^{i (k_x x + k_y y + k_z z)}
$$

Similarly, a **spherical wave** is a wave where the wavefronts are spherical and centered in the same origin. The spatial component of the electric field assumes the form:

$$
E \propto \frac{e^{i kR}}{R}
$$

where $R$ is the distance from the source.

We can immediately see that the farther we are from the source, the dimmer the electric field is. This is because the energy spreads in space, in contrast with the plane wave where the energy is simply travelling.

Huygens-Fresnel principle
---
The genious idea behind the principle proposed by Christiaans Huygens and Augustin-Jean Fresnel is that every point on a wavefront can itself be the source of spherical wavelets, and the secondary wavelets emanating from different points mutually interfere. You can think of it as a sort of "Taylor's expansion" for waves.

The sum of these spherical wavelets forms a new wavefront. So, when a beam of coherent light (a plane wave) hits an aperture, diffraction can be easily explained as the interference of the point sources that were not blocked and passed through the aperture (_{numref}`Fig. {number} <huygens>`_).

```{figure} ../figures/huygens.png
---
height: 50%
name: huygens
align: center
---
The Huygens-Fresnel principle.
```

Fraunhofer regime and Fourier transforms
---
aa

Two- and three-dimensional Fourier transforms
---
aa

Converging lenses as Fourier transformers
---
a
