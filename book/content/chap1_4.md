# Light as a particle

We have described light as a wave (with wavelength, frequency, interference and diffraction) and as a ray (a convenient geometric shortcut for tracing light through optical systems). Both descriptions are powerful, but neither prepares you for what happens when you look at how light interacts with matter at the atomic scale. There, a third description takes over: light as a stream of **particles** called photons.

## The photoelectric effect

The story of the photon begins with a puzzle that baffled physicists at the turn of the 20th century. When light shines on a metal surface, it can knock electrons out of the metal. This is the **photoelectric effect**, and at first glance it seems perfectly reasonable: the energy in the light wave shakes the electrons loose. But the details did not match the wave picture at all.

If light were purely a wave, its energy would be proportional to its intensity (the square of the amplitude). Increasing the intensity should give the electrons more energy. But experimentally, increasing the intensity only increased the _number_ of ejected electrons, not their individual energy. Even more puzzling, below a certain threshold frequency, _no electrons were emitted at all_, no matter how intense the beam. You could blast the metal with an arbitrarily bright red light and nothing would happen, while a faint ultraviolet beam would immediately kick out electrons.

As we described in the historical chapter, Einstein and Marić proposed in 1905 that light comes in discrete packets (quanta) of energy. Each photon carries an energy:

$$
E = h\nu = \frac{hc}{\lambda}
$$

where $h = 6.626 \times 10^{-34}$ J$\cdot$s is Planck's constant, $\nu$ is the frequency, and $\lambda$ is the wavelength. This equation is deceptively compact, but it encodes a profound idea: the energy of a single photon depends only on its frequency (or equivalently, its wavelength), not on the intensity of the light. Higher intensity simply means more photons per second.

The photoelectric effect now made perfect sense. An electron is ejected when a _single_ photon transfers enough energy to overcome the binding energy of the metal. If the photon's frequency is too low (its wavelength too long), no single photon has enough energy, and no electrons are released, regardless of how many photons arrive. If the frequency is above the threshold, each photon can eject one electron, and increasing intensity (more photons) means more ejected electrons.

```{figure} ../figures/photoelectric.png
---
width: 70%
name: photoelectric
align: center
---
The photoelectric effect. The wave model predicts that increasing intensity should increase electron energy. The photon model correctly predicts that energy depends on frequency, not intensity. Copyright: Ponor, CC BY-SA 4.0, via Wikimedia Commons
```

## Why photons matter for microscopy

You might wonder why a 120-year-old physics experiment is relevant to a microscopy course. The answer is that the photon picture becomes essential whenever light interacts with individual molecules, which is precisely what happens in fluorescence microscopy.

Every time a fluorescent molecule absorbs light, it absorbs exactly one photon. The energy of that photon must match (or exceed) the energy gap between the molecule's ground state and its excited state. This is why fluorescent molecules have specific **excitation wavelengths**: only photons with the right energy can be absorbed. Similarly, when the molecule emits fluorescence, it emits exactly one photon. The energy (and therefore the wavelength) of the emitted photon is determined by the energy gap of the transition.

This is fundamentally different from the wave picture of image formation, where we think about amplitude, phase and interference. In fluorescence microscopy, the relevant question is not "how do the waves interfere?" but "how many photons did each molecule emit, and did we detect them?" This shift in perspective, from wave to particle, is one of the conceptual transitions that students of microscopy need to make.

## Photon phenomena: absorption, emission and stimulated emission

The interaction between photons and matter involves three fundamental processes, all of which play important roles in microscopy.

**Absorption** occurs when a photon is absorbed by an atom or molecule, transferring its energy to an electron, which jumps from a lower energy state to a higher one. The photon disappears in the process. This only happens when the photon's energy matches the energy difference between the two states. In fluorescence microscopy, this is the first step: the excitation laser provides photons at the right wavelength to be absorbed by the fluorophore.

**Spontaneous emission** is the reverse: an electron in an excited state spontaneously drops back to a lower state, releasing a photon in the process. The emitted photon has an energy equal to the energy difference between the two states. The direction and timing of this emission are random. This is the process that produces fluorescence: after absorbing an excitation photon, the molecule relaxes to the lowest vibrational level of the excited state (losing some energy as heat), and then emits a fluorescence photon at a _longer_ wavelength (lower energy) than the excitation photon. This wavelength difference between excitation and emission is called the **Stokes shift**, and it is what allows us to separate excitation light from fluorescence using filters.

**Stimulated emission** is a subtler process. When a photon of exactly the right energy encounters an already excited atom, it can stimulate the atom to emit a second photon. This second photon is identical to the first: same energy, same direction, same phase. The atom returns to the ground state, and two photons continue onward where there was one before. Stimulated emission is the mechanism behind lasers (the acronym stands for Light Amplification by Stimulated Emission of Radiation). It also plays a central role in super-resolution microscopy: STED (Stimulated Emission Depletion) microscopy, which we will encounter in {ref}`Chapter 9 <chap9>`, uses a laser tuned to the emission wavelength to force excited fluorophores back to the ground state before they can fluoresce, effectively shrinking the fluorescent spot below the diffraction limit.

```{figure} ../figures/photon_phenomena.png
---
width: 80%
name: photon_phenomena
align: center
---
The three fundamental photon-matter interactions. In absorption, a photon excites an electron to a higher state. In spontaneous emission, the electron drops down and a photon is released in a random direction. In stimulated emission, an incoming photon triggers the release of a second, identical photon.
```

## Example of photon phenomena in biology

A practical example ties this together beautifully: photosynthesis. Chlorophyll molecules in plant cells absorb blue and red photons, using most of the energy to drive chemical reactions (the conversion of water and CO$_2$ into sugars). Furthermore, a small fraction of the absorbed energy (roughly 1-2%) is re-emitted as red fluorescence. This is why leaves glow faintly red under UV illumination, and it is the same physical process that makes GFP, DAPI and all other fluorescent probes work in the microscope.

```{figure} ../figures/photosynthesis.png
---
width: 90%
name: photosynthesis
align: center
---
The Z-scheme of photosynthesis. Light energy absorbed by Photosystem II (P680) and Photosystem I (P700) excites electrons to higher energy states. Between the two photosystems, the electrons lose energy through an electron transport chain, driving the synthesis of ATP. The final electron acceptor is NADPH. Water serves as the initial electron donor, replacing the electrons lost by P680. Copyright: CC BY-SA 4.0, via Khan Academy
```

## General properties of light

Before moving on, here is some vocabulary that cuts across all three descriptions and that will be useful throughout the rest of the book:

- **Monochromatic** vs. **polychromatic**: light of a single wavelength vs. a mixture of wavelengths. Lasers are nearly monochromatic; white light is polychromatic.
- **Polarized** vs. **unpolarized**: a fixed oscillation direction vs. a random mixture. Lasers are typically linearly polarized; sunlight is unpolarized.
- **Coherent** vs. **incoherent**: waves with a fixed phase relationship vs. random phases. Laser light is coherent; a light bulb is incoherent. Coherence matters for interference: only coherent light produces stable interference patterns.
- **Collimated** vs. **divergent**: rays traveling in parallel vs. spreading out. A laser beam is well collimated; a point source emits divergent light.

```{figure} ../figures/light_properties.png
---
width: 80%
name: light_properties
align: center
---
General properties of light. Each pair describes a continuum, and real light sources fall somewhere between the extremes.
```

## Light-matter interactions

When light encounters matter, a range of things can happen: it can be **transmitted**, **reflected**, **refracted**, **diffracted**, **absorbed**, **scattered**, or converted to a different wavelength through **luminescence** (of which fluorescence is one type). Every contrast mechanism in microscopy exploits one or more of these interactions. The chapters that follow will build on these foundations, one interaction at a time.

```{figure} ../figures/light_matter.png
---
width: 80%
name: light_matter
align: center
---
The main types of light-matter interactions. Each one is the basis for one or more contrast mechanisms in microscopy.
```
