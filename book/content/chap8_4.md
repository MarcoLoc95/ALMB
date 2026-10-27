(chap8_4)=
# 8.4 - Label-free techniques

Almost everything in this book has depended on a label. Chapters 4 and 7 spent a great deal of effort on making fluorophores brighter, more specific and more photostable, and all of it exists because the molecules we care about are, optically speaking, nearly invisible.

Labels are not free. They require genetic engineering or staining, which take time and do not always work. They perturb what they report on, because a fluorescent protein fused to your target is a substantial addition to it. They bleach. And, as Chapter 4.1 showed, an excited fluorophore that reaches its triplet state and meets oxygen is an efficient source of reactive oxygen species, which makes labels the main origin of phototoxicity.

So it is worth asking a question that sounds naive and is not: can biological structure produce contrast by itself? For some structures, the answer is yes, and the three techniques in this section show how.

## Real states and virtual states

All three techniques are nonlinear optical processes, and they run on the same hardware as multiphoton microscopy: a near-infrared femtosecond pulsed laser, a scanner, and point detectors. What separates them from multiphoton fluorescence is where the molecule goes between absorbing and emitting.

```{figure} ../figures/chap8_nonlinear_energy_diagrams.png
---
width: 95%
name: chap8_nonlinear_energy_diagrams
align: center
---
Energy diagrams for four nonlinear processes. Two- and three-photon fluorescence reach a real excited state, relax vibrationally, and then emit a red-shifted photon. Second- and third-harmonic generation pass only through virtual states and emit at exactly twice or three times the incident frequency.
```

Chapter 5.4 introduced the virtual state as a stepping stone: in two-photon excitation, the first photon lifts the molecule to a virtual level that survives for about $10^{-16}$ s, and the second photon must arrive in that window to complete the journey to the real excited state $S_1$. From there, everything proceeds as in ordinary fluorescence. Compare the four diagrams in _{numref}`Fig. {number} <chap8_nonlinear_energy_diagrams>`_. In harmonic generation, the journey never reaches a real state at all. The photons drive the electron cloud through virtual levels only, and the energy comes straight back out as a single photon. Three consequences follow, and they are the reason these techniques exist:

- **No energy is deposited in the molecule.** There is no excited-state population, hence no photobleaching, no triplet state, and essentially no phototoxicity from the contrast mechanism itself.
- **No fluorophore is required.** The signal comes from the structure of the material.
- **The emission is exactly at $\lambda/2$ or $\lambda/3$.** It is a narrow line locked to the laser, not a broad band at whatever wavelength the emitter happens to prefer.

```{tip}
**Worked example: telling SHG from two-photon fluorescence at the microscope.**

You excite a tissue sample at 900 nm and record a bright signal at 450 nm. Is it second-harmonic generation from collagen, or two-photon excited autofluorescence?

Tune the laser to 860 nm. If the signal moves to 430 nm, it is SHG: harmonics track the excitation exactly. Fluorescence emission belongs to the emitting molecule, so its spectrum stays where it was. If you have a spectral detector, look at the width as well: SHG is a few nanometres wide, set by the bandwidth of the laser pulse, while fluorescence spans tens of nanometres.

A third clue: SHG is coherent and therefore strongly forward-directed, while fluorescence is emitted in all directions. A signal that is much stronger in transmission than in epi-detection is very likely a harmonic.
```

## Second-harmonic generation

### Why asymmetry matters

The physics is easier to feel than to derive. An electron bound in a molecule sits in a potential well, and the oscillating electric field of the laser pushes it back and forth. If the well is perfectly parabolic, the electron follows the field faithfully and re-radiates at the same frequency. Real wells are not perfectly parabolic, and at the intensities of a focused femtosecond pulse the difference matters: the response becomes distorted, and a distorted periodic signal contains harmonics.

Which harmonics depends on the shape of the well, and that is the whole story of SHG. The animation in _{numref}`Fig. {number} <chap8_anharmonic_oscillator>`_ compares two wells, one symmetric and one strongly asymmetric, driven far below any resonance as in a real SHG experiment. The trick for seeing the harmonics is to subtract the part of the motion that simply follows the laser, and look at what is left over.

```{figure} ../figures/chap8_anharmonic_oscillator.gif
---
width: 100%
name: chap8_anharmonic_oscillator
align: center
---
An electron driven by the laser field in a symmetric well (top) and an asymmetric well (bottom). Left: the well, with the electron moving in it. Middle: the electron's motion (orange) compared with a pure sine at the laser frequency (dashed). Right: what is left after subtracting that sine, magnified. In the symmetric well the leftover repeats three times per laser cycle: a third harmonic, and nothing at twice the frequency. In the asymmetric well the electron swings further one way than the other, and the leftover repeats twice per cycle: a second harmonic. The anharmonicity is exaggerated for visibility; in real materials the harmonics are far weaker.
```

A symmetric well, however anharmonic, distorts the two halves of each cycle identically, and such a distortion contains only odd harmonics: $3\omega$, $5\omega$, and so on. That is the top row. An asymmetric well treats the two halves differently, flattening one and sharpening the other, and that lopsidedness is what generates $2\omega$. That is the bottom row. The second harmonic is the signature of a material that responds differently to being pushed left and being pushed right.

There is one more condition. Even if every molecule in a sample is individually asymmetric, a solution of them, randomly oriented, produces no SHG, because the contributions from molecules pointing in opposite directions cancel. The asymmetry must survive at the scale of the focal volume. SHG therefore requires materials that are _non-centrosymmetric_ in bulk: ordered assemblies of asymmetric building blocks with a consistent orientation.

### What lights up

In biology that selects, with remarkable specificity, for a handful of structures:

- **fibrillar collagen**, by far the strongest and most widely used source;
- **myosin** thick filaments in the regular sarcomeres of skeletal and cardiac muscle;
- **microtubules** arranged in polarised bundles, such as those of the mitotic spindle and axons;
- in plants, **cellulose** and **starch** granules.

The examples in _{numref}`Fig. {number} <chap8_ex_shg>`_ show how selective this contrast is: each image contains only the ordered structures, and nothing else in the tissue is visible.

```{figure} ../figures/chap8_ex_shg.png
---
width: 70%
name: chap8_ex_shg
align: center
---
Second-harmonic generation without any label. (a) Collagen lamellae in human cornea. (b) Sarcomeric banding in zebrafish skeletal muscle, generated by myosin. (c) The crimped collagen fibres of a mouse tail tendon. (d) The collagen matrix of horse knee cartilage, with the dark lacunae that house the chondrocytes. Copyright: BP-Aegirsson, CC BY-SA 4.0, via Wikimedia Commons.
```

Because the signal is coherent, its intensity and direction depend on how the emitters are arranged, and its strength depends on the polarisation of the laser relative to the fibres. Rotating the polarisation and watching the signal change reports on fibre orientation directly, which is information a fluorescent label would not give you.

That selectivity is why SHG has real clinical traction. Collagen architecture is remodelled in fibrosis, in wound healing, in osteoarthritis, and in the stroma around tumours, where straightened, aligned collagen fibres oriented perpendicular to the tumour boundary have been associated with invasion and poorer outcomes. SHG measures that architecture in unstained, unfixed tissue.

## Third-harmonic generation

### Contrast from cancellation

Third-harmonic generation combines three photons into one at three times the frequency. Unlike SHG it has no symmetry requirement: the animation above shows a third harmonic even in the symmetric well, and indeed every material, water included, has a non-zero third-order response.

That raises an obvious objection. If everything generates a third harmonic, everything should be bright, and there should be no contrast at all. The resolution of this paradox is one of the most elegant details in the chapter.

A focused beam does not keep a constant phase as it passes through its waist. It picks up an extra half-cycle of phase shift relative to a plane wave, known as the _Gouy phase shift_. The third harmonic generated at each point along the focus inherits three times the local phase of the driving field, so harmonic light generated after the focus is out of step with harmonic light generated before it. In a uniform medium, for a tightly focused beam, what is built up on the way into the focus is undone on the way out, essentially completely.

```{figure} ../figures/chap8_thg_interface.gif
---
width: 100%
name: chap8_thg_interface
align: center
---
Why THG sees only interfaces. Top: the laser focus (light travelling from left to right, the triangle marking the focal point) is scanned along the optical axis through a fixed interface between two media, as it would be when imaging. Bottom: the THG signal recorded at each focus position. While the focus lies entirely inside one medium the signal is essentially zero; it appears only while the focus straddles the interface. The width of the peak equals the confocal parameter of the focus (twice its Rayleigh range), here 1.6 μm, typical for an objective of NA 0.8 at 1200 nm.
```

_{numref}`Fig. {number} <chap8_thg_interface>`_ shows what this means in practice, as the focus is scanned through an interface. While the whole focus sits inside one medium, the light generated on the way into the focus and on the way out of it cancels, and the detector sees nothing. When the focus straddles the interface, the material on one side responds differently from the material on the other, so the two contributions no longer balance. The cancellation fails, and a signal appears.

THG is therefore an **interface detector**. It lights up wherever the refractive index or the nonlinear response changes within the focal volume, and the signal falls away as soon as the focus moves more than about a Rayleigh range from the interface, under a micrometre for a high-NA objective, which gives THG its own optical sectioning. In tissue that means:

- **membranes and cell boundaries**;
- **lipid droplets, vesicles and myelin**, whose lipid content differs strongly from the surrounding cytoplasm;
- **red blood cells**, which are particularly bright for a different reason: haemoglobin absorbs near the third-harmonic wavelength, and this resonance boosts the signal.

The result is something close to histology without staining. In _{numref}`Fig. {number} <chap8_ex_thg>`_, THG alone outlines the cells of a living zebrafish embryo, and a side-by-side comparison with a fluorescent membrane label shows that it does so at least as well, without any genetic modification. In _{numref}`Fig. {number} <chap8_ex_thg_cerebellum>`_, THG imaging through a cranial window in a living mouse resolves the layers of the cerebellar cortex one by one, down to the white matter more than 300 μm below the surface. THG has also been explored for rapid, label-free assessment of human brain tumour tissue during surgery, where the alternative is to wait for a frozen section to be stained.

```{figure} ../figures/chap8_ex_thg_zebrafish.png
---
width: 70%
name: chap8_ex_thg
align: center
---
A living zebrafish embryo imaged at two depths (top and bottom rows). Left (A, D): third-harmonic generation, with no label. Right (B, E): two-photon excited fluorescence from mCherry targeted to the cell membranes. THG outlines the cells as well as the fluorescent membrane label does, and the deep cells even better; it also highlights the surface of the embryo, which the label misses. The white boxes mark regions magnified in the original publication. Scale bar: 100 μm. Copyright: Olivier et al. (2010), via Science.
```

```{figure} ../figures/chap8_ex_thg_cerebellum.png
---
width: 95%
name: chap8_ex_thg_cerebellum
align: center
---
Label-free THG imaging of the mouse cerebellum in vivo, through a cranial window. (A) The layers of the cerebellar cortex: molecular layer (ML), Purkinje cell layer (PCL), granular layer (GL) and white matter (WM). (B) Three-dimensional reconstruction of a stack of THG images. (C to F) Single planes at depths of 60, 160, 260 and 360 μm, falling in the ML, PCL, GL and WM respectively; the dashed yellow line in (D) marks the Purkinje cell layer. Scale bars: 100 μm. Copyright: Yu et al. (2025), via ACS Photonics.
```

## Coherent anti-Stokes Raman scattering

The last technique is the most ambitious, because it does not report on structure at all. It reports on chemistry.

### Raman scattering

When light meets a molecule, nearly all of it is scattered elastically: same energy in, same energy out. This is Rayleigh scattering. Very occasionally the molecule is left in a different vibrational state from the one it started in, and the scattered photon carries away, or gains, exactly the difference.

```{figure} ../figures/chap8_raman_cars_levels.png
---
width: 95%
name: chap8_raman_cars_levels
align: center
---
(a) Spontaneous Raman scattering. Most light scatters elastically (Rayleigh); occasionally the molecule changes vibrational state, shifting the photon energy by the vibrational quantum $\Omega$ (Stokes, red-shifted; anti-Stokes, blue-shifted). (b) In CARS, pump and Stokes beams whose frequency difference matches $\Omega$ drive the vibration coherently, and a probe photon scatters off it into a strong, blue-shifted anti-Stokes signal.
```

If the molecule ends up vibrationally excited, the photon is red-shifted: _Stokes_ scattering, panel (a) of _{numref}`Fig. {number} <chap8_raman_cars_levels>`_. If it started out already excited, which at room temperature is rare, and ends in the ground state, the photon is blue-shifted: _anti-Stokes_ scattering. In both cases the energy shift, conventionally quoted in wavenumbers [cm$^{-1}$], is the vibrational frequency of a particular chemical bond in a particular environment. Plot the scattered intensity against shift and you obtain a chemical fingerprint, like the one in _{numref}`Fig. {number} <chap8_ex_raman_spectrum>`_.

```{figure} ../figures/chap8_ex_raman_spectrum.jpg
---
width: 55%
name: chap8_ex_raman_spectrum
align: center
---
The fingerprint region of the Raman spectrum of a cervical cancer cell line (CaSki), with the main bands assigned to glycogen, proteins, lipids and nucleic acids. Copyright: Ramos et al. (2015), CC BY, via BioMed Research International.
```

Raman spectroscopy has been a workhorse of analytical chemistry for a century. Its problem for microscopy is that the effect is extraordinarily weak, many orders of magnitude weaker than fluorescence. Building an image pixel by pixel from spontaneous Raman spectra takes tens of minutes to hours, which rules out anything alive and moving.

### Making it coherent

CARS solves the sensitivity problem by not waiting for spontaneous events. It drives the vibration deliberately.

Two synchronised pulsed lasers illuminate the sample: a _pump_ at frequency $\omega_p$ and a _Stokes_ beam at $\omega_S$, tuned so that

$$ \omega_p - \omega_S = \Omega, $$

the vibrational frequency of interest. When that condition holds, the two beams beat together at exactly the frequency of the bond and drive it resonantly, and they drive _every_ such bond in the focal volume in phase. A third photon, in practice another pump photon, scatters off this coherently oscillating population and emerges at the anti-Stokes frequency $2\omega_p - \omega_S$.

Because the molecules radiate in phase, their fields add before being squared, so the signal grows as the square of the number of molecules rather than linearly. That coherent enhancement turns an unusable effect into an imaging technique fast enough for living cells. The output also arrives in a convenient place: the anti-Stokes signal is blue-shifted relative to both lasers, whereas fluorescence is always red-shifted, so a simple short-pass filter separates the two.

```{figure} ../figures/chap8_cars_setup.png
---
width: 95%
name: chap8_cars_setup
align: center
---
A CARS microscope. Pump and Stokes pulses must overlap in space, which the dichroic mirror ensures, and in time, which the delay line ensures: two of the Stokes mirrors sit on a translation stage, and moving it lengthens or shortens the Stokes path. The image is built by scanning; after the sample, a condenser collects the light and a short-pass filter passes only the blue-shifted anti-Stokes signal to the detector.
```

The one unfamiliar element in _{numref}`Fig. {number} <chap8_cars_setup>`_ is the **delay line**. The pulses are only a few hundred femtoseconds long, so they must reach the sample simultaneously to within a fraction of that. A pair of mirrors on a translation stage lengthens or shortens one beam's path: light travels 0.3 mm in a picosecond, so moving the stage by a fraction of a millimetre is exactly the scale of control needed.

Tuning $\omega_S$ with $\omega_p$ fixed sweeps through the vibrational spectrum. In practice you tune to one band at a time, the CH$_2$ stretch of lipids near 2850 cm$^{-1}$ being the brightest and most popular, and record a map of where that bond is. The engineered cartilage in _{numref}`Fig. {number} <chap8_ex_cars>`_ shows how naturally these techniques combine: the collagen is imaged by SHG and the fat deposits by CARS, in the same unlabelled specimen and on the same microscope.

```{figure} ../figures/chap8_ex_cars_cartilage.png
---
width: 55%
name: chap8_ex_cars
align: center
---
Cartilage-like tissue grown in the lab from bone marrow stem cells, imaged without labels. Collagen fibres (cyan) are imaged by second-harmonic generation and fat deposits (orange) by CARS. Colours adapted. Copyright: Catarina Moura, Sumeet Mahajan, Richard Oreffo and Rahul Tare (University of Southampton), via Nikon Small World 2017.
```

### The catch, and its successor

Alongside the resonant signal, the same beams generate a **non-resonant background** through the electronic response of everything in the focus, water included. This background carries no chemical information, and worse, it interferes with the resonant signal: 
CARS peaks come out shifted and lopsided compared with the Raman spectrum, and the signal is not proportional to concentration, which makes quantification awkward. This is why **stimulated Raman scattering** (SRS) has become increasingly popular. SRS uses the same two lasers but detects something different: not a new colour, but the tiny fraction of energy transferred from the pump beam to the Stokes beam when the bond is driven. That transfer occurs only at a genuine vibrational resonance, so SRS is free of the non-resonant background, reproduces the spontaneous Raman spectrum, and scales linearly with concentration. If CARS is the technique that proved coherent Raman imaging was possible, SRS is increasingly the one people use.

## Pulling the family together

These techniques belong together for a practical reason, not just a conceptual one. Two- and three-photon fluorescence, SHG, THG and CARS all need intense, ultrashort, near-infrared pulses focused to a diffraction-limited spot and scanned across the sample. They therefore run on the same instrument, and a single multiphoton microscope with the right filters and detectors can record several of them simultaneously, from the same scan: fluorescence from whatever you labelled, SHG from ordered filaments, THG from interfaces, and CARS from a chosen chemical bond.

## Summary

- **Advantages**: no labelling, so no perturbation, no staining protocol and no genetic engineering; very low phototoxicity, because the main source of reactive oxygen species is gone; contrast with a direct physical meaning (molecular order for SHG, interfaces for THG, chemical composition for CARS); the depth penetration and intrinsic sectioning of multiphoton microscopy; compatible with fluorescence on the same instrument.
- **Drawbacks**: weak signals, since none of these processes evolved to be efficient; contrast so specific that it cuts both ways, so SHG shows collagen beautifully and nothing else at all; CARS in particular needs two synchronised pulsed sources and suffers from the non-resonant background; expensive equipment throughout.

Used well, these techniques answer a question that fluorescence cannot: what is actually there, in tissue that nobody has touched.
