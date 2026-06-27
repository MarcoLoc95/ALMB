# The compound microscope

In {ref}`Chapter 2 <chap2>`, we studied the thin lens and its ability to form images of objects. A single converging lens can magnify, but only up to a point: beyond a certain magnification, aberrations and the geometry of the system become limiting. The compound microscope overcomes this by splitting the job between two lens groups: the _objective_ and the _eyepiece_ (or _ocular_). Each one contributes a modest magnification, and their combined effect is multiplicative.

The eyepiece is positioned so that the intermediate image falls at or just inside its front focal point. In this configuration, the eyepiece works exactly like a magnifying glass: it takes the intermediate image and produces a _virtual_ image ($v$) that appears to originate far behind the instrument. Your eye's own lens then focuses this virtual image onto the retina, just as it would focus a distant object. The result is an image that appears both large and comfortably viewable.

The total magnification of the system is the product of the two individual magnifications:

$$
M_{\text{total}} = M_{\text{obj}} \times M_{\text{eye}}
$$

A 40x objective paired with a 10x eyepiece therefore gives 400x total magnification. This multiplicative principle is the reason compound microscopes can reach magnifications of 1000x or more, far beyond what any single lens could deliver without intolerable aberrations.

## Upright and inverted microscopes

Every transmitted-light microscope we have built up so far can be assembled in one of two physical layouts, and although the optics are identical, the choice matters a great deal in practice.

In an **upright** microscope the objective sits above the specimen and the condenser below it, so light travels upward from the lamp, through the sample, and into the objective. This is the classical arrangement, the one most people picture, and it remains the standard for fixed, mounted preparations such as histological sections, stained smears, and polished blocks in materials science. The specimen sits on the stage with its cover glass facing up, and you focus by moving the objective toward the sample.

In an **inverted** microscope the geometry is turned over: the objective is below the stage and the condenser above it, and light now travels downward through the specimen. This looks like a pointless flip until you try to image living cells. Cells in culture grow on the bottom of a dish under several millimeters of medium. An upright objective would have to reach down through all that liquid to find them, whereas an inverted objective simply looks up through the thin glass bottom, placing its high-NA front element exactly where it belongs. Gravity helps too, holding the cells against the glass and in optical contact with the immersion medium.

The inverted layout has a second decisive advantage: it leaves the top of the sample completely open. While you image from below, you can add reagents, lower a patch-clamp pipette onto a single cell, perform a microinjection, or run a perfusion line across the dish, none of which disturbs the optics underneath. This is why the inverted frame, combined with a water- or oil-immersion objective and an incubation chamber holding the cells at 37°C and 5% CO$_2$, is the standard platform for live-cell imaging.

What does not change is the optics. The lenses, the diaphragms, the Köhler illumination scheme, and the conjugate planes are the same in both designs; an inverted microscope is just an upright one folded over, with a few mirrors steering the light to a conveniently placed eyepiece and camera. Resolution, magnification, and contrast obey exactly the same physics either way.

```{figure} ../figures/chap3_uprightinverted.png
---
width: 100%
name: uprightinverted
align: center
---
The two standard geometries of a transmitted-light microscope. In the _upright_ configuration (left) the objective sits above the specimen and the condenser below it, and light travels upward. In the _inverted_ configuration (right) the layout is flipped: the objective is below the stage and the condenser above, so the objective can image cultured cells directly through the thin glass bottom of their dish. The lenses, apertures, and conjugate planes are identical in both arrangements; only the physical orientation of the light path differs.
```

```{tip}
If you work with living cells, you will almost certainly use an inverted microscope. The combination of an inverted frame, a water- or oil-immersion objective, and an incubation chamber (to keep cells at 37°C and 5% CO$_2$) is the standard setup in any cell biology lab.
```

## Finite-tube-length and infinity-corrected configuration

In older microscope designs (and many educational microscopes still in use), the objective is designed to form the intermediate image at a fixed distance from its shoulder, called the **mechanical tube length**. The international standard, established by the Royal Microscopical Society in the 19th century, is 160 mm. In this configuration, the objective and the eyepiece are mounted at opposite ends of a tube whose length is precisely controlled.

The magnification of the objective in a **finite system** is simply the ratio of the image distance to the object distance:

$$
M_{\text{obj}} = \frac{s_i}{s_o}
$$

where $s_i$ is measured from the back principal plane of the objective to the intermediate image, and $s_o$ from the front principal plane to the specimen.

This design works well for simple setups, but it has a significant limitation: anything placed in the light path between the objective and the eyepiece (a filter, a polarizer, a beam splitter for fluorescence) changes the effective optical path length, shifting the position of the intermediate image. This means the image goes slightly out of focus, and the correction for aberrations (which was optimized for exactly 160 mm) is no longer valid. Every additional optical element in the tube requires the entire system to be recalibrated.

Modern research microscopes solve this problem with an elegant trick. Instead of forming the intermediate image directly, the objective is designed so that light from an in-focus point on the specimen exits as a _parallel beam_ (collimated light). A second lens, called the **tube lens**, is then placed after the objective to converge these parallel rays and form the intermediate image at its focal plane.

The space between the objective and the tube lens is called the **infinity space**. Because the beam is collimated there, you can insert flat optical elements (filters, dichroic mirrors, analyzers, beam splitters) without introducing any focus shift or additional aberrations. This is the reason virtually all modern research microscopes use the infinity-corrected design: it makes the system modular. You can swap optical components in and out of the infinity space without touching the focus or the image quality.

The magnification of the objective in an **infinity-corrected** system is determined by the ratio of the tube lens focal length to the objective's focal length:

$$
M_{\text{obj}} = \frac{f_{\text{tube}}}{f_{\text{obj}}}
$$

Different manufacturers use different tube lens focal lengths: Nikon and Leica use 200 mm, Olympus uses 180 mm, and Zeiss uses 165 mm. This is why objectives from different brands are generally _not_ interchangeable, even though they may have the same thread: a 40x Nikon objective paired with a Zeiss tube lens will not give exactly 40x magnification.

:::{raw} html
<div style="overflow:hidden; height:800px;">
    <iframe
        src="../content/finite_vs_infinity_widget.html"
        width="125%"
        height="1000"
        style="
            transform:scale(0.8);
            transform-origin:top left;
            border:none;">
    </iframe>
</div>
:::

Both systems are sharp only when the specimen sits in its design plane; move it and both images blur. The difference is the **magnification**. In the finite system it drifts with focus, and inserting any glass into the tube shifts the image and forces a refocus that changes it again. The infinity-corrected system holds magnification fixed at $f_{tube} / f_{obj}$ and ignores flat elements dropped into the collimated infinity space. That stability is why every modern research microscope is built this way.

```{tip}
A common source of confusion: the magnification printed on an objective refers to the magnification when used with the _matching_ tube lens from the same manufacturer. If you mix brands, the actual magnification will differ from the label. For quantitative work, always calibrate with a stage micrometer.
```

## Reading an objective

A microscope objective carries a surprising amount of information engraved or printed on its barrel. Learning to read these markings is an essential skill for any microscopist. The interactive figure below lets you explore each marking on a typical high-end objective: hover over (or tap on) any part to learn what it encodes.

:::{raw} html
<iframe src="../content/objective_explorer.html" width="100%" height="520px" frameborder="0" style="border: none;"></iframe>
:::

Let us go through the most important parameters one by one.

**Magnification and numerical aperture.** These are always printed prominently, for example "40x/0.95". The first number is the magnification (with the matching tube lens), and the second is the numerical aperture, which we will discuss in detail in the next section.

**Optical correction class.** Objectives are corrected for aberrations to different degrees. The most common classes are:
- _Achromat_: corrected for chromatic aberration at two wavelengths and spherical aberration at one. Affordable and suitable for routine work.
- _Fluorite_ (or _semi-apochromat_): corrected for chromatic aberration at two to three wavelengths, with improved spherical correction. A good compromise between cost and performance.
- _Apochromat_ (Apo): corrected for chromatic aberration at three or more wavelengths and spherical aberration at two or more. The highest optical quality, and the highest price.
- _Plan_: indicates a flat field correction (reduced field curvature). Most modern objectives combine this with one of the above (Plan Achromat, Plan Apo, etc.).

**Immersion medium.** If the objective is designed for use with an immersion medium, this is indicated on the barrel (Oil, Water, Glycerol, or the corresponding abbreviation). Dry objectives (used with air) typically have no immersion marking.

**Cover glass thickness.** Most biological objectives are designed for use with a standard 0.17 mm cover glass (indicated as "0.17" on the barrel). Some specialized objectives are corrected for no cover glass ("0") or have a correction collar for variable cover glass thickness.

**Working distance.** The free distance between the front element of the objective and the specimen when in focus. High-NA oil objectives may have working distances as short as 0.1 mm, while low-magnification air objectives can have several millimeters.

**Parfocal distance.** The distance from the nosepiece mounting surface to the focal plane. Most modern objectives are standardized at 45 mm, meaning that when you rotate the turret to switch objectives, the specimen stays approximately in focus. This only works if all objectives on the turret share the same parfocal distance.

**Iris diaphragm.** Some high-NA objectives (typically 60x and 100x oil) have an internal adjustable iris that lets you reduce the effective numerical aperture. This is indicated on the barrel by a range (for example "1.35 ► ◄ 0.5") and by the abbreviation "Iris". Reducing the NA is useful for darkfield microscopy, where the illumination NA must exceed the collection NA of the objective.