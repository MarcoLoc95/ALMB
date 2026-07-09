# Contrast techniques for transmitted light microscopy

A perfectly transparent specimen in brightfield illumination is, by definition, invisible. Light passes through it without any change in amplitude, and the detector records a featureless bright field. Yet the specimen _is_ there: it bends wavefronts, it diffracts light, it shifts the phase of the transmitted wave. The challenge is to convert these invisible optical effects into visible intensity changes that a camera (or your eye) can detect.

Over the past century, microscopists have developed several ingenious techniques to do exactly this. All of them work by manipulating light in specific conjugate planes of the Köhler illumination system. In this section we will cover the three most important ones: darkfield microscopy, phase contrast, and differential interference contrast (DIC). Together with brightfield, they form the family of _transmitted-light contrast techniques_, sometimes collectively referred to as _label-free_ imaging because they require no fluorescent dyes or stains.

## Darkfield microscopy

### The principle

Darkfield is conceptually the simplest contrast technique. The idea is to illuminate the specimen so that the direct (unscattered) light never reaches the detector, while light that is *scattered* or *diffracted* by the specimen does. The result is a dark background with bright features: structures in the sample appear as glowing objects against blackness.

To separate the two, darkfield uses **annular illumination**. An opaque disk (a *patch stop*) is placed at the center of the condenser's aperture plane, blocking all on-axis light and leaving only an outer ring open. The condenser turns this ring into a **hollow cone** of oblique light that illuminates the specimen. Note that this stop sits in an *aperture* plane, not a *field* plane, so it does not cast a dark hole onto the sample: every open point of the ring produces an oblique beam that covers the entire field of view, and the specimen, center included, is lit uniformly.

The separation of direct and scattered light happens at the **objective's back focal plane**. Recall from the discussion of conjugate planes that this plane is optically equivalent to the condenser aperture: whatever pattern sits in the illumination aperture is reproduced there. The undiffracted light carries only the oblique illumination angles, so it is focused into a bright **ring** at the back focal plane, an image of the condenser annulus. Light scattered by the specimen, in contrast, is redirected into new angles and spreads across the rest of that plane. Placing a matching **ring stop** at the back focal plane therefore blocks the direct light while letting the scattered light pass on through the tube lens to form the image ({numref}`Fig. {number} <darkfield_scheme>`).

```{figure} ../figures/chap3_darkfield_scheme.png
---
width: 100%
name: darkfield_scheme
align: center
---
Darkfield microscopy with two forms of annular illumination. In both cases a hollow cone of light illuminates the specimen, and the undiffracted (direct) light is focused by the objective into a ring at its back focal plane, where a ring stop blocks it; only light scattered by the specimen passes around the stop and is relayed by the tube lens to form a bright image on a dark background. The two settings differ only in whether the hollow cone is focused on the specimen or delivered as collimated oblique beams; both exclude the direct light with the same ring stop at the objective back focal plane.
```

There is also a second, purely geometric way to keep the direct light out, without any ring stop: make the illumination cone *steeper than the objective can collect*. If the hollow cone's half-angle exceeds the objective's acceptance angle, the direct light simply passes outside the objective aperture and never enters it. This works whenever the **illumination NA is higher than the objective's collection NA**, which is easy to arrange with low- and medium-power objectives (up to about 40x). For high-NA oil-immersion objectives the condition is harder to meet: it requires special darkfield condensers of very high NA (up to ~1.4), or an objective with an internal iris that stops its effective collection NA down below the illumination NA.

```{tip}
Darkfield imaging is extremely sensitive to dust, scratches, and air bubbles, because all of these scatter light and will appear as bright features. A clean cover glass and clean optics are essential. On the positive side, this sensitivity is precisely what makes darkfield so useful for detecting very small objects.
```

### Alternative configuration: axial illumination

The scheme above uses annular illumination and a ring stop, but darkfield can also be produced with ordinary **axial (on-axis) illumination** and a single **central stop** in the objective back focal plane. This is the historically original form, sometimes called *central dark-ground*.

The light path is straightforward. The condenser sends a collimated beam straight down the axis onto the specimen. The undiffracted (direct) light carries only the axial direction, so the objective focuses it to a single spot at the **center** of its back focal plane. Light diffracted by the specimen is redirected into other angles and lands **off-center** in that plane, at a radius that grows with spatial frequency. A small opaque **central stop** at the back focal plane therefore removes the direct light while the diffracted light passes around it, and the tube lens rebuilds a bright image on a dark background ({numref}`Fig. {number} <darkfield_alt>`).

```{figure} ../figures/chap3_darkfield_alt.png
---
width: 100%
name: darkfield_alt
align: center
---
Darkfield with axial illumination. The condenser illuminates the specimen with an on-axis beam, so the direct light focuses to the center of the objective back focal plane and is removed by a central stop. Only light scattered by the specimen lands off-axis, passes around the stop, and is relayed by the tube lens to the image.
```

The essential requirement is that the central stop must be large enough to cover the entire disk that the direct light fills at the back focal plane. Each point of the condenser aperture produces one illumination direction, whose zero-order light lands at a back-focal-plane radius proportional to its angle. The aperture center maps to the plane center, but the aperture edge maps to a ring further out. If the condenser diaphragm is opened, the direct light spreads into an annulus wider than the central stop, and the oblique zero-order beams slip past the stop and reappear as background. For this reason the condenser diaphragm must be kept nearly closed, so that the whole zero-order disk stays inside the stop. Equivalently, the illumination NA must be small.

**Advantages.** The setup is mechanically simple: a plain axial beam and a single central stop, with no annular condenser insert to align. It is a clean high-pass spatial filter, removing the DC background and low frequencies while passing the fine structure and edges, which makes it useful as an intuitive teaching case and for simple edge enhancement.

**Disadvantages.** The requirement of a nearly closed condenser diaphragm is limiting. It forces a low illumination NA, so the images are dim, and any residual direct light or glare that is not perfectly on-axis leaks around the small central stop and degrades the contrast. The technique does not extend well to high-NA objectives. These are exactly the shortcomings that the annular-condenser and ring-stop configuration avoids: by parking the direct light at a thin ring at high radius, it frees the entire remaining aperture to collect scattered light, giving brighter, cleaner, higher-NA darkfield. In practice, that is why the annular scheme is the standard implementation and axial illumination is mostly of historical and conceptual interest.

## Phase contrast microscopy

### The problem: phase objects

Most biological specimens (living cells, bacteria, thin tissue sections) are nearly transparent. They absorb very little light, so they are invisible in brightfield. However, they do interact with light in a subtler way: different parts of the specimen have slightly different refractive indices (the cytoplasm, the nucleus, organelles, membranes), and these refractive index variations cause the transmitted wave to be _delayed_ (phase-shifted) relative to the undeviated background light. Such specimens are called **phase objects**: they change the _phase_ of the wave, not its _amplitude_ ({numref}`Fig. {number} <phase_objects>`).

```{figure} ../figures/chap3_phase_objects.png
---
width: 100%
name: phase_objects
align: center
---
Amplitude objects versus phase objects. An amplitude object (such as a stained section) absorbs light, reducing the wave's amplitude. A phase object (such as a living cell) is transparent but retards the wave, shifting its phase. The human eye and standard detectors are sensitive only to intensity (amplitude squared), not to phase, which is why phase objects are invisible in brightfield.
```

The human eye and camera sensors measure _intensity_, which is proportional to the square of the amplitude. Phase differences, by themselves, produce no intensity changes. The wave that passes through a cell and the wave that passes next to it have the same amplitude; they only differ in phase. When these waves reach the detector, they produce the same intensity reading, and the cell is invisible.

The challenge, then, is to convert phase differences into amplitude (intensity) differences. This is precisely what phase contrast microscopy achieves.

### Zernike's insight

The solution was devised by the Dutch physicist Frits Zernike in the 1930s (for which he received the 1953 Nobel Prize in Physics). Zernike's reasoning went as follows.

The light transmitted by a phase object can be decomposed into two components:

1. The **undeviated (direct) light**: the zeroth-order component that passes through the specimen without being scattered. This is essentially the background illumination.
2. The **diffracted light**: the light scattered by the refractive index structures in the specimen. This carries all the information about the specimen's structure.

For a thin, weakly scattering phase object, the diffracted light is phase-shifted by approximately $\lambda/4$ (90°) relative to the direct light. This is a consequence of the scattering process itself. The total transmitted wave is the sum of the direct and diffracted components, and because they are 90° out of phase, the resulting intensity is nearly the same as the direct light alone. The specimen is invisible.

Zernike's key idea: if we could shift the phase of the direct light by an _additional_ $\lambda/4$ (either advancing or retarding it), the direct and diffracted components would end up either perfectly in phase or perfectly out of phase (0° or 180° relative phase). In the first case, they would interfere constructively, making the specimen appear brighter than the background (_bright_ or _negative_ phase contrast). In the second case, they would interfere destructively, making the specimen appear darker than the background (_dark_ or _positive_ phase contrast, the more common mode).

### A phasor picture

Zernike's argument becomes much clearer if we represent each wave as a **phasor**: a vector in the complex plane whose length is the amplitude and whose angle is the phase. Dropping the common time factor $e^{-i\omega t}$, the light emerging from a weak phase object is

$$
U_0\,e^{-i\varphi} \;=\; U_0\bigl(\cos\varphi - i\sin\varphi\bigr),
$$

where $\varphi$ is the small extra phase retardation introduced by the specimen. For a weak phase object $\varphi \ll 1$, so we can expand:

$$
U_0\,e^{-i\varphi} \;\approx\; U_0\,(1 - i\varphi) \;=\; \underbrace{U_0}_{\text{undiffracted}} \;\underbrace{-\, i\varphi U_0}_{\text{diffracted}}.
$$

This is the key decomposition. The transmitted wave splits into two phasors:

- the **undiffracted** (direct) wave $U = U_0$, the strong background, which we take to point along the real axis, and
- the **diffracted** wave $D = -i\varphi U_0$, whose amplitude $\varphi U_0$ is small and, crucially, whose factor $-i$ means it is rotated by exactly $90^\circ$ relative to $U$.

That $90^\circ$ means that scattering by a pure phase object necessarily produces light in quadrature with the background.

**Why the object is invisible in brightfield.** Adding the two phasors, $U + D$ forms a right triangle with a long horizontal side $U_0$ and a short vertical side $\varphi U_0$. Its length is

$$
|U + D| = U_0\sqrt{1 + \varphi^2} \approx U_0\Bigl(1 + \tfrac{1}{2}\varphi^2\Bigr).
$$

To first order in $\varphi$ the length is unchanged: the phase object rotates the tip of the resultant slightly but does not change its magnitude. Since the detector sees intensity (length squared), the only difference from the background is of order $\varphi^2$, which is negligible. The specimen is there in the phase, but not in the intensity.

### Making phase visible: the $90^\circ$ shift

The diffracted phasor $D$ is perpendicular to the background $U$, so it changes the *direction* of the resultant but not its *length*. The remedy is to rotate the **undiffracted** wave by $90^\circ$ so that it becomes **collinear** with $D$. Then the two phasors add (or subtract) along the same line, and the small quantity $\varphi$ finally shows up as a change in length, hence in intensity.

This is exactly what the phase ring at the objective back focal plane does: it multiplies the direct light (and only the direct light, which is concentrated in the ring) by $e^{\pm i\pi/2} = \pm i$. There are two choices of sign, and they give the two complementary modes of phase contrast:

**Advancing the direct light** ($U \to +iU$):

$$
U + D \;\to\; iU_0 - i\varphi U_0 \;=\; i\,(1 - \varphi)\,U_0,
\qquad I \propto (1-\varphi)^2 .
$$

The resultant is now shorter than the background wherever $\varphi > 0$. Dense structures (larger $\varphi$) appear **darker** than the surroundings. This is *positive* (dark) phase contrast, the mode used on most routine microscopes.

**Retarding the direct light** ($U \to -iU$):

$$
U + D \;\to\; -iU_0 - i\varphi U_0 \;=\; -i\,(1 + \varphi)\,U_0,
\qquad I \propto (1+\varphi)^2 .
$$

Now the resultant is longer, and dense structures appear **brighter** than the background. This is *negative* (bright) phase contrast.

In both cases the trick is the same: rotate the reference wave so it lies along the diffracted wave. Only the sign differs, deciding whether the two add or cancel. And note that the intensity now varies as $(1 \pm \varphi)^2 \approx 1 \pm 2\varphi$, that is, **linearly** in the specimen's phase to first order, which is why phase contrast gives a faithful, roughly quantitative rendering of optical path differences rather than the edge-only response of darkfield.

### Attenuating the direct light to boost contrast

There is one more improvement. The visible signal is the *difference* in length between the object resultant and the background, but that difference sits on top of a large background $U_0$. The fractional modulation is therefore small, because $D$ is tiny compared to $U$.

To fix this, the phase ring is also made **partially absorbing** (a neutral-density, or OD, coating on the ring). It attenuates the strong direct light by a factor $t < 1$, while the diffracted light, spread over the rest of the back focal plane, passes essentially untouched. With attenuation, the dark mode gives

$$
U + D \;\to\; i\,(t - \varphi)\,U_0,
\qquad
C \;=\; \frac{I - I_{\text{bg}}}{I_{\text{bg}}} \;=\; \frac{(t-\varphi)^2 - t^2}{t^2} \;\approx\; -\,\frac{2\varphi}{t}.
$$

The contrast scales as $2\varphi/t$: the more the direct light is knocked down (smaller $t$), the larger the fractional intensity swing produced by the same specimen phase $\varphi$. Physically, attenuating $U$ brings the two interfering phasors closer to equal length, and interference between two comparable beams produces a much deeper modulation than interference between a huge beam and a tiny one. In practice the ring transmits only some 10 to 30 % of the direct light, a compromise between contrast (which wants heavy attenuation) and image brightness (which wants light).

```{figure} ../figures/chap3_phase_phasor.png
---
width: 90%
name: phase_phasor
align: center
---
Phasor picture of phase contrast. The transmitted wave splits into a strong undeviated component $U$ (orange) and a weak diffracted component $D=-i\varphi U_0$ (teal), which the factor $-i$ places $90^\circ$ from $U$. (a) In brightfield the two are perpendicular, so the resultant length, and hence the intensity, is unchanged to first order and the object is invisible. (b) Advancing $U$ by $+90^\circ$ makes it collinear with $D$ and the two subtract: the resultant is shorter than the background, so the specimen appears dark (positive phase contrast). (c) Retarding $U$ by $-90^\circ$ makes them add: the resultant is longer and the specimen appears bright (negative phase contrast). (d) Attenuating the direct light by a factor $t$ brings $U$ and $D$ to comparable lengths, deepening the modulation; the contrast scales as $C\approx 2\varphi/t$. The specimen phase $\varphi$ is exaggerated for clarity.
```

### The phase plate

How do we selectively shift the phase of the direct light without affecting the diffracted light? This is where the conjugate plane structure of Köhler illumination becomes essential.

In a phase contrast microscope, the condenser is equipped with an **annular diaphragm** (a ring-shaped opening) that produces a hollow cone of illumination, similar to darkfield. The direct, undeviated light passes through the specimen and is focused by the objective into a ring-shaped image of the condenser annulus at the **back focal plane** of the objective (an aperture conjugate plane). The diffracted light, on the other hand, is spread across the entire back focal plane.

A **phase plate** is placed at the back focal plane of the objective ({numref}`Fig. {number} <phase_contrast_scheme>`). This plate has a ring-shaped groove (or ridge) whose position and size match the image of the condenser annulus exactly. The groove introduces an additional $\lambda/4$ phase shift to the direct light passing through it, while the diffracted light, which is spread over the rest of the plate, passes through unaltered. The phase plate also typically attenuates the direct light (the ring region is partially absorbing), which improves contrast by bringing the amplitudes of the direct and diffracted components closer together.

```{figure} ../figures/phase_contrast_scheme.png
---
width: 90%
name: phase_contrast_scheme
align: center
---
Principle of phase contrast microscopy. The condenser annulus produces a ring-shaped illumination cone. At the back focal plane of the objective, the direct light passes through the phase ring, which advances (or retards) it by $\lambda/4$ and attenuates it. The diffracted light passes through the rest of the plate unaltered. When the two components recombine at the image plane, their interference produces intensity variations that reveal the specimen's phase structure.
```

When the direct and diffracted components recombine at the image plane, their relative phase is now either 0° or 180° (depending on the sign of the phase shift), and the interference produces intensity changes that make the phase structures visible. Dense structures like the nucleus, which retard the wave more, appear darker or brighter than the surrounding cytoplasm.

```{tip}
Phase contrast is by far the most widely used technique for routine observation of living cells. If you look through the eyepiece of almost any cell culture microscope in a biology lab, you are looking at a phase contrast image. The characteristic bright halo around cells and the dark appearance of the nucleus are the hallmarks of this technique.
```

### Limitations of phase contrast

Phase contrast is powerful but not perfect. The most visible artifact is the **halo effect**: a bright or dark halo surrounding edges of specimens where there is a sharp change in optical path length. This halo arises because the phase ring in the back focal plane also intercepts some of the diffracted light near the ring (low-order diffracted light overlaps spatially with the direct light image). This diffracted light receives the same phase shift and attenuation as the direct light, distorting the image near edges.

Another limitation is that the phase plate absorbs some of the fluorescence emission as well. If you try to combine phase contrast with fluorescence imaging, the phase ring will attenuate any fluorescence that happens to pass through it, reducing the overall fluorescence signal and slightly degrading the effective NA. For simultaneous transmitted-light and fluorescence imaging, DIC (discussed next) is often a better choice.

## Differential interference contrast (DIC)

### The principle

Differential interference contrast, developed by Georges Nomarski in 1955, takes a completely different approach to visualizing phase objects. Instead of comparing diffracted light with direct light (as in phase contrast), DIC compares the phase of the wave at two points in the specimen that are separated by a tiny lateral distance, typically less than the resolution limit of the objective. The technique is sensitive to _gradients_ of optical path length rather than the absolute path length itself. The result is an image that has a distinctive relief-like, three-dimensional appearance, as if the specimen were a landscape illuminated from the side.

### How it works

DIC uses polarized light and a pair of specialized prisms called **Wollaston prisms** (or **Nomarski prisms**, which are a modified design). The optical path is as follows ({numref}`Fig. {number} <dic_scheme>`):

1. Unpolarized light from the source passes through a **polarizer**, producing linearly polarized light.
2. A first Wollaston prism (located near the condenser) splits this polarized beam into two beams with orthogonal polarizations, separated by a very small lateral distance (the _shear_, typically 100-200 nm). The two beams travel through the specimen on nearly identical paths, offset by the shear distance.
3. Both beams pass through the specimen, acquiring phase shifts that depend on the local optical path length at their respective positions.
4. After the objective, a second Wollaston prism recombines the two beams into a single beam. The recombined beam has a polarization state that depends on the _phase difference_ between the two sheared beams, which in turn depends on the gradient of the refractive index across the shear distance.
5. An **analyzer** (a second polarizer, oriented at 90° to the first) converts the polarization changes into intensity variations. Where the phase gradient is zero (uniform regions), the two beams cancel and the image is dark. Where there is a gradient, light passes through the analyzer, and the feature appears bright.

```{figure} ../figures/dic_scheme.png
---
width: 90%
name: dic_scheme
align: center
---
Principle of differential interference contrast. A polarizer and a Wollaston prism split the illumination into two orthogonally polarized beams separated by a sub-resolution shear distance. After passing through the specimen, a second Wollaston prism and an analyzer recombine the beams. The resulting intensity encodes the gradient of the optical path length across the shear direction.
```

### Advantages over phase contrast

DIC has several practical advantages. First, it does not produce halos, because it does not rely on a phase ring that can intercept diffracted light. The images have a clean, crisp appearance. Second, DIC produces very thin optical sections: because the contrast arises from local phase gradients rather than the total phase shift through the specimen, out-of-focus structures contribute very little to the image. This makes DIC excellent for imaging thick, transparent specimens. Third, DIC is fully compatible with fluorescence: the Wollaston prisms and polarizers can be removed from the light path, and no element in an aperture conjugate plane absorbs fluorescence.

The relief-like appearance of DIC images is visually striking, but it can also be misleading. The apparent "shadow" direction depends on the orientation of the shear, not on the actual three-dimensional shape of the specimen. Rotating the specimen by 90° will change which edges appear bright and which appear dark. It is important to remember that DIC reveals _phase gradients in one direction_, not true topography.

### Nomarski versus classical DIC

In the original design by Smith (1947) and the later refinement by Nomarski (1955), the Wollaston prisms sit at the front focal plane of the condenser and at the back focal plane of the objective, respectively (both aperture conjugate planes). Nomarski's modification uses a modified prism that can be placed _outside_ the back focal plane of the objective, which is more practical because the back focal plane of a high-NA objective is usually inside the lens barrel and physically inaccessible. This is why the technique is often referred to as Nomarski DIC, and why the Nomarski prism has become the standard component in modern microscopes.

```{tip}
DIC is the technique of choice when you need to overlay a transmitted-light reference image on a fluorescence dataset. Many cell biologists use DIC to show the outline of cells and then overlay the fluorescence channels to show where specific proteins are located. The clean optical sectioning and absence of halos make DIC ideal for this purpose.
```

## Summary: choosing the right technique

Each of the four transmitted-light modes we have discussed has its strengths and its niche:

**Brightfield** is the simplest and works well for stained or naturally pigmented specimens. It provides no contrast for transparent, unstained biological material.

**Darkfield** produces high-contrast images of scattering objects against a black background. It excels at detecting very small particles (nanoparticles, bacteria, thin filaments) and is useful when you need extreme sensitivity to scattered light. Its main limitation is that the image does not convey information about the internal structure of thick specimens.

**Phase contrast** is the workhorse for routine live-cell observation. It converts phase shifts into intensity and reveals the internal structure of transparent cells (nucleus, organelles, membranes). The halo artifact and the interference with fluorescence are its main drawbacks.

**DIC** produces relief-like images with excellent optical sectioning, no halos, and full compatibility with fluorescence. It is the premium transmitted-light technique for research imaging. Its main disadvantage is cost (the Wollaston prisms and polarizers are expensive) and the fact that it does not work well with plastic dishes or birefringent specimens.

In practice, most research microscopes are equipped with all four modes, and experienced microscopists switch between them depending on the specimen and the question at hand.
