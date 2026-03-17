# Thin lens equation

```{tip}
A video version of this section is available below, covering the same derivations with live demonstrations on a whiteboard.
```

<iframe src="https://player.vimeo.com/video/1172901768?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" width="100%" height="400" frameborder="0" allowfullscreen></iframe>

## What is a lens?

At its simplest, a **lens** is a piece of transparent material whose surfaces are curved. When a ray of light enters the lens, it slows down (or speeds up, depending on the material), and because the surfaces are not flat, different parts of the wavefront change speed at different times. The net effect is that the ray bends: it _refracts_. By shaping the surfaces carefully, we can make all the rays from a single point converge to another single point, forming an image.

Most lenses you will encounter in optics courses and in the laboratory have surfaces that are portions of spheres. This is partly a historical coincidence (spherical surfaces are relatively easy to grind and polish) and partly a matter of convenience (the geometry of spheres is well understood). We will see later in this chapter that the spherical shape is also the root cause of several aberrations, but for now it is a perfectly good starting point.

## Refraction at a single spherical surface

Before tackling a full lens with two curved surfaces, let us start with something simpler: a single spherical interface between two media with refractive indices $n_1$ (the surroundings, say air) and $n_2$ (the lens material, say glass). The surface has a radius of curvature $R$, and we place a point source on the optical axis at a distance $s_o$ from the surface.

A ray leaving the source at a small angle $\alpha$ hits the surface at height $h$ above the axis, where the local normal points toward the center of curvature. Using the geometry of the triangle formed by the source, the point of incidence, and the center of curvature, we can express the angles of incidence $\theta_1$ and refraction $\theta_2$ in terms of $\alpha$, the angle $\phi$ subtended at the center, and the angle $\beta$ at which the refracted ray crosses the axis on the other side:

$$
\theta_1 = \alpha + \phi, \qquad \theta_2 = \phi - \beta
$$

```{figure} ../figures/chap2_spherical_surface.png
---
width: 90%
name: chap2_spherical_surface
align: center
---
Refraction at a single spherical surface. A point source at distance $s_o$ emits a ray that refracts and crosses the axis at distance $s_i$. The height $h$, the angle $\phi$ at the center of curvature, and the angles $\alpha$ and $\beta$ are all related by simple trigonometry.
```

From the figure we can also write:

$$
\tan\alpha = \frac{h}{s_o}, \qquad \tan\beta = \frac{h}{s_i}, \qquad \sin\phi = \frac{h}{R}
$$

At this point the exact expressions are messy: they involve inverse trigonometric functions and do not simplify into anything memorable. This is where we introduce the **paraxial approximation**. If the angles are small (rays stay close to the axis), we can replace $\sin\theta \approx \theta$ and $\tan\theta \approx \theta$, which are just the first-order Taylor expansions. Under this approximation the three relations become:

$$
\alpha \approx \frac{h}{s_o}, \qquad \beta \approx \frac{h}{s_i}, \qquad \phi \approx \frac{h}{R}
$$

Now we apply Snell's law. In the paraxial regime, $n_1 \sin\theta_1 = n_2 \sin\theta_2$ simplifies to $n_1 \theta_1 = n_2 \theta_2$. Substituting the expressions for $\theta_1$ and $\theta_2$:

$$
n_1(\alpha + \phi) = n_2(\phi - \beta)
$$

Replacing $\alpha$, $\beta$ and $\phi$ with their expressions in terms of $h$, $s_o$, $s_i$ and $R$:

$$
n_1\left(\frac{h}{s_o} + \frac{h}{R}\right) = n_2\left(\frac{h}{R} - \frac{h}{s_i}\right)
$$

The height $h$ cancels entirely, which is a crucial result: the image position does not depend on where the ray hits the surface (as long as we stay in the paraxial regime). Rearranging, we obtain the **refraction equation for a spherical surface**:

$$
\frac{n_1}{s_o} + \frac{n_2}{s_i} = \frac{n_2 - n_1}{R}
$$

This single equation tells us where the image of a point source forms after refraction at one curved interface, given the refractive indices and the radius of curvature.

```{tip}
Keep an eye on the sign conventions. In this treatment: $s_o$ is positive when the object is to the left of the surface, $s_i$ is positive when the image is to the right, and $R$ is positive when the center of curvature lies to the right of the surface. A flat surface corresponds to $R \to \infty$.
```

## From one surface to two: the lensmaker equation

A real lens has two surfaces. Consider a lens of refractive index $n$ (we use $n_2 = n$ and $n_1 = 1$ for air) with radii of curvature $R_1$ (front surface) and $R_2$ (back surface), separated by a thickness $d$.

```{figure} ../figures/chap2_thick_lens.png
---
width: 90%
name: chap2_thick_lens
align: center
---
A lens with two spherical surfaces of radii $R_1$ and $R_2$, separated by thickness $d$. The image formed by the first surface becomes the (virtual) object for the second surface.
```

We apply the refraction equation twice. At the first surface:

$$
\frac{1}{s_o} + \frac{n}{s_{i1}} = \frac{n - 1}{R_1}
$$

The refracted ray would form an image at $s_{i1}$ if it were not intercepted by the second surface. For the second surface, this intermediate image acts as a virtual object at a distance $s_{i1} - d$ behind it. Because we are now going from glass ($n$) back into air ($1$), the refraction equation at the second surface reads:

$$
\frac{n}{d - s_{i1}} + \frac{1}{s_i} = \frac{1 - n}{R_2}
$$

Adding the two equations and collecting terms:

$$
\frac{1}{s_o} + \frac{1}{s_i} = (n-1)\left(\frac{1}{R_1} - \frac{1}{R_2}\right) + \frac{n_2 \, d}{s_{i1}(d - s_{i1})}
$$

This is the general result for a _thick_ lens. For a **thin lens** we set $d \approx 0$, and the last term vanishes. What remains is clean and powerful:

$$
\frac{1}{s_o} + \frac{1}{s_i} = (n-1)\left(\frac{1}{R_1} - \frac{1}{R_2}\right)
$$

The right-hand side depends only on the lens material and geometry, not on the object or image positions. We therefore define the **focal length** $f$ through:

$$
\frac{1}{f} = (n-1)\left(\frac{1}{R_1} - \frac{1}{R_2}\right)
$$

This is the **lensmaker equation**. It tells you the focal length of any thin lens given its refractive index and the curvatures of its two surfaces. With this definition, the thin lens equation takes its most familiar form:

$$
\boxed{\frac{1}{s_o} + \frac{1}{s_i} = \frac{1}{f}}
$$

A lens with a positive focal length ($f > 0$) is _converging_ (convex), while one with a negative focal length ($f < 0$) is _diverging_ (concave).

## Special cases worth remembering

Two limiting cases of the thin lens equation will appear again and again throughout this book.

**Object at the focal point ($s_o = f$).** Substituting into the thin lens equation: $\frac{1}{f} + \frac{1}{s_i} = \frac{1}{f}$, which gives $\frac{1}{s_i} = 0$, meaning $s_i \to \infty$. The rays exit the lens _parallel_ to each other.

**Object at infinity ($s_o \to \infty$).** Now $\frac{1}{\infty} + \frac{1}{s_i} = \frac{1}{f}$, so $s_i = f$. Parallel incoming rays converge at the focal point. This is how a lens focuses sunlight, and it is the basic principle of every camera and telescope.

## Rays through the center

There is one more important property of a thin lens that does not come from the refraction equation, but from a simple symmetry argument. Consider a ray that passes through the exact center of the lens. At the center, the two surfaces are locally parallel (think of an infinitesimally thin parallel slab). A ray entering a parallel slab exits with the same direction, just shifted sideways. For a thin lens the shift is negligible, so the ray passes through the center undeviated.

We can prove this more formally. At the first surface, Snell's law gives $n_1 \sin\theta_1 = n_2 \sin\theta_2$. At the second surface, by the same geometry, $n_2 \sin\theta_3 = n_1 \sin\theta_4$. Because the surfaces are parallel at the center, $\theta_2 = \theta_3$, and therefore $\theta_4 = \theta_1$: the exit angle equals the entrance angle, regardless of the paraxial approximation. This is a general result, valid for any ray passing through the center of a thin lens.

## Magnification

Now consider an extended object of height $y_o$ placed at distance $s_o$ from the lens. A ray from the tip of the object passes through the center of the lens and continues in a straight line. In the paraxial regime, the angle this ray makes with the axis can be written in two ways:

$$
\theta \approx \frac{y_o}{s_o} = \frac{-y_i}{s_i}
$$

where $y_i$ is the image height (negative because the image is inverted for the case drawn in _{numref}`Fig. {number} <chap2_magnification>`_). Rearranging gives the **lateral magnification**:

$$
M = \frac{y_i}{y_o} = -\frac{s_i}{s_o}
$$

```{figure} ../figures/chap2_magnification.png
---
width: 80%
name: chap2_magnification
align: center
---
An extended object at distance $s_o$ produces an inverted image at distance $s_i$. The magnification is the ratio of image height to object height.
```

When $|M| > 1$ the image is magnified; when $|M| < 1$ it is minified. A positive $M$ means the image is upright (same orientation as the object), while a negative $M$ means the image is inverted. In a typical microscope objective, $M$ is negative and its absolute value can range from 4 to 100 or more.

## Real and virtual images

When the object is placed beyond the focal point ($s_o > f$), the three rays converge on the other side of the lens. A screen placed at $s_i$ would show a real, inverted image. This is the configuration used in every microscope objective and every camera.

When the object is placed _inside_ the focal point ($s_o < f$), the rays diverge after the lens and never actually meet. However, if you extend them backward (as dashed lines), they appear to originate from a point on the same side as the object. This is a **virtual image**: you can see it by looking through the lens (as with a magnifying glass), but you cannot project it onto a screen. Virtual images are upright and magnified, which is precisely why a magnifying glass works the way it does.

```{tip}
A useful mnemonic: real images live where light actually goes; virtual images live where light _appears_ to come from. In a microscope, the objective creates a real intermediate image, while the eyepiece (when used visually) creates a virtual image at a comfortable viewing distance for the eye. We will explore these configurations in detail in {ref}`Chapter 3 <chap3>`.
```

These results are elegant and practical, but they rest on the paraxial approximation: small angles, thin lenses, and perfectly spherical surfaces. In the next section we will see what happens when these assumptions start to break down, and meet the family of _monochromatic aberrations_ that every real lens suffers from to some degree.