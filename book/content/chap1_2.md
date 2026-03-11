# Light as a wave

If you have ever watched waves in a pond, you already have a surprisingly good mental model for understanding light. Drop a pebble into still water and you see circular wavefronts expanding outward. The distance between two consecutive crests is the wavelength, the number of crests passing a fixed point each second is the frequency, and the height of the crests is the amplitude. Light works in much the same way, except that it does not need water (or any medium at all) to propagate, and it oscillates not as a physical displacement but as an oscillation of the electromagnetic field.

## The electromagnetic wave

What exactly oscillates in a light wave? Two fields: the electric field $\vec{E}$ and the magnetic field $\vec{B}$. They oscillate perpendicular to each other and perpendicular to the direction the wave is moving. This makes light a **transverse wave**: the oscillation is at right angles to the propagation direction, unlike a sound wave, where air molecules compress and expand along the same axis.

```{figure} ../figures/emwave.png
---
width: 70%
name: em_wave
align: center
---
A light wave consists of oscillating electric ($\vec{E}$) and magnetic ($\vec{B}$) fields, perpendicular to each other and to the direction of propagation.
```

We can describe the spatial shape of the wave by freezing time and looking at how the field varies in space, or we can sit at one point and watch how the field changes over time. These two views give us the two most important parameters of any wave:

- The **wavelength** $\lambda$ is the distance between two consecutive peaks (or troughs, or any two equivalent points) along the wave at a single instant.
- The **frequency** $f$ (sometimes written $\nu$) is the number of complete oscillations per second, measured in Hertz (Hz).

These two quantities are related through one of the most fundamental equations in physics:

$$
c = \lambda \cdot f
$$

where $c \approx 3 \times 10^8$ m/s is the speed of light in vacuum. Because $c$ is a constant, wavelength and frequency are inversely related: shorter wavelengths correspond to higher frequencies, and vice versa. This is worth internalizing, because throughout this book we will switch freely between talking about wavelength and frequency depending on which is more convenient.

A few other terms are useful. The **period** $T = 1/f$ is the time for one complete oscillation. The **amplitude** $A$ is the maximum value of the electric field, and it determines the intensity (brightness) of the light: specifically, intensity is proportional to $A^2$.

## The electromagnetic spectrum

Visible light, the light our eyes can detect, occupies only a tiny sliver of the electromagnetic spectrum: wavelengths from about 400 nm (violet) to 700 nm (red). But the same physics governs an enormous range of radiation. Radio waves have wavelengths of meters to kilometers. Microwaves, the ones that heat your food, have wavelengths of centimeters. Infrared radiation is what you feel as warmth from a fire. On the other side of visible light, ultraviolet radiation is what gives you a sunburn, X-rays pass through soft tissue to image bones, and gamma rays are emitted by radioactive nuclei.

```{figure} ../figures/em_spectrum.png
---
width: 90%
name: em_spectrum
align: center
---
The electromagnetic spectrum. Visible light occupies a remarkably narrow band of wavelengths. The approximate scale of objects that interact with each type of radiation is shown below.
```

What makes this relevant for microscopy? The wavelength of the light you use sets a fundamental limit on the size of the features you can resolve. Visible light interacts with structures on the order of hundreds of nanometers to micrometers, which is precisely the scale of cells, organelles and subcellular structures. This is not a coincidence: it is the reason optical microscopy became biology's most important tool.

```{tip}
A useful number to keep in your head: 500 nm, roughly in the middle of the visible spectrum (green light), is the typical wavelength used as a reference when discussing resolution in fluorescence microscopy.
```

## Interference

Because light is a wave, two (or more) light waves can overlap and combine. What happens when they do depends on the relationship between their phases: the relative position of their peaks and troughs.

If two waves arrive at the same point with their peaks aligned (in phase), their amplitudes add up. The result is a brighter wave. This is **constructive interference**. If they arrive with the peaks of one aligned with the troughs of the other (exactly out of phase, or $\pi$ radians apart), their amplitudes cancel. The result is darkness. This is **destructive interference**.

```{figure} ../figures/interference.png
---
width: 70%
name: interference
align: center
---
(a) Destructive interference: when waves arrive out of phase, they cancel. (b) Constructive interference: when waves arrive in phase, they reinforce each other.
```

This might sound like an abstract curiosity, but interference is central to almost every topic in this book. Image formation in a microscope is fundamentally an interference process: light scattered by different parts of the specimen recombines to form the image. The resolution limit, the contrast mechanisms we will discuss in later chapters, and even techniques like phase contrast and structured illumination microscopy all depend on interference. We will revisit it in depth in {ref}`Chapter 6 <chap6>`, where we connect it to Fourier optics.

## Diffraction

Closely related to interference is **diffraction**: the phenomenon by which waves spread out and bend when they encounter an obstacle or pass through an opening. You can see diffraction of water waves at a harbor entrance, where the wave does not simply cast a sharp shadow behind the wall but fans out into the sheltered area. Light does the same thing, but because its wavelength is so short compared to everyday objects, the effect is usually too subtle to notice in daily life.

In microscopy, however, diffraction is impossible to ignore. Every lens has a finite aperture, and when light passes through it, it diffracts. The practical consequence is that a point source of light, no matter how small, is never imaged as a perfect point. Instead, it appears as a central bright disc surrounded by concentric rings, a pattern called the **Airy pattern** (after the astronomer George Biddell Airy). The size of this pattern depends on the wavelength of light and on how much of the diffracted light the lens can collect. This is the origin of the resolution limit we mentioned in the historical chapter, and we will analyze it quantitatively in {ref}`Chapter 6 <chap6_1>`.

```{figure} ../figures/airy_disk.png
---
width: 60%
name: airy_disk
align: center
---
When parallel light passes through a lens with finite aperture, the focal point is not a perfect point but an Airy pattern: a central disc surrounded by concentric rings of decreasing intensity.
```

```{tip}
If you ever wonder why microscopy has a resolution limit, here is the one-sentence answer: because lenses have finite size, they cannot collect all diffracted light, and information is lost. Everything else is a more precise version of this statement.
```

## Polarization

The electric field of a light wave oscillates perpendicular to the direction of propagation, but in which direction _exactly_? If the field always oscillates along the same axis (say, vertically), the light is **linearly polarized**. If the direction rotates as the wave moves forward, the light can be **circularly** or **elliptically polarized**. Most natural light sources (the sun, a lamp, a candle) emit **unpolarized** light, meaning the field direction changes randomly from moment to moment.

A polarizing filter selects only the component of the electric field along one axis and blocks the rest. If you place a vertical polarizer in a beam of unpolarized light, the light that comes through is vertically polarized, with roughly half the original intensity. If you then place a second polarizer oriented horizontally after the first, almost no light gets through: the vertically polarized light has no horizontal component to transmit.

```{figure} ../figures/polarization.png
---
width: 80%
name: polarization
align: center
---
A vertical polarizer transmits only the vertically oscillating component. A second, horizontal polarizer blocks the remaining light almost completely.
```

Polarization might seem like a niche topic, but it turns up repeatedly in microscopy. Differential interference contrast (DIC) microscopy uses polarized light to visualize transparent specimens. Fluorescence anisotropy measurements use polarization to study the rotation of molecules. And the design of many optical components (beam splitters, waveplates, liquid crystal devices) relies on manipulating the polarization state of light.

## Waves inside media

So far we have talked about light traveling in vacuum at speed $c$. But what happens when light enters a material like glass or water?

Light slows down. The ratio of the speed of light in vacuum to its speed $v$ in a medium defines the **refractive index** of that material:

$$
n = \frac{c}{v}
$$

For vacuum, $n = 1$ by definition. Air is very close to 1 (about 1.0003). Water has $n \approx 1.33$, glass typically $n \approx 1.5$, and diamond $n \approx 2.42$.

Here is something important and perhaps counterintuitive: when light enters a medium with a higher refractive index, its speed decreases and its wavelength shrinks, but its frequency stays the same. The frequency is set by the source and does not change when light crosses an interface. Since $v = \lambda f$ must still hold inside the medium, a slower speed with the same frequency means a shorter wavelength:

$$
\lambda_{\text{medium}} = \frac{\lambda_0}{n}
$$

where $\lambda_0$ is the wavelength in vacuum.

```{figure} ../figures/refractive_index.png
---
width: 80%
name: refractive_index
align: center
---
When light passes from a medium with low refractive index to one with high refractive index, it slows down and its wavelength decreases, while the frequency remains constant.
```

This fact has profound consequences for microscopy. When we talk about the resolution limit $d = \lambda / (2 \cdot \text{NA})$, the $\lambda$ that matters is the wavelength _inside the specimen_, not in air. Immersion objectives, which place oil or water between the lens and the specimen, exploit this: by matching the refractive index of the medium, they effectively shorten the wavelength and increase the numerical aperture, both of which improve resolution. We will discuss this in more detail in {ref}`Chapter 3 <chap3>`.

The refractive index also explains why light bends at interfaces between different materials. When a wavefront hits a surface at an angle, the part that enters the denser medium first slows down while the rest is still traveling at the original speed. This causes the wavefront to tilt, and the direction of propagation changes. This bending is called **refraction**, and it is the basis of all lens design. We will formalize it with Snell's law in the next section.
