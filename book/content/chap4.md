# 4 - Fluorescence microscopy

So far we have treated the microscope as an instrument that faithfully collects whatever light the sample sends back to us. In {ref}`Chapter 3 <chap3>` we ran into the catch that makes biology hard to image: most cells are almost perfectly transparent, so a wave passing through them emerges with nearly the same intensity it had going in. Phase contrast and dark field get around this by exploiting the phase or the diffraction angle of the light. They are powerful, but they share one limitation. They reveal whatever happens to scatter or delay light, not any specific molecule or organelle.

Fluorescence solves this problem. Instead of squeezing contrast out of an unlabeled sample, we attach (or genetically express) molecules that light up on command. Shine one color of light, collect a second color, and only the labeled structures appear, glowing against a dark background. This is why fluorescence images are instantly recognizable: bright, colorful features floating in black, rather than shades of grey on white.

A warning about those colors, though: they are almost always false. We pick a lookup table that assigns, say, cyan to one channel and magenta to another. The fluorophore does not "know" it is cyan. We decided that, purely for display.

This chapter is deliberately short. First we look at the physics: where fluorescence comes from, how we describe a fluorophore quantitatively, and the two problems you can never fully escape, autofluorescence and photobleaching. Then we look at the practical toolkit: the three families of fluorophores you will actually meet in the lab, and how they trade brightness, photostability, and toxicity against one another.

```{figure} ../figures/chap4_fluorescence_wrapper.png
---
width: 100%
name: chap4_fluorescence_wrapper
align: center
---
No book on light microscopy is complete until it contains a pretty picture of fluorescent cells. So here is a collage of beautiful samples, fluorescently labelled. Credits (left to right, top to bottom): super-resolution image of a neuron from deep in the brain (Ilaria Testa, via Biohub on Facebook/Instagram); confocal image of a Macrocystis V-type gametophyte (Siobhan Braybrook, on X); confocal image of astrocytes in a culture of rat retinal cells (Sandra Correia, from the 2018 EMBL Photoclub calendar, CC BY-SA 3.0); confocal image of Bovine Pulmonary Artery Endothelial cells undergoing mitosis (Caleb Foster, from Dreamstime.com).
```

At the end of this chapter you should be able to:

- Explain why fluorescence provides molecular specificity that phase contrast and dark field cannot.
- Read a Jablonski diagram and use it to describe absorption, vibrational relaxation, fluorescence, intersystem crossing, and phosphorescence.
- Distinguish singlet and triplet states and connect them to the timescales of fluorescence and phosphorescence.
- Relate the shape of excitation and emission spectra to the vibrational structure of a molecule.
- Compare key quantitative parameters of a fluorophore: radiative and non-radiative decay rates, quantum yield, lifetime, molar extinction coefficient, Stokes shift and brightness.
- Describe autofluorescence, photobleaching, and phototoxicity, and explain why turning up the excitation power is a double-edged sword.
- Explain the principle of FRET and why its steep distance dependence turns it into a molecular ruler.
- Compare organic dyes, genetically encoded fluorescent proteins, and quantum dots in terms of size, brightness, photostability, and toxicity, and choose between them for a given experiment.
