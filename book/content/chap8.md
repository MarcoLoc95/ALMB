(chap8)=
# 8 - Advanced techniques

Every chapter so far has been answering, in one way or another, the same question: _where is the fluorescence?_ Chapter 3 told us how finely we can locate it, Chapter 4 how to make it specific, Chapter 5 how to locate it in three dimensions without drowning in light from elsewhere, and Chapters 6 and 7 why the instruments that do this look the way they do. That question is the backbone of light microscopy, and most published images are still answers to it.

This chapter asks different questions. Not only where a molecule is, but how fast it moves, whether it is stuck to something, whether it is touching a partner, what the pH or the temperature or the membrane voltage is around it, and, in the last section, whether we need to label it at all. Each section is built around one of those questions:

- **Can we watch a living cell in three dimensions, fast, for hours, at the diffraction limit in every direction?** Section 8.1 follows up on the promise at the end of Chapter 5.3 and builds a light sheet out of interfering Bessel beams.
- **How do molecules move, and whom do they touch?** Section 8.2 covers fluorescence correlation spectroscopy, fluorescence recovery after photobleaching and Förster resonance energy transfer, three techniques that trade pictures for numbers.
- **What is the environment around a fluorophore?** Section 8.3 replaces the brightness of a fluorophore with its lifetime, which turns out to be a far more trustworthy observable.
- **What can the sample tell us without any label?** Section 8.4 uses the same pulsed lasers as multiphoton microscopy to generate contrast from collagen, membranes and chemical bonds directly.

```{figure} ../figures/chap8_collage.png
---
width: 90%
name: chap8_collage
align: center
---
A gallery of what the techniques in this chapter can do. A neutrophil-like cell crawling through a collagen matrix, recorded with lattice light-sheet microscopy; a fluorescence lifetime map of a zebrafish embryo expressing a voltage sensor; second-harmonic generation from collagen; third-harmonic generation outlining every cell of a zebrafish embryo; and engineered cartilage imaged with SHG and CARS together, with collagen in cyan and lipid deposits in orange. The last three required no label of any kind.
```

## Advanced, but still diffraction limited

One distinction is worth making explicit before we start, because it organises both this chapter and the next.

Everything in Chapter 8 is _diffraction limited_. However sophisticated these techniques are, ask any of them to separate two points in the focal plane and the answer comes back at roughly the 200 to 300 nm that Abbe gave us. FRET will report on distances of a few nanometres, but it never _resolves_ anything: it tells you that two molecules are close, not where they are. What these methods buy is something other than resolution: speed and gentleness, quantitative measurements of molecular behaviour, sensitivity to the local environment, or contrast without a label.

Chapter 9 is different in kind. Super-resolution techniques go below the diffraction limit, and every one of them does it by injecting information that the optics alone do not have: a known illumination pattern, a sample that has been physically expanded, a beam that switches molecules off, a sequence of sparse blinking events. When you meet a new super-resolution method, the first question to ask is what extra information is being injected and what it costs.

## Seven questions to ask of any technique

Chapter 7.3 argued that every design decision starts from the sample, and that the photon budget is the currency everything is paid in. When the decision is between techniques rather than between components, the trade-offs are conventionally expressed along seven axes. They are the columns of most comparison tables in the literature, so it pays to be fluent in them.

- **Lateral resolution**: the minimum resolvable distance in the focal plane.
- **Axial resolution**: the minimum resolvable distance along the optical axis.
- **Temporal resolution**: the time between two acquisitions. It depends on the field of view and the detector, so a number quoted without both is close to meaningless.
- **Penetration depth**: how deep you can go and still obtain a resolved image rather than a bright blur.
- **Resistance to photobleaching and phototoxicity**: how well the signal, and the sample, survive realistic imaging.
- **Labelling efficiency**: how reliably you can make only the features you care about visible.
- **Multiplexing**: how many species you can observe at once and still tell apart.

Only the first two are optics in the narrow sense. The other five belong to the sample, the probe, the detector and your patience, which is why choosing a technique is never a purely optical decision.

```{tip}
Resolution figures quoted in isolation are one of the most common ways in which microscopy papers mislead, usually without meaning to. A technique that achieves 230 nm on fluorescent beads lying on a coverslip may deliver 500 nm in an organoid 80 μm deep. Whenever you read a number, ask what it was measured on, at what depth, and with how many photons. 
```

---

At the end of this chapter you should be able to:

- distinguish diffraction-limited advanced techniques from super-resolution methods, and state what each technique in this chapter buys in exchange for its costs
- describe a beam in terms of the light distribution in the back focal plane, and explain why a thinner annulus produces a longer beam with stronger side lobes
- estimate the length of a Bessel beam from the inner and outer numerical aperture of the annulus that produces it
- explain how interference between Bessel beams redistributes power from the side lobes into a thin sheet, and why dithering a lattice is faster than scanning a single beam
- read the optical schematic of a lattice light-sheet microscope and identify the role of each element, in particular the annular mask in the Fourier plane
- interpret an FCS autocorrelation curve, extracting concentration from its amplitude and the diffusion coefficient from its decay time
- design a FRAP experiment, calculate the mobile fraction and diffusion coefficient from a recovery curve, and distinguish a true immobile fraction from depletion of a finite pool
- choose between intermolecular and intramolecular FRET designs for a given biological question, and explain why a negative FRET result does not prove that two molecules do not interact
- explain why fluorescence lifetime is independent of concentration, excitation intensity and photobleaching, and describe how time-correlated single-photon counting measures it
- explain the origin of pile-up and estimate the acquisition time of a FLIM image from the photon budget
- distinguish second-harmonic generation, third-harmonic generation and coherent anti-Stokes Raman scattering in terms of their energy diagrams, the physical requirement for each signal, and the structures they reveal
- select an appropriate technique for a given biological question and defend the choice against the seven criteria above
