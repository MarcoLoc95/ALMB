# 9 - Super-resolution techniques

A molecule of fluorescein, the dye that makes highlighter ink glow, measures about one nanometer across. Put it under the best objective money can buy and it shows up as a blurry spot roughly 250 nm wide: the point spread function we met in {ref}`Chapter 3 <chap3_2>`. The dye has not grown. The microscope simply cannot draw anything smaller than the diffraction limit. This is the problem with the nano-world: most of the machinery of the cell (receptors, motor proteins, synaptic vesicles, the nuclear pore) lives between one and a few hundred nanometers, right where a conventional light microscope turns everything into the same blob (_{numref}`Fig. {number} <chap9_scale>`_).

```{figure} ../figures/chap9_scale.png
---
width: 100%
name: chap9_scale
align: center
---
Sizes of some biological objects (top) compared with the resolution typically reached by the techniques in this chapter (bottom). The shaded band marks the diffraction limit of conventional light microscopy. Electron microscopy is shown in grey for reference.
```

For most of the twentieth century this barrier was considered final. Then, starting in the 1990s, a handful of groups found ways around it, and in 2014 Eric Betzig, Stefan Hell and William Moerner received the Nobel Prize in Chemistry for the development of super-resolved fluorescence microscopy. None of them broke the laws of diffraction. What they did was smarter: they found ways to add information that a conventional microscope throws away, or never collects.

## Where is the trick?

It is worth keeping one picture in mind for the whole chapter (_{numref}`Fig. {number} <chap9_trick>`_). An object, the _ground truth_, passes through an imaging system and comes out as a diffraction-limited image. Some information is lost on the way, and no amount of clever processing can recover what the system never transmitted. To obtain a super-resolved image we must feed **extra information** into the pipeline: either into the imaging system itself (a special illumination pattern, a second laser, a swollen sample) or into the reconstruction algorithm (knowledge about the PSF, about the fluorophores, about how sparse the molecules are).

```{figure} ../figures/chap9_trick.png
---
width: 100%
name: chap9_trick
align: center
---
Every super-resolution technique adds extra information to the imaging pipeline. Whether the result truly matches the ground truth, or contains artifacts introduced by wrong assumptions, noise or the algorithm, is a question that has to be asked every time.
```

We have already met the simplest example in {ref}`Chapter 6 <chap6_3>`: deconvolution. If we know the PSF, we can partially undo the blur. But deconvolution can only rebalance the frequencies that the objective transmitted; everything beyond the cutoff frequency was multiplied by zero and is gone. It sharpens, but it does not truly beat the diffraction limit. The techniques in this chapter go further because the extra information they add is physical: it changes what reaches the detector.

So, whenever you encounter a super-resolution technique, including ones that will be invented after this book is written, ask two questions. _What is the trick?_ What extra information is being added? And, as a direct consequence, _what happens if that information is wrong?_ The answer to the second question tells you where the artifacts will come from. A super-resolved image is never a photograph of the ground truth; it is a reconstruction that is only as good as the assumptions behind it. This is why super-resolution results must be validated with controls, repeated on many samples, and when possible compared with an independent method such as electron microscopy (which, of course, has its own artifacts).

## A map of the chapter

The techniques we will discuss use very different tricks, and it helps to sort them before diving in (_{numref}`Fig. {number} <chap9_overview>`_).

```{figure} ../figures/chap9_overview.png
---
width: 100%
name: chap9_overview
align: center
---
The tricks behind the techniques of this chapter (top), and simulated images of the same test structure at the resolution each technique typically reaches (bottom). The structure is a ring of eight subunits, each carrying two labels 12 nm apart. The values are indicative and depend strongly on the sample, the labels and the instrument.
```

- **Structured illumination microscopy (SIM)** illuminates the sample with a known striped pattern. The pattern mixes fine details into coarser moiré fringes that the objective can transmit, and an algorithm unmixes them. The trick is a known pattern; the gain is about a factor of two.
- **Expansion microscopy (ExM)** does not touch the optics at all. It embeds the sample in a swellable gel and physically enlarges it four to twenty times. The trick is a known and uniform expansion.
- **STED microscopy** uses a second, doughnut-shaped laser to switch off fluorescence everywhere except in a tiny spot at the center. The trick is a known depletion pattern combined with the photophysics of the dye.
- **Single-molecule localization microscopy (PALM, STORM, PAINT)** lets only a few, well-separated molecules emit at any time, finds the center of each one with nanometer precision, and builds up an image from millions of localizations. The trick is sparsity.
- **MINFLUX and MINSTED** combine the last two ideas: they localize single switched-on molecules with a doughnut-shaped beam whose zero is placed next to the molecule, and reach precisions of a few nanometers or below.

Along the way we will need to be careful with words. _Resolution_ is the smallest distance at which two objects can still be told apart. _Localization precision_ is how well we can pin down the position of one isolated object. The two are related but not the same, and much confusion in the super-resolution literature comes from mixing them up.

At the end of this chapter you should be able to:
- Explain why every super-resolution technique needs extra information, and identify that information for each method
- Describe how a structured illumination pattern shifts high spatial frequencies into the passband of the objective, and why the gain of linear SIM is limited to a factor of two
- Explain the principle of expansion microscopy and discuss the roles of the expansion factor, isotropy and label size
- Describe stimulated emission depletion, derive qualitatively how the effective PSF shrinks with depletion power, and explain the main sources of STED artifacts
- Distinguish detection from localization, and relate localization precision to the number of detected photons
- Compare the switching mechanisms of PALM, STORM and PAINT and choose between them for a given experiment
- Explain how MINFLUX uses an intensity zero to localize molecules with few photons, and why it works iteratively
- Critically evaluate a super-resolution image in terms of artifacts, labelling density, label size and validation
