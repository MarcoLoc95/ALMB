# The compound microscope

In {ref}`Chapter 2 <chap2>`, we studied the thin lens and its ability to form images of objects. A single converging lens can magnify, but only up to a point: beyond a certain magnification, aberrations and the geometry of the system become limiting. The compound microscope overcomes this by splitting the job between two lens groups: the _objective_ and the _eyepiece_ (or _ocular_). Each one contributes a modest magnification, and their combined effect is multiplicative.

## Real and virtual images

Let us trace the light path through a simple compound microscope ({numref}`Fig. {number} <compound_microscope>`). The specimen (labeled $w$ in the figure) is placed just outside the front focal point of the objective. According to the thin lens equation, the objective produces a _real_, _inverted_, _magnified_ intermediate image (labeled $t$) on the other side of the lens. This intermediate image is a genuine distribution of light in space: you could place a screen there and see it.

```{figure} ../figures/compound_microscope.png
---
width: 90%
name: compound_microscope
align: center
---
Ray diagram of a compound microscope. The objective forms a real, inverted, magnified intermediate image $t$. The eyepiece acts as a magnifying glass, producing a virtual image $v$ that the eye perceives as coming from a large, distant object.
```

The eyepiece is positioned so that the intermediate image falls at or just inside its front focal point. In this configuration, the eyepiece works exactly like a magnifying glass: it takes the intermediate image and produces a _virtual_ image ($v$) that appears to originate far behind the instrument. Your eye's own lens then focuses this virtual image onto the retina, just as it would focus a distant object. The result is an image that appears both large and comfortably viewable.

The total magnification of the system is the product of the two individual magnifications:

$$
M_{\text{total}} = M_{\text{obj}} \times M_{\text{eye}}
$$

A 40× objective paired with a 10× eyepiece therefore gives 400× total magnification. This multiplicative principle is the reason compound microscopes can reach magnifications of 1000× or more, far beyond what any single lens could deliver without intolerable aberrations.

## Finite-tube-length configuration

In older microscope designs (and many educational microscopes still in use), the objective is designed to form the intermediate image at a fixed distance from its shoulder, called the **mechanical tube length**. The international standard, established by the Royal Microscopical Society in the 19th century, is 160 mm. In this configuration, the objective and the eyepiece are mounted at opposite ends of a tube whose length is precisely controlled.

The magnification of the objective in a finite system is simply the ratio of the image distance to the object distance:

$$
M_{\text{obj}} = \frac{s_i}{s_o}
$$

where $s_i$ is measured from the back principal plane of the objective to the intermediate image, and $s_o$ from the front principal plane to the specimen.

This design works well for simple setups, but it has a significant limitation: anything placed in the light path between the objective and the eyepiece (a filter, a polarizer, a beam splitter for fluorescence) changes the effective optical path length, shifting the position of the intermediate image. This means the image goes slightly out of focus, and the correction for aberrations (which was optimized for exactly 160 mm) is no longer valid. Every additional optical element in the tube requires the entire system to be recalibrated.

## Infinity-corrected configuration

Modern research microscopes solve this problem with an elegant trick. Instead of forming the intermediate image directly, the objective is designed so that light from an in-focus point on the specimen exits as a _parallel beam_ (collimated light). A second lens, called the **tube lens**, is then placed after the objective to converge these parallel rays and form the intermediate image at its focal plane ({numref}`Fig. {number} <infinity_config>`).

```{figure} ../figures/infinity_config.png
---
width: 90%
name: infinity_config
align: center
---
Comparison of the finite-tube-length (top) and infinity-corrected (bottom) optical configurations. In the infinity-corrected design, the space between the objective and the tube lens contains collimated light, allowing optical elements to be inserted without affecting image formation.
```

The space between the objective and the tube lens is called the **infinity space**. Because the beam is collimated there, you can insert flat optical elements (filters, dichroic mirrors, analyzers, beam splitters) without introducing any focus shift or additional aberrations. This is the reason virtually all modern research microscopes use the infinity-corrected design: it makes the system modular. You can swap optical components in and out of the infinity space without touching the focus or the image quality.

The magnification of the objective in an infinity-corrected system is determined by the ratio of the tube lens focal length to the objective's focal length:

$$
M_{\text{obj}} = \frac{f_{\text{tube}}}{f_{\text{obj}}}
$$

Different manufacturers use different tube lens focal lengths: Nikon and Leica use 200 mm, Olympus uses 180 mm, and Zeiss uses 165 mm. This is why objectives from different brands are generally _not_ interchangeable, even though they may have the same thread: a 40× Nikon objective paired with a Zeiss tube lens will not give exactly 40× magnification.

```{tip}
A common source of confusion: the magnification printed on an objective refers to the magnification when used with the _matching_ tube lens from the same manufacturer. If you mix brands, the actual magnification will differ from the label. For quantitative work, always calibrate with a stage micrometer.
```

## Reading an objective

A microscope objective carries a surprising amount of information engraved or printed on its barrel. Learning to read these markings is an essential skill for any microscopist. The interactive figure below lets you explore each marking on a typical high-end objective: hover over (or tap on) any part to learn what it encodes.

:::{raw} html
<iframe src="../content/objective_explorer.html" width="100%" height="600px" frameborder="0" style="border: none;"></iframe>
:::

Let us go through the most important parameters one by one.

**Magnification and numerical aperture.** These are always printed prominently, for example "40×/0.95". The first number is the magnification (with the matching tube lens), and the second is the numerical aperture, which we will discuss in detail in the next section.

**Optical correction class.** Objectives are corrected for aberrations to different degrees. The most common classes are:
- _Achromat_: corrected for chromatic aberration at two wavelengths and spherical aberration at one. Affordable and suitable for routine work.
- _Fluorite_ (or _semi-apochromat_): corrected for chromatic aberration at two to three wavelengths, with improved spherical correction. A good compromise between cost and performance.
- _Apochromat_ (Apo): corrected for chromatic aberration at three or more wavelengths and spherical aberration at two or more. The highest optical quality, and the highest price.
- _Plan_: indicates a flat field correction (reduced field curvature). Most modern objectives combine this with one of the above (Plan Achromat, Plan Apo, etc.).

**Immersion medium.** If the objective is designed for use with an immersion medium, this is indicated on the barrel (Oil, Water, Glycerol, or the corresponding abbreviation). Dry objectives (used with air) typically have no immersion marking.

**Cover glass thickness.** Most biological objectives are designed for use with a standard 0.17 mm cover glass (indicated as "0.17" on the barrel). Some specialized objectives are corrected for no cover glass ("0") or have a correction collar for variable cover glass thickness.

**Working distance.** The free distance between the front element of the objective and the specimen when in focus. High-NA oil objectives may have working distances as short as 0.1 mm, while low-magnification air objectives can have several millimeters.

**Parfocal distance.** The distance from the nosepiece mounting surface to the focal plane. Most modern objectives are standardized at 45 mm, meaning that when you rotate the turret to switch objectives, the specimen stays approximately in focus. This only works if all objectives on the turret share the same parfocal distance.

**Iris diaphragm.** Some high-NA objectives (typically 60× and 100× oil) have an internal adjustable iris that lets you reduce the effective numerical aperture. This is indicated on the barrel by a range (for example "1.35 ► ◄ 0.5") and by the abbreviation "Iris". Reducing the NA is useful for darkfield microscopy, where the illumination NA must exceed the collection NA of the objective.