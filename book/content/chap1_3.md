# Light as a ray

In the previous section we described light as a wave, with all the richness that entails: interference, diffraction, polarization. But if you have ever watched sunbeams streaming through a gap in the clouds, you might have noticed something: light seems to travel in straight lines. Shadows have sharp edges. Beams from a flashlight or a laser pointer cross a room without spreading noticeably. This is the regime where a much simpler description of light becomes useful: the **ray model**.

## What is a ray?

A ray is an idealized line that points in the direction light is traveling. More precisely, it is drawn perpendicular to the wavefronts and points in the direction of energy flow. If the wavefronts are planar (as in a laser beam traveling through air), the rays are a set of parallel straight lines. If the wavefronts are spherical (as in light diverging from a point source), the rays fan out radially from that point.

```{figure} ../figures/ray_wavefront.png
---
width: 70%
name: ray_wavefront
align: center
---
Rays are perpendicular to the wavefronts. For plane waves the rays are parallel; for spherical waves they diverge from the source.
```

The ray picture is a simplification, and like all simplifications, it comes with a cost. Rays carry no information about wavelength, phase or polarization. They cannot explain interference or diffraction. In fact, the entire resolution limit we discussed earlier is invisible in the ray model: rays say nothing about why a point source does not image as a perfect point. So why bother with rays at all?

Because they are extraordinarily useful for understanding how lenses, mirrors and optical systems redirect light to form images. When the objects and openings involved are much larger than the wavelength of light, the wave effects become negligible and the ray picture gives accurate predictions with far less mathematical effort. Most of the practical design of microscope objectives, eyepieces and condensers is done using ray optics. The formal name for this framework is **geometrical optics**.

## Refraction and Snell's law

At the end of the previous section we noted that light bends when it crosses an interface between two materials with different refractive indices. The ray picture turns this into a precise, calculable rule.

Consider a ray of light hitting a flat interface at an angle $\theta_1$ to the normal (the line perpendicular to the surface). Part of the light is reflected, bouncing off at the same angle $\theta_1$ on the other side of the normal. The rest is transmitted into the second medium, but its direction changes. The transmitted angle $\theta_2$ is related to the incident angle by **Snell's law**:

$$
n_1 \sin \theta_1 = n_2 \sin \theta_2
$$

where $n_1$ and $n_2$ are the refractive indices of the two media.

```{figure} ../figures/snell.png
---
width: 50%
name: snell
align: center
---
Snell's law: a ray crossing from medium 1 to medium 2 bends toward the normal when entering a denser medium ($n_2 > n_1$), and away from the normal when entering a less dense one.
```

The intuition is straightforward: light bends _toward_ the normal when it enters a denser medium (higher $n$), and _away_ from the normal when it enters a less dense one. If you have ever noticed that a straw in a glass of water looks bent at the surface, you have seen Snell's law in action.

A useful special case is **normal incidence**, when the ray hits the surface head-on ($\theta_1 = 0$). In this case there is no bending (the transmitted ray continues straight through), but some light is still reflected. The fraction of intensity that is reflected is given by the **Fresnel reflection coefficient**:

$$
R = \left( \frac{n_1 - n_2}{n_1 + n_2} \right)^2
$$

and the fraction transmitted is simply $T = 1 - R$.

This formula tells you, for example, that at an air-glass interface ($n_1 = 1.0$, $n_2 = 1.5$), about 4% of the light is reflected at each surface. This is why uncoated lenses in a microscope with many elements can lose a significant amount of light, and why anti-reflection coatings are important. It also explains why immersion oil (with $n \approx 1.515$, matching the glass of the coverslip) eliminates the reflection at the coverslip-medium interface, allowing more light to be collected.

## The lensmaker's equation

Lenses work by exploiting Snell's law at two curved surfaces. Each surface bends the rays a little, and the net effect is that a well-shaped lens can redirect all incoming rays so that they converge to a common point: the **focus**.

For a thin lens (one whose thickness is small compared to the radii of curvature of its surfaces), the focal length $f$ is determined by the shape and material of the lens through the **lensmaker's equation**:

$$
\frac{1}{f} = (n - 1) \left( \frac{1}{R_1} - \frac{1}{R_2} \right)
$$

where $n$ is the refractive index of the lens material, and $R_1$ and $R_2$ are the radii of curvature of the two surfaces. A convex (converging) lens has a positive focal length, a concave (diverging) lens has a negative one.

```{figure} ../figures/lensmaker.png
---
width: 60%
name: lensmaker
align: center
---
The focal length of a thin lens depends on its refractive index and the curvature of its two surfaces.
```

Once you know the focal length, you can predict where a lens will form an image using the **thin lens equation**:

$$
\frac{1}{s_o} + \frac{1}{s_i} = \frac{1}{f}
$$

where $s_o$ is the distance from the object to the lens, and $s_i$ is the distance from the lens to the image. This simple formula is the starting point for understanding image formation in any optical system, including a microscope, and we will use it extensively in {ref}`Chapter 3 <chap3>`.

## Ray tracing for converging lenses

One of the most practical skills in geometrical optics is **ray tracing**: drawing a few special rays to figure out where an image forms and what it looks like. For a thin converging lens, you only need to remember four rules:

1. A ray traveling **parallel to the principal axis** passes through the **back focal point** after the lens.
2. A ray passing through the **center of the lens** continues straight, without bending.
3. A ray passing through the **front focal point** exits the lens **parallel to the principal axis**.
4. Rays that are **parallel to each other** (but at an angle to the axis) all converge to the **same point on the back focal plane**.

```{figure} ../figures/ray_tracing.png
---
width: 80%
name: ray_tracing
align: center
---
The four principal rays for a converging lens. Any two of them are sufficient to locate the image of a point object.
```

Rules 1 through 3 are the classic ones you learn in introductory physics. Rule 4 is less commonly taught but particularly important for microscopy: it is the basis for understanding how lenses perform Fourier transforms, which we will encounter in {ref}`Chapter 6 <chap6_1>`. In short, each angle of incidence maps to a unique point on the focal plane. This means the focal plane contains information about the _directions_ (and therefore the spatial frequencies) present in the light, not the positions. This is why the back focal plane of a microscope objective is sometimes called the Fourier plane.

## The magnification

Using the thin lens equation, we can also calculate how much larger (or smaller) the image is compared to the object. The **magnification** $M$ is defined as the ratio of image height to object height, which for a thin lens turns out to be:

$$
M = -\frac{s_i}{s_o}
$$

The minus sign indicates that a real image formed by a single converging lens is inverted (flipped upside down) compared to the object. If $|M| > 1$, the image is magnified; if $|M| < 1$, it is demagnified.

In a compound microscope, two lenses work in series. The objective produces a magnified, real, inverted intermediate image, and the eyepiece magnifies it further. The total magnification is the product of the two. But magnification alone is not useful without resolution: you can always make an image bigger, but you cannot reveal details that were not resolved in the first place. This is sometimes called "empty magnification," and it is a trap that beginners fall into when they crank up the zoom on a digital image.

## But don't forget waves...

After all this talk of rays traveling in neat straight lines and focusing to perfect points, it is worth pausing to remember what we learned in the previous section. Rays are a _model_, and a simplified one at that. In reality, the light passing through a lens is a wave, and it diffracts at the finite aperture of the lens.

This means that even a perfect lens with no aberrations at all does not focus a point source to a perfect point. Instead, it produces an Airy pattern. The ray model predicts a point; the wave model predicts a disc surrounded by rings. For large-scale design of optical systems, the ray model is fast and accurate. For understanding the ultimate performance limits of a microscope, you need waves.

```{figure} ../figures/ray_vs_wave.png
---
width: 70%
name: ray_vs_wave
align: center
---
A perfect lens according to the ray model focuses parallel light to a single point. In reality, diffraction at the lens aperture produces an Airy pattern, setting a fundamental limit to how small the focal spot can be.
```

This interplay between the ray picture and the wave picture will be a recurring theme throughout this book. In {ref}`Chapter 2 <chap2>`, we will use the ray model to analyze aberrations and understand how imperfect lenses degrade images. In {ref}`Chapter 6 <chap6>`, we will use the wave model to understand resolution, spatial frequencies and image formation at a deeper level. Both descriptions are tools, and the art of optics lies in knowing when to use which.
