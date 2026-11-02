# Sub-nanometer imaging: MINFLUX and MINSTED

STED and single-molecule localization approach the diffraction problem from opposite directions. STED uses a pattern of light with a zero to decide _where_ molecules may emit, and needs no algorithm, but pays with a high light dose. SMLM lets molecules switch on at random and decides _when_ they emit, then uses many photons per molecule to locate it. In 2017 the group of Stefan Hell combined the two ideas into a technique called **MINFLUX**, for MINimal emission FLUXes, which localizes single molecules with a precision of one to a few nanometers using only a few hundred photons. It has been called a microscope that reaches the size of molecules, and it pushes fluorescence microscopy to the point where the label, not the light, becomes the limit.

## Why photons at the peak are wasted

Let us start from the last observation of the previous section. In camera-based localization, each detected photon is a sample from the PSF, and the precision is $s/\sqrt{N}$. Most photons arrive near the peak of the PSF, where the intensity is almost flat: moving the molecule by a few nanometers barely changes how many photons land there. These photons tell us that the molecule is "somewhere around here" and little more. To localize better, we must either collect more of them or make each one more informative.

How can a photon be more informative? Imagine probing the molecule with a beam whose intensity changes steeply with position. Then the number of photons the molecule emits under that beam depends strongly on where it sits. The steepest relative change in a beam profile is found not at its maximum but near a **zero**: close to the center of a doughnut beam, a displacement of a few nanometers changes the local intensity by a large factor. If we place the zero of the excitation doughnut close to the molecule and count the photons, very few photons mean the molecule is very close to the zero. Localizing a molecule by bringing it toward the zero, where it emits _minimal_ fluorescence, is the idea behind the name MINFLUX.

## Localizing with a zero

Consider first one dimension. Near its zero at position $x_0$, the intensity of a doughnut beam is well approximated by a parabola, $I(x) \approx c\,(x - x_0)^2$. Since the fluorescence emitted by a molecule at $x$ is proportional to the excitation intensity, the photon count is proportional to $(x-x_0)^2$. Now we expose the molecule twice, with the zero placed at $x_0 = -L/2$ and at $x_0 = +L/2$, and count $n_1$ and $n_2$ photons respectively (_{numref}`Fig. {number} <chap9_minflux_principle>`_). The constant $c$ drops out of their ratio:

$$
\frac{n_1}{n_2} \approx \frac{(x + L/2)^2}{(x - L/2)^2}
$$

A molecule exactly in the middle gives equal counts; a molecule closer to $+L/2$ gives fewer photons in the second exposure. From the measured ratio we can solve for $x$. The distance $L$ between the two zero positions, the size of the **probing pattern**, is chosen by the experimenter.

```{figure} ../figures/chap9_minflux_principle.png
---
width: 100%
name: chap9_minflux_principle
align: center
---
Principle of MINFLUX. Left: in one dimension, the molecule (green star) is excited twice, with the zero of a doughnut beam at $-L/2$ (solid) and at $+L/2$ (dashed); the markers show the excitation intensity the molecule receives in each exposure. Middle: the resulting share of detected photons reveals its position. Right: in two dimensions the zero is placed at the corners of a triangle and at its center; the share of photons detected at each position encodes the position of the molecule.
```

How precise is this? Counting how the photons are shared between the two exposures is again a statistical problem, and its answer can be calculated with the same tools used for camera localization. For a molecule in the center of the pattern, the result is remarkably simple:

$$
\sigma_{1D} = \frac{L}{4\sqrt{N}}
$$

Compare this with $\sigma = s/\sqrt{N}$ for a camera. The width of the PSF, $s \approx 100$ nm, has been replaced by the size of the pattern, $L$, which we are free to make small. With $L = 50$ nm and $N = 100$ photons, MINFLUX localizes to about 1 nm, while a camera with the same photons gives 10 nm.

```{tip}
The 1D result can be derived in a few lines. With the molecule at $x$ near the center, the probability that a detected photon comes from the first exposure is $p = (x+L/2)^2/[(x+L/2)^2 + (x-L/2)^2]$, which gives $p = 1/2$ and $dp/dx = 2/L$ at $x = 0$. Out of $N$ photons, the number in the first exposure follows a binomial distribution with variance $Np(1-p) = N/4$, so the fraction $n_1/N$ fluctuates by $1/(2\sqrt{N})$. Dividing by the slope $dp/dx$ converts this into a position uncertainty: $\sigma = \frac{1/(2\sqrt{N})}{2/L} = \frac{L}{4\sqrt{N}}$.
```

In two dimensions, the zero is placed at three points on a circle of diameter $L$ and usually at its center as well. The calculation gives a precision of about $L/\sqrt{8N}$ per axis for a molecule near the center, with the same scaling as in 1D. _{numref}`Fig. {number} <chap9_minflux_precision>`_ compares this with camera-based localization: at any photon number, shrinking the pattern buys precision that a camera could only reach with tens to hundreds of times more photons.

```{figure} ../figures/chap9_minflux_precision.png
---
width: 65%
name: chap9_minflux_precision
align: center
---
Localization precision as a function of the number of detected photons for camera-based SMLM (ideal, $s = 100$ nm) and for 2D MINFLUX with different pattern sizes $L$, for a molecule at the center of the pattern and no background.
```

## Iterating toward the molecule

If a smaller $L$ is always better, why not start with $L = 1$ nm? Because the parabolic model and the estimate work only if the molecule lies inside, or close to, the probing pattern. A molecule far outside the circle produces photon ratios that the estimator cannot interpret correctly, and the result is biased. Initially we know where the molecule is only to within a few hundred nanometers, the size of the PSF.

MINFLUX therefore works **iteratively** (_{numref}`Fig. {number} <chap9_minflux_iterative>`_). A first localization with a large pattern, comparable to the PSF, gives a rough position. The pattern is recentered on that estimate and shrunk, typically by a factor of two, and the measurement is repeated. After a few iterations, $L$ has reached a few tens of nanometers and the molecule sits close to the center, where the method is most precise. The beams are moved with electro-optical deflectors, which reposition them in microseconds, so the whole sequence takes a few milliseconds per molecule.

```{figure} ../figures/chap9_minflux_iterative.gif
---
width: 55%
name: chap9_minflux_iterative
align: center
---
Iterative MINFLUX localization, shown at a fixed scale (left) and magnified around the molecule (right; the dotted square in the overview). In each iteration the doughnut zero is placed at four positions (circles) and the photons detected at each are counted. The estimated position (blue cross; blue dots show the spread of repeated estimates) becomes the center of the next, smaller pattern; earlier estimates are shown in grey.
```

Two more ingredients complete the method. First, as in SMLM, only one molecule may be active within the region probed by the beam, so MINFLUX uses photoactivatable or photoswitchable fluorophores, or DNA-PAINT imagers, to switch on single molecules stochastically. MINFLUX is thus a true hybrid: stochastic switching separates the molecules, and a coordinate-targeted pattern of light with a zero localizes them. Second, the third dimension can be included by adding a doughnut with zeros above and below the focus, similar to the "bottle" beam of 3D STED.

## What MINFLUX can see

Because it localizes with few photons, MINFLUX reaches precisions of 1-3 nm in three dimensions on fixed samples. One of the first showcases was the nuclear pore complex, whose eightfold symmetric ring of nucleoporins, about 100 nm across, is a standard test structure for super-resolution: MINFLUX resolves the individual subunits, at a level of detail that approaches what electron tomography shows of the same structure (_{numref}`Fig. {number} <chap9_ex_minflux_npc>`_).

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_minflux_npc.png
---
width: 100%
name: chap9_ex_minflux_npc
align: center
---
Nuclear pore complexes imaged by transmission electron microscopy (left) and by MINFLUX (right). In the MINFLUX image, labelled nucleoporins appear as clusters arranged in rings with eightfold symmetry. Source: [reference to be added].
```

Perhaps even more striking is what MINFLUX does in time. Because only a few photons are needed per localization, a single molecule can be localized thousands of times per second, and the pattern can follow it as it moves, keeping it close to the zero. In 2023, two groups used this to track the motor protein kinesin-1 walking along microtubules, including in living cells, resolving its 16 nm steps and the substeps between them with millisecond time resolution (_{numref}`Fig. {number} <chap9_ex_minflux_kinesin>`_). Optical tweezers had measured such steps before, but only by attaching the motor to a large bead; MINFLUX observed the protein with a single small fluorophore.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_minflux_kinesin.png
---
width: 90%
name: chap9_ex_minflux_kinesin
align: center
---
Tracking kinesin with MINFLUX. The molecule is followed by repeatedly placing the probing pattern around its latest position (left); its trajectory along the microtubule shows discrete 16 nm steps over a fraction of a second (right). Source: [reference to be added].
```

## The limits of minimal fluxes

The trick of MINFLUX is the **known position and profile of the excitation beam**, and above all the assumption that a low photon count means the molecule is close to the zero. Every factor that breaks this assumption limits the method.

**Background.** Photons that do not come from the molecule (light leaking into an imperfect zero, autofluorescence, out-of-focus emitters, detector dark counts) are indistinguishable from the precious few photons near the zero. As $L$ shrinks, the signal from the molecule at the pattern positions drops roughly as $L^2$, while the background stays the same. Below a certain pattern size, background dominates and the precision gets _worse_, not better (_{numref}`Fig. {number} <chap9_minflux_background>`_). Even a background of 0.5% of the doughnut peak puts the optimum near $L \approx 20$ nm. A perfect zero, a sparse sample and low autofluorescence are therefore essential.

```{figure} ../figures/chap9_minflux_background.png
---
width: 65%
name: chap9_minflux_background
align: center
---
Calculated precision of 2D MINFLUX as a function of the pattern size $L$, for 500 detected photons and a molecule at the center of the pattern. Without background the precision improves in proportion to $L$. With a background, given as a fraction of the doughnut peak intensity, there is an optimal pattern size (dots) below which the precision degrades again. At large $L$ all curves bend upward because the doughnut is no longer parabolic over the pattern.
```

**Photobleaching and blinking.** "No photons" should mean "the molecule is at the zero", not "the molecule has bleached or entered a dark state". Robust fluorophores with predictable photophysics are required, and the algorithms must detect when a molecule has switched off.

**Stability and alignment.** Localizing to one nanometer requires knowing the position of the beam to better than one nanometer. Thermal drift, vibrations of mirrors and stage, and aberrations of the beam all enter directly into the result. MINFLUX microscopes use active stabilization of the sample position at sub-nanometer level, and their cost, of the order of a million euros, reflects this complexity.

**The label.** At this scale, the fluorophore and its linker dominate. A precision of 1 nm on the position of a dye attached to a 10-15 nm antibody does not give the position of the protein to 1 nm. Even the orientation of the dye matters: a fixed fluorophore emits as a dipole, and its tilted emission pattern can shift its apparent position by several nanometers. This is why MINFLUX work uses small labels such as self-labelling tags, and why the real resolution of nanometer-scale methods is still actively debated. Measuring structures of known geometry, such as DNA origami with dyes at defined distances, is the standard way to test the claims.

## MINSTED: localizing with a STED spot

MINSTED, introduced by the same group in 2021, applies the same idea of localizing with a steep beam profile, but with a different tool: instead of an excitation doughnut it uses the effective PSF of a STED microscope, the **E-PSF**. As we saw in {ref}`Section 9.3 <chap9_3>`, a Gaussian excitation spot combined with a STED doughnut produces a fluorescent spot that can be made a few tens of nanometers wide (_{numref}`Fig. {number} <chap9_minsted>`_, left).

In MINSTED, this E-PSF is moved on a circle of radius $R$ around the current estimate of the position of a single active molecule. The molecule emits most strongly when the E-PSF passes closest to it. Each time a photon is detected, the estimated position is moved a small step toward the point where the E-PSF was at that moment. Photon by photon, the center of the circle converges onto the molecule; meanwhile the STED power is increased and the circle shrunk, so that the E-PSF becomes smaller and its edge steeper (_{numref}`Fig. {number} <chap9_minsted>`_, right). The localization precision scales with the size of the E-PSF divided by $\sqrt{N}$, the analogue of $L/\sqrt{N}$ in MINFLUX.

```{figure} ../figures/chap9_minsted.png
---
width: 100%
name: chap9_minsted
align: center
---
MINSTED. Left: a STED doughnut shrinks the excitation spot to a small effective PSF (E-PSF). Right: simulated localization. The E-PSF (green) circles around the estimated position (dashed and dotted circles at the start and end); each detected photon moves the estimate a small step, and the trajectory (blue) converges onto the molecule (star) while the circle and the E-PSF shrink.
```

Using STED to define the probing spot brings an advantage: the doughnut also switches off any other molecule or background fluorescence around the spot, so MINSTED is less sensitive to background than MINFLUX. Because the STED beam is red-shifted and is not absorbed by the dye in its ground state, the light dose seen by the molecule remains moderate. MINSTED has reached localization precisions of about one nanometer, and later reports pushed it into the Ångström range on fixed samples (_{numref}`Fig. {number} <chap9_ex_minsted>`_).

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_minsted.png
---
width: 70%
name: chap9_ex_minsted
align: center
---
The same structure imaged with confocal microscopy, STED and MINSTED. Source: [reference to be added].
```

## Strengths and limitations

MINFLUX and MINSTED reach the highest precisions of any far-field fluorescence method, down to a few nanometers or less, with quantitative single-molecule data. They need far fewer photons than camera-based SMLM, which makes them faster, allows tracking of single molecules at kilohertz rates, and makes them compatible with some live-cell experiments. On the other hand, the instruments are complex and very expensive, the choice of fluorophores is limited to very photostable and well-behaved ones, they work best on sparse samples and struggle in dense environments, and alignment and stability are absolutely crucial. And, as always, the most impressive numbers describe the precision with which a dye is localized, which is not the same as the resolution with which the biology is seen.
