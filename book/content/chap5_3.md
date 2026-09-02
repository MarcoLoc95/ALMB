(chap5_3)=
# Light-sheet microscopy

## The photon budget of an embryo

Consider what a confocal microscope does to a specimen over the course of a $z$-stack. To record plane 1, it illuminates the entire depth. To record plane 2, it illuminates the entire depth again. After fifty planes, every fluorophore in the specimen has been excited fifty times, and forty-nine of those excitations produced light that was thrown away at the pinhole.

For a fixed sample this is merely wasteful. For a living one it is often fatal. A zebrafish embryo imaged every thirty seconds for twenty-four hours needs about three thousand stacks. At fifty planes each, that is 150 000 full-depth illuminations of a developing animal. Long before you get there, the fluorophores have bleached and the embryo has stopped developing normally, because the light itself is toxic: excited fluorophores generate reactive oxygen species, and doing so a hundred thousand times has consequences.

The realisation that fixes this is almost embarrassingly simple. The confocal pinhole is on the detection side, and by the time light reaches it the damage has been done. Move the selectivity to the *illumination* side, and the problem disappears rather than being cleaned up afterwards.

## One plane at a time, from the side

**Light-sheet microscopy**, also called **selective plane illumination microscopy** (SPIM), uses two objectives at right angles. One illuminates the specimen with a thin sheet of light lying exactly in the focal plane of the other, which collects the fluorescence and forms an image on a camera (_{numref}`Fig. {number} <chap5_lightsheet_geometry>`_).

```{figure} ../figures/chap5_lightsheet_geometry.png
---
width: 90%
name: chap5_lightsheet_geometry
align: center
---
The light-sheet geometry, seen edge on. A thin sheet of light enters from the side and illuminates one plane of a three-dimensional specimen. A second objective at right angles images that plane onto a camera, and the resulting image is drawn at the top: only the fluorophores inside the sheet appear in it, and everything above and below stays dark because it was never excited in the first place. The sheet is a focused Gaussian beam, so it is thinnest at the waist and spreads on either side, which is what limits the usable field of view.
```

Every property of the technique follows from this one arrangement.

Because only the imaged plane is illuminated, **out-of-focus fluorescence is never generated**. There is nothing to reject, so no pinhole is needed and no signal is discarded.

Because nothing outside the plane is excited, **photobleaching and phototoxicity drop by orders of magnitude**. Over a full stack, each fluorophore is excited once rather than once per plane. This is the reason light-sheet microscopy exists, and the reason developmental biology was transformed by it.

Because there is no pinhole, **detection is widefield**: the whole plane is recorded at once on a camera. Light-sheet microscopy is therefore as fast as widefield imaging, hundreds of frames per second, while still sectioning.

Because sectioning comes from the illumination rather than the detection, **the detection objective does not need a high numerical aperture**. It can be a long-working-distance, moderate-NA lens that reaches deep into a large specimen, which is exactly what you want for an embryo or a cleared brain.

```{tip}
The idea is much older than it looks. In 1903 **Henry Siedentopf** and **Richard Zsigmondy** built the _ultramicroscope_ at Zeiss: they illuminated a colloidal suspension with a thin sheet of sunlight through a slit and observed it from the side, making individual gold particles far below the resolution limit visible as points of scattered light. Zsigmondy received the 1925 Nobel Prize in Chemistry for the colloid work this made possible. The optical arrangement then sat unused in microscopy for most of a century. It returned for fluorescence in 1993 with Voie's imaging of the cochlea, was approached independently from the confocal side by Stelzer and Lindek, and reached the modern form in 2004, when Huisken and colleagues in Stelzer's group published SPIM in _Science_ and used it to follow the development of a Medaka embryo.
```

## Making the sheet, and the price of making it thin

There are two common ways to produce the sheet.

The first is a **cylindrical lens**. Picture the biconvex lens you have been drawing since {ref}`Chapter 2 <chap2_1>`, then imagine extruding that cross-section sideways so that the lens becomes a long bar, curved in one direction and perfectly flat in the other. Light entering it is focused in the curved direction and passes straight through in the flat one, so a round beam is squeezed into a line at the focus. Around that line the beam is a flat, converging then diverging blade of light, and that blade is the sheet. It is simple and cheap, and typically gives sheets 5 to 10 µm thick.

The second is a **scanned pencil beam**: sweep an ordinary focused beam rapidly across the field, so that over a single camera exposure the specimen has effectively seen a sheet. This is digitally scanned light-sheet microscopy (DSLM), and it gives a more uniform sheet and independent control of the illumination in each direction.

A complete instrument is then short enough to list in one breath. Laser, a beam expander to fill the optics, a scanning mirror to translate the sheet up and down in $z$, the cylindrical lens, and an illumination objective that projects the sheet into the specimen. At right angles: the detection objective, an emission filter to reject the scattered laser light, a tube lens, and a camera. There is nothing conceptually harder than the widefield microscope of {ref}`Chapter 4 <chap4_1>`; the whole trick is the right angle.

Either way, the sheet is a focused laser beam, and focused laser beams obey a rule that limits everything. A Gaussian beam focused to a waist radius $w_0$ stays approximately that narrow only over its **Rayleigh range**

$$
z_R = \frac{\pi n w_0^2}{\lambda}
$$

on each side of the waist, after which it spreads. The sheet thickness is $2w_0$ and the usable field of view is about $2z_R$. The quadratic relation is the whole story: halve the thickness and the usable field shrinks by a factor of four (_{numref}`Fig. {number} <chap5_lightsheet_tradeoff>`_).

```{figure} ../figures/chap5_lightsheet_tradeoff.png
---
width: 100%
name: chap5_lightsheet_tradeoff
align: center
---
The field of view over which a Gaussian light sheet stays thin, as a function of its thickness, for three wavelengths in water. The relation is quadratic, so thin sheets are thin only over a short distance: halving the thickness shortens the usable field by a factor of four. The three marked points are for 561 nm, a typical excitation line, and read as blunt design rules: a 2 µm sheet is usable across a single cell, a 5 µm sheet across a small organoid, and an 8 µm sheet across an embryo.
```

```{tip}
**Worked example.** At 488 nm in water ($n$ = 1.33):

- A 2 µm sheet ($w_0$ = 1 µm) stays thin over only 17 µm. Good enough for a single cell.
- A 5 µm sheet ($w_0$ = 2.5 µm) stays thin over 107 µm, which covers a zebrafish embryo.

You cannot have both. If you need a thin sheet across a wide field, the standard answer is to scan the waist across the field and stitch, or to accept a thicker sheet at the edges.
```

This is also where the axial resolution of a light-sheet microscope comes from, and it is worth being blunt about it. The optical section is set by whichever is worse, the sheet thickness or the axial extent of the detection point spread function. With a moderate-NA detection objective the latter is 1 to 2 µm, and typical sheets are thicker than that. In most practical light-sheet microscopes, the sectioning is set by the illumination and is several micrometres. Light-sheet microscopy wins decisively on speed, gentleness and depth. It does not generally beat a good confocal on section thickness.

## Bessel beams, lattices, and stripes

Two problems recur often enough to have standard solutions.

The first is the thickness-versus-field trade-off we just derived, which applies to Gaussian beams. There exist beams that do not diffract: the **Bessel beam**, produced by sending a collimated beam through a conical lens called an **axicon**, has a narrow central core whose width is independent of propagation distance. Using one gives a sheet 1 to 2 µm thick over a large field, breaking the trade-off.

It breaks it by cheating. A Bessel beam carries a large fraction of its energy in concentric side lobes surrounding the core, and those side lobes are perfectly capable of exciting fluorophores several micrometres away from the plane being imaged. You get a thin core and a fat halo of out-of-plane background, which is much of what you were trying to avoid. The fixes are ingenious: excite the side lobes two-photon so their lower intensity suppresses them (see {ref}`Chapter 5.4 <chap5_4>`), subtract them with structured illumination, or arrange many Bessel beams in a periodic pattern whose side lobes interfere destructively. That last approach is **lattice light-sheet microscopy**, introduced by Betzig's group in 2014, and it produces the thinnest sheets in routine use.

The second problem is **shadowing**, and it is the one to remember, because the Bessel beam turns out to solve it almost incidentally. Illumination enters from one side, so any strongly absorbing or scattering object in the specimen casts a shadow across everything behind it. The result is an image striped with dark bands running in the direction of illumination, which is not subtle, is easy to mistake for biology, and cannot be repaired afterwards because the fluorophores in the stripe were never excited.

A Gaussian beam has no defence against this. Block part of it and that part stays blocked. A Bessel beam does, and the reason is the geometry that produces it. The axicon sends light towards the axis from all around, at a fixed angle, so the core at any given point along the beam is not a continuation of the core just before it: it is being rebuilt continuously from rays arriving obliquely from the sides. Obstruct the core and those oblique rays keep arriving and reconstruct it a short distance downstream. This is called **self-reconstruction** or self-healing, and in a light sheet it means the beam closes back up behind a scatterer and carries on illuminating. Side by side, a Gaussian sheet and a Bessel sheet of the same specimen differ exactly as you would expect: dark stripes in one, none in the other.

Two blunter remedies exist and are used constantly, often alongside the above: illuminate from both sides alternately and merge the two images, or pivot the beam through a small range of angles during the exposure so that shadows are smeared out rather than fixed.

## Sample preparation is the hard part

In a confocal microscope you put your sample on a coverslip. In a light-sheet microscope you cannot, because a coverslip sitting between the two orthogonal objectives would be in the way of at least one of them.

The usual solution is to embed the specimen in a cylinder of low-percentage agarose and either extrude it from a glass capillary or hold it in a tube of FEP, a plastic whose refractive index nearly matches water. The cylinder hangs in a chamber of medium into which both objectives dip. This is more involved than mounting a slide, it takes practice, and it constrains what you can image.

It also brings one large compensation: because the sample hangs freely, it can be **rotated**. Acquire stacks from several angles, register them and fuse them, and you recover a specimen that is uniformly resolved throughout, rather than progressively degraded on the far side. Multi-view fusion is standard practice for embryos.

For large fixed specimens, light-sheet microscopy is usually paired with **optical clearing**, which removes lipids and matches the refractive index throughout the tissue so that light travels in straight lines. CLARITY, iDISCO, BABB and their relatives make a whole mouse brain transparent, and a cleared brain imaged in a light sheet can be reconstructed in its entirety in hours. The combination is now the standard approach to whole-organ neuroanatomy.

## Summary

- **Advantages**: very high speed, comparable to widefield, because detection is camera-based; optical sectioning with no light discarded; photobleaching and phototoxicity one to three orders of magnitude below confocal, which makes long-term live imaging of developing organisms possible; deep penetration, especially in cleared samples; the detection objective is free to be long-working-distance.
- **Drawbacks**: sample mounting is demanding and unfamiliar; two objectives must be aligned and kept aligned; the section thickness is usually set by the sheet and is worse than a good confocal; shadowing artefacts require active correction; the geometry does not fit standard coverslip-based samples.

One requirement runs underneath all of this and is easy to forget: the specimen has to be close to transparent. The sheet has to travel sideways across the whole field before it is imaged, and it has to stay a sheet while doing so. A dense, scattering specimen destroys it within a few tens of micrometres, and no amount of alignment will help. This is why the canonical light-sheet organisms are the transparent ones, and why clearing is not an optional refinement for large fixed tissue but the thing that makes the technique work at all.

The typical applications follow the strengths exactly. Zebrafish and _Drosophila_ development, followed continuously for a day or more, with the embryo still developing normally at the end of it. Whole-brain neural activity in transparent larvae, where the point is to catch every neuron at once rather than a few of them beautifully. Three-dimensional cultures: spheroids and organoids imaged over hours to watch astrocyte networks form, or to follow how a tumour organises itself in three dimensions in a mammary organoid, which is a question you simply cannot ask of a technique that flattens the specimen or kills it. And whole cleared organs, reconstructed in their entirety. What all of these have in common is that they are large, alive or intact, and would not survive a confocal microscope.

