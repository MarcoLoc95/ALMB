# Illumination and microscope design

So far we have focused on how the objective collects light from the specimen and forms an image. But the quality of that image depends just as much on how the specimen is _illuminated_. A poorly illuminated sample will produce artifacts, uneven brightness, and reduced contrast, regardless of how good the objective is. In this section we look at the overall architecture of a transmitted-light microscope and then examine the illumination system in detail, culminating in the elegant design known as Köhler illumination.

## Anatomy of a widefield microscope

A transmitted-light widefield microscope has two distinct optical paths: the **illumination path**, which delivers light to the specimen, and the **imaging path**, which collects light from the specimen and forms an image. Both paths share the specimen plane, but they are otherwise largely independent, each with its own set of lenses, apertures and conjugate planes.

The essential components, in order along the illumination path, are:

1. A **light source** (historically a tungsten-halogen lamp, increasingly an LED).
2. A **collector lens** that gathers light from the source.
3. A **field diaphragm** (also called the field stop) that controls the area of the specimen that is illuminated.
4. A **condenser lens** that focuses the illumination onto the specimen.
5. An **aperture diaphragm** (also called the condenser diaphragm) that controls the angular range of the illumination cone, and therefore the effective illumination NA.

On the imaging side:

1. The **objective** collects light from the specimen.
2. In infinity-corrected systems, the **tube lens** forms the intermediate image.
3. The **eyepiece** (or a camera sensor) captures the final image.

## Critical illumination

The simplest way to illuminate a specimen is to image the light source directly onto the sample plane. This is called **critical illumination** (sometimes also called Nelsonian illumination). A collector lens takes the light from the lamp filament and the condenser focuses it onto the specimen, so that the filament and the specimen are in conjugate planes.

Critical illumination has one major advantage: it is optically efficient. A large fraction of the lamp's output reaches the specimen. However, it has a devastating drawback: any structure in the light source (the coils of a filament, dust on the lamp housing, spatial non-uniformities in an arc lamp) is imaged _directly_ onto the specimen. The result is an illumination field that is far from uniform. Bright and dark bands from the lamp filament appear superimposed on the specimen image, ruining contrast and making quantitative intensity measurements impossible ({numref}`Fig. {number} <critical_illum>`).

```{figure} ../figures/critical_illum.png
---
width: 80%
name: critical_illum
align: center
---
In critical illumination the light source is imaged directly onto the specimen plane. Any structure in the source (lamp filament, dust) appears superimposed on the specimen image, producing non-uniform illumination.
```

For casual observation this may be tolerable (especially with modern LEDs, which are spatially more uniform than filament lamps), but for any serious microscopy, critical illumination is inadequate. We need a smarter approach.

## Köhler illumination

In 1893, August Köhler, working at the Carl Zeiss company in Jena, published a short paper describing an illumination scheme that solved every problem of critical illumination in one stroke. His design is so effective that it became, and remains, the universal standard for research-grade transmitted-light microscopy. Every modern microscope is designed for Köhler illumination.

The core idea is elegant: instead of imaging the light source onto the specimen, Köhler illumination _defocuses_ the source at the specimen plane, so that every point on the specimen receives light from the entire source. The source structure is completely washed out at the sample, producing beautifully uniform illumination. At the same time, the field diaphragm (not the source) is imaged onto the specimen, giving the user precise control over the illuminated area.

### How it works

Köhler illumination uses a four-element optical train ({numref}`Fig. {number} <koehler_scheme>`):

1. The **collector lens** images the light source onto the front focal plane of the condenser, where the **aperture diaphragm** sits.
2. The **condenser lens** takes this light and produces a collimated (or near-collimated) beam at the specimen plane. Because the source is now at the focal plane of the condenser, each point on the source contributes a plane wave that illuminates the entire field of view. The specimen sees uniform illumination, with no trace of the filament structure.
3. The **field diaphragm**, which sits in a plane conjugate to the specimen, controls how large an area on the sample is illuminated. Closing the field diaphragm restricts illumination to a smaller region, reducing stray light and improving contrast.
4. The **aperture diaphragm**, located at the front focal plane of the condenser, controls the cone angle of the illumination. Opening it increases the illumination NA; closing it reduces it.

```{figure} ../figures/koehler_scheme.png
---
width: 100%
name: koehler_scheme
align: center
---
Schematic of Köhler illumination showing the two sets of conjugate planes. The illumination path (yellow) and the imaging path share the specimen plane but are otherwise decoupled. The light source is imaged onto the aperture diaphragm and the back focal plane of the objective (never onto the specimen). The field diaphragm is imaged onto the specimen and the intermediate image plane.
```

### Conjugate planes

The most powerful way to understand Köhler illumination is through its system of **conjugate planes**: planes that are images of each other. In a properly aligned Köhler system, there are two independent sets of conjugate planes ({numref}`Fig. {number} <conjugate_planes>`).

**Set 1: the field planes (imaging conjugates).** These planes are all images of the specimen:
- Field diaphragm
- Specimen plane
- Intermediate image plane
- Retina (or camera sensor)

An object placed in any of these planes (a reticle in the eyepiece, a pinhole at the field diaphragm) will appear in sharp focus superimposed on the specimen image.

**Set 2: the aperture planes (illumination conjugates).** These planes are all images of the light source:
- Light source (lamp filament or LED chip)
- Aperture diaphragm (front focal plane of the condenser)
- Back focal plane of the objective (also called the pupil plane)
- Exit pupil of the eyepiece (the Ramsden disk)

An object placed in any of these planes will _not_ appear in the specimen image. Instead, it modifies the angular distribution of light. This is the reason the source structure is invisible at the specimen plane: the source is conjugate to the aperture planes, not to the field planes.

```{figure} ../figures/conjugate_planes.png
---
width: 100%
name: conjugate_planes
align: center
---
The two sets of conjugate planes in Köhler illumination. Top (blue): field (imaging) conjugates, all images of the specimen. Bottom (orange): aperture (illumination) conjugates, all images of the light source. The two sets are interleaved but optically independent.
```

```{tip}
Understanding conjugate planes is the key to understanding _every_ contrast technique in microscopy. Phase contrast works by placing a phase plate in an aperture conjugate plane (the back focal plane of the objective). Darkfield works by blocking the zeroth order in an aperture conjugate plane. Fluorescence filter cubes are inserted in the infinity space precisely because it is an aperture conjugate region. Once you internalize the conjugate-plane picture, the design logic of every microscopy technique becomes transparent.
```

### The role of the aperture diaphragm

The aperture diaphragm deserves special attention, because it directly affects both the resolution and the contrast of the image.

Opening the aperture diaphragm increases the illumination NA, which in turn increases the effective NA of the imaging system. In the Abbe framework, oblique illumination extends the range of spatial frequencies that contribute to the image, improving resolution. With the aperture diaphragm wide open (illumination NA matching the objective NA), you achieve the best possible resolution.

However, wide-open illumination also means that more stray light reaches the image, reducing contrast. For specimens with low inherent contrast (unstained cells, for example), slightly closing the aperture diaphragm can dramatically improve visibility, at the cost of a small reduction in resolution. In practice, most microscopists set the aperture diaphragm to about 70-80% of the objective NA as a compromise between resolution and contrast.

### The role of the field diaphragm

The field diaphragm is simpler: it controls the illuminated area on the specimen. Closing it so that it just circumscribes the field of view reduces the amount of light entering the optical system outside the observed region. This minimizes stray light, veiling glare, and internal reflections, all of which degrade contrast. A properly closed field diaphragm is one of the easiest and most effective ways to improve image quality.

## From brightfield to contrast techniques

With Köhler illumination providing uniform, well-controlled light, we now have a solid foundation for brightfield imaging. In brightfield mode, the specimen is illuminated with white light and imaged directly: structures that absorb light appear dark against a bright background. This works well for stained specimens (histological sections, Gram-stained bacteria), but most biological specimens in their native state are nearly transparent. They absorb almost no light and are essentially invisible in brightfield.

The next section introduces a family of contrast techniques that make transparent specimens visible without staining: darkfield microscopy, phase contrast, and differential interference contrast. Each of these techniques works by manipulating light in one of the conjugate planes we have just identified, which is why understanding Köhler illumination is a prerequisite for understanding them.
