# Fourier optics in microscopy

So far we have built the machinery: in the far field we measure the Fourier transform of the object, a converging lens brings that transform into its back focal plane, and the finite objective behaves like a circular aperture that discards the high spatial frequencies, spreading every point into an Airy disk. In this section we try to talk more practically about images in terms of spatial frequencies, to describe blurring as a single elegant operation called convolution, and to understand precisely what image processing can and cannot recover.

## Images in terms of spatial frequencies

Let us start from the simplest possible image: a sinusoidal grating, a pattern of stripes whose brightness varies as a cosine. This is the spatial equivalent of a pure musical tone, and just like a tone it is described by only a handful of numbers. It has an **amplitude** (the contrast between bright and dark stripes), a **frequency** (how tightly the stripes are packed), a **direction** (the orientation of the stripes) and a **phase** (where the bright stripes sit).

In the Fourier transform, this grating collapses to something remarkably compact: a single pair of bright points placed symmetrically around the center, plus the unavoidable DC component at the very center (the average brightness). Each of the grating's four properties maps onto a property of that pair of points:

- the **direction** of the stripes sets the orientation of the two points around the center;
- the **frequency** of the stripes sets their distance from the center, so a finer grating pushes the points farther out;
- the **phase** of the stripes sets the phase of the two points, without changing where they sit or how bright they are;
- the **amplitude** sets their brightness.

:::{raw} html
<iframe src="../content/grating_fourier_widget.html" width="100%" height="620px" frameborder="0" style="border: none;"></iframe>
:::

This is the heart of the matter. Any image, no matter how complicated, can be written as a sum of such gratings, exactly as any sound can be written as a sum of tones. Adding just a few gratings already produces recognizable structure; adding thousands reconstructs the picture faithfully. The Fourier transform of a full image is therefore a map that tells us, for every possible direction and frequency, how much of that particular grating is present and with what phase.

There is a simple and extremely useful rule for reading these maps. The **center of the transform holds the low frequencies**: the coarse, slowly varying content, the overall shapes and the average brightness. The **outskirts hold the high frequencies**: the sharp edges, the fine textures and the small details. This is precisely the intuition we met with the rolling hills at the start of the chapter, where the smooth sky sat at the lowest frequencies and the grass blades at the highest, now made quantitative.

### Types of filters

Take the transform of a photograph, erase everything outside a small disk around the center, and transform back. Out comes the same picture, softened. The outlines are still there, the fine texture has gone. Now do the opposite and erase the middle instead. The uniform areas collapse to a flat grey, the overall brightness vanishes, and what is left behind is a map of edges. Nothing was added to the image in either case. We only chose which gratings to keep.

Those two experiments have names, and between them they cover most of what filtering does to a picture. A **low-pass** filter keeps the central disk and throws away the rest, which smooths the image and, since noise lives mostly out at high frequencies, removes a good deal of it. The bill is paid in genuine fine detail, which lived out there too. A Gaussian blur is a low-pass filter with a soft edge, nothing more. A **high-pass** filter blocks the center instead. It sharpens edges, but its real use in the lab is more mundane: uneven illumination, a haze of out-of-focus fluorescence, a gradient left by a badly seated filter, all vary slowly across the field and therefore lives at the very lowest frequencies, and a high-pass strips it out without touching the structures you actually care about.

A **band-pass** filter keeps a ring, so it selects a size. Anything much coarser than the chosen scale goes out with the background, anything much finer goes out with the noise, and what survives is whatever sits in between. Most spot detectors work this way. A **directional** filter keeps a wedge, so it selects an orientation. Here it pays to remember where the spots of a grating sit: along the direction in which the brightness varies, which is across the stripes and not along them. A wedge therefore removes the structures that run orthogonally to it and keeps the others.

:::{raw} html
<center><iframe src="../content/spatial_filter_widget.html" width="90%" height="800px" frameborder="0" style="border: none;"></iframe></center>
:::

### Filtering in the back focal plane

If the aperture of the objective acts as a mask, then the Fourier plane is a real plane sitting inside the instrument. We saw earlier in this chapter that a lens brings the far field of the sample into its back focal plane, which means the spectrum of your specimen is physically laid out in there. Several of the classical contrast methods do nothing more than employing some sort of filtering in the Fourier plane.

Place an opaque disk on the axis and you block the zero order (the undiffracted light, the part of the beam that went through), which sits in the center of the back focal plane. Everything that then recombines to form the image has been scattered by the specimen and contains information about it. The background goes black and the scatterers light up. This is exactly what we measure in **darkfield** microscopy, and in the language of this section it is a simple high-pass filter.

The reverse trick is just as common. Put a pinhole at the focus of a beam expander and only the low frequencies of the beam survive, so the speckle and the diffraction rings cast by every speck of dust upstream disappear.

### Noise in the Fourier space

Everything we have done so far assumed a clean image, but real measurements are acually always affected by noise. In fluorescence microscopy the dominant contribution is _shot noise_: light arrives as discrete photons, and the number counted in a pixel during the exposure follows a Poisson distribution. Shot noise fluctuates from pixel to pixel even when the sample is perfectly uniform. On top of it sits the _read noise_ of the detector. What matters for us is a property both share: the fluctuation in one pixel is independent of the fluctuation in its neighbours.

Transforming noise produces only another random field of noise, with, on average, the same power at every spatial frequency. This is what is meant when we refer to this as **white noise** (just like the color white, containing all the visible frequencies). The transform of noise is noise ({numref}`Fig. {number} <noise_fourier>`), spread evenly over the entire spectrum.

```{figure} ../figures/chap6_noise_fourier.png
---
width: 100%
name: noise_fourier
align: center
---
Noise transforms into noise. The noise alone (left) is grainy in real space and just as grainy in Fourier space, filling the spectrum uniformly rather than collecting anywhere. The noise-free image (centre) has a spectrum concentrated near the origin. The measured image (right) is the sum of the two, so its spectrum is dominated by the signal near the centre and by the noise everywhere else. Photograph by Krzysztof P. Jasiutowicz, CC BY-SA 2.5, via Wikimedia Commons.
```

Now let's put the two spectra side by side. The signal is concentrated at low frequencies and its power falls steeply as we move outwards, while the noise floor stays flat all the way to the edge. The two curves must therefore cross ({numref}`Fig. {number} <noise_spectra>`). Below the crossing the image is mostly signal; above it, mostly noise.

```{figure} ../figures/chap6_noise_spectra.png
---
width: 90%
name: noise_spectra
align: center
---
Radially averaged power of the three images above. The signal (blue) falls by more than four orders of magnitude across the spectrum, while the noise (grey) is flat. Beyond the frequency where they cross, the measured image (orange) is essentially pure noise.
```

This picture explains both the power and the limits of filtering. In fact, a low-pass filter placed near the crossing throws away the band where there is almost no signal left to lose and a great deal of noise to gain by discarding, which is why smoothing genuinely improves the appearance of a noisy image. At the same time, below the crossing, signal and noise sit at exactly the same spatial frequencies, superimposed. A mask can only multiply a frequency as a whole; it has no way of telling which part of the amplitude at that frequency came from the sample and which part came from the photon statistics. Filtering can improve the signal-to-noise ratio by removing the frequencies where noise dominates, but it can never remove noise completely, and every attempt to push it further removes real detail along with it.

The only honest cure is to collect more photons. Averaging $n$ independent frames adds the signal coherently and the noise incoherently, improving the signal-to-noise ratio by $\sqrt{n}$ and pushing the crossing point outwards. 

## Convolution

Every real image is a blurred version of the true object, and the blurring agent is the point spread function. Because the imaging system responds to each individual point of the object by drawing a PSF there, scaled by how bright that point is, the recorded image is built by stamping a copy of the PSF at every object point and summing them all up. This "stamp everywhere and add" operation is called a **convolution**, written with the symbol $\ast$:

$$
i(\vec r) = (o \ast \text{PSF})(\vec r) = \int o(\vec r\,') \, \text{PSF}(\vec r - \vec r\,') \, d\vec r\,'
$$

where $o$ is the true object, $i$ is the measured image and PSF is the point spread function. In words: the image is the object convolved with the point spread function.

Convolutions are awkward to compute and even more awkward to reason about in intuitive terms. This is where Fourier optics comes in handy, through the **convolution theorem**: a convolution in real space becomes a plain multiplication in frequency space. Transforming the equation above, we get

$$
\hat i(\vec k) = \hat o(\vec k) \cdot \text{OTF}(\vec k)
$$

where the hats denote Fourier transforms and $\text{OTF} = \mathcal{F}\{\text{PSF}\}$ is the **optical transfer function**. Its modulus tells us how strongly each spatial frequency survives the trip through the microscope. The OTF is nothing other than the low-pass filter we have been describing: it is close to one for low frequencies, decreases towards higher frequencies, and drops to exactly zero beyond a cutoff set by the numerical aperture.

### The resolution limit is a spatial filtering problem

Recall the two equivalent statements of image formation: in real space, the image is the object convolved with the point spread function, and in Fourier space that convolution becomes the multiplication $\hat i(\vec k) = \hat o(\vec k)\cdot\text{OTF}(\vec k)$. Read the second one again with the eyes of this section. The microscope takes the spectrum of the object and multiplies it by a fixed mask. That is a spatial filtering operation, performed by the optics, and the only difference from the filters we designed ourselves is that we do not get to choose this one ({numref}`Fig. {number} <resolution_lowpass>`).

```{figure} ../figures/chap6_resolution_lowpass.png
---
width: 100%
name: resolution_lowpass
align: center
---
Imaging as a filtering operation. The object $f(x,y)$ is transformed, its spectrum $|F(u,v)|$ is multiplied by the transfer function of the objective, and the result $|G(u,v)|$ is transformed back to give the image $g(x,y)$. The OTF is zero beyond the cut-off (dashed circle), so those frequencies are not attenuated but erased: the Dom tower of Utrecht survives, its finer details do not.
```

For a circular pupil the mask is a disk. Frequencies that fall inside it are transmitted, frequencies that fall outside it are not, and the edge of the disk sits at the cut-off

$$
k_c = \frac{2\,\text{NA}}{\lambda}.
$$

The reciprocal of that cut-off, $1/k_c = \lambda/2\text{NA}$, is the Abbe limit we met in the previous section. The diffraction limit, the Airy disk and the cut-off of a low-pass filter are three descriptions of the same phenomenon.

### Deconvolution

This reformulation suggests an irresistible idea. If the image is the object multiplied by the OTF in frequency space, why not simply divide it back out to recover the object?

$$
\hat o(\vec k) = \frac{\hat i(\vec k)}{\text{OTF}(\vec k)}
$$

This process is called **deconvolution**, and in an ideal noiseless world it would work perfectly. Reality intrudes in two ways. Where the OTF is small, near the cutoff, dividing by it multiplies the inevitable noise by a huge factor, and the reconstruction is swamped by amplified noise rather than restored detail. Second, where the OTF is exactly zero, beyond the cutoff, the division is undefined: that information was never recorded and cannot be conjured back.

Practical deconvolution replaces the blunt division with a regularized estimate that balances sharpening against noise. For instance, the **Wiener filter** weights each frequency by how much signal it is likely to contain relative to noise, tapering the correction where the OTF is weak. Iterative methods repeatedly refine a guess of the object while enforcing sensible constraints, first and foremost that brightness cannot be negative. These algorithms recover a great deal of the detail that lies within the passband, without exploding the noise.

The strengths and weaknesses of deconvolution follow directly from this. The advantages are:

- improved detail and contrast within the microscope's passband;
- restoration of detail that blurring had smeared but not destroyed;
- better quantitative accuracy, since intensities are reassigned closer to their true positions;
- partial correction of spherical aberration when the PSF is measured under the same conditions;
- a cost-effective improvement, since it is done via software.

Its drawbacks are:

- it is computationally intensive, especially in three dimensions;
- it depends critically on an accurate PSF measurement (or modelling);
- it can introduce artifacts if pushed too hard;
- it is unreliable on noisy data.

The honest bottom line is that deconvolution optimally restores the frequencies the microscope actually captured, but it does not break the diffraction limit: it cannot recover what was lost beyond the cutoff.

## Fourier Ring Correlation (FRC)

Abbe and Rayleigh tell us the best resolution the optics could ever achieve, but the resolution of an actual image also depends on noise, labeling density, sample contrast and drift. How can we measure the true, effective resolution of a real image, from the data alone? **Fourier Ring Correlation** provides an objective answer, and it does so with the frequency-space framework we have developed throughout this chapter.

The idea is to acquire two independent images of the same structure that share the same underlying signal but carry independent noise. In practice this is done by splitting the acquisition into two halves, for example odd and even camera frames, or two consecutive exposures, or two halves of the localizations in single-molecule imaging. We then compute the Fourier transform of each half and, for every ring of constant spatial frequency in the transform, measure how well the two transforms correlate over that ring:

$$
\text{FRC}(k) = \frac{\displaystyle\sum_{\vec k \in \text{ring}(k)} \hat i_1(\vec k)\,\hat i_2^{\,*}(\vec k)}{\sqrt{\displaystyle\sum_{\vec k \in \text{ring}(k)} |\hat i_1(\vec k)|^2 \sum_{\vec k \in \text{ring}(k)} |\hat i_2(\vec k)|^2}}
$$

where $\hat i_1$ and $\hat i_2$ are the transforms of the two halves and the asterisk denotes complex conjugation. At low frequencies both images are dominated by the same real signal, so the correlation sits close to one. At high frequencies each image is dominated by its own independent noise, which is uncorrelated between the two, so the correlation falls towards zero.

```{figure} ../figures/chap6_frc.gif
---
width: 100%
name: frc
align: center
---
Fourier Ring Correlation. Two acquisitions of the same neuron share the signal but not the noise. Their spectra are compared frequency by frequency, bright meaning the two agree, and averaging that agreement over a ring of growing radius traces the curve on the right. Where it crosses the $1/7$ threshold sits $k_{\text{FRC}}$, the finest spatial frequency the data can be trusted to contain. Credits: Sergb95, CC BY-SA 4.0, via Wikimedia Commons
```

The frequency $k_{\text{FRC}}$ at which the curve drops below a chosen threshold, commonly the fixed value $1/7 \approx 0.143$ or the so-called three-sigma curve, marks the highest spatial frequency that is reliably present in the data. The effective resolution is simply its inverse, $d = 1/k_{\text{FRC}}$. This number reflects the experiment as it happened, noise and all, which is why it has become a standard resolution measure in super-resolution microscopy.

A couple of caveats keep the method honest. The two halves must share identical signal but truly independent noise; correlated noise will make the correlation look better than it should and overstate the resolution. Sample drift between the two acquisitions will do the opposite, degrading the correlation and understating it. Used carefully, however, Fourier Ring Correlation turns the abstract spectra of this chapter into a single, honest number for the resolution of a microscope, which is a fitting place to end our tour of Fourier optics.