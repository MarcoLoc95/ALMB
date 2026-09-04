# 7 - Imaging system design

Everything we have done so far has treated the microscope as an idea. In {ref}`Chapter 2 <chap2>` it was a thin lens obeying a formula. In {ref}`Chapter 3 <chap3>` it was a pair of conjugate planes with an aperture between them. In {ref}`Chapter 6 <chap6>` it dissolved entirely into a low-pass filter acting on spatial frequencies. Those abstractions are powerful, and they are the reason you can now predict what a microscope will and will not show you.

But nobody has ever bought a spatial frequency filter. What you buy, or inherit, or find gathering dust in a corner of the lab, is a table covered in metal cylinders and black boxes with cables coming out of them. Somebody chose every one of those parts. They chose a light source with a particular spectrum, a mirror with a particular coating, a camera with a particular pixel size, and they chose them because of the biology they wanted to see.

This chapter is about that translation, and it runs in both directions. Forwards, from a pile of components to a working instrument. Backwards, from a schematic in a paper to an understanding of what the authors were trying to do. Both directions rest on the same foundation: knowing what each part is for, what it costs you, and what it gives you in return.

```{figure} ../figures/chap7_building_blocks_map.png
---
width: 95%
name: chap7_building_blocks_map
align: center
---
The families of components that make up any imaging system. Light is generated at a source, shaped and filtered on its way to the sample, collected by an objective, filtered again, and converted into numbers by a detector.
```

We begin with the parts themselves: sources, mirrors, lenses, filters, detectors, and the specialized optical and mechanical components that show up once you leave the world of catalogue microscopes. Then we practise reading real published schematics, because that skill is what lets you pick up a methods paper and work out what the instrument actually does. Finally we turn the problem around and ask how you would design an instrument yourself, starting from a biological question.

This is also where the first half of the course meets the second. Almost every advanced technique in {ref}`Chapter 8 <chap8>` and {ref}`Chapter 9 <chap9>` is a rearrangement of the components introduced here. Once you recognise a pulsed laser, a pair of galvanometric mirrors and a photomultiplier tube in a figure, you have already worked out that you are looking at a multiphoton microscope, before reading a word of the caption.

## Learning objectives

At the end of this chapter you should be able to:

- Describe the emission characteristics of thermal lamps, arc lamps, LEDs and lasers, and select an appropriate source for a given fluorophore and application.
- Explain how stimulated emission in a resonant cavity produces monochromatic, coherent and collimated light, and distinguish continuous wave from pulsed operation.
- Calculate the peak power and duty cycle of a pulsed laser from its average power, pulse duration and repetition rate.
- Distinguish metallic from dielectric mirror coatings and explain why coated surfaces must never be touched.
- Distinguish bandpass, longpass, shortpass, neutral density and dichroic filters, and explain why blocking is specified as optical density rather than as transmission.
- Compare CCD, EMCCD, CMOS and sCMOS detectors in terms of sensitivity, speed, noise and cost, and argue which is appropriate for a given experiment.
- Explain how a photomultiplier tube amplifies a single photon into a measurable current, and why it carries no spatial information.
- Describe the function of galvanometric mirrors, digital micromirror devices and spatial light modulators, and identify which one suits a given task.
- Trace the optical path in a published schematic from source to detector, identify each intermediate component, and infer the function of the instrument.
- Argue, from a stated biological question, which sample preparation, label, light source, filter set, objective and detector you would choose, and justify the trade-offs.
