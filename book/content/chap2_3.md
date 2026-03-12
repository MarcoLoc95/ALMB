# Chromatic aberrations

```{tip}
A video version of this section is available below, covering the derivations and correction strategies with live demonstrations.
```

<iframe src="https://player.vimeo.com/video/1172906310?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" width="100%" height="400" frameborder="0" allowfullscreen></iframe>

https://player.vimeo.com/video/1172906310?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479

The monochromatic aberrations we discussed in the previous section arise from the geometry of the lens and persist even with perfectly monochromatic light. Chromatic aberrations have a fundamentally different origin: they arise because the refractive index of any transparent material is not a single number but a function of wavelength. The word "chromatic" comes from the Greek _chroma_ (color), and the phenomenon it describes is familiar to anyone who has seen a prism split white light into a rainbow. In a lens, this wavelength dependence means that blue light and red light are focused at different positions, degrading the image whenever the illumination is not perfectly monochromatic.

## Why does the focal length depend on wavelength?

Recall the lensmaker equation:

$$
\frac{1}{f} = (n - 1)\left(\frac{1}{R_1} - \frac{1}{R_2}\right)
$$

The radii of curvature $R_1$ and $R_2$ are fixed geometric properties of the lens. They do not change with wavelength. The refractive index $n$, however, does. For ordinary glass, $n$ is higher for short wavelengths (blue, violet) and lower for long wavelengths (red, infrared). This behaviour is called **dispersion**, and it is well described by the empirical Cauchy equation:

$$
n(\lambda) \approx A + \frac{B}{\lambda^2}
$$

where $A$ and $B$ are material-specific constants. The constant $A$ is approximately what we refer to when we treat $n$ as a single number; the $B/\lambda^2$ term captures the wavelength dependence.

Substituting the Cauchy expression into the lensmaker equation, the focal length becomes an explicit function of $\lambda$:

$$
\frac{1}{f(\lambda)} = \left(A - 1 + \frac{B}{\lambda^2}\right)\left(\frac{1}{R_1} - \frac{1}{R_2}\right)
$$

Because $B > 0$ for normal glass, shorter wavelengths have a larger $n$ and therefore a _shorter_ focal length. Blue light is focused closer to the lens than red light.

## Longitudinal chromatic aberration

When a lens is illuminated with white light, each wavelength focuses at a different distance along the optical axis (_{numref}`Fig. {number} <chap2_longitudinal_chromatic>`_). Blue light, being refracted more strongly, converges first; red light converges farther away. This spread of focal positions is called **longitudinal** (or **axial**) **chromatic aberration**.

```{figure} ../figures/chap2_longitudinal_chromatic.png
---
width: 80%
name: chap2_longitudinal_chromatic
align: center
---
Longitudinal chromatic aberration. A white-light beam is focused by a single lens into a series of color-dependent focal points along the axis. Blue light is focused closest to the lens, red light farthest.
```

At any given screen position, only one wavelength is in perfect focus. The others contribute defocused halos, giving the image a characteristic color fringe. Somewhere between the blue and red foci there is a plane where the overall spot is smallest: the circle of least confusion, analogous to the one we encountered for spherical aberration. This circle is typically located closer to the red focus than to the blue, because the relationship between $n$ and $\lambda$ is not linear.

## Lateral chromatic aberration

There is a second effect. Because different wavelengths have different focal lengths, they also produce images of different sizes. Consider an off-axis point: the blue image and the red image are formed at different heights in their respective focal planes. Even if we could somehow bring both colors into the same plane, the two images would not overlap. The difference in image size is called **lateral** (or **transverse**) **chromatic aberration**, and it manifests as colored fringes at the edges of objects, especially toward the periphery of the field of view.

```{figure} ../figures/chap2_lateral_chromatic.png
---
width: 70%
name: chap2_lateral_chromatic
align: center
---
Lateral chromatic aberration. Because the red and blue images have different magnifications, off-axis features show colored fringes.
```

## Correcting chromatic aberration: achromatic doublets

Can we design a lens system where different wavelengths focus at the same point? The answer is yes, and the key idea is to combine two lens elements made of different glass types so that their dispersions partially cancel.

### Thin achromatic doublet (contact doublet)

Consider two thin lenses in contact ($d = 0$). The combined focal length is:

$$
\frac{1}{f_\text{total}} = \frac{1}{f_1} + \frac{1}{f_2}
$$

We want $f_\text{total}$ to be the same for red and blue light. Writing out the lensmaker equation for each lens at each wavelength and requiring $1/f_\text{red} = 1/f_\text{blue}$, one can show that the condition reduces to:

$$
\frac{\rho_1}{\rho_2} = -\frac{n_{2,B} - n_{2,R}}{n_{1,B} - n_{1,R}}
$$

where $\rho_i = 1/R_{1,i} - 1/R_{2,i}$ collects the geometric factors of each lens, and $n_{i,B}$, $n_{i,R}$ are the refractive indices of glass $i$ at the blue and red wavelengths. This condition links the curvatures of the two lenses to the dispersive properties of their glass types.

### Abbe numbers

To put this on a more practical footing, we introduce a convenient quantity. For each glass we pick three reference wavelengths: a "yellow" wavelength $\lambda_y$ in between the blue $\lambda_B$ and the red $\lambda_R$. The **Abbe number** (also called the V-number or dispersive index) of the glass is defined as:

$$
V = \frac{n_y - 1}{n_B - n_R}
$$

A large $V$ means low dispersion (the refractive index changes little across the visible spectrum); a small $V$ means high dispersion. Typical crown glass has $V \approx 60$, while flint glass has $V \approx 35$.

Using the Abbe numbers, the condition for an achromatic doublet can be written in a compact and elegant form:

$$
\boxed{\frac{f_{1,y}}{V_1} + \frac{f_{2,y}}{V_2} = 0}
$$

where $f_{1,y}$ and $f_{2,y}$ are the focal lengths evaluated at the yellow wavelength. This tells us something important: one lens must be converging and the other diverging (their focal lengths have opposite signs), and the ratio of their focal lengths is set by the ratio of their Abbe numbers. By choosing two glasses with sufficiently different $V$ values, we can design a doublet that brings red and blue light to the same focus while still having a net positive (or negative) focal power.

The most common practical realization is the **Fraunhofer cemented doublet**: a positive crown-glass element bonded to a negative flint-glass element. Such doublets are inexpensive, compact, and effective for many applications.

### Same-glass correction

There is an alternative approach that does not require two different glass types. If we take two lenses made of the _same_ glass and separate them by a suitable distance $d$, the combined system can also be made achromatic. Starting from the general two-lens equation with $d \neq 0$ and requiring the focal lengths for red and blue to be equal, one obtains:

$$
d = \frac{1}{n_B + n_R - 2} \cdot \frac{\rho_1 + \rho_2}{\rho_1 \, \rho_2}
$$

This approach is used in some specialized instruments, but it tends to produce longer optical systems and is less common than the doublet solution.

## The secondary spectrum

An achromatic doublet corrects for two wavelengths: red and blue. What about all the wavelengths in between? Unfortunately, they are not automatically corrected. If we plot the focal shift $\Delta f$ as a function of wavelength for an achromat, we find that the red and blue curves cross zero (they are perfectly corrected), but the green and yellow wavelengths still show a small residual shift. This residual is called the **secondary spectrum**.

```{figure} ../figures/chap2_secondary_spectrum.png
---
width: 70%
name: chap2_secondary_spectrum
align: center
---
Focal shift as a function of wavelength for different levels of chromatic correction. An achromat corrects red and blue but leaves a residual secondary spectrum. An apochromat corrects three wavelengths, and a superachromat four, progressively flattening the curve.
```

For many applications the secondary spectrum is negligible. But when high color fidelity is required (multicolor fluorescence microscopy, for example), it becomes a problem. The solution is to add more lens elements and correct for more wavelengths.

## Apochromats and superachromats

An **apochromat** uses three or more lens elements to bring _three_ wavelengths to a common focus. The secondary spectrum is dramatically reduced across the visible range (_{numref}`Fig. {number} <chap2_secondary_spectrum>`_). Apochromatic objectives are the workhorses of modern fluorescence microscopy, where multiple fluorophores emitting at different wavelengths must be imaged with high precision.

A **superachromat** takes this one step further, correcting for four wavelengths and producing an even flatter focal-shift curve. The price is complexity: superachromatic objectives may contain six or more individual lens elements, each made of a carefully selected glass type. The materials themselves (such as fluorite, CaF$_2$) can be expensive, which is why these objectives carry premium price tags.

Between the achromat and the apochromat there is an intermediate class called **fluorite** (or semi-apochromat) objectives, which correct for two to three wavelengths and offer a practical middle ground in terms of both performance and cost.

## Which correction do you need?

The right level of chromatic correction depends entirely on your application. Here is a rough guide:

**Achromatic objectives** are adequate for routine brightfield microscopy with stained samples. The residual color error is small enough that it rarely limits the useful resolution, especially if you use narrow-band filters.

**Fluorite objectives** are a good choice when you work with two or three fluorescence channels and need better color registration than an achromat can provide, without paying the full price of an apochromat.

**Apochromatic objectives** are recommended for demanding multicolor fluorescence imaging, live-cell work, and any experiment where quantitative colocalization matters. They offer excellent correction from the near-UV to the near-IR.

**Superachromatic objectives** are reserved for the most demanding applications: simultaneous imaging across a very wide spectral range, or experiments where even tiny residual chromatic shifts would compromise the measurement.

```{tip}
The naming conventions on microscope objectives encode the level of correction. "Achro" or "Achromat" means two-color correction. "Fluor" or "Fl" indicates a fluorite objective. "Apo" means apochromatic. Adding "Plan" in front (e.g. "Plan-Apochromat") indicates that field curvature has also been corrected. We will decode these labels systematically in {ref}`Chapter 3 <chap3>`.
```

One final, practical note. If your experiment uses only a single excitation wavelength (as in many confocal or single-molecule setups), chromatic aberration in the excitation path is irrelevant. The correction then matters only for the emission, and even there the spectral bandwidth of a single fluorophore is usually narrow enough that an achromat performs well. The expensive apochromatic objectives earn their keep primarily in _multicolor_ experiments, where you need red, green and blue channels to register perfectly on the same detector. So, as with all equipment choices in microscopy: understand the physics, know what your experiment demands, and invest accordingly.
