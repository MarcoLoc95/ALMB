(chap8_1)=
# 8.1 - Lattice light-sheet microscopy

Chapter 5.3 left us with a problem and a promise. The problem: a Gaussian light sheet can be thin or long, but not both, because its usable length grows only with the square of its thickness. The promise: Bessel beams break that trade-off, at the price of side lobes that excite fluorophores away from the focal plane, and a periodic arrangement of Bessel beams can make those side lobes cancel. That arrangement is the _lattice_, and this section is about how it works and what it has made possible.

We will not repeat the axicon picture of Chapter 5.3. Instead we will look at the same beams from the back focal plane, because that is where the lattice is actually designed, and because Chapter 6 has given us exactly the tools to do it.

## Thinking in the pupil

Recall from Chapter 6.3 that the field in the back focal plane of a lens and the field at its focus are a Fourier pair. Read in the forward direction, this gives a very physical rule: _every point in the pupil becomes a plane wave at the focus_, travelling at an angle $\theta$ set by how far that point is from the centre. Light near the centre of the pupil becomes waves travelling almost along the axis; light near the edge becomes the steepest waves the objective can deliver, with $n\sin\theta$ equal to the numerical aperture.

A focused spot, a Gaussian sheet, a Bessel beam and a lattice are then simply four different ways of lighting the pupil:

- a filled disc gives waves at every angle up to the maximum, which pile up into a tight, short focus;
- a thin ring gives waves that all travel at the _same_ angle to the axis, which is precisely what the axicon of Chapter 5.3 produces;
- a few isolated points on that ring give a handful of plane waves, which interfere into a periodic pattern: the lattice.

The animation below makes the first two cases concrete. It is a full diffraction calculation, not a cartoon. On the left is the light entering the back focal plane: it starts as a filled disc and is progressively narrowed into a thin ring, always with the same outer edge (NA 0.55). In the middle is the beam this produces, seen from the side. On the right is the same beam seen end-on, as a cross-section through the focus.

```{figure} ../figures/chap8_annulus_sweep.gif
---
width: 100%
name: chap8_annulus_sweep
align: center
---
From a filled pupil to a thin ring. Left: the light entering the back focal plane. Middle: the beam near the focus seen from the side, with its length marked (488 nm light in water; the vertical axis is stretched relative to the horizontal one). Right: the beam seen end-on at the focus. As the ring narrows, the beam grows from 3.5 μm to nearly 50 μm long while its central spot barely changes, but the share of the light in the side rings rises from 15% to over 90%.
```

Three things are worth reading off _{numref}`Fig. {number} <chap8_annulus_sweep>`_.

First, the size of the central spot, in the end view, hardly changes. It is set almost entirely by the _outer_ edge of the ring, which never moves: the steepest waves determine the finest interference fringe, so the core width tracks the maximum NA.

Second, the length of the beam, in the side view, is set by the _width_ of the ring. That is where the trade-off of Chapter 5.3 comes from, seen now from the other side. Two plane waves travelling at slightly different angles have slightly different speeds along the axis, so they slowly drift out of step. The narrower the range of angles, the longer they stay in step, and the longer the beam. In the limit of an infinitely thin ring every wave has the same axial speed, they never drift apart, and the beam is infinitely long: the ideal Bessel beam.

Third, and this is the uncomfortable part, the side lobes are not a separate defect that happens to accompany long beams. They are the _same_ phenomenon. With a filled pupil, about 85% of the light sits in the central spot, which you may recognise as the Airy disk of Chapter 3.2. As the ring narrows, the end view turns into a bullseye and the light drains steadily into the rings. You cannot have the length without the lobes, at least not with a single beam.

```{tip}
**Worked example: predicting the length of a beam from its pupil.**

A plane wave at angle $\theta$ to the axis has an axial wavevector $k_y = (2\pi n/\lambda_0)\cos\theta$. Two waves at the extreme angles of the annulus drift a full cycle out of step over a distance

$$ L \approx \frac{\lambda_0}{n\,(\cos\theta_{\min} - \cos\theta_{\max})}, \qquad n\sin\theta = \mathrm{NA}. $$

For 488 nm light in water with an annulus from NA 0.53 to 0.55: $\cos\theta_{\min} = 0.917$, $\cos\theta_{\max} = 0.911$, so $L \approx 0.488\ \mu\text{m}/(1.33 \times 0.0067) \approx 55$ μm. The full calculation in _{numref}`Fig. {number} <chap8_annulus_sweep>`_ gives 48 μm. For a filled pupil up to NA 0.55, the same formula gives about 4 μm, against 3.5 μm calculated.

One line of trigonometry, and you can design a light sheet. Notice the denominator: the length depends on a _difference_ of cosines, which for a thin ring is a very small number. That is why small changes in the annulus width have such a large effect on the beam.
```

## Interference to the rescue

If one Bessel beam wastes most of its power in rings, the idea behind the lattice is to make several Bessel beams share that power, arranged so that their rings interfere destructively between the cores and constructively at them.

In the sample this looks like a row of Bessel beams placed side by side. Because they come from the same laser they are mutually coherent, so where their side lobes overlap, the fields add with signs that depend on the spacing. At the right spacing, the lobes between the beams are largely cancelled and the energy is pushed back into the central plane, as _{numref}`Fig. {number} <chap8_lattice_interference>`_ shows.

```{figure} ../figures/chap8_lattice_interference.gif
---
width: 75%
name: chap8_lattice_interference
align: center
---
A row of mutually coherent Bessel beams brought progressively closer together. Top: the cross-section through the row. Bottom: the full two-dimensional pattern. As the spacing changes, the interference reinforces the peaks and suppresses the ring structure between them.
```

In the pupil, the same thing is achieved by lighting the ring not all the way around but at a few chosen points. A handful of plane waves at the same angle to the axis keeps the non-diffracting property of the Bessel beam, because they all share the same axial speed, while their limited number confines the interference pattern to a regular grid of peaks. This is why the lattice is designed in the back focal plane: you choose which points of the ring to light, and the pattern in the sample follows.

A lattice is still a set of bright points rather than a sheet. Turning it into a uniform sheet of illumination takes one more step, and here the lattice has a decisive advantage over a single beam.

A single beam has to be _scanned_ across the whole field of view during each camera exposure, so that the time-averaged illumination is a sheet. A lattice only has to be _dithered_: moved back and forth over the distance between two neighbouring peaks, which is under a micrometre. Because the galvanometric mirror (Chapter 7.1) only has to travel a tiny distance, it can do so at kilohertz rates, and every point of the sheet is illuminated many times during a single exposure. _{numref}`Fig. {number} <chap8_scanning_vs_dithering>`_ compares the two strategies.

```{figure} ../figures/chap8_scanning_vs_dithering.gif
---
width: 85%
name: chap8_scanning_vs_dithering
align: center
---
Top row: instantaneous illumination. Bottom row: the time average seen by the camera. A scanned Gaussian spot (left) sweeps a long line; a dithered Gaussian spot (centre) covers a short one; a dithered lattice of eleven Bessel beams (right) illuminates the whole field at once while moving only by the spacing between neighbouring peaks.
```

The result is compared with the alternatives in _{numref}`Fig. {number} <chap8_lattice_psf>`_. A dithered lattice is not quite as tightly confined as an ideal single Bessel core, but it beats a Gaussian sheet comfortably and, crucially, without the halo of side-lobe excitation that a swept Bessel beam leaves behind.

```{figure} ../figures/chap8_lattice_psf_chen2014.png
---
width: 60%
name: chap8_lattice_psf
align: center
---
Instantaneous intensity at the sample, the swept or dithered intensity, and the resulting overall point spread function, for a Gaussian beam, a Bessel beam and a square lattice. Copyright: Chen et al. (2014), via Science.
```

## Reading the instrument

With the pupil picture in hand, the optical layout in _{numref}`Fig. {number} <chap8_llsm_schematic>`_ reads almost like a sentence. Following the approach of Chapter 7.2, trace the light and ask what each element is for.

```{figure} ../figures/chap8_llsm_schematic.png
---
width: 95%
name: chap8_llsm_schematic
align: center
---
Simplified optical layout of a lattice light-sheet microscope. The excitation beam (orange) is expanded into a stripe, patterned by the SLM and filtered by the annular mask, so that only a ring of light, seen here in cross-section as two bands, travels on to the excitation objective. The objective turns that ring into light arriving at a shallow angle from all sides, which overlaps over an extended length to form the sheet. Fluorescence (green) is collected at right angles and focused onto the camera. The drawing is unfolded and simplified: the SLM is a reflective device, the galvo unit contains two mirrors with relay optics between them, and in the real instrument both objectives are tilted and dip into a shared bath of medium.
```

The beam from a set of continuous-wave lasers is first reshaped by cylindrical lenses into a thin stripe, which illuminates a narrow band across a spatial light modulator. The SLM in the original instrument is a binary ferroelectric device, each pixel imposing either no phase shift or a phase shift of $\pi$, and the pattern written on it is the lattice to be projected into the sample. Because the SLM sits in a plane conjugate to the sample, a thin stripe on the SLM becomes a lattice confined to a thin slab in the sample.

The next lens is the important one. It performs the Fourier transform of Chapter 6, so in its back focal plane the light from the SLM is spread out according to angle: each diffraction order of the SLM pattern arrives at a different point. An opaque mask with a transparent annulus sits exactly there. It passes only the components lying on the ring, discarding the unwanted orders that a binary SLM inevitably produces and fixing the minimum and maximum NA of the illumination, which, as we just saw, fix the length and thickness of the sheet. This is spatial filtering in the back focal plane, the same idea met in Chapter 6, used here as a routine piece of engineering.

From there, relay lenses carry the filtered pattern to galvanometric mirrors that dither the lattice in $x$ and step it in $z$, and a final mirror turns the beam down into the excitation objective, which points at the sample from above. The relays and their conjugation of the mirrors to the objective pupil are there for exactly the reasons given in the scan lens tip of Chapter 7.1. The detection arm is a perfectly ordinary widefield path: a high-NA objective at right angles to the excitation, a tube lens, an emission filter and an sCMOS camera. Because the sheet travels downwards and is thin in the direction the detection objective looks along, it appears in the schematic as a narrow vertical stripe.

The SLM has one further advantage over a fixed axicon: the pattern can be changed in software. Switching between a single Bessel beam, a square lattice, a hexagonal lattice or a Gaussian sheet is a matter of loading a different image.

## Two ways of using the lattice

In its **dithered mode**, the one described so far, the lattice is smeared into a uniform sheet and the instrument behaves as an exceptionally thin, exceptionally gentle light-sheet microscope. The original report quoted a resolution of roughly 230 nm laterally and 370 nm axially in this mode, at hundreds of planes per second.

In its **structured illumination mode**, the lattice is not smeared out. It is stepped through several positions, an image is recorded at each, and the images are combined computationally to recover detail finer than the diffraction limit. This is the principle of structured illumination microscopy, which belongs to Chapter 9, and it costs speed and photons. In practice the dithered mode is what most lattice light-sheet experiments use.

## Summary

- **Advantages**: photobleaching and phototoxicity low enough that living cells can be imaged in three dimensions for hours, with fluorescent proteins in some cases bleaching more slowly than the cell replaces them; resolution close to the diffraction limit in all three directions, with axial resolution far better than any Gaussian light sheet; speed high enough for genuine four-dimensional imaging, because dithering is fast and every plane is recorded in a single camera exposure; a sheet that is reconfigurable in software.
- **Drawbacks**: alignment is demanding and in practice repeated before every session; illumination is still one-photon, so scattering limits imaging to cells, small clusters and thin tissue rather than millimetre-thick samples; mounting between two closely spaced objectives is specialised; the instrument is complex and expensive.

The applications that made the technique famous all share one feature: they are fast, three-dimensional processes in living cells that would not survive a confocal microscope. Filopodia extending and retracting from the surface of a HeLa cell, followed as full volumes for many minutes. A neutrophil-like HL-60 cell migrating through a three-dimensional collagen matrix, which is far closer to the mechanical environment of real tissue than a glass coverslip. The immunological synapse between a T cell and an antigen-presenting cell in two colours, with actin flowing towards and away from the contact as the T cell decides whether to respond. And a _C. elegans_ embryo shortly before hatching, imaged in a single plane at the maximum frame rate of the camera, resolving individual muscle contractions and, minutes later, the larva levering itself out of the eggshell.

Two developments since the original instrument are worth knowing about. Adding adaptive optics, with the deformable mirrors and SLMs of Chapter 7.1 correcting the aberrations introduced by the sample, has extended lattice light-sheet imaging into living zebrafish embryos and other multicellular specimens. And commercial instruments now exist, including designs that image through a standard coverslip, which removes much of the burden of sample mounting.

Lattice light-sheet microscopy is, in a sense, the most refined answer this book gives to the question of making better images. The next section stops asking for images altogether.
