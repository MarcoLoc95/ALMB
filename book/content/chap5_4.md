(chap5_4)=
# Multiphoton microscopy

## Why confocal microscopy stops at 100 µm

Every technique so far has assumed something we have not examined: that light travels in straight lines from the objective to the focus and back. In water and in cleared tissue that is nearly true. In living tissue it is not.

Brain, muscle and skin are dense mixtures of membranes, protein aggregates and organelles with refractive indices that differ by a few percent over sub-micrometre distances. Light passing through them is scattered. The **scattering mean free path**, the distance over which a photon is likely to be deflected, is around 50 to 100 µm in cortex at visible wavelengths. Focus 200 µm deep and only a small fraction of the excitation light is still in the ballistic beam; the rest is diffusely spread around it, exciting fluorophores where it should not.

The confocal microscope is hit twice. Its excitation is degraded on the way in, and on the way out its pinhole rejects every emitted photon that was scattered, which by then is most of them. The two effects compound, and confocal image quality in living tissue collapses somewhere between 50 and 150 µm.

**Multiphoton microscopy** fixes both, using a single trick that turns out to solve the sectioning problem for free.

## Two photons at once

In 1931, **Maria Göppert-Mayer** submitted a doctoral dissertation at Göttingen predicting that a molecule could absorb two photons simultaneously, each carrying half the energy of the transition, provided they arrived within an extraordinarily short window of one another. The prediction sat unverified for thirty years, because no light source in existence was intense enough to make the event likely. It was confirmed in 1961 by Kaiser and Garrett, immediately after the invention of the laser. Göppert-Mayer spent most of her career in unpaid or nominal academic positions and received the 1963 Nobel Prize in Physics for the nuclear shell model, becoming only the second woman to win it after Marie Curie. The unit of two-photon absorption cross-section, the GM, is named after her. Turning the prediction into a microscope took another twenty-nine years, and was done by Denk, Strickler and Webb at Cornell.

The mechanism is shown in _{numref}`Fig. {number} <chap5_twophoton_principle>`_(a). A molecule that normally absorbs at 488 nm can instead absorb two photons of about 976 nm. The first photon lifts the molecule into a **virtual state**, which is not a real energy level and has no lifetime in the usual sense: it persists for something of order $10^{-16}$ s. If a second photon arrives within that window, the molecule reaches the genuine excited state $S_1$ and everything from that point on proceeds exactly as in {ref}`Chapter 4 <chap4_1>`. It relaxes vibrationally and emits a normal fluorescence photon at the normal emission wavelength. From the emission side, two-photon and one-photon excitation are indistinguishable.

```{figure} ../figures/chap5_twophoton_principle.png
---
width: 100%
name: chap5_twophoton_principle
align: center
---
Left: one-photon and two-photon excitation of the same fluorophore. Two photons of roughly twice the wavelength, arriving within about $10^{-16}$ s of one another, reach the same excited state through a virtual level, and the emission that follows is identical. Middle: the consequence for the illumination cone. One-photon excitation makes the whole double cone fluoresce, while two-photon excitation confines the glow to the focal volume. Right: the same statement quantitatively. The distance from focus is measured in Rayleigh ranges, the Rayleigh range $z_R$ being the distance along the axis over which a focused beam widens by a factor $\sqrt{2}$, so it is the natural unit for the depth of a focus: one Rayleigh range away, the beam is already half again as wide in area as it is at the waist. In those units, the fluorescence emitted per axial plane is flat for one-photon excitation, which is precisely the origin of the out-of-focus haze, and falls as $1/z^2$ for two-photon excitation.
```

Because the process requires a coincidence, its rate depends on the **square** of the intensity:

$$
R_{2\text{P}} \propto I^2 \qquad \text{whereas} \qquad R_{1\text{P}} \propto I
$$

That single exponent is the whole technique.

## Why $I^2$ gives sectioning for free

Return to the argument in the chapter introduction. In a focused cone, the intensity at a distance $z$ from the focus falls as $1/z^2$, because the beam area grows as $z^2$. The number of fluorophores in that plane grows as $z^2$ for the same reason. For one-photon excitation, the fluorescence emitted per plane is therefore proportional to $(1/z^2) \times z^2$, a constant: every plane contributes equally, which is exactly the problem we set out to solve.

For two-photon excitation, the rate per fluorophore goes as $(1/z^2)^2 = 1/z^4$, while the number of fluorophores still goes as $z^2$. The fluorescence per plane therefore falls as $1/z^2$ (_{numref}`Fig. {number} <chap5_twophoton_principle>`_c). Out-of-focus planes contribute a rapidly diminishing amount, and in practice essentially all of the fluorescence comes from a femtolitre-scale volume at the focus.

This has a consequence worth stating on its own line, because it is where the depth performance comes from. **If all the fluorescence originates at the focus, then every detected photon must have come from the focus, no matter what path it took to reach the detector.** There is no need to reject anything, so there is no pinhole. You can put a large-area detector as close to the objective as physically possible and collect scattered photons along with ballistic ones, which is called **non-descanned detection**. In scattering tissue this is worth an enormous amount: the photons that a confocal pinhole would discard are exactly the ones that carry the deep signal.

## What it takes

The catch is that two-photon absorption is a very unlikely event, and making it happen at a useful rate requires intensities that would destroy a sample if delivered continuously. The way out is to concentrate the light in time rather than raising the average power.

The standard source is a mode-locked **titanium-sapphire laser**, tunable across roughly 680 to 1080 nm, emitting pulses about 100 fs long at a repetition rate of 80 MHz.

```{tip}
**Worked example: why pulses.** The duty cycle of such a laser is

$$
100 \times 10^{-15}\ \text{s} \times 80 \times 10^{6}\ \text{s}^{-1} = 8 \times 10^{-6}
$$

so the light is only present for eight parts per million of the time. The peak power is therefore about $1/(8\times10^{-6}) \approx 1.25 \times 10^{5}$ times the average power. At 10 mW average power at the sample, entirely tolerable for a living cell, the peak power is about **1.25 kW**. Because the rate goes as $I^2$, the pulsed beam produces roughly $10^5$ times more two-photon excitation than a continuous beam of the same average power. Pulsing is not a refinement here. Without it the technique does not work.
```

The second advantage comes from the wavelength. Scattering falls steeply with increasing wavelength, and the near-infrared range from about 700 to 1300 nm also sits in the **optical window** of tissue, where absorption by haemoglobin, melanin and water is at a minimum. Excitation light at 900 nm penetrates far better than at 450 nm, on top of everything gained from non-descanned detection. In practice, two-photon microscopy images 500 µm to over 1 mm into living cortex, against roughly 100 µm for confocal.

## The costs

**Resolution is worse.** The excitation wavelength is doubled, and diffraction scales with wavelength. The $I^2$ dependence squares the point spread function and buys back a factor of $\sqrt{2}$, but not the full factor of two. A typical two-photon microscope delivers a lateral resolution of 0.3 to 0.5 µm and an axial resolution of 1 to 2 µm, roughly one and a half times coarser than a good confocal. In exchange, that resolution is maintained at a depth where a confocal produces nothing at all.

**The laser is expensive**, both to buy and to keep aligned, and it dominates the cost of the instrument.

**Photodamage is not eliminated, it is relocated.** Out-of-focus bleaching genuinely does disappear, which is a large gain. At the focus, however, the peak intensity is enormous and higher-order processes become possible, so damage there can be more severe than in a confocal. The failure mode is different: instead of bleaching the whole cone gently, you can ablate the focal volume.

**Two-photon spectra are not simply the one-photon spectra at double the wavelength.** The selection rules differ, so two-photon excitation spectra are typically broader and often blue-shifted relative to twice the one-photon peak. Do not assume that a dye excited at 488 nm is best excited at 976 nm; look up its two-photon spectrum. The broadening has an upside: a single wavelength will often excite several fluorophores at once, which makes multi-colour imaging easier than it is with one-photon excitation.

```{tip}
Two related processes come along for free, because they need the same femtosecond laser and the same tight focus.

**Second harmonic generation** (SHG) converts two photons into a single photon of exactly half the wavelength, with no absorption and no excited state at all. It occurs only in materials that lack a centre of symmetry, which in tissue means collagen fibres, myosin filaments and microtubule bundles. Because nothing is absorbed, SHG cannot bleach and requires no label.

**Third harmonic generation** (THG) is similarly label-free and highlights interfaces and lipid bodies.

**Three-photon microscopy**, using 1300 or 1700 nm, applies the same logic one step further: an $I^3$ dependence and even less scattering, at the cost of needing higher peak powers still. It reaches through the entire mouse cortex into the hippocampus.
```

## Choosing between the four

To summarise multiphoton microscopy on its own terms:

- **Advantages**: intrinsic optical sectioning with no pinhole and no discarded light; the deepest penetration of any fluorescence technique discussed here; no out-of-focus photobleaching; access to SHG and THG contrast; near-infrared light is less phototoxic to bulk tissue.
- **Drawbacks**: lateral and axial resolution about 1.5 times coarser than confocal; point scanning, so the same speed limitations as a laser scanning confocal; a very expensive laser; intense photodamage possible at the focal volume; two-photon spectra must be measured rather than inferred.

And to close the chapter, the comparison that actually matters at the microscope:

| | Section thickness | Speed | Depth | Phototoxicity |
|---|---|---|---|---|
| **Confocal, point scanning** | ~0.5 to 1 µm | slow (~1 frame/s) | ~100 µm | high, whole depth illuminated |
| **Confocal, spinning disk** | ~1 µm, worse in thick samples | very fast (up to ~1000 frames/s) | ~50 µm | high, whole depth illuminated |
| **TIRF** | ~100 nm | very fast (widefield) | 0, surface only | very low, only the shell is excited |
| **Light sheet** | ~1 to 10 µm, set by the sheet | very fast (widefield) | large, especially when cleared | very low, only the plane is excited |
| **Multiphoton** | ~1 to 2 µm | slow (point scanning) | 500 µm to >1 mm | low outside the focus, high at it |

Read the table as a set of questions rather than a ranking. Is the biology at the coverslip? Then TIRF, and nothing else comes close. Is the specimen a living embryo that must survive a day of imaging? Light sheet. Is it 400 µm inside a living mouse brain? Multiphoton. Is it a fixed, well-stained 20 µm section where you want the cleanest possible image and have no particular hurry? Confocal, which is why it remains the default.

In {ref}`Chapter 6 <chap6>` we will change register entirely and ask what all of these instruments are doing in terms of spatial frequencies, which will let us say precisely what information an imaging system keeps and what it destroys.
