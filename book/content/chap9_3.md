# STED microscopy

Of all super-resolution techniques, STimulated Emission Depletion (STED) microscopy is probably the one whose name everybody has heard, even outside microscopy. Proposed by Stefan Hell and Jan Wichmann in 1994 and demonstrated experimentally a few years later, it was the first far-field method to show that the diffraction limit is not a fundamental limit for fluorescence imaging. Its trick is conceptually simple: if the excitation spot cannot be made smaller than about 200 nm, then make sure that only the molecules in its very center are _allowed_ to fluoresce.

## Stimulated emission, revisited

In {ref}`Chapter 1 <chap1_4>` we listed three ways in which light and matter interact: absorption, spontaneous emission and stimulated emission. Fluorescence is spontaneous emission: after excitation the molecule relaxes to the lowest vibrational level of $S_1$, waits on average a few nanoseconds, and then drops back to the ground state emitting a photon in a random direction (_{numref}`Fig. {number} <chap9_sted_jablonski>`_).

```{figure} ../figures/chap9_sted_jablonski.png
---
width: 60%
name: chap9_sted_jablonski
align: center
---
Jablonski diagram of STED. After excitation, a molecule in $S_1$ can relax by spontaneous fluorescence, or a photon of the STED beam can force it down to a high vibrational level of $S_0$ before it fluoresces. The stimulated photon is identical to the STED photon and is removed by the detection filters.
```

If, while the molecule is in $S_1$, a photon with the right energy passes by, it can _stimulate_ the transition to the ground state. The molecule emits a second photon that is an exact copy of the first: same wavelength, same direction, same phase and polarization. This is the process at the heart of every laser. In STED it serves a different purpose. The stimulating beam, the **STED beam**, is tuned to the red tail of the emission spectrum, so that it pulls the molecule down to a high vibrational level of $S_0$ that quickly relaxes thermally. Two consequences follow. First, the stimulated photons have the wavelength of the STED laser and travel along with it, so they are easily separated from the fluorescence by a filter. Second, a molecule that has been forced back to the ground state can no longer fluoresce: its fluorescence has been **depleted**.

The probability that a molecule escapes depletion falls off exponentially with the intensity of the STED beam:

$$
\eta(I) = \exp\left(-\ln 2 \cdot \frac{I}{I_s}\right)
$$

Here $I_s$ is the **saturation intensity**, the STED intensity at which half of the excited molecules are depleted. It depends on the fluorophore (its cross-section for stimulated emission) and on the timing of the pulses, and for common dyes it lies in the range of a few MW/cm². The important feature of this equation is its steepness: at $I = 5 I_s$ only 3% of the molecules still fluoresce, at $I = 10 I_s$ fewer than one in a thousand. Depletion behaves almost like a switch that turns fluorescence off once the STED intensity exceeds a few times $I_s$.

## The doughnut

Now imagine overlaying the normal Gaussian excitation spot with a STED beam shaped like a doughnut: intense all around, but with a point of exactly zero intensity in the center. Everywhere in the ring, the STED intensity is far above $I_s$ and fluorescence is switched off. Only in a small region around the zero, where the STED intensity remains below about $I_s$, can molecules still fluoresce. The detector, which cannot tell where the photons came from, now receives light only from this central region. The effective PSF has shrunk.

How small does it get? Near its zero, the doughnut intensity grows quadratically with the distance $r$ from the center, $I(r) \approx I_{max}\, r^2/a^2$ for some length $a$ comparable to the size of the excitation spot. Plugging this into the depletion law gives a survival probability $\exp(-\ln 2\, I_{max} r^2/(I_s a^2))$, a Gaussian whose width shrinks as $1/\sqrt{I_{max}/I_s}$. Multiplying by the excitation spot leads to the well-known STED resolution formula:

$$
d_{STED} \approx \frac{\lambda}{2\,\mathrm{NA}\sqrt{1 + I/I_s}} = \frac{d_{Abbe}}{\sqrt{1 + I/I_s}}
$$

where $I$ is the maximum intensity of the doughnut. Without the STED beam ($I = 0$) we recover Abbe's limit. As the STED intensity grows, the resolution improves without bound, at least on paper. In practice, with $I/I_s$ between 10 and 100, STED reaches 20-70 nm in biological samples, an improvement of five to ten times over confocal microscopy (_{numref}`Fig. {number} <chap9_sted_power>`_).

```{figure} ../figures/chap9_sted_power.gif
---
width: 90%
name: chap9_sted_power
align: center
---
As the STED intensity increases, the doughnut switches off fluorescence closer and closer to its center, and the effective PSF shrinks. The doughnut is shown on a scale that saturates at $5 I_s$, where almost all fluorescence is depleted, so its dark center marks the region where molecules can still emit.
```

Notice that nothing here violates diffraction. Both the excitation spot and the doughnut are perfectly diffraction-limited beams. What makes the difference is the strongly **nonlinear** response of the molecules to the STED light, which turns a smooth, broad intensity profile into a sharp boundary between molecules that can and cannot emit. This is the same lesson we drew from nonlinear SIM in {ref}`Section 9.1 <chap9_1>`. STED is often described as _diffraction-unlimited_ for this reason: the optics are limited, but the resolution is set by how hard we can drive the switch.

## Building a STED microscope

A STED microscope is a confocal laser-scanning microscope ({ref}`Chapter 5 <chap5_1>`) with a second laser added (_{numref}`Fig. {number} <chap9_sted_setup>`_). The excitation and STED beams are combined with dichroic mirrors, focused by the same objective and scanned together across the sample. The fluorescence travels back through the objective, passes the dichroics and a pinhole, and reaches a sensitive point detector, usually an avalanche photodiode (APD) or, increasingly, an array of single-photon avalanche diodes (SPADs).

```{figure} ../figures/chap9_sted_setup.png
---
width: 100%
name: chap9_sted_setup
align: center
---
Simplified STED microscope. A vortex phase plate gives the STED beam a helical phase from 0 to 2π, which makes it focus into a doughnut with a zero at the center (insets, bottom left). Excitation and STED beams are overlapped and scanned across the sample; the fluorescence is separated by dichroic mirrors and detected through a pinhole. The side view at focus (right) shows the doughnut (orange) surrounding the effective PSF (green).
```

The doughnut is produced by a **vortex phase plate**, a transparent plate whose thickness increases like a spiral staircase around its center, so that it delays the beam by a phase that grows from $0$ to $2\pi$ around the optical axis. When this beam is focused, light from opposite sides of the pupil arrives at the focus with opposite phases and interferes destructively. The result is a ring of light with a dark center. For the zero to be truly dark, the STED beam must also be circularly polarized with the correct handedness, a detail that is easy to get wrong and that has a large effect on performance. A second type of phase plate, with a central disk that delays the light by $\pi$, produces a "bottle" beam with zeros above and below the focus, which is used to improve the axial resolution in 3D STED.

Instead of a fixed phase plate, many modern systems use a **spatial light modulator** (SLM), a liquid crystal display that can imprint any phase pattern on the beam. It costs more and loses some light, but it can display the vortex together with corrections for the aberrations of the optics and the sample, shift the doughnut in $x$, $y$ and $z$ to align it with the excitation spot, and switch between 2D and 3D depletion patterns in software.

### Pulsed and continuous STED, and why timing matters

Depletion must happen _after_ excitation and _before_ spontaneous emission. In pulsed STED, a picosecond excitation pulse is followed within a few tens of picoseconds by a longer STED pulse, which depletes the molecules before most of them have had time to fluoresce. Simpler and cheaper systems use a continuous-wave (CW) STED laser instead. In CW STED the depletion acts throughout the excited-state lifetime, so molecules at the edge of the doughnut are not fully switched off but have their fluorescence lifetime shortened. Recording only the photons that arrive after a short delay, a technique called **time-gated detection** (gated STED), rejects those early photons and recovers most of the resolution. This is one of the places where the lifetime concepts of {ref}`Chapter 8 <chap8_3>` meet super-resolution.

## STED in practice

_{numref}`Fig. {number} <chap9_ex_sted_confocal>`_ compares confocal and STED images of the cytoskeleton. Filaments that merge into a single line in the confocal image separate into individual strands with STED, and a line profile across them shows several peaks where the confocal profile shows one broad hump.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_sted_confocal.png
---
width: 100%
name: chap9_ex_sted_confocal
align: center
---
Confocal (left) and STED (right) images of cytoskeletal filaments in a cell. Source: [reference to be added].
```

Because STED is a purely optical technique working with ordinary fluorophores, including fluorescent proteins, it can be applied to living samples, and even to living animals. In a famous experiment, dendritic spines of neurons expressing a yellow fluorescent protein were imaged through a cranial window in the brain of an anesthetized mouse (_{numref}`Fig. {number} <chap9_ex_sted_invivo>`_). The spine necks, which are thinner than 100 nm, were resolved with a width of about 67 nm, and changes in spine shape were followed over tens of minutes.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_sted_invivo.png
---
width: 100%
name: chap9_ex_sted_invivo
align: center
---
STED imaging in the cortex of a living mouse. Dendrites and spines of neurons expressing a yellow fluorescent protein are imaged through a cranial window; time-lapse images show the spines changing shape, and a line profile across a spine neck gives a width of 67 nm. Source: [reference to be added].
```

Since STED scans a point across the sample like a confocal, its speed is similar to confocal microscopy, and in fact usually slower, because the pixels must be smaller to sample the finer resolution (remember the Nyquist criterion). On small fields of view, however, frame rates of tens of images per second have been reached, enough to follow the movement of synaptic vesicles.

## Exploring STED

The widget below lets you change the STED intensity and introduce the two most common imperfections of a real system: some light left in the center of the doughnut, and a misalignment between the doughnut and the excitation spot. The map shows the STED light in units of $I_s$, the plot shows how the effective PSF is built, and the images below compare a confocal and a STED microscope on pairs of lines with decreasing spacing.

:::{raw} html
<iframe src="../content/sted_widget.html" width="100%" height="940px" frameborder="0" style="border: none;"></iframe>
:::

## Where are the problems?

The trick of STED is the **known spectrum, position and shape of the depletion beam**, combined with the known photophysics of the dye. Unlike SIM or the localization methods of the next section, STED needs no reconstruction algorithm: the effective PSF is physically smaller, and the image is formed directly by scanning it across the sample. (Deconvolution can still be applied afterwards, as for any other image.) Its problems come from the parts of the trick that are hard to control.

**Light dose.** The resolution improves only with the _square root_ of the STED intensity, so halving the effective PSF requires roughly four times more power. STED intensities in the focus reach hundreds of MW/cm² or more, orders of magnitude above what is needed for confocal imaging. Although the STED wavelength is red-shifted and is not absorbed much by the fluorophores, every molecule is cycled through many excitation and depletion events, and the intense light can promote excited molecules to higher states from which they bleach. Photobleaching and phototoxicity are therefore the main practical limitation, and the reason STED work relies on particularly photostable dyes.

**The zero.** The depletion of the central molecules depends entirely on how dark the center of the doughnut really is. If a fraction $\varepsilon$ of the maximum intensity remains there, the central molecules are depleted too, by a factor $\exp(-\ln 2\cdot \varepsilon I/I_s)$. With $\varepsilon = 2\%$ and $I/I_s = 100$, three quarters of the signal is lost, and the PSF hardly shrinks further. Aberrations in the optics or in the sample, wrong polarization, or a poorly made phase plate all fill in the zero. This is why aberration correction with SLMs and adaptive optics is so important, especially deep in tissue.

**Alignment.** If the doughnut zero and the excitation spot do not coincide, the effective PSF becomes dimmer and asymmetric, and its center moves. The microscope then assigns photons to the wrong position, producing images that are distorted rather than simply blurred. Because the excitation and depletion beams have different wavelengths, chromatic effects in the objective can also shift their foci relative to each other.

```{tip}
STED belongs to a broader family of methods called RESOLFT (REversible Saturable OpticaL Fluorescence Transitions). Any transition that switches a fluorophore between a bright and a dark state, and that can be saturated by a doughnut-shaped beam, can be used in the same way. With reversibly switchable fluorescent proteins, the switching requires intensities of only W/cm² to kW/cm², a million times less than STED, at the cost of slower switching and therefore slower imaging.
```

## Strengths and limitations

STED improves the resolution by five to ten times over confocal microscopy, works with standard fluorophores and labelling protocols, delivers images directly without computational reconstruction, which makes it quantitative and relatively robust to noise, and is applicable to fixed and living samples, from cells to whole animals. On the other side of the balance are a high light dose with the photobleaching and phototoxicity that come with it, a scanning acquisition that is relatively slow, and a strong sensitivity to aberrations and misalignment, which lead to artifacts.

STED decides deterministically, with light, _where_ a molecule is allowed to emit. The next family of techniques takes a completely different approach: it lets the molecules themselves decide, at random, _when_ to emit.
