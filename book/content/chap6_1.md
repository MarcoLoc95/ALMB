# What's Fourier got to do with it?
The example of the rolling hills in the introduction of this chapter might suggest a different way to look at images, but it is still not straightforward _why_ Fourier transforms are involved in optics and, ultimately, microscopy. Advanced optics books do not usually spend many words on it and directly dive into complex math, manipulating formulas until a Fourier transform appears. On the other side of the spectrum, biology-oriented books seldom mention spatial frequencies and explain every phenomenon in terms of diffraction and interference, sweeping many problems under the carpet with this explanation. The average biophysicist might get frustrated and confused with either treatment and wonder about the actual physical meaning. In this section we will try to approach this topic without taking any important step for granted.

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
The genius idea behind the principle proposed by Christiaan Huygens and Augustin-Jean Fresnel is that every point on a wavefront can itself be the source of spherical wavelets, and the secondary wavelets emanating from different points mutually interfere. You can think of it as a sort of "Taylor's expansion" for waves.

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

The function $f(y)$ is called the _aperture function_. It can also represent a diffracting object.

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


## Converging lenses as Fourier transformers

When referring to physics-oriented resources, you might come across the statement that "*a converging (positive) lens performs a Fourier transform of the object in its focal plane*". Without further explanation, this statement might sound nonsensical, especially after having studied ray optics. The statement is indeed true, but it deserves a better clarification.

As we have just seen in the Fraunhofer regime, the Fourier transform appears in the far field, where the waves are approximately plane. In practice, this can mean meters away from the diffracting object, with the drawback that the pattern gets dimmer the farther you go.

A lens brings the far field much closer. Place the object in the front focal plane of a converging lens and illuminate it with coherent light ({numref}`fourier_lens_orders`). Instead of following the light that comes from one *point* of the object, follow the light that leaves the object in one *direction*. Rays leaving the object at the same angle $\theta$, from every point of the object at once, are parallel to each other, and we know from the tracing rules that parallel rays entering a lens all cross at a single point of its back focal plane, at height

$$
u = f\tan\theta
$$

Every point of the back focal plane therefore collects exactly one direction of propagation, that is, one plane wave travelling away from the object. This is precisely what we would see on a screen infinitely far away, where each direction also ends up at its own position. So the lens itself does not perform any obscure mathematical operation: it simply brings the picture at infinity into its back focal plane.

```{figure} ../figures/fourier_lens_orders.png
:name: fourier_lens_orders

A grating in the front focal plane of a converging lens, illuminated with a coherent plane wave. Light leaves the grating in a few discrete directions: straight on (0, gray) and at the diffraction angles $\pm\theta$ ($+1$ teal, $-1$ orange). Rays with the same direction, wherever they start on the object, cross at the same point of the back focal plane, at height $u = f\tan\theta$. Each point of the back focal plane corresponds to one direction, and light from any single point of the object reaches all of them.
```

On the principal axis of the lens the undiffracted rays all converge into the focal point. That bright spot at the center of the diffraction pattern corresponds to zero spatial frequency (using terminology from electronics, the **DC component**). As this component would be present even without a diffracting object in front of the lens, it carries no information about the structure of the sample. For semi-transparent objects, this is always the brightest component in the spectrum. In imaging terms, the zero-frequency part of the image is responsible for the average brightness (the background level). Without the DC component, the image would appear darker overall, and only the details with higher spatial frequencies (edges, textures and fine structures) would remain visible.

### What sets the size of the pattern

To see which spatial frequency ends up where, compare with the Fraunhofer derivation. There, a point at height $Y$ on a screen at distance $D$ corresponded to the spatial frequency $k_y = k\,Y/D$. With the lens, the focal length takes the place of the screen distance, and for small angles

$$
k_y = k\,\frac{u}{f} \qquad \text{or, in cycles per unit length,} \qquad \nu = \frac{u}{\lambda f}
$$

A periodic structure of period $p$ diffracts light at the angle given by the grating equation, $\sin\theta = \lambda/p$, so for small angles its first orders land at

$$
u \approx \frac{\lambda f}{p}
$$

Fine details land far from the axis, coarse details close to it. With $\lambda$ = 0.5 µm and $f$ = 100 mm, a grating with a period of 20 µm puts its first orders 2.5 mm from the axis, and one with a period of 50 µm puts them at 1 mm ({numref}`fourier_lens_scale`a,b). The overall size of the object plays a different role: making the grating wider does not move the spots, it makes each of them narrower, roughly $\lambda f/h$ for a grating of width $h$ ({numref}`fourier_lens_scale`c). This is the same reciprocity we will meet again in the appendix: what is narrow in one domain is wide in the other.

```{figure} ../figures/fourier_lens_scale.png
:name: fourier_lens_scale

Computed intensity in the back focal plane of a lens with $f$ = 100 mm at $\lambda$ = 0.5 µm, for three gratings with a 50% duty cycle. (a, b) The period sets where the orders land, $u = \lambda f/p$, so the finer grating in (a) spreads its spectrum 2.5 times farther than the coarser one in (b). The weak peaks in (b) at ±3 and ±5 mm are the third and fifth orders; even orders vanish for a 50% duty cycle. (c) The same period as (a) over a three times wider area: the orders stay in place but become three times narrower.
```

```{tip}
**Why not trace the rays from the edges of the object?** It is tempting to estimate the size of the pattern by drawing the rays from the two edges of the object through the center of the lens and seeing where they hit the back focal plane. That construction gives a "magnification" of one, but it measures the wrong thing: it tells you the angle the object subtends, not where its diffracted light goes. A point of the back focal plane is not the image of any point of the object; it collects one direction from all of them. Two gratings of the same width but different period would get the same answer from this construction, while {numref}`fourier_lens_scale` shows that their spectra are very different.
```

### Where to put the object

The front focal plane is the textbook position, but the object does not have to sit exactly there ({numref}`fourier_lens_positions`).

If the object is moved closer to the lens, at a distance $s_o < f$, rays leaving it in the same direction are still parallel to each other and still cross at $u = f\tan\theta$. The spectrum therefore appears in the back focal plane with exactly the same scale. What changes is the phase: writing the aperture function as $t(y)$ to avoid confusion with the focal length, the field in the back focal plane becomes

$$
E(u) \propto e^{\,i\frac{k}{2f}\left(1-\frac{s_o}{f}\right)u^2} \int_{-\infty}^{+\infty} t(y)\, e^{-ik\frac{u}{f}y}\, dy
$$

The prefactor has modulus one, so the measured intensity is unchanged, and its phase disappears when $s_o = f$, which is why the front focal plane gives the exact Fourier transform, phase included; this matters only when you need the phase too, for instance when a second lens transforms the field back into an image. Moving the object closer does have one practical advantage: light leaving the edges of the object at large angles is less likely to miss the lens altogether, so less of the spectrum is lost to the rim of the lens. If the spectrum looks incomplete in the lab, this is worth trying. If it looks too small, use a lens with a longer focal length.

```{figure} ../figures/fourier_lens_positions.png
:name: fourier_lens_positions

Two positions of the same grating in front of a converging lens. (a) Object in the front focal plane: the orders cross at $u = f\tan\theta$. The $\pm1$ rays leaving the edges of the object at large angles miss the lens (crosses), so part of the spectrum is lost at the rim. (b) Object closer to the lens: rays with the same direction still cross at $u = f\tan\theta$, so the pattern has the same size, and the high-angle rays now pass through the lens.
```

In a microscope, the specimen sits in the front focal plane of the objective, so the back focal plane of the objective holds the Fourier transform of the specimen. Its finite aperture lets through only the directions up to the numerical aperture, and as the next section shows, this is exactly where the limit to resolution comes from.