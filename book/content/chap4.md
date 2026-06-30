# 4 - Fluorescence microscopy

So far we have treated the microscope as an instrument that faithfully collects whatever light the sample sends back to us. In {ref}`Chapter 3 <chap3>` we ran into the catch that makes biology hard to image: most cells are almost perfectly transparent, so a wave passing through them emerges with nearly the same intensity it had going in. Phase contrast and dark field get around this by exploiting the phase or the diffraction angle of the light. They are powerful, but they share one limitation. They reveal whatever happens to scatter or delay light, not the specific molecule you actually care about.

Fluorescence solves a different problem. Instead of squeezing contrast out of an unlabeled sample, we attach (or genetically grow) molecules that light up on command. Shine one color of light, collect a second color, and only the labeled structures appear, glowing against a dark background. This is why fluorescence images are instantly recognizable: bright, often colorful features floating in black, rather than shades of grey on white. A warning about those colors, though. They are almost always false. We pick a lookup table that assigns, say, cyan to one channel and magenta to another. The fluorophore does not "know" it is cyan. We decided that, purely for display.

The entire field rests on one physical fact: certain molecules can absorb a photon, hold that energy for a brief moment, and then release a new photon of lower energy. _{numref}`Fig. %s <fluorescence_overview>`_ is that idea stripped to its essentials, and learning to read its full version is the goal of the first half of this chapter.

```{figure} ../figures/fluorescence_overview.png
---
width: 75%
name: fluorescence_overview
align: center
---
Fluorescence in one picture. A fluorophore absorbs a high-energy (short-wavelength) photon, loses a little of that energy as heat, and emits a lower-energy (longer-wavelength) photon. The shift toward longer wavelengths is precisely what lets us separate excitation from emission with filters.
```

This chapter is deliberately short. It is built around a single lecture, and it splits naturally into two parts. First we look at the physics: where fluorescence comes from, how we describe a fluorophore quantitatively, and the two problems you can never fully escape, autofluorescence and photobleaching. Then we look at the practical toolkit: the three families of fluorophores you will actually meet in the lab, and how they trade brightness, photostability, and toxicity against one another.

```{tip}
We skip two topics here on purpose. The optical filters that make the two-color trick work, and the layout of a complete widefield fluorescence microscope, belong with the instrument itself: widefield is covered in {ref}`Chapter 3 <chap3>`, and filters return later when we design imaging systems. For now we keep our attention on the light and the molecules that produce it.
```

## Learning objectives

At the end of this chapter you should be able to:

- Explain why fluorescence provides molecular specificity that phase contrast and dark field cannot.
- Read a Jablonski diagram and use it to describe absorption, vibrational relaxation, fluorescence, intersystem crossing, and phosphorescence.
- Distinguish singlet and triplet states and connect them to the timescales of fluorescence and phosphorescence.
- Relate the shape of excitation and emission spectra to the vibrational structure of a molecule, and define the Stokes shift.
- Define and use the key quantitative parameters of a fluorophore: radiative and non-radiative decay rates, quantum yield, lifetime, molar extinction coefficient, and brightness.
- Describe autofluorescence, photobleaching, and phototoxicity, and explain why turning up the excitation power is a double-edged sword.
- Explain the principle of FRET and why its steep distance dependence turns it into a molecular ruler.
- Compare organic dyes, genetically encoded fluorescent proteins, and quantum dots in terms of size, brightness, photostability, and toxicity, and choose between them for a given experiment.
