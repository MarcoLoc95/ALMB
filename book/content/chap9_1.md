# Structured illumination microscopy

The first technique of this chapter is, in a sense, the most direct heir of the Fourier optics we developed in {ref}`Chapter 6 <chap6_3>`. Structured illumination microscopy (SIM) uses no exotic fluorophores, no extreme laser powers and no special sample preparation. It simply lights up the sample with a pattern of stripes instead of uniform light, and lets mathematics do the rest. The resulting gain in resolution is modest compared with other techniques in this chapter, about a factor of two, but SIM is gentle, fast and compatible with live cells, which has made it one of the most widely used super-resolution methods.

## Moiré patterns

You have probably seen the effect on which SIM is based without knowing its name. Hold two fine combs or two pieces of mesh curtain on top of each other, or take a photograph of a striped shirt on a digital camera, and broad, wavy bands appear that are not present in either object. These are **moiré patterns**. They arise whenever two fine periodic structures are superimposed: where the lines of the two patterns fall on top of each other the overlap looks bright, and where they interleave it looks dark. Artists have long exploited the effect, and some digital artists today use it to hide portraits that only appear when a striped transparency is laid over a seemingly random image.

The key property of a moiré pattern is that its fringes are much _coarser_ than either of the patterns that produce it. This immediately suggests a strategy. Suppose the sample contains a fine structure that the microscope cannot resolve. If we illuminate it with a fine, _known_ striped pattern, the product of the two will contain coarse moiré fringes, which the microscope _can_ resolve. Since we know the pattern we put in, we should be able to work backwards from the fringes to the fine structure that generated them (_{numref}`Fig. {number} <chap9_moire>`_).

```{figure} ../figures/chap9_moire.png
---
width: 100%
name: chap9_moire
align: center
---
The moiré effect in real and Fourier space. A sample grating too fine to pass through the objective (first column) is multiplied by a known illumination pattern (second column). The product (third column) contains new components at the sum and difference of the two spatial frequencies. The difference frequency falls inside the passband of the objective (dashed circle), so the camera records coarse fringes (fourth column) that carry information about the unresolvable sample.
```

## What happens in Fourier space

Let us make this precise. In {ref}`Chapter 6 <chap6_3>` we saw that for a linear, shift-invariant imaging system the image is the convolution of the object with the PSF, and that in Fourier space this convolution becomes a simple product with the optical transfer function (OTF). For a fluorescent sample, what emits light is not the fluorophore distribution $f(\vec{r})$ alone, but the fluorophore distribution multiplied by the local excitation intensity. With uniform illumination the latter is a constant and we can forget about it. With a sinusoidal pattern of spatial frequency $\vec{k}_p$ and phase $\varphi$ we have instead:

$$
o(\vec{r}) = \Big[f(\vec{r})\cdot\big(1 + \cos(\vec{k}_p\cdot\vec{r} + \varphi)\big)\Big] * \mathrm{PSF}(\vec{r})
$$

The "1 +" makes sure that the illumination intensity is never negative: the stripes go from zero to twice the average intensity. Note that the sample and the pattern are _multiplied_, not added: where the illumination is zero, no fluorescence is emitted, whatever the fluorophore density.

Taking the Fourier transform turns the convolution into a product, and the product inside the brackets into a convolution. The transform of the constant is a delta at the origin, and the transform of a cosine is a pair of deltas at $\pm\vec{k}_p$. Since convolving any function with a shifted delta simply shifts the function, we obtain:

$$
O(\vec{k}) = \Big[F(\vec{k}) + \tfrac{1}{2}e^{i\varphi}F(\vec{k}-\vec{k}_p) + \tfrac{1}{2}e^{-i\varphi}F(\vec{k}+\vec{k}_p)\Big]\cdot \mathrm{OTF}(\vec{k})
$$

This equation is the whole of SIM. The first term is the ordinary widefield image: the spectrum of the sample, cut off by the OTF at the cutoff frequency $k_c$. The other two terms are _copies of the same spectrum, shifted by_ $\pm\vec{k}_p$. Because the OTF window does not move, the shifted copies let it see a different region of the sample spectrum. Information that originally sat at frequency $\vec{k}_p + \vec{k}$, outside the passband, now appears at $\vec{k}$, inside it. In the language of the previous section, the fine structure has been encoded into coarse moiré fringes.

## Unmixing the components

There is a catch. A single raw image contains all three components on top of each other, and from one image alone we cannot tell which part of the signal at a given frequency came from which component. The solution is to record several images while shifting the pattern sideways, changing only the phase $\varphi$. The widefield term does not depend on $\varphi$, while the two shifted terms acquire phase factors $e^{\pm i\varphi}$. With three phases, typically $0$, $2\pi/3$ and $4\pi/3$, we obtain three equations for three unknowns at every point of Fourier space, and we can solve for each component separately.

Once separated, each shifted component is moved back to its true position in Fourier space, and all components are combined into a single, larger spectrum. Where several components overlap, they are averaged with weights that favor the more reliable one, using a generalized form of the Wiener filter we met for deconvolution. An inverse Fourier transform then gives the super-resolved image.

## How far can we extend the spectrum?

Each shifted copy of the passband is a disk of radius $k_c$ centered at $\pm\vec{k}_p$, so after the reconstruction the accessible region reaches out to $k_c + k_p$ along the direction of the stripes (_{numref}`Fig. {number} <chap9_sim_fourier>`_). One pattern orientation therefore improves the resolution in one direction only. To fill the plane, the pattern is rotated: with two orientations at 90° the support takes the shape of a four-leaf clover with gaps along the diagonals, and with three orientations at 60° from each other it becomes an almost round flower. Three orientations and three phases, nine raw images in total, are the standard for two-dimensional SIM.

```{figure} ../figures/chap9_sim_fourier.png
---
width: 100%
name: chap9_sim_fourier
align: center
---
Region of Fourier space accessible to the microscope. In widefield it is a disk of radius $k_c$. A striped pattern of frequency $k_p$ adds two shifted copies of the disk along one direction. Two orientations leave gaps between the copies; three orientations give an almost isotropic extension up to $k_c + k_p$ (orange dashed circle).
```

Why not use a much finer pattern and push the copies further out? Because the pattern itself has to be projected onto the sample, and it is projected through the same objective. In practice, two or three diffracted beams are brought to interfere at the sample, and the finest pattern they can produce has a spatial frequency equal to the cutoff of the objective. So $k_p \leq k_c$, and the best SIM can do is:

$$
k_{max} = k_c + k_p \approx 2k_c \qquad\Longrightarrow\qquad d_{SIM} \approx \frac{d_{Abbe}}{2}
$$

For visible light and a high-NA oil objective this means going from roughly 250 nm to about 100-120 nm laterally.

```{tip}
A frequent question at this point: even if we could make a finer pattern, would it help? Only partially. If $k_p$ were larger than $k_c$, the shifted disks would no longer touch the central one, and the frequencies between them would be missing. The reconstructed image would contain fine detail but would lack some intermediate spatial scales, which typically shows up as ringing and false structures. Extending the spectrum is useful only if the extension is continuous.
```

The process of recording the nine raw images is shown in _{numref}`Fig. {number} <chap9_sim_raw>`_. Notice that each raw image looks like a slightly striped widefield image: the super-resolution information is hidden in subtle differences between them, invisible to the eye.

```{figure} ../figures/chap9_sim_raw.gif
---
width: 80%
name: chap9_sim_raw
align: center
---
Simulated SIM acquisition. For each of three pattern orientations the stripes are shifted to three phases, giving nine raw images. Each raw image (right) is a diffraction-limited image of the sample multiplied by the pattern (left).
```

The same reasoning extends to three dimensions. If the illumination is produced by three interfering beams instead of two, the pattern is also modulated along the optical axis, and the axial resolution doubles too. This 3D-SIM, introduced by Mats Gustafsson and colleagues in 2008, uses five phases per orientation, so fifteen raw images per plane.

## Building a SIM microscope

The original way to make the pattern is a **diffraction grating** placed in a plane conjugate to the sample. A laser beam hitting the grating is split into diffraction orders; all orders except the $0$ and $\pm 1$ are blocked, and the remaining beams interfere at the sample to form a sinusoidal pattern. Shifting the phase means translating the grating by a fraction of its period, and changing the orientation means rotating it. Mechanical rotation is slow and must be extremely reproducible, because the reconstruction assumes that the pattern is exactly where we think it is.

Modern systems therefore use a **spatial light modulator** (SLM) or a **digital micromirror device** (DMD) instead. A DMD is an array of microscopic mirrors that can each be tilted on or off thousands of times per second. Displaying a striped pattern on the DMD and imaging it onto the sample produces structured illumination without moving parts, so switching between phases and orientations takes microseconds to milliseconds instead of seconds. DMD-based SIM can even work with LEDs instead of lasers, which makes it relatively inexpensive.

Since SIM is a widefield technique, the raw images are recorded on a camera, the field of view is as large as in a conventional microscope, and frame rates of several super-resolved images per second are possible. This combination of speed and low light dose is the main reason SIM is popular for live-cell imaging. _{numref}`Fig. {number} <chap9_ex_sim_actin>`_ and _{numref}`Fig. {number} <chap9_ex_sim_widefield>`_ show typical results.

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_sim_actin.png
---
width: 60%
name: chap9_ex_sim_actin
align: center
---
Actin filaments in a fixed mouse embryonic fibroblast stained with phalloidin-TRITC, imaged in widefield and with SIM. Individual filaments and bundles that merge into a haze in the widefield image are resolved after reconstruction. Source: [reference to be added].
```

% TODO: verify source and add reference
```{figure} ../figures/chap9_ex_sim_widefield.png
---
width: 100%
name: chap9_ex_sim_widefield
align: center
---
Widefield (top-left of the dashed line) and SIM (bottom-right) images of multicolor-labelled cells. Source: [reference to be added].
```

## Exploring SIM

The widget below runs a complete, if simplified, SIM experiment: it simulates the raw images with shot noise, camera noise and out-of-focus background, separates the components, shifts them back and recombines them. Change the pattern frequency and the number of orientations and watch how the spectrum fills up. Then try to break the reconstruction: lower the photon count and see how the choice of the Wiener parameter turns noise into texture, or introduce an error in the phase steps that the algorithm does not know about.

:::{raw} html
<iframe src="../content/sim_widget.html" width="100%" height="680px" frameborder="0" style="border: none;"></iframe>
:::

## Artifacts: when the algorithm believes something false

Return for a moment to the question from the introduction of this chapter: what is the trick? In SIM, the extra information is the **known illumination pattern**: its spatial frequency, orientation, phase and contrast. The reconstruction treats this knowledge as exact. In practice these parameters are estimated from the raw data themselves, and every error propagates into the final image as a characteristic artifact.

A wrong pattern frequency or phase leaves residues of one component inside another, which typically appear as faint stripes or a honeycomb texture aligned with the pattern directions. Low modulation contrast, caused for instance by out-of-focus fluorescence or by scattering in a thick sample, weakens the shifted components so that they are buried in noise; the algorithm then amplifies noise at high frequencies, producing grainy, "hammer-stroke" or honeycomb textures that look deceptively like real structure. How strongly this happens depends on the Wiener parameter, which in most SIM software is chosen by the user: a low value gives a sharper-looking image but amplifies the noise, a high value suppresses the texture at the cost of resolution. Two reconstructions of the same raw data can look quite different. Sample motion between the nine raw images, bleaching during the acquisition, and refractive index mismatch distort the pattern in ways the algorithm cannot account for.

The lesson is that a SIM image should never be judged by itself. Look at the raw data and their Fourier transforms, check that the pattern is visible and that its contrast is good, and be suspicious of fine regular textures that follow the illumination directions. Open-source tools such as SIMcheck have been developed precisely to run these quality checks.

## Going beyond a factor of two

The limit of two comes from the fact that the emitted fluorescence is _linear_ in the illumination intensity: a sinusoidal pattern of light produces a sinusoidal pattern of emission, with the same single frequency $k_p$. If the response is made nonlinear, for instance by driving the fluorophores into saturation so that the bright stripes are clipped, the emission pattern acquires harmonics at $2k_p$, $3k_p$ and beyond. Each harmonic shifts a further copy of the spectrum into the passband. This **nonlinear** or **saturated SIM**, demonstrated by Gustafsson in 2005, reached resolutions around 50 nm, and later versions using photoswitchable fluorescent proteins brought it to living cells. The price is many more raw images, more light, and a reconstruction that is even more sensitive to noise.

Keep this idea in mind: a nonlinear response of the fluorophore to light is the key that unlocks resolution well beyond the factor of two. It is exactly the principle that STED will exploit in {ref}`Section 9.3 <chap9_3>`.

## Strengths and limitations

SIM halves the conventional resolution limit with a modest addition to a widefield microscope. It works with standard fluorophores and labelling protocols, it covers large fields of view, it is fast compared with the other techniques in this chapter, and its light dose is low enough for long live-cell recordings, especially when the pattern is generated with a DMD.

Its weaknesses all derive from its trick. The gain is limited to about a factor of two in linear SIM. The reconstruction can introduce artifacts and distortions, particularly on noisy data. The method needs bright, high-contrast samples with a clearly visible pattern, which excludes weak fluorophores, dense or thick samples, and strongly scattering tissue, where the pattern washes out before it reaches the focal plane.

If we cannot shrink the PSF by more than a factor of two with clever illumination, could we instead make the sample bigger? That is the remarkably simple idea behind the next technique.
