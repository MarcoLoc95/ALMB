# 7 - Imaging system design

We have so far discussed optics in rather general and abstract terms. However, what you buy, or inherit, or find gathering dust in a corner of the lab, is a table covered in metal cylinders and black boxes with cables coming out of them. At a certain point somebody chose every one of those parts. They chose a light source with a particular spectrum, a mirror with a particular coating, a camera with a particular pixel size, and they chose them because of the specific biology they wanted to see.

This chapter is about that translation. We will see how to go from a pile of components to a working instrument, but also from a schematic in a paper to an understanding of what the authors were trying to do. The foundation is essentially the same: knowing what each part is for, what it costs you, and what it gives you in return.

We begin with the parts themselves: sources, mirrors, lenses, filters, detectors, and the specialized optical and mechanical components that show up as soon as you leave the world of commercial microscopes. Then, we practice reading real published schematics, a useful skill that lets you pick up a methods paper and work out what the instrument actually does. Finally, we turn the problem around and ask how you would design an instrument yourself, starting from a biological question.

Almost every advanced technique in {ref}`Chapter 8 <chap8>` and {ref}`Chapter 9 <chap9>` is a rearrangement of the components introduced here. Once you recognise a pulsed laser, a pair of galvanometric mirrors and a photomultiplier tube in a figure, you have already worked out that you are looking at a multiphoton microscope, before reading a word of the caption.

```{figure} ../figures/chap7_building_blocks_map.png
---
width: 95%
name: chap7_building_blocks_map
align: center
---
The families of components that make up any imaging system. Light is generated at a source, shaped and filtered on its way to the sample, collected by an objective, filtered again, and converted into numbers by a detector.
```

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
