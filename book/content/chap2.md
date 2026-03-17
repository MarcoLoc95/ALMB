# 2 - Geometrical optics

In {ref}`Chapter 1 <chap1>` we explored the dual nature of light, discovering that it behaves as a wave and as a particle depending on the experiment we perform. While that picture is physically complete, it is often more than we need. When the objects we care about are much larger than the wavelength of light (think lenses, mirrors, apertures of a few millimeters or more), we can safely ignore the wave character and describe light as a collection of _rays_ that travel in straight lines through uniform media and bend at interfaces. This simplification is called **geometrical optics**, and it is the language in which virtually every optical instrument, from a magnifying glass to a state-of-the-art microscope objective, is first designed and understood.

The power of geometrical optics lies in its economy: a handful of rules about how rays refract and reflect are enough to predict where an image forms, how large it is, and whether it is upright or inverted. These predictions are remarkably accurate as long as we stay in the regime where the ray picture holds. The moment the predictions start to fail, we learn something equally important: we discover the _aberrations_, systematic deviations from the ideal image that arise because real lenses are not the perfectly thin, perfectly shaped objects we assume in the simplest treatment.

```{figure} ../figures/chap2_lens_overview.png
---
width: 90%
name: chap2_lens_overview
align: center
---
A converging lens bends incoming rays to form an image. Geometrical optics lets us predict where that image forms, how it is magnified, and what can go wrong when the idealized assumptions break down.
```

In this chapter we will start from first principles: Snell's law and the geometry of a curved surface, building up to the thin lens equation and the rules for ray tracing. We will then explore what happens when the paraxial approximation breaks down, leading to monochromatic aberrations such as spherical aberration, coma, astigmatism and field curvature. Finally, we will see that the refractive index of glass is not the same for all wavelengths, giving rise to chromatic aberrations, and learn how lens designers correct for them using achromatic doublets, apochromats and more. These concepts will become essential when we discuss microscope objectives and image formation in {ref}`Chapter 3 <chap3>`.

At the end of this chapter you should be able to:
- Derive the thin lens equation from Snell's law applied to two spherical surfaces
- Apply the lensmaker equation to calculate the focal length of a thin lens
- Use ray tracing rules to locate and characterize the image of an object
- Explain how the paraxial approximation leads to the thin lens equation and why its failure produces aberrations
- Describe the five Seidel aberrations and their physical origins
- Estimate the longitudinal and lateral chromatic aberration given two colors and the dispersion of the lens
- Explain the principle behind achromatic, apochromatic and superachromatic objectives
- Argue which level of aberration correction is appropriate for a given microscopy application