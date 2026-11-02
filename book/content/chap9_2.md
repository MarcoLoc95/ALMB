# Expansion microscopy

Every technique in this chapter tries to squeeze more resolution out of light. Expansion microscopy (ExM) takes the opposite route: it leaves the microscope alone and changes the sample. If two proteins sit 60 nm apart, no conventional microscope can separate them. If we could pull them four times further apart, to 240 nm, an ordinary confocal would see two spots. The idea sounds almost too naive to work, and when Fei Chen, Paul Tillberg and Edward Boyden published it in 2015 it surprised much of the microscopy community. Yet the principle is sound, and expansion microscopy has since become one of the most accessible ways to reach nanoscale resolution in biology.

## A gel that swells

To expand a cell uniformly we need a material that can grow by a large and predictable factor in all three dimensions, and that can drag the biological molecules along with it. The material of choice is a **polyacrylate hydrogel**, essentially the same superabsorbent polymer found in baby diapers.

A hydrogel is a network of long polymer chains connected at random points by **crosslinker** molecules. In ExM the chains are made of sodium acrylate (often mixed with acrylamide), and the crosslinker is a small molecule called bisacrylamide that links two chains together. The acrylate groups carry negative charges, balanced by positive counter-ions. When the gel is placed in pure water, the counter-ions want to spread out into the water, and osmotic pressure pulls water into the network. The chains, repelling each other electrostatically, stretch out, and the whole gel swells. The crosslinks keep it from dissolving: they define a mesh that simply becomes larger. Because the crosslinks are distributed at random and in all directions, the swelling is, ideally, the same along every axis. In salty buffer the charges are screened and the gel shrinks back; dried completely, it collapses.

The linear **expansion factor** $X$ of standard protocols is about four, which means the volume grows by $X^3 \approx 64$. The resolution, measured in the original, biological coordinates, improves by the same linear factor:

$$
d_{ExM} = \frac{d_{min}}{X}
$$

where $d_{min}$ is the resolution of the microscope used to image the gel. A confocal microscope with $d_{min} \approx 250$ nm and a fourfold expansion gives an effective resolution of about 60-70 nm, comparable to STED, using an instrument found in nearly every imaging facility.

Note what this formula does and does not say. The PSF is not changed at all: each fluorophore still produces a 250 nm blob in the expanded gel. What changes is the distance between fluorophores. Expansion is a magnification that happens _before_ the light is collected, and unlike optical magnification it is not bound by diffraction (_{numref}`Fig. {number} <chap9_exm_expand>`_).

```{figure} ../figures/chap9_exm_expand.gif
---
width: 70%
name: chap9_exm_expand
align: center
---
Two fluorophores (green) 100 nm apart are anchored to the polymer network. As the gel expands, their separation grows while the size of their image, set by the PSF, stays the same. The two overlapping blobs become two resolved peaks.
```

## The protocol step by step

Making a cell expand like the gel around it requires several steps (_{numref}`Fig. {number} <chap9_exm_workflow>`_). Recipes differ between labs and between versions of the method, but the logic is always the same.

```{figure} ../figures/chap9_exm_workflow.png
---
width: 100%
name: chap9_exm_workflow
align: center
---
The main steps of expansion microscopy. Proteins or labels in a fixed cell are equipped with chemical anchors; a hydrogel network is polymerized through the sample and the anchors bind to it; the cell is digested or denatured so that it no longer resists swelling; finally the gel is placed in water and expands, carrying the labels apart while preserving their relative positions.
```

1. **Fixation and anchoring.** The sample is chemically fixed and then treated with a small bifunctional molecule (for example acryloyl-X, a reagent that reacts with amine groups on proteins on one side and carries an acrylate group on the other). The acrylate end will be built into the gel during polymerization, so every anchored protein becomes covalently attached to the network. This step is essential: if the structures of interest are not linked to the gel, the gel expands around them and leaves them behind.
2. **Gelation.** The sample is soaked with a solution of monomers and crosslinker, and polymerization is started chemically. The gel grows through the entire cell and around it, incorporating the anchors.
3. **Homogenization.** A cell is full of stiff components (membranes, cytoskeleton, chromatin) that would resist swelling or tear apart unevenly. In the original protocol, a protease (proteinase K) digests most proteins into fragments, while the anchored pieces carrying the labels stay attached to the gel. Later variants, such as U-ExM (ultrastructure expansion microscopy), replace digestion with denaturation by heat and detergent, which unfolds the proteins but keeps them in the gel.
4. **Expansion.** The gel is washed in water, sometimes in several rounds, and swells to its final size.

Labels can be introduced before gelation, or, when proteins are denatured instead of digested, after expansion. Some protocols, like the one in the lecture slides for parasites, even expand, shrink the gel back in buffer to stain it, and expand again. Each choice has consequences for the final image, as we will see shortly.

## What expansion buys: an example

_{numref}`Fig. {number} <chap9_ex_exm_synapses>`_ shows one of the first demonstrations of the method. A synapse is a gap of a few tens of nanometers between a presynaptic terminal and a postsynaptic density, and the proteins that mark the two sides overlap completely in a conventional confocal image. After expansion, the presynaptic and postsynaptic markers separate into two distinct layers. Expansion has since been used to map the nanoscale organization of synapses, centrioles, cilia, viruses, parasites and whole tissues, and it is compatible with every imaging technique: an expanded sample can be imaged with SIM or STED to multiply the gains.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_exm_synapses.png
---
width: 100%
name: chap9_ex_exm_synapses
align: center
---
Expansion microscopy of mouse brain tissue labelled for the presynaptic protein Bassoon and the postsynaptic protein Homer1, imaged on a conventional confocal microscope. After expansion the two sides of individual synapses are resolved. Source: [reference to be added].
```

## The fine print

### Isotropy

The entire method rests on one assumption: the sample expands by the same factor everywhere and in every direction. If the gel swells more along one axis than another, or if a stiff structure resists while its surroundings expand, the image is distorted, and we would measure the wrong shapes and distances without any obvious warning sign.

How can we check? The most direct way is to image the same cell before and after expansion and compare the two images with a nonrigid registration, mapping how every point moved (_{numref}`Fig. {number} <chap9_exm_distortion>`_). From the resulting displacement field one can calculate how wrong a length measurement would be as a function of the length measured. For standard protocols the errors are typically a few percent of the measured length.

```{figure} ../figures/chap9_exm_distortion.png
---
width: 100%
name: chap9_exm_distortion
align: center
---
Measuring the isotropy of expansion (simulated). Left: the same filaments imaged before expansion (magenta) and after expansion, scaled back by the measured expansion factor (green); white indicates overlap. Middle: the displacement field obtained by nonrigid registration of the two images; the dashed square marks the region shown on the left. Right: the root-mean-square error of length measurements grows with the length measured, here to about 1%.
``` Another approach is to include internal rulers: structures of well-known size and shape, such as nuclear pore complexes or centrioles, whose apparent dimensions after expansion reveal both the actual expansion factor and any anisotropy. The expansion factor itself should always be measured for each experiment rather than taken from the protocol, because it depends on the exact composition of the gel, on temperature and on the ionic strength of the water.

### Label size

A more subtle problem appears as soon as we push the expansion factor up. The microscope does not see proteins; it sees fluorophores, and the fluorophores are attached to the protein by some kind of label. In immunofluorescence, the most common choice, a primary antibody binds the protein and a secondary antibody carrying the dyes binds the primary. Each IgG antibody is about 10 nm long, so the dye can sit up to about 20 nm away from the protein (_{numref}`Fig. {number} <chap9_labels>`_). This offset is called the **linkage error**.

```{figure} ../figures/chap9_labels.png
---
width: 100%
name: chap9_labels
align: center
---
Common labels drawn approximately to scale, with the typical distance between the target protein and the fluorophore. Antibodies displace the dye by 10-20 nm, while nanobodies, self-labelling tags fused to the protein and small dyes attached by click chemistry bring it within a few nanometers.
```

When labelling is performed _before_ expansion, the antibodies are anchored to the gel like every other protein. An intact, folded antibody cannot stretch, but digestion cuts it into fragments (or denaturation unfolds it), and each anchored piece, dyes included, is carried along with the gel. The dye therefore moves away from its target protein by the expansion factor, like everything else, so in biological coordinates the linkage error stays at 10-20 nm no matter how much we expand. Once the optical resolution $d_{min}/X$ falls below this value, further expansion does not reveal more: we just see the antibody cloud around the protein more sharply.

When labelling is performed _after_ expansion, the situation reverses. The proteins have already been pulled apart, the antibody binds to the expanded protein, and its 20 nm length now corresponds to only $20/X$ nm in the original sample. Post-expansion labelling also improves access to epitopes that were buried in crowded structures before expansion. _{numref}`Fig. {number} <chap9_exm_prepost>`_ compares the two strategies. The catch is that the epitopes must survive gelation and homogenization, which is why denaturation-based protocols are used for this purpose. Small labels, such as nanobodies or genetically encoded tags, are another way out.

```{figure} ../figures/chap9_exm_prepost.png
---
width: 90%
name: chap9_exm_prepost
align: center
---
Labelling before and after expansion, drawn to scale in gel coordinates for a fourfold expansion. Top: antibodies attached before expansion are anchored to the gel; digestion breaks them into fragments, and the anchored fragments and dyes are pulled apart with the gel (dotted: the original antibody shape, expanded). The dye stays about 20 nm from its protein in biological units. Bottom: antibodies applied after expansion bind proteins that are already four times further apart, and their 20 nm length corresponds to only 5 nm in the original sample.
```

```{tip}
A quick estimate of the effective resolution in an ExM experiment combines the optical limit and the label displacement: $d_{eff} \approx \sqrt{(d_{min}/X)^2 + \ell^2}$, where $\ell$ is the linkage error in biological coordinates ($\ell$ for pre-expansion labelling, $\ell/X$ for post-expansion labelling). For a confocal microscope, a 10-fold expansion and pre-expansion antibodies: $\sqrt{25^2 + 20^2} \approx 32$ nm, so the antibodies, not the optics, set the limit.
```

### Signal dilution and practicalities

Expanding the sample by $X$ in every direction spreads the same number of fluorophores over $X^3$ times the volume. At $X = 4$ the fluorophore density drops to less than 2% of the original, and at $X = 10$ to 0.1%. The image of each individual fluorophore is not dimmer, but there are far fewer of them within each diffraction-limited volume, so the overall signal drops dramatically. Bright, photostable labels and efficient detection become essential.

The gel is also large and delicate. A cell 10 µm thick becomes 40 µm thick after a fourfold expansion, and the volume that must be imaged to cover it grows 64 times. Since the expanded gel is more than 99% water, its refractive index is close to 1.33, so water-immersion objectives give the best images; oil objectives introduce spherical aberration that worsens with depth, as discussed in {ref}`Chapter 2 <chap2_2>`. Light-sheet microscopy ({ref}`Chapter 5 <chap5_3>`) is a natural match for imaging large expanded tissues quickly. Finally, the gel floats and drifts unless it is immobilized, for instance with poly-lysine-coated coverslips.

## Pushing further

The expansion factor of a single round is limited by how much the gel can swell before it becomes too fragile. Two strategies push beyond it. In **iterative expansion**, a second gel is polymerized inside the first expanded one, the labels are transferred, and the second gel is expanded again, for total factors around 15-20. Alternatively, gels with a different chemistry swell by about ten times in a single step. Combined with post-expansion labelling, or with STED or single-molecule localization of the expanded sample, these approaches reach effective resolutions of 10-25 nm, and the most recent variants combine strong expansion with statistical analysis of fluorescence fluctuations to visualize the shapes of individual large proteins.

## Exploring expansion

In the widget below you can expand a nuclear pore complex (eight subunits on a ring of 107 nm diameter) or a microtubule seen from the side (a hollow tube 25 nm wide), choose the microscope used on the gel, the label and when it is applied, and introduce some anisotropy. The left panel shows where the targets (grey) and fluorophores (green) are; the right panel shows the image you would get, scaled back to biological size.

:::{raw} html
<iframe src="../content/exm_widget.html" width="100%" height="650px" frameborder="0" style="border: none;"></iframe>
:::

## Strengths and limitations

The trick of expansion microscopy is the **known, isotropic expansion factor**. Everything else is ordinary microscopy, which gives the method its main advantages: it works with any microscope, including inexpensive widefield and confocal systems, it is compatible with every other technique in this chapter, it covers large fields of view and even whole tissues, and the reagents are cheap.

The drawbacks are equally clear. The sample preparation is long and delicate; gel chemistry is sensitive to small variations, and protocols must be followed strictly. Distortions due to anisotropic or incomplete expansion are always possible and must be checked rather than assumed. The signal is diluted, and at high expansion factors the label size becomes the limit. Above all, the sample is fixed, anchored, digested and swollen in water: expansion microscopy is fundamentally incompatible with living cells, and it can only report on structure, not on dynamics.

To see nanoscale structure in a living sample, we need to change not the specimen but the way it emits light. The next technique does exactly that, by switching off fluorescence where we do not want it.
