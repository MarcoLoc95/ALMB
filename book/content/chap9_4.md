# Localization microscopy

The diffraction limit tells us how close two point sources can be before their images merge. It says nothing about how precisely we can determine the position of a _single_ point source. If we know that a blurry spot on the camera comes from one molecule, and only one, we can find its center far more precisely than the width of the spot. This observation is the foundation of a whole family of techniques collectively called **single-molecule localization microscopy** (SMLM). The best known members are PALM, STORM and PAINT. They differ in how they make molecules light up one at a time, but they share everything else.

## Localizing a single molecule

The image of a single fluorophore on the camera is the PSF, sampled by the pixels and corrupted by noise. Near its peak, an Airy pattern is very well approximated by a two-dimensional Gaussian, so we can fit a Gaussian to the pixel values and take its center as the position of the molecule. The fit does not care that the center falls between pixels: it uses the shape of the whole spot to interpolate a position with sub-pixel accuracy (_{numref}`Fig. {number} <chap9_localization>`_).

How good is this estimate? Each detected photon is a random sample drawn from the PSF, a distribution with standard deviation $s$ (roughly 100 nm for visible light and a high-NA objective). Estimating the center of a distribution from $N$ independent samples is a classic statistics problem: the uncertainty of the mean, the _standard error of the mean_, is

$$
\sigma_{loc} = \frac{s}{\sqrt{N}}
$$

This is the **localization precision**. It does not depend on the wavelength alone, but on the ratio between the PSF width and the square root of the number of collected photons. A molecule that delivers 1000 photons can be localized with a precision of about 3 nm, almost a hundred times smaller than the PSF.

```{figure} ../figures/chap9_localization.png
---
width: 100%
name: chap9_localization
align: center
---
Localizing a single molecule. Left: the image of one molecule on a camera with 100 nm pixels; the fitted center (orange cross) lies within a few nanometers of the true position (blue). Middle: repeating the experiment gives a cloud of estimates whose spread shrinks as more photons are collected. Right: the precision of simulated maximum-likelihood fits follows the $1/\sqrt{N}$ law. Pixelation and background make it slightly worse than the ideal $s/\sqrt{N}$, as predicted by the formula of Thompson and colleagues (solid line).
```

In real experiments the precision is somewhat worse than this ideal. Pixels of size $a$ add uncertainty about where in the pixel each photon landed, and the background $b$ (photons per pixel from out-of-focus light, autofluorescence and camera noise) adds random counts that have nothing to do with the molecule. A widely used approximation, due to Thompson and colleagues, is:

$$
\sigma_{loc}^2 = \frac{s^2 + a^2/12}{N} + \frac{8\pi s^4 b^2}{a^2 N^2}
$$

The first term is our ideal result corrected for pixel size; the second term shows that background becomes dominant when the molecule is dim. In practice, typical SMLM experiments achieve localization precisions of 5-20 nm.

```{tip}
Localization requires that you know each spot comes from exactly one molecule. Finding the spots in a noisy frame is called **detection**; finding their centers is **localization**. Detection asks _is there a molecule?_, localization asks _where exactly is it?_ Errors in the first step (two overlapping molecules detected as one, or noise detected as a molecule) produce localizations that look perfectly precise and are completely wrong.
```

## Sparse in space, separated in time

A labelled cell contains thousands of fluorophores per square micrometer. If they all emit at once, their PSFs overlap and we cannot localize anything. The essential trick of SMLM is to make the fluorophores **blink**: at any moment, only a small random subset is in a fluorescent "on" state, sparse enough that each diffraction-limited region contains at most one emitting molecule. We record a frame, localize every isolated spot, let those molecules switch off, and record the next frame with a new random subset. After thousands to tens of thousands of frames, nearly every molecule has been localized at least once, and plotting all localizations together produces the super-resolved image (_{numref}`Fig. {number} <chap9_smlm_blinking>`_).

```{figure} ../figures/chap9_smlm_blinking.gif
---
width: 100%
name: chap9_smlm_blinking
align: center
---
Principle of single-molecule localization microscopy. In each camera frame a few molecules emit (left; crosses mark the true positions). Summing all frames gives an ordinary diffraction-limited image (middle). Localizing each molecule frame by frame and plotting all localizations builds up a super-resolved map (right).
```

How sparse is sparse enough? If a diffraction-limited area of about $0.1\ \mu m^2$ contains $n$ labels, each label may spend at most about $1/n$ of its time in the on state, otherwise two neighbors will often be on at the same time. For a densely labelled microtubule with hundreds of labels per diffraction-limited area, the fraction of time a fluorophore is on, its **duty cycle**, must be well below one percent. Controlling this duty cycle is exactly what PALM, STORM and PAINT do, each with a different mechanism (_{numref}`Fig. {number} <chap9_switching>`_).

```{figure} ../figures/chap9_switching.png
---
width: 100%
name: chap9_switching
align: center
---
Three ways to make molecules blink. In PALM, photoactivatable or photoconvertible fluorescent proteins are switched irreversibly by violet light. In STORM, organic dyes are pushed into long-lived dark states by a chemical buffer and return stochastically. In DNA-PAINT, short fluorescent DNA strands bind transiently to complementary docking strands on the target and are only localized while bound.
```

## PALM: switching on with light

**PhotoActivated Localization Microscopy** (PALM), published by Eric Betzig, Harald Hess and colleagues in 2006 (and at the same time, under the name FPALM, by Samuel Hess and colleagues), uses fluorescent proteins whose properties change when they absorb violet light, typically at 405 nm. **Photoactivatable** proteins such as PA-GFP are dark until activated, after which they fluoresce normally under blue excitation. **Photoconvertible** proteins such as mEos or Dendra2 fluoresce green before activation and red after it, so imaging in the red channel sees only converted molecules. Both changes involve a chemical modification of the chromophore (recall the chromophore chemistry from {ref}`Chapter 4 <chap4_2>`) and are irreversible.

A PALM experiment cycles through three steps. A very weak violet pulse activates a few random molecules; the readout laser excites them until they bleach, while the camera records them; the activation is repeated to create a new subset. The strength of the activation light sets how many molecules are on at once. Because each molecule is activated and bleached essentially once, PALM is well suited for _counting_ molecules, although real fluorescent proteins blink a little before bleaching, and this must be corrected to avoid overcounting.

Since fluorescent proteins are genetically encoded, PALM labels its targets with perfect specificity and with a small linkage error, and it can be used in living cells. Two-color PALM revealed how actin and the adhesion protein paxillin are organized in focal adhesions (_{numref}`Fig. {number} <chap9_ex_palm_adhesions>`_), and live-cell PALM followed the slow remodeling of adhesion complexes over minutes, with a time resolution of tens of seconds per super-resolved frame.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_palm_adhesions.png
---
width: 90%
name: chap9_ex_palm_adhesions
align: center
---
Two-color PALM of actin (green) and paxillin (red) in focal adhesions. The enlarged region (right) shows the two proteins organized in distinct but interleaved nanoscale structures. Source: ZEISS Microscopy Online Campus.
```

## STORM: switching off with chemistry

**STochastic Optical Reconstruction Microscopy** (STORM), introduced by Xiaowei Zhuang's lab in 2006, achieves blinking with small organic dyes and a special buffer. The original version used pairs of cyanine dyes placed close together, an *activator* such as Cy3 and a *reporter* such as Cy5: red light drives the reporter into a dark state, and light absorbed by the activator switches it back on. Changing the activator changes the colour of light that switches the reporter on, which is how the multicolor images of {numref}`chap9-ex-storm-clathrin` were made. Two years later, Mike Heilemann, Markus Sauer and colleagues showed that a single conventional dye in the right buffer blinks by itself, without an activator. This simpler variant, called direct STORM (dSTORM), is now the most widely used form, and it relies on the dark states we introduced in Chapter 4. An excited dye can cross into its triplet state, and from there react with the buffer to form a radical or reduced form that does not absorb at the excitation wavelength. In this dark state the dye can survive for milliseconds to minutes before returning to the ground state, from which it can fluoresce again ({numref}`chap9-storm-jablonski`). Intersystem crossing is a property of the dye and is rare: in almost every excitation cycle the molecule simply fluoresces. But under the intense illumination used in STORM each molecule is excited thousands of times per millisecond, so the rare detour into the triplet state, and from there into the long-lived dark state, happens within milliseconds. Since the way back takes seconds, each molecule spends most of its time dark, and only a sparse subset emits at any moment.

```{figure} ../figures/chap9_storm_jablonski.png
---
width: 85%
name: chap9_storm_jablonski
align: center
---
Photophysics of STORM blinking. From time to time an excited dye crosses into its triplet state $T_1$, where the thiol in the buffer reduces it to a radical and then to a fully reduced form. Neither absorbs the excitation light, so the molecule is dark for milliseconds to minutes, until oxygen (or violet light) returns it to the ground state. Removing oxygen with the GLOX system prolongs the dark states. The scheme follows the model proposed for rhodamine and oxazine dyes; cyanines such as Alexa Fluor 647 reach a similar dark state by binding the thiol.
```

Two components of the buffer control this cycle. A **thiol**, a reducing agent such as mercaptoethylamine (MEA) or β-mercaptoethanol, reacts with the triplet dye and stabilizes the dark, reduced state. An **oxygen-scavenging system** removes dissolved oxygen, which would otherwise quickly bring the dye back to the ground state and also cause photobleaching. A common choice is the GLOX system, in which the enzyme glucose oxidase consumes oxygen by oxidizing glucose,

$$
\text{glucose} + \mathrm{O_2} \longrightarrow \text{gluconolactone} + \mathrm{H_2O_2}
$$

and catalase removes the hydrogen peroxide produced:

$$
2\,\mathrm{H_2O_2} \longrightarrow 2\,\mathrm{H_2O} + \mathrm{O_2}
$$

Under intense red illumination (several kW/cm²) almost all dye molecules are rapidly driven into the dark state, and only a sparse, random subset returns at any moment. Violet light can be added to speed up the return when too few molecules remain active. The result is that each dye blinks many times before it finally bleaches.

Alexa Fluor 647 and related cyanine dyes blink so well that they have become the workhorses of STORM. Multicolor STORM resolved clathrin-coated pits as hollow spheres alongside individual microtubules (_{numref}`Fig. {number} <chap9_ex_storm_clathrin>`_), and 3D STORM revealed an unexpected periodic organization of the cytoskeleton in axons, where actin rings wrap around the axon every 190 nm, connected by spectrin (_{numref}`Fig. {number} <chap9_ex_storm_axon>`_). This structure had escaped decades of electron microscopy and was found by super-resolution.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_storm_clathrin.png
---
width: 90%
name: chap9_ex_storm_clathrin
align: center
---
Two-color STORM of clathrin (red) and microtubules (green). In the conventional image (left) clathrin-coated pits appear as blobs; in the STORM images they are resolved as rings, the projections of hollow spherical cages. Source: Bates et al. (2007), via Science.
```

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_storm_axon.png
---
width: 60%
name: chap9_ex_storm_axon
align: center
---
3D STORM images of βII-spectrin, βIV-spectrin and adducin in axons, color-coded by height. All three proteins follow a periodic pattern along the axon. Source: Xu et al. (2013), via Science.
```

The price of STORM is its buffer. The reducing agents, the absence of oxygen and the intense illumination are harmful to living cells, so STORM is used almost exclusively on fixed samples.

## PAINT: switching by binding

The third approach does not switch the fluorophores at all. In **Point Accumulation for Imaging in Nanoscale Topography** (PAINT), the fluorescent probes float freely in the solution and only become visible when they bind to the target. A diffusing molecule moves across many pixels during one camera exposure and is smeared into a faint background, while a bound molecule stays put and appears as a sharp spot. The first PAINT experiments used a dye that becomes fluorescent when it inserts into lipid membranes.

The version that has taken over is **DNA-PAINT**, developed by Ralf Jungmann and colleagues. The target is labelled with a short single-stranded DNA sequence, the **docking strand**, typically 8-10 nucleotides long. The buffer contains a low concentration of complementary **imager strands**, each carrying a dye. An imager binds to a docking strand for a fraction of a second to a few seconds, then unbinds and diffuses away. The binding duration is set by the length and sequence of the DNA, and the frequency of binding events by the imager concentration, so the blinking kinetics can be tuned almost at will, independently of the dye photophysics.

This decoupling brings remarkable advantages. Bleaching hardly matters, because a bleached imager is replaced by a fresh one from the solution. The same site can be visited hundreds of times, and each visit can be long and bright, so DNA-PAINT routinely reaches localization precisions of a few nanometers. And because the imagers differ only in their DNA sequence, several targets can be imaged one after the other with the same dye, by washing out one imager and adding the next (Exchange-PAINT), with dozens of targets in principle. On the labelling side, the docking strand can be attached to antibodies, but also to much smaller binders such as nanobodies, affimers or aptamers, and to peptides that are genetically encoded in living cells. Since label size matters more and more as precision improves, this flexibility is a major reason for the popularity of DNA-PAINT.

The drawback is speed. Binding events are rare and slow, so a DNA-PAINT image can take tens of minutes to hours. The freely diffusing imagers also produce background, which is why DNA-PAINT is usually combined with TIRF or highly inclined illumination ({ref}`Chapter 5 <chap5_2>`), although with careful design it can also image deeper planes inside cells (_{numref}`Fig. {number} <chap9_ex_paint_cells>`_).

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_paint_cells.png
---
width: 80%
name: chap9_ex_paint_cells
align: center
---
DNA-PAINT images of cells acquired at different depths above the coverslip. The sketch at the top indicates the position of the detection volume. Source: Schueder et al. (2017), CC BY, via Nature Communications.
```

## From localizations to an image

Whatever the switching mechanism, the raw output of an SMLM experiment is not an image but a table: a list of millions of localizations, each with coordinates, photon count, background and estimated precision. To display it, the localizations are rendered, for instance by counting them in small pixels (a 2D histogram) or by drawing each one as a small Gaussian whose width is its precision. Several corrections are applied along the way. Over the minutes of an acquisition the stage drifts by tens of nanometers, so the drift is measured with fiducial markers such as fluorescent beads, or by cross-correlating images reconstructed from successive blocks of frames, and subtracted. Localizations with too few photons or with abnormal shapes, which are likely to come from overlapping molecules, are filtered out. The final resolution can then be estimated with Fourier ring correlation ({ref}`Chapter 6 <chap6_3>`), by splitting the localizations into two halves and comparing them.

Three-dimensional SMLM is possible by making the PSF shape depend on depth. The simplest method places a weak cylindrical lens in the detection path, so that the spot becomes elongated horizontally above the focus and vertically below it; the ellipticity of each spot then encodes its axial position over a range of about a micrometer.

## Precision is not resolution

A localization precision of 5 nm does not mean that the image has a resolution of 5 nm. At least three other factors intervene.

The first is **labelling density**. To see a structure, it must be sampled finely enough. By an argument analogous to the Nyquist sampling theorem, the average distance between localized labels must be at most half the size of the smallest feature we want to resolve. A ring that carries only a few labels will look like a few dots, however precisely each dot is localized.

The second is **label size**, the linkage error we discussed in {ref}`Section 9.2 <chap9_2>`. With primary and secondary antibodies, the dyes sit up to about 20 nm from the protein. A microtubule, a tube 25 nm in diameter, therefore appears in antibody-based SMLM images as a hollow tube about twice as wide: an accurate image of the antibody cloud, not of the microtubule.

The third is the **stability of the sample** during the acquisition. SMLM assumes that the molecules do not move between the first and the last frame. Residual drift, sample deformation or, in living cells, the motion of the structures themselves, blur the reconstruction and set the actual resolution, regardless of the precision of each localization.

## Exploring SMLM

The widget below simulates an SMLM experiment on a field of filaments and rings. Choose the photons per localization, the background, the number of molecules on per frame, the number of frames, the labelling density and the drift, then press Measure: the acquisition runs frame by frame, showing the camera frames with their localizations, the blinking signal in one pixel, the widefield sum and the localization map as it builds up. Localizations that come from overlapping molecules are tinted orange: in a real experiment, of course, nothing would tell you which ones they are.

:::{raw} html
<iframe src="../content/smlm_widget.html" width="100%" height="790px" frameborder="0" style="border: none;"></iframe>
:::

## Strengths and limitations

The trick of all SMLM methods is the same: **sparse molecules that do not move (much)**, combined with a localization and reconstruction algorithm. If the molecules are not sparse, overlapping spots are fitted as single molecules at wrong positions; if they move, the image is a blurred average.

In exchange, SMLM offers single-molecule sensitivity, nanometer localization precision, and quantitative data that can be analyzed statistically, molecule by molecule: distances, cluster sizes, molecular counts. It is compatible with many labelling strategies, supports multicolor imaging (particularly with DNA-PAINT), and the instrumentation is relatively simple: a widefield or TIRF microscope with good lasers, a sensitive camera and a stable stage.

The limitations are equally characteristic. Acquisitions take minutes to hours, so the temporal resolution is poor. The long and intense illumination causes photobleaching and phototoxicity. Sample preparation, especially the STORM buffers and the PAINT labelling, is delicate and can vary from batch to batch. Artifacts and localization errors are common when density, drift or background are not under control, and live-cell imaging is possible only in limited cases, mostly with PALM and some forms of PAINT. Finally, it bears repeating that an SMLM image is not a picture of the sample but a map of estimated positions, as good as the assumptions that went into it.

Notice also that the precision of SMLM is ultimately limited by the number of photons a molecule can emit before it bleaches, because each photon carries only a little information about the position of the molecule. Most photons land near the peak of the PSF, where the intensity barely changes with position. Is there a smarter way to use photons? That question leads to the last section of this chapter.
