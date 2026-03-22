# 3 - Widefield microscopes and image formation

If you take a magnifying glass and look at a small insect, you will see a larger version of it: more detail, more texture, more color than your naked eye could ever resolve. Now imagine stacking a second lens behind the first one, and suddenly the insect appears even larger. This is, in essence, the principle behind the compound microscope: two or more lenses working together to produce magnifications that a single lens could never achieve on its own. But a microscope is much more than a stack of lenses. The way light is collected, bent, filtered and recombined determines not only how large the image appears, but how much _detail_ it actually contains.

This distinction between magnification and resolution is perhaps the single most important idea in microscopy. A cheap magnifying app on your phone can zoom in a thousand times on a photograph, but you will not see anything new: the image just becomes blurry. A good microscope, on the other hand, reveals structures that were genuinely invisible before. Understanding _why_ this is the case requires us to think about how light interacts with the sample, how lenses collect and focus that light, and what physical limits nature imposes on the process.

In this chapter, we will build up the complete picture of a widefield transmitted-light microscope, step by step. We start from the basic compound microscope and work our way through the optics of modern infinity-corrected systems. We will then confront the diffraction limit head-on: why it exists, what determines it, and how the numerical aperture of the objective governs resolution. From there, we will look at how the illumination system (Köhler illumination in particular) is designed to produce uniform, artifact-free images. Finally, we will explore a family of elegant contrast techniques (darkfield, phase contrast, and differential interference contrast) that allow us to image transparent biological specimens without any staining or fluorescent labeling.

These transmitted-light methods may seem old-fashioned compared to the fluorescence techniques we will encounter in {ref}`Chapter 4 <chap4>`, but they remain indispensable in the modern laboratory. Phase contrast is still the go-to method for checking cell cultures, darkfield microscopy is used to track single nanoparticles with nanometer precision, and DIC produces stunning images of unstained tissue. More importantly, the optical principles introduced here (image formation, resolution, conjugate planes, spatial filtering) form the foundation for everything that follows in this book.

```{figure} ../figures/widefield_overview.png
---
width: 90%
name: widefield_overview
align: center
---
Overview of a transmitted-light widefield microscope showing the illumination path (left) and the imaging path (right). The interplay between these two paths determines the quality and contrast of the final image.
```

At the end of this chapter you should be able to:
- Explain the difference between real and virtual images in a compound microscope
- Describe the advantages of the infinity-corrected optical configuration over the finite-tube-length design
- Read and interpret the markings on a microscope objective
- Define numerical aperture and explain its role in determining resolution
- State and apply the Abbe and Rayleigh resolution criteria
- Explain why immersion media improve resolution and when to use oil versus water
- Describe the principles of Köhler illumination and identify the conjugate planes in a microscope
- Distinguish between brightfield, darkfield, phase contrast, and DIC imaging and explain the physical basis of each technique
