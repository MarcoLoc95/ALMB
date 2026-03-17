# Monochromatic aberrations

```{tip}
A video version of this section is available below, with live demonstrations and sketches of each aberration type.
```

<iframe src="https://player.vimeo.com/video/1172909607?badge=0&amp;autopause=0&amp;player_id=0&amp" width="100%" height="400" frameborder="0" allowfullscreen></iframe>

In the previous section we derived the thin lens equation under the paraxial approximation, assuming that all angles are small enough that $\sin\theta \approx \theta$. The result was clean and powerful: all rays from a point source converge to the same image point, regardless of where they hit the lens. Real lenses, however, have finite apertures, and rays that strike the lens far from the center make large angles with the axis. For these rays, the paraxial approximation is no longer valid, and the image degrades. The resulting imperfections are called **monochromatic aberrations**, because they occur even when we use light of a single wavelength. They are purely geometric in origin: they arise from the shape of the lens surfaces and from the angles at which rays travel through the system.

## Where do aberrations come from?

To see how aberrations creep in, let us go back to Snell's law at a spherical surface. In the paraxial treatment we replaced $\sin\theta$ with $\theta$. A more accurate expansion to third order gives:

$$
\sin\theta \approx \theta - \frac{\theta^3}{6}
$$

The first term is the paraxial part; the second is the leading correction. If we substitute this into the Snell's law expressions from the previous section and work through the algebra (the full derivation can be found in most optics textbooks), the refraction equation for a spherical surface acquires an extra term proportional to $h^2$:

$$
\frac{n_1}{s_o} + \frac{n_2}{s_i} = \frac{n_2 - n_1}{R} + (\text{terms} \propto h^2)
$$

In the paraxial regime $h$ is small and this correction is negligible. But when $h$ grows, the correction becomes measurable, and the image position starts to depend on _where_ the ray hits the lens. Different rays no longer converge to the same point, and the image blurs. This is the physical origin of all monochromatic aberrations.

The five classical monochromatic aberrations were systematically classified by Ludwig von Seidel in the 1850s and are therefore known as the **Seidel aberrations**: spherical aberration, coma, astigmatism, field curvature and distortion. Let us examine each of them.

## Spherical aberration

Spherical aberration is the most fundamental of the five, and the one most directly connected to the $h^2$ correction we just described. It affects rays from an _on-axis_ point source, so it is present even when everything is perfectly aligned.

```{figure} ../figures/chap2_spherical_aberration.png
---
width: 90%
name: chap2_spherical_aberration
align: center
---
Spherical aberration. Paraxial rays (close to the axis) focus at the paraxial focal point, while marginal rays (far from the axis) are focused closer to the lens. The distance between the two focal points is the longitudinal spherical aberration.
```

Because the correction term grows with $h^2$, rays that pass through the outer zones of the lens are focused at a different point than those that pass near the center. For a simple positive lens, marginal rays are bent too strongly and converge _before_ the paraxial focus (_{numref}`Fig. {number} <chap2_spherical_aberration>`_). The separation along the axis between the marginal and paraxial focal points is called the **longitudinal spherical aberration**. If we place a screen at the paraxial focus, the marginal rays produce a blurred halo around the central spot; the radius of this halo on the screen is the **transverse spherical aberration**.

Between the marginal and paraxial foci there is a plane where the spot size is smallest: this is the **circle of least confusion**, the best compromise when spherical aberration cannot be fully corrected.

```{figure} ../figures/chap2_sa_simulation.png
---
width: 60%
name: chap2_sa_simulation
align: center
---
Simulation of spherical aberration on a test image. At the marginal focus (left), the core is relatively sharp but surrounded by a bright ring-like halo. At the circle of least confusion (center), the overall spot size is minimized and the image is sharpest. At the paraxial focus (right), fine details near the axis are preserved but the broad halo from uncorrected marginal rays washes out the contrast. In all three cases the image is degraded compared to the original object (top), illustrating why spherical aberration must be corrected in any high-resolution imaging system.
```

### How to correct it

There are several strategies, listed here from simplest to most effective:

**Reduce the aperture.** Placing a _stop_ (a physical aperture) in front of the lens blocks the marginal rays and forces all light to travel close to the axis, where the paraxial approximation is good. The drawback is obvious: less light reaches the image, reducing the signal. In microscopy, this is rarely an acceptable trade-off, because we often need every photon we can get.

**Orient the lens correctly.** For a plano-convex lens (one flat surface, one curved), the spherical aberration depends on which side faces the incoming light. Orienting the curved surface toward the incoming parallel rays distributes the refraction more evenly over the two surfaces, reducing the aberration. This is a simple and free improvement that you should always keep in mind when setting up an optical system.

**Use an aspherical lens.** The root cause of spherical aberration is the spherical shape of the surface. If we design a surface whose curvature varies across its aperture (an _aspherical_ surface), we can eliminate the $h^2$ term entirely and bring all rays to a common focus. Modern aspherical lenses are manufactured with high precision and are standard in microscope objectives, laser optics and high-quality camera lenses.

```{figure} ../figures/chap2_aspherical.png
---
width: 40%
name: chap2_aspherical
align: center
---
An aspherical lens corrects for spherical aberration by varying the curvature across its aperture, so that marginal and paraxial rays converge to the same focal point. Copyright: ArtMechanic, CC BY-SA 3.0, via Wikimedia Commons
```

How does one design an aspherical surface in practice? The shape of any rotationally symmetric optical surface can be described by its _sag_, the distance $z$ from a flat reference plane as a function of the radial distance $r$ from the optical axis:

$$
z(r) = \frac{r^2 / R}{1 + \sqrt{1 - (1+\kappa)\,r^2/R^2}} + A_4\,r^4 + A_6\,r^6 + A_8\,r^8 + \cdots
$$

The first term is a conic section: $R$ is the vertex radius of curvature and $\kappa$ is the **conic constant**, which selects the type of surface ($\kappa = 0$ for a sphere, $\kappa = -1$ for a paraboloid, $\kappa < -1$ for a hyperboloid). The higher-order coefficients $A_4, A_6, A_8, \ldots$ are free parameters that the lens designer optimizes numerically to minimize aberrations across the full aperture. A spherical lens corresponds to $\kappa = 0$ and all $A_i = 0$. In modern microscope objectives, these coefficients are tuned with sub-nanometer precision, which is one of the reasons why high-quality objectives are so expensive to manufacture.

```{tip}
Even a perfectly designed aspherical objective can exhibit spherical aberration if you use it under conditions it was not designed for. A common example in microscopy: an oil-immersion objective ($n = 1.515$) used to image deep into a watery sample ($n = 1.33$). The mismatch between the immersion medium and the sample introduces spherical aberration that worsens with imaging depth. This is why matching the immersion medium to the sample is so important (and why water-immersion objectives exist).
```

## Coma

Coma is the aberration of _off-axis_ point sources imaged through a lens with a large aperture. The name comes from the characteristic comet-shaped spot that appears in the image: a bright core with a flared tail pointing away from (or toward) the optical axis.

```{figure} ../figures/chap2_coma.png
---
width: 70%
name: chap2_coma
align: center
---
Coma. An off-axis point source is imaged as a comet-shaped smear because rays passing through different zones of the lens are focused at different heights in the image plane.
```

The physical origin is related to the fact that the principal planes of the lens (the planes where refraction can be thought of as occurring) are flat only in the paraxial region. For rays farther from the axis, these planes are actually curved, which means that different annular zones of the lens produce images of different sizes and at slightly different positions. The superposition of all these displaced images creates the characteristic asymmetric tail.

### The Abbe sine condition

Is there a systematic way to guarantee that coma vanishes? Yes, and it comes from a powerful result called the **Abbe sine condition** (or optical sine theorem). It states that if we want the magnification to be the same for both paraxial and marginal rays, the following relation must hold:

$$
\frac{\sin\alpha_o}{\sin\alpha_i} = \frac{\alpha_{o,\text{paraxial}}}{\alpha_{i,\text{paraxial}}} = \text{constant}
$$

where $\alpha_o$ and $\alpha_i$ are the angles of a marginal ray in the object and image space, and the paraxial angles are their small-angle counterparts.

For the important special case where the object is very far away (parallel incoming rays), the sine condition reduces to the requirement that there be no spherical aberration. In other words, if you correct for spherical aberration when the object is at infinity, you automatically correct for coma as well. This is why high-quality objectives are designed to satisfy the Abbe sine condition: it ensures that both on-axis and off-axis points are imaged sharply.

When the object is _not_ at infinity (as is typically the case in microscopy), a practical trick is to use a pair of lenses in a configuration where the object sits at the front focal plane of the first lens. The rays exit the first lens as a parallel bundle, creating an _infinity space_ between the two lenses. The second lens then images this bundle, and because the input is now effectively at infinity, the sine condition is satisfied. This **infinity-corrected** configuration is the standard in modern research microscopes, and we will discuss it in more detail in {ref}`Chapter 3 <chap3>`.

### Simpler corrections

If a full correction is not available, coma can be reduced by ensuring that the object is on-axis (so that the oblique configuration does not arise in the first place) or by stopping down the aperture, just as with spherical aberration.

## Astigmatism

The word _astigmatism_ comes from the Greek for "not a point" (a-stigma), and that is exactly what it describes: a point source is imaged not as a point but as two perpendicular line segments at different distances from the lens.

```{figure} ../figures/chap2_astigmatism.png
---
width: 80%
name: chap2_astigmatism
align: center
---
Astigmatism for an off-axis point source. Rays in the tangential (meridional) plane and in the sagittal plane focus at different distances, producing two orthogonal line images. The circle of least confusion lies between them.
```

This happens because an off-axis point source "sees" the lens asymmetrically. Rays in the plane containing the optical axis and the object point (the _tangential_ or _meridional_ plane) encounter a different effective curvature than rays in the perpendicular plane (the _sagittal_ plane). The two planes therefore have different focal lengths. At the tangential focus the image is a short line oriented along the sagittal direction; at the sagittal focus it is a line oriented along the tangential direction. Between the two foci lies the circle of least confusion, which is the best approximation to a point that the system can produce.

Astigmatism can also arise from a second, distinct cause: the lens itself may have slightly different curvatures in two perpendicular directions. This is common in the human eye (where it is corrected with cylindrical lenses in glasses) but rare in well-manufactured optical elements. In microscopy, astigmatism is mostly a concern for off-axis points in wide-field imaging, and modern objectives are designed to minimize it. Lenses corrected for astigmatism are called **anastigmats**.

## Field curvature

Even if we correct for spherical aberration, coma and astigmatism, the image of a flat object is in general not flat. Instead, the sharp-focus positions trace out a curved surface called the **Petzval surface**, named after the Hungarian mathematician and physicist József Petzval who first described it.

```{figure} ../figures/chap2_field_curvature.png
---
width: 70%
name: chap2_field_curvature
align: center
---
Field curvature. Points at the edge of the field are in focus on a curved surface (the Petzval surface), not on the flat image plane. This means that when the center is in focus, the edges are blurred, and vice versa.
```

For a single thin lens with refractive index $n$ and focal length $f$, the displacement $\Delta x$ of the focal point from the flat image plane at a height $y$ off axis is:

$$
\Delta x = \frac{y^2}{2nf}
$$

For a system of $j$ thin lenses, this generalizes to:

$$
\Delta x = \frac{y^2}{2} \sum_j \frac{1}{n_j f_j}
$$

The condition for a _flat_ image field is therefore:

$$
\sum_j \frac{1}{n_j f_j} = 0
$$

This is the **Petzval condition**. A single positive lens always has a curved field, but by adding a second lens (a _field flattener_) with the right combination of refractive index and focal length, the Petzval sum can be driven to zero. In microscopy, objectives labelled with the prefix "Plan" (e.g. Plan-Apochromat) satisfy this condition and produce a flat image across the entire field of view. This is essential for any quantitative measurement or for tiling images of large specimens.

```{tip}
Another approach to field curvature is to use a curved detector instead of a flat one. Some astronomical telescopes do this, and there have been proposals for curved image sensors in cameras. In microscopy, however, flat sensors remain the norm, so correcting the optics is the practical solution.
```

## Distortion

The last Seidel aberration, **distortion**, is different from the previous four in an important way: it does not blur the image. Instead, it changes the _magnification_ across the field. If the magnification increases with distance from the axis, straight lines bow outward (pincushion distortion); if it decreases, they bow inward (barrel distortion).

Distortion does not affect resolution, but it does affect the accuracy of geometric measurements. In microscopy, it can cause artifacts when stitching tiled images or when measuring distances across a large field. Modern Plan objectives are designed to minimize distortion along with field curvature.

## Summary and practical message

Modern microscope objectives are complex assemblies of many lens elements, precisely designed to minimize all five Seidel aberrations simultaneously. When you read the label on an objective (Achromat, Fluorite, Apochromat, Plan-Apochromat), each term tells you something about which aberrations have been corrected and to what degree, as we will see in the next section and in {ref}`Chapter 3 <chap3>`.

The practical takeaway is threefold. First, know the origin of each aberration so that you can recognize it when it appears in your images. Second, use the simplest corrections available: align your system carefully (many aberrations worsen off-axis), match your immersion medium to your sample, and orient lenses with the curved surface toward the incoming light. Third, invest in better-corrected objectives only when your application demands it: a standard achromat may be perfectly adequate for routine brightfield imaging, while quantitative fluorescence microscopy on thick samples may require a Plan-Apochromat with a correction collar.

In the next section we will see that there is yet another family of aberrations that arise not from geometry but from the fact that the refractive index of glass depends on the wavelength of light.
