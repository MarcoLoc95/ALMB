# What's Fourier got to do with it?
The example of the rolling hills in the introduction of this chapter might suggest a different way to look at images, but it is still not straightforward _why_ Fourier transforms are involved in optics and, ultimately, microscopy. Advanced optics books do not usually spend many words on it and directly dive into complex math, manipulating formulas until a Fourier transform appears. On the other side of the spectrum, biology-oriented books seldom mention spatial frequencies and explain every phenomenon in terms of diffraction and interference, sweeping many problems with this explanation under the carpet. The average biophysicist might get frustrated and confused with either treatment and wonder about the actual physical meaning. In this section we will try to approach this topic without taking any important step for granted.

As we have mentioned in Chapter 3, every object can be considered as a collection of individual point sources, each emitting spherical waves. All these waves travel a very large distance before reaching our eyes or our phone camera: the spherical curvature of the wavefronts gradually becomes flatter and flatter the farther we get from the source, until we can approximate it to a plane (_{numref}`Fig. {number} <fraunhofer>`_).

```{figure} ../figures/fraunhofer.png
---
width: 80%
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

This principle lets us treat diffraction by simpler terms interfering with each other, regardless of the complexity of the aperture.

Fraunhofer regime and Fourier transforms
---
```{figure} ../figures/huygensfraunhofer.png
---
height: 50%
name: huygensfraunhofer
align: center
---
The Fraunhofer regime.
```

Let us look at the plane $x=0$ like in _{numref}`Fig. {number} <huygensfraunhofer>`_ and let us place a screen at distance $D$ from the aperture. Each point along the $y$-axis in the aperture will generate a spherical wave with (infinitesimally small) electric field $dE$:

$$
dE \propto \frac{e^{ikR}}{R}
$$

where $R=\sqrt{D^2+(Y-y)^2}$ depends on the position of the source $y$, the distance $D$ and the observation point $Y$. 

Therefore, the total electric field observed on the screen at position $Y$ is the result of the interference of all the spherical waves in the aperture:

$$
E(Y) = \int_{-\infty}^{+\infty} dE \propto \int_{-\infty}^{+\infty} f(y) \frac{e^{ikR}}{R} dy, \qquad \text{where } f(y)=\begin{cases}1 \text{ in the aperture}\\
0 \text{ elsewhere} \end{cases}
$$

The function $f(y)$ is called the _aperture fuction_. It can also represent a diffracting object.

We can rewrite $R$  as:

$$
R=D\sqrt{1+\bigg(\frac{Y-y}{D}\bigg)^2}
$$

When the screen is placed far enough, we are in the so called **Fraunhofer regime**. There, $y\ll Y\ll D$ and therefore $R$ can be expanded to the first Taylor order in $\frac{Y-y}{D}$:

$$
R\approx D\bigg(1+\frac{1}{2}\bigg(\frac{Y-y}{D}\bigg)^2\bigg) =D\bigg(1+\frac{1}{2}\bigg(\frac{Y^2}{D^2}-\frac{2Yy}{D^2}+\frac{y^2}{D^2}\bigg)\bigg)
$$

but because $y$ is even smaller than $Y$ we can drop the quadratic term $y^2$:

$$
R\approx D+\frac{Y^2}{2D}-\frac{Yy}{D}
$$

The total electric field then approximates to:

$$
E(Y) \propto \int_{-\infty}^{+\infty} f(y) \cdot \underbrace{\frac{e^{ik\bigg(D+\frac{Y^2}{2D}\bigg)}}{D+\frac{Y^2}{2D}}}_{\text{constant}} \cdot e^{-ik\frac{Y}{D}y} dy
$$

The constant term can be brought out of the integral, not depending on the integration variable $y$. Since $k\frac{Y}{D}$ is the projection of $k$ onto the $Y$-axis, we can write it as:

$$
E \propto \int_{-\infty}^{+\infty} f(y) \cdot e^{-ik_y y} dy
$$

Formally, this integral is equivalent to the Fourier transform of $f(y)$, where $k_y$ are the spatial frequencies. In other words, in the far field the diffracted field corresponds to the Fourier transform of the diffracting object. The astonishing aspect is that nature performs such complicated mathematical operation just by propagating the waves, and what is even more mind-blowing is that this happens _at the speed of light_. 

Let us not forget that detectors do not directly sense the electric field, which can assume complex values, but its intensity $I$:

$$
I \propto |E|^2
$$

Therefore the measured signal will be:

$$
I \propto \bigg| \int_{-\infty}^{+\infty} f(y) \cdot e^{-ik_y y} dy \bigg |^2
$$

Two-dimensional Fourier transforms
---

In the previous treatment we calculated the 1-dimensional Fourier transform, but in reality apertures and diffracting objects lay on a plane ({numref}`Fig. {number} <fourier2D>`). 

```{figure} ../figures/fourier2D.png
---
height: 50%
name: fourier2D
align: center
---
Diffraction leads to a 2-dimensional Fourier transform in the Fraunhofer regime.
```

Following the same derivation, we can obtain a very similar formula, which takes into account all the contributions in two dimensions:

$$
E(k_x,k_y) \propto \int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty} f(x,y) \cdot e^{-i(k_x x+ k_y y)} dxdy
$$

The Fourier transform in this case will be 2-dimensional, containing information not only on the spatial frequencies, but also the _direction_ of the features in the image.

Although rich of information, 2D Fourier transforms are not the easiest mathematical objects to manipulate. For this reason, in the rest of this chapter we will calculate 1D transforms where needed, and extend to 2D only by means of computation in Python.


Converging lenses as Fourier transformers
---
When referring to physics-oriented resources, you might come across the statement that "_a converging (positive) lens performs a Fourier transform of the object in its focal plane_". Without further explanation, this statement might sound nonsensical, especially after having studied ray optics. The statement is indeed true, but it deserves a better clarification.

As we have just said regarding the Fraunhofer regime, the Fourier transform appears in the far field where the waves are approximately plane. In practice, this can mean meters away from the diffracting object, plus the drawback of a decreasing intensity of the image the farther you get from the source. 

However, if we place the diffracting object in the front focal plane of the lens, we know from the tracing rules that the rays will exit the lens parallel to each other ({numref}`Fig. {number} <lensfourier1>`). This is equivalent to saying that the waves generated by a point source in the front focal plane will be plane after the lens. This is very handy, because in this case we do not need to go to the far field for the Fraunhofer approximation to be valid. Rays with the same angle cross again in the back focal plane of the lens, where they superimpose and interfere with each other, forming the Fourier transform as we would measure in the far field. So, the lens itself does not perform any obscure mathematical operation: it simply focuses the rays at infinity. 

```{figure} ../figures/lensfourier1.png
---
width: 80%
name: lensfourier1
align: center
---
When an object is placed in the front focal plane of a converging lens and illuminated with coherent light, its Fourier transform forms in the back focal place (cell illustration modified from [Freepik](www.freepik.com)).
```

On the principal axis of the lens the undiffracted rays all converge into the focal point. That bright spot at the center of the diffraction pattern corresponds to zero spatial frequency (using terminology from electronics, the **DC component**). As this component would be present even without a diffracting object in front of the lens, it does not contain any useful information about the sample. For semi-transparent objects, this is always the brightest component in the spectrum. In imaging terms, the zero-frequency part of the image is responsible for the average brightness (the background level). Without the DC component, the image would appear darker overall, and only the details with higher spatial frequencies (edges, textures and fine structures) would remain visible.

```{figure} ../figures/lensfourier1mag.png
---
width: 80%
name: lensfourier1mag
align: center
---
Estimation of the magnification of the diffraction pattern for an object placed in the front focal plane of a converging lens.
```

By tracing the rays generated at the extremities of the object and passing through the optical center of the lens, we can estimate the magnification of such a system ({numref}`Fig. {number} <lensfourier1mag>`). Please note that, in this context, magnification refers to the characteristic size of the diffraction pattern as compared to the object size, not the magnification of the image compared to the object. Consider an object of size $h$ centered on the principal axis of the lens. The ray passing through the center will be unchanged, so the angle formed with the principal axis $\alpha$ will be the same. But then we can write the tangent of the angle in two ways:

$$
\begin{cases} \tan(\alpha) = \frac{h/2}{f}\\
\tan(\alpha) = \frac{h'/2}{f} \end{cases}  \qquad \Rightarrow \frac{h/2}{f} = \frac{h'/2}{f} \qquad \Rightarrow h'=h
$$

The magnification will then result:

$$
M=\frac{h'}{h}=1
$$

This result tells us that the size of the diffraction pattern is roughly going to be of the same order of the size of the object.

One might wonder what would happen if we were to place the object closer to the lens ({numref}`Fig. {number} <lensfourier2>`). While it is true that in this configuration the wavefronts won't be exactly plane after the lens, you have to imagine as if the rays were coming from a virtual object placed at $s_i=\frac{1}{\frac{1}{f}-\frac{1}{s_o}}$. Since in every configuration $s_i < -s_o$, it would be the same as placing the object _farther_ from the observation plane, and we know that this means that the Fraunhofer approximation would hold better than without the lens. By tracing the rays we can easily see that they still cross in the back focal plane, in a way similar to {numref}`Fig. {number} <lensfourier1>`.

```{figure} ../figures/lensfourier2.png
---
width: 100%
name: lensfourier2
align: center
---
When an object is placed close to a converging lens and illuminated with coherent light, its Fourier transform also forms in the back focal place (cell illustration modified from [Freepik](www.freepik.com)).```

The difference from the first case is that the rays cross now farther apart in the back focal plane ({numref}`Fig. {number} <lensfourier2mag>`). By calculating the magnification in the same way as before we get:

$$
\begin{cases} \tan(\alpha) = \frac{h/2}{s_o}\\
\tan(\alpha) = \frac{h'/2}{f} \end{cases}  \qquad \Rightarrow \frac{h/2}{s_o} = \frac{h'/2}{f} \qquad \Rightarrow h'=h \frac{f}{s_o}
$$

$$
M=\frac{h'}{h}=\frac{f}{s_o} > 1
$$

```{figure} ../figures/lensfourier2mag.png
---
width: 100%
name: lensfourier2mag
align: center
---
Estimation of the magnification of the diffraction pattern for an object placed after the front focal plane of a converging lens.
```

A greater magnification means that, the closer the object to the lens, the better distinguishable the components in the Fourier transform will get. There are of course some practical limitations to it (what does infinite magnification mean here?), but this reasoning provides a solid argument for trying this configuration in the laboratory, when the first one does not provide a clear spectrum.

