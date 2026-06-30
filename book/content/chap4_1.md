# Principles of fluorescence

In 1852, George Gabriel Stokes was puzzling over a glass of quinine solution. Back then, this alkaloid extracted from the bark of the cinchona tree was the prescribed to treat malaria, but due to its intensely foul, bitter taste, soldiers mixed it with carbonated water, sugar, and lime. This mix became the world's first tonic water. To make the medicine even easier to swallow, British officers added their daily gin rations to the mixture, accidentally inventing the iconic Gin & Tonic as we know it today. Where were we? Ah, yes, fluorescence.

Stokes noticed that when the quinine solution was lit by the invisible, ultraviolet part of sunlight, the liquid glowed a soft blue. In his paper _On the Change of Refrangibility of Light_ he worked out what was happening: the solution was absorbing light the eye cannot see and giving back light of a longer wavelength that it can. He even realized he could separate the two with colored glass, using one piece to let only the exciting ultraviolet through and another to block it on the way out, so that only the blue glow reached his eye. Stokes named the effect _fluorescence_, and that simple two-filter trick is, in essence, every fluorescence microscope ever built. If you have a UV "blacklight" and a bottle of tonic water at home, you can easily reproduce his observation (and surprise your friends at any party).

```{figure} ../figures/chap4_stokesquinine.png
---
width: 100%
name: chap4_stokesquinine
align: center
---

Sunlight passes through the blue glass of a church window, which acts as an excitation filter and transmits only short wavelengths below 400 nm. This light excites a solution of quinine, which re-emits at longer wavelengths. A glass of yellow wine then serves as an emission filter, blocking the leftover excitation light and passing only the emitted light above 400 nm, so the quinine appears to glow. From: "Introduction to Fluorescence", Principles of Fluorescence Spectroscopy (2006), Springer, DOI: [10.1007/978-0-387-46312-4_1](https://doi.org/10.1007/978-0-387-46312-4_1)
```

## Light-matter interaction

### He was a photon, she was a molecule, could I make it any more obvious?

Recall from {ref}`Chapter 1 <chap1>` that light sometimes behaves as a stream of photons, each carrying a packet of energy set by its wavelength: short wavelength means high energy, long wavelength means low energy. In a single atom, electrons sit in shells, and a photon with the right energy can kick an electron from a stable inner shell up to a higher, less stable one. After a short wait the electron drops back down and a photon comes out. That is just absorption followed by spontaneous emission.

Molecules are richer. Instead of clean atomic shells we have to deal with molecular orbitals, most importantly the highest one that is normally filled, and the lowest one that is normally empty. We call the stable, filled configuration the **ground state**. Think of it as the sofa at the end of a long day: the molecule will always tend to settle there. When a photon of the right energy is absorbed, an electron is promoted to an **excited state**, and the molecule now holds extra energy it must eventually shed. There are many ways to shed it, and the map of all of them is called the Jablonski diagram.

### The Jablonski diagram

_{numref}`Fig. %s <jablonski>`_ organizes the whole process by energy, which increases as you move up the page. The thick horizontal lines are electronic states: the ground state $S_0$ at the bottom, and excited states $S_1$, $S_2$ above it. Stacked above each electronic state is a ladder of thinner lines, the **vibrational sublevels**. These exist because a molecule is not a rigid object: it can stretch, bend, and rotate, and each of those motions adds a little energy on top of the electronic state. The sublevels get denser the higher you go, so for almost any photon energy in the absorption band there is some vibrational level ready to receive it.

```{figure} ../figures/jablonski.png
---
width: 85%
name: jablonski
align: center
---
A Jablonski diagram. Straight vertical arrows are radiative transitions involving a photon (absorption in blue, fluorescence in green, phosphorescence in red). Wavy arrows are non-radiative: internal conversion and vibrational relaxation (grey) shed energy as heat, while intersystem crossing (orange) flips an electron spin and routes the molecule into the triplet state. The small paired and parallel arrows show the singlet ($S$) and triplet ($T$) spin configurations.
```

Reading the diagram from left to right tells the story of one excitation cycle:

1. **Absorption** (blue, pointing up) is a photon lifting an electron from the bottom of $S_0$ up into a vibrational level of $S_1$ or $S_2$. It is staggeringly fast, on the order of femtoseconds, $10^{-15}$ s, among the shortest events we can speak of.
2. **Vibrational relaxation and internal conversion** (grey wavy arrows) follow almost immediately. The molecule dumps its excess vibrational energy as heat into its surroundings and tumbles down to the lowest vibrational level of $S_1$. This is also quick, sub-picosecond to picosecond. It is the reason almost all fluorescence starts from the same place regardless of which color excited it.
3. **Fluorescence** (green, pointing down) is the electron finally falling from the bottom of $S_1$ back to one of the vibrational levels of $S_0$, releasing the leftover energy as a photon. The molecule lingers in $S_1$ for a few nanoseconds before this happens, far longer than the steps above but still a flash.

If the ground state is the sofa, the bottom of $S_1$ is a chair the molecule perches on briefly before flopping back down. Crucially, the emitted photon carries less energy than the absorbed one, because some energy was lost to heat on the way. Less energy means longer wavelength, and that color shift is the whole basis of the technique.

### Singlet, triplet, and phosphorescence

There is one more path on the diagram, and it has consequences far beyond its size. You do not need quantum mechanics for this course, but the names are worth decoding. Electrons carry a property called spin, which we can picture as a tiny arrow pointing up or down. In the ground state the relevant pair of electrons is paired, one up and one down, a configuration with a single possible arrangement: a **singlet** state, hence $S_0$. Excitation usually keeps the spins as they were, so the molecule lands in an excited singlet, $S_1$. Spin is a conserved quantity, so flipping it is not something light does easily, which is exactly why the singlet route dominates.

Occasionally, though, an electron does flip its spin. Now the two spins are parallel, and quantum mechanics allows three such arrangements rather than one: a **triplet** state, $T_1$, drawn slightly below $S_1$ because flipping the spin costs a little energy. The molecule can decay from $T_1$ back to $S_0$ by emitting a photon, and that is **phosphorescence**. Because the return again requires an awkward spin flip, it is slow, ranging from microseconds to seconds or even minutes. This is why glow-in-the-dark stars keep shining after you switch off the light, whereas fluorescence stops the instant the excitation does.

```{tip}
The timescale ladder is worth committing to memory because it explains so much downstream. Absorption: femtoseconds. Vibrational relaxation: picoseconds. Fluorescence: nanoseconds. Phosphorescence: microseconds to seconds. Each step is roughly a thousand to a million times slower than the one before.
```

## Excitation and emission spectra

We cannot see individual energy levels, but we can measure spectra, and a spectrum is a direct fingerprint of those levels. Sweep the excitation wavelength and record how strongly the molecule fluoresces: that is the **excitation spectrum**, and it traces the upward arrows, with stronger absorption where a transition is more probable. Fix the excitation and record the colors that come out: that is the **emission spectrum**, tracing the downward fluorescence arrows. Because excitation samples the vibrational levels of the excited state and emission samples those of the ground state, and because the two ladders are usually similar, the spectra often look like mirror images of each other (_{numref}`Fig. %s <spectra_stokes>`_).

```{figure} ../figures/spectra_stokes.png
---
width: 80%
name: spectra_stokes
align: center
---
Excitation (blue, dashed) and emission (green, solid) spectra of a typical fluorophore, with the characteristic near-mirror symmetry. The emission is shifted toward longer wavelengths. The gap between the two peaks is the Stokes shift, $\Delta\lambda$.
```

The single most useful feature of this plot is the gap between the two peaks, the **Stokes shift** $\Delta\lambda$, named after the same Stokes:

$$\Delta\lambda = \lambda_\text{em,max} - \lambda_\text{ex,max}$$

A large Stokes shift is a gift. The further the emission peak sits from the excitation peak, the easier it is to throw away every scrap of excitation light with a filter and collect only the genuine signal, even when the fluorophore is dim. A small Stokes shift means excitation and emission overlap, so some exciting light inevitably leaks into your detector as background. When you choose a fluorophore, the Stokes shift is one of the first numbers you check.

## Quantifying a fluorophore

Two fluorophores can both glow green and still behave completely differently. To compare them we need numbers, and a handful of parameters do most of the work. They all flow from a simple competition: once a molecule reaches $S_1$, it can either emit a photon or get rid of its energy some other way.

The **radiative decay rate** $\Gamma_r$ [s$^{-1}$] is the rate at which the excited molecule emits a photon. The **non-radiative decay rate** $\Gamma_{nr}$ [s$^{-1}$] lumps together every other route back to the ground state, all of which produce heat instead of light. From these two rates everything else follows.

The **lifetime** $\tau$ [ns] is the average time the molecule spends in $S_1$ before returning to $S_0$, set by the total rate of leaving:

$$\tau = \frac{1}{\Gamma_r + \Gamma_{nr}}$$

It is an average over a stochastic process. If $\tau = 1$ ns, most photons appear within a nanosecond or two, a few stragglers come out after three, and rarely one escapes after half a nanosecond. We will return to lifetime later in the course, because measuring it gives a way to distinguish fluorophores that share the same color.

The **quantum yield** $\Phi$ (written $Y$ on the lecture slides, and sometimes $Q$ elsewhere) is the fraction of excited molecules that decay by emitting a photon:

$$\Phi = \frac{\Gamma_r}{\Gamma_r + \Gamma_{nr}} = \Gamma_r\,\tau$$

Read it as an efficiency. If $\Gamma_{nr}$ is tiny compared to $\Gamma_r$, then $\Phi \approx 1$ and essentially every absorbed photon comes back out as fluorescence. If non-radiative losses dominate, $\Phi$ falls toward zero. Good probes often sit close to one, and a quantum yield of 0.7 or 0.8 is still very usable. Some specialized sensors are far worse: certain genetically encoded voltage indicators have quantum yields around 3 percent, meaning that of a hundred absorbed photons only three are re-emitted.

The **molar extinction coefficient** $\varepsilon$ [M$^{-1}$ cm$^{-1}$] measures the other half of the story: how strongly the molecule absorbs at a given wavelength in the first place. Combining absorption and emission gives the **brightness**:

$$B = \varepsilon \cdot \Phi$$

Brightness is what you actually perceive at the eyepiece, and it has a practical consequence. Both $\varepsilon$ and $\Phi$ are fixed by the molecule, so if a fluorophore is intrinsically dim there is only one lever left: pump in more photons by raising the excitation power. That sounds like a free win until we meet photobleaching, where the bill arrives.

```{tip}
Brightness is a product, so a fluorophore can be dim for two very different reasons: it barely absorbs (low $\varepsilon$), or it absorbs well but wastes the energy as heat (low $\Phi$). Diagnosing which one is failing tells you whether to change the excitation wavelength or change the molecule.
```

The last parameter on the list is not a property of the fluorophore but of your measurement: the **signal-to-noise ratio (SNR)**, the ratio of the signal carrying real information to everything else you detect, including background and random noise from the camera. We will spend real time on SNR in the image-analysis part of the course; for now, just note that brighter fluorophores and lower background both push it in the right direction.

## Autofluorescence

Here is an uncomfortable fact: if you put a slice of unlabeled tissue under the microscope, it will probably glow anyway. Cells are full of molecules that fluoresce on their own, including reduced nucleotides such as NADH, aromatic amino acids in proteins, and natural pigments like flavins and porphyrins. Anything with color in nature, from fruit to leaves, contains such pigments. This intrinsic glow is called **autofluorescence**, and the inconvenient part is that it appears across the whole spectrum, from the violet to the near-infrared, so there is no single color where you are guaranteed to be safe.

You cannot really engineer it away, at least not without stripping the cell of the very molecules that keep it alive, which defeats the purpose of imaging biology in its natural state. What you can do is manage it: push your signal into a spectral region where autofluorescence is weaker, the near-infrared often being a good choice, and subtract a measured background during analysis. The practical lesson for the bench is simple but easy to forget: not every glowing thing in your image is the thing you labeled.

## Photobleaching and phototoxicity

The triplet state we met earlier is a quiet troublemaker. It is chemically reactive, and a molecule that lingers there can react with nearby oxygen, which cells always have, to produce **reactive oxygen species (ROS)**: singlet oxygen, superoxide, hydrogen peroxide, and similar aggressive radicals. When those species attack the fluorophore itself, they break or modify it: a double bond becomes a single bond, a group is cleaved, and the molecule simply stops fluorescing. This irreversible destruction is **photobleaching**, and there is no coming back from it.

It might seem that the triplet route is so rare it should not matter. For many fluorophores the transition from $S_1$ down to $S_0$ is about a billion times more probable than the crossing from $S_1$ into the triplet, $k_2 \approx 10^9\,k_3$. But a fluorophore is cycled through excitation enormous numbers of times per second, so even a one-in-a-billion detour adds up. Under ordinary illumination, a few milliwatts of excitation, a typical organic fluorophore survives only on the order of seconds before it bleaches.

```{figure} ../figures/photobleaching.png
---
width: 80%
name: photobleaching
align: center
---
Fluorescence intensity decaying over time as a population of fluorophores photobleaches. Raising the excitation power (dashed) drives the molecules through more excitation cycles per second, so they bleach sooner. Lowering the power preserves them (solid) but at the cost of a weaker signal.
```

This is the trap that makes the "just use a more powerful laser" instinct fail (_{numref}`Fig. %s <photobleaching>`_). More excitation power does buy more signal, but it also accelerates bleaching, because every extra excitation cycle is another chance to wander into the triplet state. Turn the power down to bleach more slowly and your signal drops, which is especially painful if the fluorophore was already dim. Balancing photons collected against photons survived is one of the recurring tensions in fluorescence imaging.

There is a second cost. If the ROS escape the immediate neighborhood of the fluorophore and diffuse into the cell, they damage the living sample itself, causing apoptosis, membrane disruption, mitochondrial stress, DNA damage, and disrupted signaling. Damage to the sample caused by light in this way is called **phototoxicity**. Roughly speaking, photobleaching is the fluorophore breaking, while phototoxicity is the cell paying the price. Genetically encoded proteins like GFP tend to bleach because their delicate chromophore is the casualty, whereas small, robust organic dyes often survive while their ROS go on to harm the surrounding cell.

A molecule sitting in the triplet state is, for the moment, not fluorescing. The same is true of certain radical or chemically reduced configurations. We call these non-emitting configurations **dark states**. For now, just note that they exist and that they switch a fluorophore temporarily off. Far from being a mere nuisance, the ability to push molecules into and out of dark states is the foundation of one of the most successful super-resolution methods we will discuss in {ref}`Chapter 9 <chap9>`.

## Förster Resonance Energy Transfer (FRET)

One last phenomenon deserves a place here because it turns fluorescence into a measuring tape. **FRET**, Förster Resonance Energy Transfer, is a non-radiative handoff of energy from one excited fluorophore, the **donor**, to a second fluorophore, the **acceptor**, sitting very close by. No photon is exchanged in the handoff. For it to work, two conditions must hold: the molecules must be within roughly 1 to 10 nm of each other, and their spectra must overlap, with the donor's emission matching the acceptor's absorption. When both are met, exciting the donor produces emission from the acceptor instead. If you treat the pair as a single unit, the effect looks like a greatly enlarged Stokes shift.

What makes FRET extraordinary is how sharply it depends on distance. The efficiency is

$$E = \frac{1}{1 + (r/R_0)^6}$$

where $r$ is the donor-acceptor separation and $R_0$, the **Förster radius**, is the distance at which transfer is 50 percent efficient. For common pairs $R_0$ is only a few nanometers, often around 4 to 6 nm. The sixth power is the key (_{numref}`Fig. %s <fret_efficiency>`_): efficiency plunges from near-total to near-nothing over a span of a couple of nanometers, which means the simple act of measuring how much the acceptor glows tells you the distance between the two molecules with nanometer sensitivity.

```{figure} ../figures/fret_efficiency.png
---
width: 75%
name: fret_efficiency
align: center
---
FRET efficiency as a function of donor-acceptor distance. At $r = R_0$ the efficiency is exactly 50 percent. The sixth-power dependence makes the transition extremely steep, so a change of one or two nanometers swings the efficiency from high to low. This is what turns FRET into a molecular ruler.
```

That is a remarkable trick. The diffraction limit, which we will study in {ref}`Chapter 6 <chap6>`, keeps an ordinary light microscope from resolving features closer than a couple of hundred nanometers, yet FRET reports on separations a hundred times smaller. Build a sensor in which two parts move apart when, say, a protein binds a target, label each part with one half of a FRET pair, and the acceptor's brightness becomes a live readout of that motion. We will see FRET sensors put to work later in the course, in the advanced-techniques material of {ref}`Chapter 8 <chap8>`.

With the physics of a single fluorophore in hand, the obvious next question is which fluorophores to use. That is the subject of {ref}`the next section <chap4_2>`.
