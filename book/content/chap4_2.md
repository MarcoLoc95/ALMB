# Types of fluorophores

A **fluorophore** is any molecule that emits fluorescence. That is the only thing the candidates in this section have in common. Beyond it, they could hardly be more different in size, origin, and behavior. There are three families worth knowing, and the practical skill is matching the right one to your experiment: organic dyes, genetically encoded fluorescent proteins, and quantum dots. The first two you have almost certainly met before. The third is the one most people see for the first time here.

## Organic dyes

Organic dyes are small synthetic molecules, and their fluorescence comes from **aromatic rings**, the flat hexagonal carbon structures with alternating single and double bonds. The amino acid tryptophan contains one, which is part of why proteins fluoresce faintly on their own. The bonds are not really fixed as alternating single and double; the electrons are spread out over the whole ring in what chemists call _resonance_, and all the equivalent structures coexist at once. That delocalization gives the ring its stability and the sharp, well-defined molecular orbitals that produce clean fluorescence.

Two things follow from this design. First, dyes are small, often just a handful of atoms across, which makes them far less likely to disturb whatever they are attached to than a bulky protein would be. Second, the exact ring system sets the color: change the chemistry and you shift from blue to red. The **cyanine** dyes are a familiar example, with Cy3 (green) and Cy5 (red) among the most common. You will often see sulfonate groups, written SO$_3^-$, hanging off them. These are not decoration. Sulfonation makes the dye water-soluble, so it is easy to deliver into a sample, and it reduces **quenching** after the dye is conjugated to its target.

```{tip}
**Quenching** is any loss of fluorescence caused by non-radiative energy transfer to a neighbor, the same kind of pathway that lowers quantum yield. It is the everyday enemy of a bright label: pack fluorophores too close, or let them touch the wrong partner, and they go dark. The FRET we met in the previous section is quenching put to deliberate, useful work.
```

The flagship commercial family is the **Alexa Fluor** dyes, which between them cover the whole spectrum from the ultraviolet through the near-infrared. Whatever color your experiment needs, there is an Alexa dye for it, and you simply pick the one that matches your filters. Dyes are popular for good reason: they are very bright, with high quantum yields, and finely tunable. The catch is toxicity. Through the ROS pathway from the previous section, dyes tend to harm living cells over time, so they shine in **fixed** samples where the cell is already dead and you only want to inspect its structure, and they are a poorer choice for long-term live imaging.

You attach a dye to a chosen structure through **immunofluorescence**: an antibody recognizes the target, and the dye rides along on the antibody. With the right antibodies you can light up almost anything, the nucleus, actin, mitochondria, the cytoskeleton, membranes, one target per structure, which is why immunofluorescence images of dye-labeled cells are among the most recognizable pictures in all of biology.

## Genetically encoded fluorescent proteins

The alternative is to let the cell build its own fluorophore. **Genetically encoded fluorescent proteins** are written into the cell's DNA, typically delivered on a plasmid (a small circular DNA borrowed from bacteria) or by a virus, and the cell then manufactures the glowing protein itself.

The icon of this family is the **green fluorescent protein (GFP)**, discovered in the jellyfish _Aequorea victoria_. Its story is a small monument in biology: Osamu Shimomura isolated it in the 1960s, Martin Chalfie showed in the 1990s that the gene could be expressed in other organisms to act as a living marker, and Roger Tsien engineered a whole palette of color variants and worked out how the color arises. The three shared the 2008 Nobel Prize in Chemistry. Most of the common fluorescent proteins in use today are descendants of GFP, with additional colors borrowed from proteins found in corals and sea anemones.

Structurally, GFP and its relatives are **beta-barrels**: a cylinder of rigid beta-sheets wrapped around a central **chromophore**, the small group of amino acids that actually does the fluorescing. The barrel is doing real work. It is stiff and protective, shielding the chromophore from the outside world so that it does not get quenched, much as the aromatic rings of an organic dye are themselves the emitting part. The precise chemistry of the chromophore sets the color.

The defining advantage is that the cell makes the label, which buys you two things. The labeling is genetic rather than chemical: co-express the fluorescent protein with a protein that goes to your target of interest, and wherever that target ends up, the fluorescence follows. This tends to be more reliable than immunofluorescence, which stacks antibody upon antibody. And because the cell keeps producing the protein, fluorescence is replenished over time and across cell divisions, though slowly, on the scale of the cell's own protein turnover. Like all organic fluorophores, fluorescent proteins eventually photobleach.

```{tip}
With well over a thousand fluorescent proteins now characterized, choosing one by hand is hopeless. The community-curated database [**FPbase**](https://www.fpbase.org/) lets you filter by exactly the parameters from the previous section: excitation and emission spectra, Stokes shift, brightness, quantum yield, and photostability. It is the natural place to start when you need a protein with a particular set of properties.
```

## Quantum dots

The newest family was first discovered in 1981 by the Russian scientist Alexey Ekimov, but developed for biology somewhat later, and is unlike anything organic. **Quantum dots** are tiny semiconductor nanocrystals, only a few nanometers across and sometimes only a few hundred atoms, most commonly made of cadmium selenide (CdSe). Unlike aromatic rings, they fluoresce for a reason rooted in solid-state physics.

In a bulk semiconductor, electrons live in continuous energy bands separated by a band gap. Shrink the crystal down to a few nanometers and the gap is no longer fixed: the smaller the dot, the larger the gap, and the larger the gap, the shorter the emitted wavelength. This is called **quantum confinement**, and it gives quantum dots a property no dye or protein has, namely that you tune the color simply by changing the size.

The fluorescing core is usually surrounded by several extra layers: surface ligands, a polymer coating such as PEG that acts as a spacer, and a targeting ligand on the outside. The spacer is not optional. If you bring the core too close to other molecules and energy leaks away non-radiatively, a FRET-like quenching, so the polymer holds everything at a safe distance. In size, quantum dots sit between the two organic families: bigger than a dye, smaller than a protein.

```{figure} ../figures/chap4_qdot_spectra.gif
---
width: 90%
name: qd_tunability
align: center
---
Size-tunable emission of colloidal CdSe quantum dots. Only the dot diameter changes, yet the emission peak marches from the blue toward the red as the dot grows. This is quantum confinement in action: in a crystal only a few nanometers across, the electron and hole are boxed into a space smaller than they would naturally occupy, which widens the energy gap. A smaller box means a larger gap and shorter-wavelength emission, a larger box a smaller gap and longer-wavelength emission, so a single material can be tuned across the whole visible spectrum by size alone. Notice too how narrow and symmetric each peak is, unlike the red-tailed emission of organic dyes and fluorescent proteins.
```

Quantum dots bring a striking list of advantages. They are very bright, with quantum yields near one, and because they have no troublesome triplet states they are extraordinarily photostable: you essentially have to physically destroy the particle to stop it glowing, so for practical purposes they barely photobleach at all. Furthermore, they are highly tunable through size, and their emission peaks are narrow and symmetric, much sharper than the broad, tailing peaks of organic fluorophores. That sharpness is most suitable for **multiplexing**, imaging many colors at once, because narrow peaks can be cleanly separated by filters where broad ones would bleed into each other. A single excitation wavelength can excite dots of many colors simultaneously, and four, five, or six channels become realistic. In practice they have been used to label membranes, intracellular targets, and a range of cell types including neurons and glia.

```{figure} ../figures/chap4_qd_examples.png
---
width: 80%
name: qd_examples
align: center
---
Quantum dot-based immunofluorescence labeling. (a) Her2 receptors on human SK-BR-3 breast cancer cells labeled with QD535-IgG (green). (b) Cell nuclei labeled with QD630-streptavidin (red). (c) Simultaneous labeling of microtubules (green, QD535) and nuclei (red, QD630). (d) Dual labeling of Her2 receptors (green, QD535) and nuclei (red, QD630). Scale bars: 10 μm (a); 50 μm (b-d). Adapted from Wu et al. (2003), DOI: [10.1038/nbt764](https://doi.org/10.1038/nbt764)
```

The drawback is again toxicity, and here it is twofold. There is the familiar ROS pathway, and on top of it the risk that the particle releases its cadmium, and the cadmium ion is severely toxic to cells, worse even than calcium. Protective shells around the CdSe core reduce both the oxygen exposure and the leakage, but the warning stands: with quantum dots you must always check the toxicity of the specific particle for your application. One further quirk worth knowing is that individual quantum dots tend to **blink**, switching on and off intermittently rather than glowing steadily, a behavior that is a nuisance for some measurements but, like dark states, can also be exploited.

## Choosing a fluorophore

There is no single best fluorophore, only the best one for a given experiment. The three families pull in different directions, and the table below summarizes the trade-offs.

| Property | Organic dyes | Fluorescent proteins | Quantum dots |
|---|---|---|---|
| Size | Smallest (a few atoms) | Large (a whole protein) | Intermediate (a few nm) |
| Origin | Synthetic chemistry | Made by the cell | Synthetic nanocrystal |
| Brightness | High | Moderate to high | Very high |
| Photostability | Moderate | Lower (bleaches) | Excellent (barely bleaches) |
| Emission width | Broad | Broad | Narrow (great for multiplexing) |
| Labeling | Immunofluorescence (antibody) | Genetic, co-expression | Surface ligand on coating |
| Main drawback | Toxicity over time | Bleaching, larger label | Toxicity (ROS and cadmium) |
| Best suited for | Fixed samples, bright structural imaging | Live cells, specific genetic targeting | Long imaging, many-color multiplexing |

Read the table as a set of compromises rather than a ranking. Fixing a sample and inspecting its architecture with bright, finely chosen colors points toward dyes. Watching a specific protein in a living, dividing cell points toward a fluorescent protein. Tracking something for a long time, or separating many colors at once, points toward quantum dots, provided the toxicity is acceptable. Every one of these decisions traces straight back to the quantitative parameters of {ref}`the previous section <chap4_1>`: brightness, photostability, Stokes shift, and the rest.