# Fourier optics in microscopy

So far we have built the machinery: in the far field we measure the Fourier transform of the object, a converging lens brings that transform into its back focal plane, and the finite objective behaves like a circular aperture that discards the high spatial frequencies, spreading every point into an Airy disk. All of this was, admittedly, rather abstract. In this section we cash in that theory. We will learn to look at an image as a spectrum of spatial frequencies, to describe blurring as a single elegant operation called convolution, and to understand precisely what image processing can and cannot recover. These ideas underpin deconvolution, pixel reassignment and even the way we honestly measure the resolution of a microscope from the data itself.

## Images in terms of spatial frequencies

Let us start from the simplest possible image: a sinusoidal grating, a pattern of stripes whose brightness varies as a cosine. This is the spatial equivalent of a pure musical tone, and just like a tone it is described by only a handful of numbers. It has an **amplitude** (the contrast between bright and dark stripes), a **frequency** (how tightly the stripes are packed), a **direction** (the orientation of the stripes) and a **phase** (where the bright stripes sit).

In the Fourier transform, this grating collapses to something remarkably compact: a single pair of bright points placed symmetrically around the center, plus the unavoidable DC component at the very center (the average brightness). Each of the grating's four properties maps onto a property of that pair of points ({numref}`Fig. {number} <grating_props>`):

- the **direction** of the stripes sets the orientation of the two points around the center;
- the **frequency** of the stripes sets their distance from the center, so a finer grating pushes the points farther out;
- the **phase** of the stripes sets the phase of the two points, without changing where they sit or how bright they are;
- the **amplitude** sets their brightness.

:::{raw} html
<iframe src="../content/grating_fourier_widget.html" width="100%" height="620px" frameborder="0" style="border: none;"></iframe>
:::

This is the heart of the matter. Any image, no matter how complicated, can be written as a sum of such gratings, exactly as any sound can be written as a sum of tones. Adding just a few gratings already produces recognizable structure; adding thousands reconstructs the picture faithfully. The Fourier transform of a full image is therefore a map that tells us, for every possible direction and frequency, how much of that particular grating is present and with what phase.

There is a simple and extremely useful rule for reading these maps. The **center of the transform holds the low frequencies**: the coarse, slowly varying content, the overall shapes and the average brightness. The **outskirts hold the high frequencies**: the sharp edges, the fine textures and the small details. This is precisely the intuition we met with the rolling hills at the start of the chapter, where the smooth sky sat at the lowest frequencies and the grass blades at the highest, now made quantitative.

:::{raw} html
<c><iframe src="../content/spatial_filter_widget.html" width="90%" height="800px" frameborder="0" style="border: none;"></iframe></c>
:::

### Noise in the Fourier space

Everything we have done so far assumed a clean image. Real measurements are not clean, and noise is the reason spatial filtering is useful rather than magical. In fluorescence microscopy the dominant contribution is _shot noise_: light arrives as discrete photons, and the number counted in a pixel during the exposure follows a Poisson distribution, so it fluctuates from pixel to pixel even when the sample is perfectly uniform. On top of it sits the read noise of the detector. What matters for us is a property both share: the fluctuation in one pixel is independent of the fluctuation in its neighbours.

That single property decides everything about how noise looks in Fourier space. Transforming noise produces no compact feature at all, but simply another random field, with, on average, the same power at every spatial frequency. This is what is meant by calling such noise **white**. The transform of noise is noise ({numref}`Fig. {number} <noise_fourier>`), spread thinly and evenly over the entire spectrum, and there is nowhere to aim a mask.

```{figure} ../figures/chap6_noise_fourier.png
---
width: 100%
name: noise_fourier
align: center
---
Noise transforms into noise. The noise alone (left) is grainy in real space and just as grainy in Fourier space, filling the spectrum uniformly rather than collecting anywhere. The noise-free image (centre) has a spectrum concentrated near the origin. The measured image (right) is the sum of the two, so its spectrum is the signal near the centre and the noise floor everywhere, including out where the signal has almost nothing left to say. Photograph by Krzysztof P. Jasiutowicz, CC BY-SA 2.5, via Wikimedia Commons.
```

Now put the two spectra side by side. The signal is concentrated at low frequencies and its power falls steeply as we move outwards, while the noise floor stays flat all the way to the edge. The two curves must therefore cross ({numref}`Fig. {number} <noise_spectra>`). Below the crossing the image is mostly signal; above it, mostly noise.

```{figure} ../figures/chap6_noise_spectra.png
---
width: 90%
name: noise_spectra
align: center
---
Radially averaged power of the three images above. The signal (blue) falls by more than four orders of magnitude across the spectrum, while the noise (grey) is flat. Beyond the frequency where they cross, the measured image (orange) is essentially pure noise.
```

This picture explains both the power and the limits of filtering. Its power: a low-pass filter placed near the crossing throws away the band where there is almost no signal left to lose and a great deal of noise to gain by discarding, which is why smoothing genuinely improves the appearance of a noisy image. Its limit: below the crossing, signal and noise sit at exactly the same spatial frequencies, superimposed. A mask can only multiply a frequency as a whole; it has no way of telling which part of the amplitude at that frequency came from the sample and which part came from the photon statistics. Filtering can improve the signal-to-noise ratio by removing the frequencies where noise dominates, but it can never remove noise completely, and every attempt to push it further removes real detail along with it.

The only honest cure is more photons. Averaging $n$ independent frames adds the signal coherently and the noise incoherently, improving the signal-to-noise ratio by $\sqrt{n}$ and pushing the crossing point outwards. This is also why deconvolution is delicate: dividing by a small OTF near the cutoff amplifies whatever sits there, and what sits there is mostly noise. And it is exactly what Fourier Ring Correlation, at the end of this chapter, turns to its advantage: the noise in two independent acquisitions is uncorrelated, while the signal is identical, so the two decorrelate precisely where the noise takes over.

### The resolution limit is a spatial filtering problem

We have now called the objective a low-pass filter twice without saying what the filter actually is. Everything is in place to be precise, and the answer is that the microscope performs, in glass, exactly the operation we have been performing in software.

Recall the two equivalent statements of image formation: in real space, the image is the object convolved with the point spread function, and in Fourier space that convolution becomes the multiplication $\hat i(\vec k) = \hat o(\vec k)\cdot\text{OTF}(\vec k)$. Read the second one again with the eyes of this section. The microscope takes the spectrum of the object and multiplies it by a fixed mask. That is a spatial filtering operation, performed by the optics, and the only difference from the filters we designed ourselves is that we do not get to choose this one ({numref}`Fig. {number} <resolution_lowpass>`).

```{figure} ../figures/chap6_resolution_lowpass.png
---
width: 100%
name: resolution_lowpass
align: center
---
Imaging as a filtering operation. The object $f(x,y)$ is transformed, its spectrum $|F(u,v)|$ is multiplied by the transfer function of the objective, and the result $|G(u,v)|$ is transformed back to give the image $g(x,y)$. The OTF is zero beyond the cut-off (dashed circle), so those frequencies are not attenuated but erased: the tower survives, its tracery does not.
```

For a circular pupil the mask is a disk. Frequencies that fall inside it are transmitted, frequencies that fall outside it are not, and the edge of the disk sits at the cut-off

$$
k_c = \frac{2\,\text{NA}}{\lambda}.
$$

The reciprocal of that cut-off, $1/k_c = \lambda/2\text{NA}$, is the Abbe limit we met in the previous section, and the point spread function belonging to such a band-limited pupil is exactly the Airy disk we derived there. The diffraction limit, the Airy disk and the cut-off of a low-pass filter are three descriptions of one and the same fact.

Saying it this way makes the consequences unusually clear. Inside the passband the frequencies are attenuated, some of them severely, but they are still present in the recording; they can be boosted back up, which is precisely what deconvolution does, subject to the noise we have just discussed. Beyond the cut-off the frequencies are multiplied by zero. They are not weak, not buried, not hiding under the noise: they are absent. No filter, no algorithm and no amount of contrast stretching can recover a number that was multiplied by zero, which is why the diffraction limit is a genuine limit and not merely a nuisance.


## Convolution and deconvolution

We are now ready for what is arguably the most important equation in this whole chapter. Every real image is a blurred version of the true object, and the blurring agent is the point spread function. Because the imaging system responds to each individual point of the object by drawing a PSF there, scaled by how bright that point is, the recorded image is built by stamping a copy of the PSF at every object point and summing them all up. This "stamp everywhere and add" operation is called a **convolution**, written with the symbol $\ast$:

$$
i(\vec r) = (o \ast \text{PSF})(\vec r) = \int o(\vec r\,') \, \text{PSF}(\vec r - \vec r\,') \, d\vec r\,'
$$

where $o$ is the true object, $i$ is the measured image and PSF is the point spread function. In words: the image is the object convolved with the point spread function. This single line summarizes image formation in a microscope.

Convolutions are awkward to compute and even more awkward to reason about directly. This is where Fourier optics rewards us handsomely, through the **convolution theorem**: a convolution in real space becomes a plain multiplication in frequency space. Transforming the equation above, we get

$$
\hat i(\vec k) = \hat o(\vec k) \cdot \text{OTF}(\vec k)
$$

where the hats denote Fourier transforms and $\text{OTF} = \mathcal{F}\{\text{PSF}\}$ is the **optical transfer function**. Its modulus is called the modulation transfer function (MTF) and tells us how strongly each spatial frequency survives the trip through the microscope. The OTF is nothing other than the low-pass filter we have been describing: it is close to one for low frequencies, decreases towards higher frequencies, and drops to exactly zero beyond a cutoff set by the numerical aperture (for incoherent imaging, at a spatial frequency of $2\,\text{NA}/\lambda$). Frequencies past that cutoff are not merely attenuated; they are absent.

This reformulation suggests an irresistible idea. If the image is the object multiplied by the OTF in frequency space, why not simply divide it back out to recover the object?

$$
\hat o(\vec k) = \frac{\hat i(\vec k)}{\text{OTF}(\vec k)}
$$

This is **deconvolution**, and in an ideal noiseless world it would work perfectly. Reality intrudes in two ways. Where the OTF is small, near the cutoff, dividing by it multiplies the ever-present noise by a huge factor, and the reconstruction is swamped by amplified noise rather than restored detail. Where the OTF is exactly zero, beyond the cutoff, the division is undefined: that information was never recorded and cannot be conjured back. Naive deconvolution is therefore an unstable, ill-posed problem.

Practical deconvolution replaces the blunt division with a regularized estimate that balances sharpening against noise. The **Wiener filter** weights each frequency by how much signal it is likely to contain relative to noise, tapering the correction where the OTF is weak. **Iterative methods** such as Richardson-Lucy repeatedly refine a guess of the object while enforcing sensible constraints, most usefully that brightness cannot be negative, which suits the Poisson statistics of photon counting. These algorithms recover a great deal of the detail that lies within the passband, without exploding the noise.

The strengths and weaknesses of deconvolution follow directly from this picture. Its advantages are real:

- improved resolution and contrast within the microscope's passband;
- restoration of detail that blurring had smeared but not destroyed;
- better quantitative accuracy, since intensities are reassigned closer to their true positions;
- partial correction of spherical aberration when the PSF is measured under the same conditions;
- a cost-effective improvement, since it is done in software on existing hardware.

Its drawbacks are equally real:

- it is computationally intensive, especially in three dimensions;
- it depends critically on an accurate PSF, whether measured or modeled;
- it can introduce artifacts, ringing and spurious structures, if pushed too hard;
- it can lose genuine information if over-regularized;
- it is unreliable on noisy data, where the amplification problem bites hardest.

The honest bottom line is that deconvolution optimally restores the frequencies the microscope actually captured, but it does not break the diffraction limit: it cannot recover what was lost beyond the cutoff.


## Pixel reassignment

Confocal microscopy improves resolution and provides optical sectioning by placing a pinhole in front of the detector, rejecting out-of-focus and off-axis light. There is a catch familiar to every confocal user: the tighter the pinhole, the better the resolution but the less light reaches the detector, so the sharpest setting is also the noisiest. It is natural to ask whether we can keep the resolution gain without paying in photons. Pixel reassignment is the elegant answer.

The trick, known as **image scanning microscopy** (ISM), is to replace the single-point detector behind the pinhole with a small array of detectors, a miniature camera. At every position of the scanning spot we now record not one number but a little sub-image of the local PSF. The key insight, due originally to Colin Sheppard, is that a photon landing on an off-center detector element did not most likely come from directly under the excitation spot, nor from directly under that element, but from a point roughly halfway between the two. This is because the effective PSF of the system is the product of the excitation and detection PSFs, and that product peaks between their centers. The correct thing to do, therefore, is to shift, or **reassign**, each off-center sub-image inward by about half of its offset before summing everything together ({numref}`Fig. {number} <ism>`).

```{figure} ../figures/ism.png
---
width: 90%
name: ism
align: center
---
Pixel reassignment in image scanning microscopy. Light detected off-axis most likely originated from a point between the excitation and detection PSF peaks, so each sub-image is shifted inward before all are summed.
```

The payoff is a resolution improvement of a factor of $\sqrt{2}$ over the widefield or open-pinhole confocal case, equivalent to what a fully closed pinhole would give but without discarding the light, since every photon is kept and simply placed where it belongs. Combining reassignment with a subsequent deconvolution can push the gain towards a factor of two. The best-known commercial implementation is the Zeiss Airyscan detector, a small hexagonal array of elements that performs exactly this reassignment.

Its advantages and drawbacks make an instructive contrast with deconvolution. On the positive side:

- resolution improved by a factor of $\sqrt{2}$, with better contrast;
- restoration of detail while keeping essentially all the collected light;
- computational efficiency, often fast enough for near-real-time imaging;
- wide applicability across fluorescence samples;
- a cost-effective improvement over a plain confocal.

On the negative side:

- it still depends on an accurate PSF;
- it is ineffective for thick, scattering samples, where the neat geometric assumption breaks down;
- misplacement of photons can occur, though, unlike deconvolution, it does not manufacture artifacts;
- it does not reduce noise, only relocates signal.

The deeper lesson is that pixel reassignment is a physical, optical rearrangement of light that is robust and artifact-free, whereas deconvolution is a numerical inversion that is more powerful but more prone to inventing structure. The two are complementary, and modern instruments increasingly use both.

## Fourier Ring Correlation (FRC)

We close with a practical question that the theoretical resolution limits cannot answer. Abbe and Rayleigh tell us the best resolution the optics could ever achieve, but the resolution of an actual image also depends on noise, labeling density, sample contrast and drift. How can we measure the true, effective resolution of a real image, from the data alone? **Fourier Ring Correlation** provides an objective answer, and it does so with the frequency-space thinking we have developed throughout this section.

The idea, borrowed from the Fourier Shell Correlation used in cryo-electron microscopy, is to acquire two independent images of the same structure that share the same underlying signal but carry independent noise. In practice this is done by splitting the acquisition into two halves, for example odd and even camera frames, or two consecutive exposures, or two halves of the localizations in single-molecule imaging. We then compute the Fourier transform of each half and, for every ring of constant spatial frequency in the transform, measure how well the two transforms agree over that ring:

$$
\text{FRC}(k) = \frac{\displaystyle\sum_{\vec k \in \text{ring}(k)} \hat i_1(\vec k)\,\hat i_2^{\,*}(\vec k)}{\sqrt{\displaystyle\sum_{\vec k \in \text{ring}(k)} |\hat i_1(\vec k)|^2 \sum_{\vec k \in \text{ring}(k)} |\hat i_2(\vec k)|^2}}
$$

where $\hat i_1$ and $\hat i_2$ are the transforms of the two halves and the asterisk denotes complex conjugation. The behavior of this correlation as a function of frequency is exactly what our intuition predicts ({numref}`Fig. {number} <frc>`). At low frequencies both images are dominated by the same real signal, so the correlation sits close to one. At high frequencies each image is dominated by its own independent noise, which is uncorrelated between the two, so the correlation falls towards zero.

```{figure} ../figures/frc.png
---
width: 80%
name: frc
align: center
---
A Fourier Ring Correlation curve. The correlation stays near one where signal dominates and drops to zero where noise takes over; the frequency at which it crosses the threshold sets the effective resolution.
```

The frequency $k_c$ at which the curve drops below a chosen threshold, commonly the fixed value $1/7 \approx 0.143$ or the so-called three-sigma curve, marks the highest spatial frequency that is reliably present in the data. The effective resolution is simply its inverse, $d = 1/k_c$. Unlike a theoretical limit computed from wavelength and numerical aperture, this number reflects the experiment as it actually happened, noise and all, which is why it has become a standard resolution measure in super-resolution microscopy.

A couple of caveats keep the method honest. The two halves must share identical signal but truly independent noise; correlated noise, such as a fixed sensor pattern, will make the correlation look better than it should and overstate the resolution. Sample drift between the two acquisitions will do the opposite, degrading the correlation and understating it. Used carefully, however, Fourier Ring Correlation turns the abstract spectra of this chapter into a single, honest number for the resolution of a microscope, which is a fitting place to end our tour of Fourier optics.
