(chap7_1)=
# 7.1 - Building blocks of a microscope

An imaging system, stripped to its essentials, does three things. It makes light, it does something to that light on the way to and from the sample, and it counts the light that comes back. Every component on an optical table belongs to one of those three jobs, or else it exists to hold the others still.

This section is a tour of the parts, deliberately more general than "a microscope", because the same catalogue turns up in a flow cytometer, a spectrometer and an optical tweezer setup. Some of these you have already met. What follows adds the details that matter when you have to choose a part rather than just recognise one.

## Light sources

For the first two centuries of microscopy the light source was the sun, redirected by a mirror under the stage, or a candle. Both work, and both have the obvious limitation that you cannot turn up the sun. Everything since has been an attempt to get more control: more brightness, more stability, a narrower spectrum, or the ability to switch on and off in microseconds.

Four families of source cover almost everything you will meet. They differ mainly in the shape of their emission spectrum, which is the single most useful thing to know about a lamp.

```{figure} ../figures/chap7_light_source_spectra.gif
---
width: 100%
name: chap7_light_source_spectra
align: center
---
Emission spectra of the four families of light source on a common axis, with the area under each curve tinted by the colour of the light. The vertical scales are normalised independently, so these curves say nothing about relative brightness, only about where the energy sits in wavelength. The tungsten and arc panels are fixed. The LED and laser panels cycle through typical devices, because a given LED emits one band and a given laser emits one line: which one you get is a purchasing decision, not a property of the technology.
```

### Thermal lamps

Heat something and it glows. At a few hundred degrees the glow is red, at a few thousand it is white with a blue cast. This is not an artefact of perception alone: hot bodies radiate a broad, smooth spectrum whose peak shifts to shorter wavelengths as the temperature rises, and the physics of it is the _black body radiation_ problem that so stubbornly resisted classical explanation that it eventually forced Planck to quantise energy, as we saw in {ref}`Chapter 1 <chap1_4>`.

The practical version is the **tungsten-halogen lamp**. A tungsten filament sits inside a small quartz envelope filled with an inert gas and a trace of a halogen, usually iodine or bromine. Run a current through it and the filament reaches roughly 3000 K, hot enough that the peak of its emission sits around 900 nm, with the visible spectrum riding on the rising shoulder of the curve.

Any hot filament slowly evaporates, blackening the envelope and thinning itself until it breaks. The halogen fixes this with an elegant chemical trick: evaporated tungsten reacts with the halogen to form a volatile halide, which circulates until it reaches the filament, where the temperature is high enough to break it apart again and redeposit the metal. The filament recycles itself, and lifetimes of a couple of thousand hours are routine.

```{figure} ../figures/chap7_tungsten_halogen_lamp.png
---
width: 60%
name: chap7_tungsten_halogen_lamp
align: center
---
A tungsten-halogen lamp. The filament is visible inside the quartz envelope, which must be quartz rather than glass because of the operating temperature.
```

Thermal lamps give you stable, cheap, broadband white light, which makes them excellent for brightfield and for the transmitted-light path of a commercial microscope. They are poor for fluorescence. Most of the emitted power is infrared, so you throw away the overwhelming majority of it in a filter, and what is left in the blue is weak. If your fluorophore is excited in the red you may be fine; if it is excited at 405 nm you will struggle.

### Arc lamps

The next idea is to stop heating things and start making sparks. In an arc lamp, two electrodes sit in a sealed envelope containing a gas at high pressure. Apply a large enough voltage and the gas breaks down and a discharge forms. The emitted spectrum is now not thermal at all: it is set by the electronic transitions available in the gas.

The **mercury arc lamp** was the workhorse of fluorescence microscopy for decades. A few droplets of mercury sit inside the envelope with a starter gas, and once the arc strikes, the mercury vaporises and its atomic transitions dominate the emission: intense, narrow lines on a weak continuum, the strongest at 365, 405, 436, 546 and 579 nm.

Those lines are both the strength and the weakness of the lamp. Where a line coincides with the excitation peak of your fluorophore you get a very bright, very clean excitation band with a simple filter. Where it does not, you are relying on the feeble continuum, and there is a conspicuous hole in the cyan-green between 436 and 546 nm and very little in the red. Add that mercury is toxic enough that a broken lamp is a laboratory incident, and that the useful lifetime is only a few hundred hours, and you have the reasons these lamps have largely disappeared. You will still meet them on older systems, and knowing their spectrum explains why an older paper chose the fluorophores it did.

The discharge is also an unusually good approximation of a point source, since most of the intensity comes from a small region near the cathode tip. That makes it easy to collimate and to set up Köhler illumination as described in {ref}`Chapter 3 <chap3_3>`.

The **xenon arc lamp** works on the same principle with xenon, and produces a spectrum that is smooth and nearly flat across the whole visible range, with strong line structure only in the near infrared. That flatness is its advantage: any excitation wavelength is available at roughly the same intensity, which makes calibration across colours straightforward and which is why xenon lamps sit behind monochromator-based systems.

```{figure} ../figures/chap7_arc_lamps.png
---
width: 85%
name: chap7_arc_lamps
align: center
---
Mercury and xenon arc lamps. In both cases the emitting region is the discharge near the cathode tip, which is why the pointed electrode geometry matters.
```

### Light-emitting diodes

LEDs have taken over. They are cheap, efficient, they last for tens of thousands of hours, they switch on and off in microseconds, and they come in every colour. Almost every fluorescence microscope sold today is illuminated by an LED engine.

To understand them you need the band picture of solids. In an isolated molecule, electrons occupy discrete energy levels. In a crystal, where the same structural unit repeats billions of times, those levels smear into continuous _bands_. The highest filled band is the **valence band**, the next one up is the **conduction band**, and the energy difference between them is the **band gap**.

The size of that gap sorts all materials into three classes. In a metal, the Fermi level lies inside the conduction band, so electrons are already free to move. In an insulator the gap is so wide that nothing short of a catastrophic voltage promotes an electron across it. In between sit **semiconductors**, where the gap is small enough, typically one to three electronvolts, that a single photon or a modest voltage can push an electron across.

```{figure} ../figures/chap7_band_structure.png
---
width: 85%
name: chap7_band_structure
align: center
---
Band structure of a metal, a semiconductor and an insulator. The band gap of a semiconductor is comparable to the energy of a visible photon, which is what makes it optically interesting.
```

A semiconductor on its own is a rather poor insulator. What makes it useful is _doping_: deliberately adding impurity atoms that either donate extra electrons (n-type) or leave vacant states, called holes, in the valence band (p-type). Put an n-type and a p-type region in contact and you have a **p-n junction**, which is a diode.

Apply a forward voltage and electrons flow from the n side into the junction, where they meet holes coming the other way. An electron in the conduction band drops into a hole in the valence band, and the energy difference has to go somewhere. In a suitable material it leaves as a photon whose energy is set by the band gap. That is a light-emitting diode, and it is worth noticing how closely the process parallels the fluorescence of {ref}`Chapter 4 <chap4_1>`: an excited state, a radiative transition, a photon whose colour is fixed by an energy difference you cannot easily change.

Because the emission is tied to a single gap, LED spectra are reasonably narrow, typically 20 to 40 nm wide at half maximum. That is not as sharp as an arc lamp line, let alone a laser, but with an excitation filter it is more than clean enough. And because everything is solid state, with no gas, no filament and nothing evaporating, LEDs do not wear out on the timescale of an experiment.

White light from LEDs takes one of two routes. Combine a red, a green and a blue emitter and let the eye do the mixing, which is what a display does. Or take a single blue LED and coat it with a **phosphor**, a material that absorbs part of the blue and re-emits over a very broad band at longer wavelengths, so that the leaked blue plus the broad yellow-orange hump adds up to something the eye reads as white.

```{tip}
Do not expect a "white" source to be spectrally flat. A phosphor-converted white LED has a pronounced blue spike and a broad hump, a xenon lamp is genuinely quite flat, and a tungsten lamp is heavily weighted to the red. All three look white. If you are doing quantitative work across colours, look at the spectrum, not at the label.
```

### Lasers

The name is an acronym: Light Amplification by Stimulated Emission of Radiation. Everything about a laser follows from that phrase read carefully.

Recall from {ref}`Chapter 4 <chap4_1>` that an excited molecule left alone will eventually relax and emit a photon in a random direction at a random time. That is _spontaneous_ emission, and it is what gives fluorescence. **Stimulated emission** is different. If a photon of exactly the right energy passes an already-excited molecule, it can trigger the relaxation, and the emitted photon is a clone of the one that triggered it: same wavelength, same phase, same direction. One photon in, two identical photons out.

Turning that into a light source takes three things: a **gain medium** (a gas, a dye solution, a crystal or a semiconductor) containing the transition you want to exploit, a **pump** that supplies energy to keep the medium excited, and a **resonant cavity** formed by two mirrors facing each other, one essentially perfectly reflective and the other transmitting a small percentage.

```{figure} ../figures/chap7_laser_cavity.gif
---
width: 100%
name: chap7_laser_cavity
align: center
---
Lasing building up in a resonant cavity. At first the pumped molecules fluoresce in every direction and almost all of those photons are lost. Photons travelling along the axis survive the round trip, stimulate further emission, and are cloned faster than they escape, until a fraction leaks through the output coupler as the beam. Note that the pump never switches off: once lasing starts it has to keep replacing the excited population that stimulated emission is consuming.
```

Switch on the pump and, at first, the excited molecules simply fluoresce in all directions, and almost all of those photons leave the cavity and are lost. But the few travelling along the axis are reflected back through the gain medium, where they stimulate more emission, and those clones are reflected back again. The axial mode grows while every other direction is discarded. Once the pump is strong enough that more molecules are excited than are in the ground state, a condition called **population inversion**, the amplification per round trip exceeds the losses and the field builds up rapidly.

What emerges through the output coupler is a beam of photons that are copies of one another. That is why a laser is _monochromatic_ (one transition), _coherent_ (fixed phase relationship) and _collimated_ (only the axial direction survived), and why lasers are indispensable for anything involving interference, tight focusing, or delivering large power into a diffraction-limited spot.

```{warning}
The reason lasers are dangerous is almost never the wavelength; it is the power. A 5 mW pointer is class 3R and will not blind you if you blink. A 5 W beam of exactly the same colour will burn a hole in whatever it lands on, including a retina, before the blink reflex has finished. Laser classes run from 1 (safe under all conditions) to 4 (hazardous even from diffuse reflections), and any research laser you meet is likely to be class 3B or 4. Take the safety training seriously.
```

### Continuous wave and pulsed lasers

A **continuous wave** (CW) laser emits a constant optical power for as long as it is on. Most lasers in a confocal microscope are CW.

A **pulsed laser** instead emits a regular train of very short bursts. The pulse duration can be anywhere from nanoseconds down to a few femtoseconds, and the repetition rate is set by the round-trip time of the cavity, typically tens to hundreds of megahertz. Between pulses, nothing comes out at all.

```{figure} ../figures/chap7_cw_vs_pulsed.png
---
width: 90%
name: chap7_cw_vs_pulsed
align: center
---
Output power against time for a continuous wave and a pulsed laser delivering the same average power. The pulsed laser concentrates the same energy into a tiny fraction of the time, so its peak power is enormously higher. The inset shows the corresponding consequence in the spectral domain: short pulses are necessarily broadband.
```

This matters because some processes depend not on how many photons arrive per second but on how many arrive at once. Two-photon absorption, which we will meet properly in {ref}`Chapter 8 <chap8>`, requires a molecule to absorb two photons within roughly a femtosecond of each other. The probability of that happening scales with the square of the instantaneous intensity, so squeezing your photons into short pulses buys you an enormous advantage without cooking the sample with average power.

```{tip}
**Worked example: peak power of a femtosecond laser.**

A Ti:Sapphire laser delivers 1 W of average power in 100 fs pulses at a repetition rate of 100 MHz, so one pulse every 10 ns.

Energy per pulse:

$$E_{\text{pulse}} = \frac{P_{\text{avg}}}{f_{\text{rep}}} = \frac{1 \ \text{W}}{10^{8} \ \text{s}^{-1}} = 10 \ \text{nJ}$$

Peak power during the pulse:

$$P_{\text{peak}} = \frac{E_{\text{pulse}}}{\tau} = \frac{10 \times 10^{-9} \ \text{J}}{100 \times 10^{-15} \ \text{s}} = 10^{5} \ \text{W} = 100 \ \text{kW}$$

The duty cycle is $\tau f_{\text{rep}} = 10^{-5}$, so the laser is off 99.999% of the time. The sample experiences 1 W of heating but 100 kW of instantaneous intensity. That is the entire trick of multiphoton microscopy.
```

There is a price. Pulse duration and spectral width are Fourier conjugates, exactly as position and spatial frequency were in {ref}`Chapter 6 <chap6_1>`. A pulse cannot be shorter than the inverse of its bandwidth, and for a Gaussian pulse the relation is $\Delta \nu \, \Delta t \geq 0.441$. A 100 fs pulse at 800 nm therefore carries at least about 10 nm of bandwidth. Ultrashort pulses are broadband pulses, which is occasionally useful and occasionally a nuisance.

## Mirrors

The mirror in your bathroom is a sheet of glass with silver deposited on the back and paint over the silver to stop it oxidising. It is a fine object for looking at your face and a poor one for an optical table. Light entering at an angle reflects partly from the front surface of the glass and partly from the silver, producing a **ghost image** offset from the main one, and every pass through the glass costs a little absorption.

Research mirrors put the coating on the front surface, so there is no glass in the path at all. Two strategies exist.

**Metallic coatings** of aluminium, silver or gold reflect over an extremely wide band. Aluminium works down into the ultraviolet at around 90% reflectance, silver reaches 97 to 98% across the visible, and gold is the choice for the infrared. They are broadband and forgiving of angle, but they cap out below 99% and they degrade.

**Dielectric coatings** achieve better than 99.5% by stacking many alternating layers of transparent materials with different refractive indices. Each layer is a quarter of a wavelength thick in optical path, so the partial reflections from every interface arrive in phase and interfere constructively. It is the same physics as the anti-reflection coating on your glasses, run in reverse, and because it depends on layer thickness matching wavelength, a dielectric mirror works over a specified band and can be nearly transparent outside it.

```{figure} ../figures/chap7_mirror_coatings.png
---
width: 85%
name: chap7_mirror_coatings
align: center
---
A back-surface household mirror produces ghost reflections and absorption losses. A front-surface dielectric stack builds up near-total reflection by constructive interference between many thin layers.
```

```{warning}
Coated surfaces are delicate and must never be touched. A fingerprint on a dielectric stack changes the optical thickness of the top layers locally and permanently, and cleaning it risks scratching layers that are tens of nanometres thick. Handle every optic by its edges or its mount.
```

Two habits will save you a lot of confusion. First, always check the reflectance curve for the wavelength you are actually using: a mirror that is beautifully reflective in the visible may be at 50% in the near infrared, and in a beam path with eight mirrors a 50% loss each is a factor of 256. Second, remember that losses multiply. Ten components at 98% each leave you with 82% of your light.

## Lenses and objectives

Lenses and their aberrations were the subject of {ref}`Chapter 2 <chap2>`, and the **objective** itself, its magnification, numerical aperture, immersion medium, working distance, tube length and the markings that encode all of them, was covered in {ref}`Chapter 3 <chap3_1>`. Nothing needs repeating here.

One consequence is worth carrying into the next section, though, because it is a diagnostic when you read a schematic. Between an infinity-corrected objective and its tube lens the rays are parallel, and in that region you can insert a filter, a dichroic or a modulator of any thickness without shifting the focus. So when you see components drawn in that gap, you know immediately why the designer had room to put them there. If instead you see something sandwiched into a converging beam, something unusual is going on and it is worth asking what.

```{warning}
Never put oil on a water objective or water on an oil objective. The internal elements are computed for a specific immersion refractive index, and immersion oil is very difficult to remove from a front element without damaging the coating. Objectives of this class cost 10,000 to 25,000 euros. If you are unsure what an objective takes, read the barrel or ask; do not guess.
```

## Optical filters

Filters and dichroics work by the same interference mechanism as dielectric mirrors: a stack of thin layers whose thicknesses are chosen so that some wavelengths interfere constructively on transmission and others on reflection. Modern hard-coated filters achieve edges so steep that the transition from blocking to transmitting takes a handful of nanometres.

```{figure} ../figures/chap7_filter_transmission.png
---
width: 95%
name: chap7_filter_transmission
align: center
---
The four basic filter types, plotted as transmission. A bandpass filter transmits a defined window; a longpass transmits everything above a cut-on wavelength; a shortpass transmits everything below a cut-off; a neutral density filter attenuates all wavelengths roughly equally. The small ripples in the passbands are a real feature of multilayer coatings, not noise in the measurement.
```

A **bandpass** filter is specified by its centre wavelength and bandwidth, written for example as 525/50, meaning a 50 nm wide window centred at 525 nm. **Longpass** and **shortpass** filters are specified by their edge wavelength. **Neutral density** (ND) filters attenuate broadly and are the standard way of turning down a laser that has no intensity control of its own.

Now look at those four blocking regions again. In the transmission plot they all sit flat on the axis, indistinguishable from each other and from zero. That is exactly the problem. A filter that leaks 1% and a filter that leaks 0.0001% draw the same line, and in fluorescence the difference between them is the difference between a usable image and a wash of excitation light. This is why nobody in the optics business specifies a filter by its transmission in the blocking band. They use **optical density**:

$$\mathrm{OD} = -\log_{10} T$$

Plot the same four filters this way and the blocking region becomes the informative part of the graph.

```{figure} ../figures/chap7_filter_optical_density.png
---
width: 95%
name: chap7_filter_optical_density
align: center
---
The same four filters as above, plotted as optical density. The axis runs downwards so that the passband still appears at the top: OD 0 means everything gets through, OD 6 means one part in a million does. The height of the coloured band is still how much light passes, exactly as in the previous figure.
```

An OD of 6 means one part in a million gets through. Blocking of OD 6 or better outside the passband is what makes it possible to detect a handful of emitted photons against an excitation beam that is a million times brighter. ND filters use the same definition, and their optical densities add when you stack them: an OD 1 and an OD 2 in series give OD 3, a factor of 1000.

The two figures are the same four filters, the same numbers plotted twice, which is worth dwelling on. In the transmission plot the passband ripple is obvious and the blocking region is a flat line. In the optical density plot the blocking region is full of structure and the passband ripple has vanished. Neither plot is wrong. A ripple of a few per cent in transmission is a hundredth of an OD unit, invisible on a scale that runs to six; and a factor of two in leakage, which is 0.3 OD and plainly visible, is a change from 0.0001% to 0.0002% transmission. Which representation you reach for depends entirely on which end of the curve you care about.

```{tip}
Optical densities add, transmissions multiply. If you need a factor of $10^4$ attenuation and you have OD 1, OD 1.5 and OD 2 filters, stacking OD 2 + OD 2 works, and so does OD 1 + OD 1.5 + OD 1.5. Just be aware that reflective ND filters send the rejected light straight back where it came from, which is a genuine problem if that direction contains a laser.
```

### Dichroic beam splitters

A **dichroic mirror** is a filter used in reflection and transmission at the same time. Below its edge wavelength it reflects, above it transmits, and it is mounted at 45 degrees so that the reflected and transmitted paths separate cleanly. This is the component that makes epifluorescence possible: excitation light comes in from the side, is reflected up through the objective to the sample, and the redshifted emission comes back down and passes straight through to the detector. The Stokes shift of the fluorophore ({ref}`Chapter 4 <chap4_1>`) is what creates the wavelength gap the dichroic needs.

```{figure} ../figures/chap7_dichroic_gfp.png
---
width: 90%
name: chap7_dichroic_gfp
align: center
---
A complete filter set for GFP: excitation bandpass, dichroic edge and emission bandpass, overlaid on measured EGFP excitation and emission spectra. The Stokes shift marked between the two maxima is what creates the wavelength gap the dichroic needs. The three filter curves are designed together, which is why sets are sold as matched cubes.
```

```{tip}
**Filters are specified at an angle of incidence.** Bandpass and longpass filters are characterised at 0 degrees, dichroics at 45. Tilting a multilayer filter shortens the effective optical path through each layer and shifts the whole spectrum to shorter wavelengths. This is occasionally exploited deliberately to fine-tune an edge by a few nanometres, but it is more often the reason a filter set that should work does not. Check that your components are mounted at the angle they were designed for.
```

## Detectors

At the end of every optical path something has to convert photons into numbers. All detectors do this through the photoelectric effect ({ref}`Chapter 1 <chap1_4>`): an absorbed photon promotes an electron, and the resulting charge is measured. In a silicon sensor the electron is promoted across the band gap and the electron-hole pair stays inside the material, which is the internal photoelectric effect and is essentially an LED run backwards. In a photomultiplier tube the photon ejects an electron out of the material entirely into a vacuum, which is the external photoelectric effect that Einstein explained in 1905.

The figure of merit that matters most is **quantum efficiency**, the probability that an arriving photon produces a counted electron. Modern back-illuminated scientific sensors reach 90 to 95% over much of the visible range, remarkably close to the physical limit.

An image sensor divides its light-sensitive area into pixels, each of which accumulates charge during the exposure and is then read out. What distinguishes the four main architectures is entirely how that readout happens, so each is animated below. All four start from the same deliberately faint frame, and the CCD and EMCCD animations share a common scale on the charge bar, so the comparisons are fair.

### CCD

In a **charge-coupled device**, each pixel is a potential well that collects photoelectrons during the exposure. To read the image, the array is shifted one row at a time into a serial register, which is then clocked out pixel by pixel through a single output amplifier. The usual analogy is a field of buckets collecting rain, passed hand to hand along a bucket brigade to one calibrated measuring container.

```{figure} ../figures/chap7_readout_ccd.gif
---
width: 80%
name: chap7_readout_ccd
align: center
---
A CCD reading out. Each row is shifted down into the serial register, and the register is then clocked to the right, one pixel per step, into a single amplifier. The bar tracks the charge arriving at that amplifier: with a faint sample it only just clears the read-noise line, and the digitised image comes out grainy.
```

Passing charge from well to well is extraordinarily efficient, better than 99.999% per transfer, and because every pixel is measured by the same amplifier the response is beautifully uniform. Combined with cooling to suppress thermal dark current, this gives low noise and a high dynamic range: you can measure a bright and a dim structure in the same frame and trust both. The cost is speed, since the readout is serial and cannot overlap with the exposure. CCDs are the right choice when fidelity matters more than frame rate.

### EMCCD

The **electron-multiplying CCD** attacks the one remaining noise source in a CCD, the read noise added by the output amplifier, by amplifying the signal before it gets there. The serial register is extended with a gain register clocked at high voltage, so each transfer has a small probability of generating an extra electron by impact ionisation. Repeated over hundreds of stages this multiplies the charge by a factor of hundreds or thousands, pushing even a single photoelectron far above the read noise floor.

```{figure} ../figures/chap7_readout_emccd.gif
---
width: 80%
name: chap7_readout_emccd
align: center
---
An EMCCD reading out the same faint frame, on the same bar scale. The gain register sits between the serial register and the amplifier. Watch a packet of charge cross it: each stage multiplies it a little, so it darkens on its way to the amplifier and arrives far above the read-noise line. Nothing about the sensor collects more photons. The difference is entirely that the amplification happens before the noise is added rather than after.
```

Most EMCCDs also use a frame-transfer architecture, shifting the whole image in one fast step into a masked storage area so the next exposure can begin while the previous frame is read.

The result is genuine single-photon sensitivity, and EMCCDs are the traditional detector for single-molecule localisation microscopy ({ref}`Chapter 9 <chap9>`). Two caveats. The multiplication is stochastic, so it adds its own **excess noise**, which in the shot-noise limit costs about a factor of two in effective quantum efficiency. And it saturates easily: too much gain on a bright sample fills the register, destroys all contrast, and can damage the device. Set the gain to the highest value that never saturates, and no higher.

### CMOS

A **complementary metal-oxide-semiconductor** sensor abandons the bucket brigade entirely. Every pixel has its own amplifier and readout circuitry, and pixels are addressed in parallel. That makes CMOS sensors fast, scalable, cheap and low in power consumption, which is why the camera in your phone is one.

```{figure} ../figures/chap7_readout_cmos.gif
---
width: 80%
name: chap7_readout_cmos
align: center
---
A CMOS sensor reading out. There is no bucket brigade and no shared amplifier: the triangle drawn in every cell is that pixel's own amplifier and analogue-to-digital converter, so the whole frame leaves in a single step. Compare how many steps this takes against the CCD.
```

The drawback is uniformity. Each pixel has slightly different gain and offset, and the resulting **fixed-pattern noise** shows up as a static texture in the image. Read noise per pixel is also higher than in a CCD. For a bright, high-contrast sample none of this matters; for a dim one it matters a great deal.

### sCMOS

**Scientific CMOS** sensors keep the speed of CMOS while fixing the noise, using per-column low-noise amplifiers and analogue-to-digital converters, careful factory calibration of every pixel, and large, well-designed pixels. Read noise comes down to around one electron, better than most CCDs, at frame rates of hundreds per second over a large field of view.

```{figure} ../figures/chap7_readout_scmos.gif
---
width: 80%
name: chap7_readout_scmos
align: center
---
An sCMOS sensor reading out. Every pixel in a column shares one amplifier and one analogue-to-digital converter at the foot of that column, which is where the low noise comes from, and the exposure window rolls down the sensor rather than opening everywhere at once.
```

sCMOS sensors usually read out with a **rolling shutter**: rather than exposing the whole sensor at once, the exposure window sweeps down it row by row. This is a readout pattern, not a physical shutter, and on its own it is a nuisance, since different rows correspond to different moments in time and a fast-moving object can appear sheared. But it can be turned into an advantage. Synchronise a scanned line of illumination with the moving exposure window and the sensor only ever accepts light from the region currently being illuminated, rejecting everything scattered from elsewhere. This is the principle behind confocal line-scanning light-sheet systems.

The remaining drawback is cost: a research-grade sCMOS runs to several tens of thousands of euros.

```{list-table} Detector comparison
:header-rows: 1
:name: chap7_detector_table

* - Feature
  - CCD
  - EMCCD
  - CMOS
  - sCMOS
* - Sensitivity
  - High
  - Extreme (single photon)
  - Moderate
  - High
* - Speed
  - Slow
  - Slow
  - Fast
  - Fast
* - Noise
  - Low
  - Low, but excess noise at high gain
  - High and non-uniform
  - Low
* - Dynamic range
  - High
  - Limited by gain saturation
  - Moderate
  - High
* - Cost
  - Moderate
  - High
  - Low
  - High
* - Best for
  - Low light, high fidelity
  - Ultra-low light, single molecules
  - High speed on a budget
  - High speed with sensitivity
```

### Photomultiplier tubes

A **photomultiplier tube** (PMT) is not an image sensor. It has one channel and returns one number: how much light is arriving right now.

A photon strikes a photocathode and ejects a single electron into the vacuum. An electric field accelerates that electron onto the first of a chain of electrodes called **dynodes**, each held at a progressively higher potential. The electron arrives with enough kinetic energy to knock several secondary electrons out of the dynode surface, those are accelerated to the next dynode, and the cascade continues. Ten dynodes with a yield of four each give a gain of $4^{10} \approx 10^{6}$. The resulting charge pulse is easily measured, and it arrives within nanoseconds of the original photon.

```{figure} ../figures/chap7_pmt.png
---
width: 80%
name: chap7_pmt
align: center
---
A photomultiplier tube. One photoelectron released at the photocathode triggers a cascade down the dynode chain, producing a measurable current pulse.
```

Because a PMT has no spatial structure, it can only be used in systems where the position information comes from somewhere else, namely from scanning. In a confocal microscope ({ref}`Chapter 5 <chap5_1>`) the image is built pixel by pixel by scanning the excitation spot, and the PMT simply reports the brightness at each position. The same is true in multiphoton microscopy. This is why spotting a PMT in a schematic immediately tells you that the system scans.

PMTs are fast and extremely sensitive, but their quantum efficiency is modest, typically 20 to 40% in the blue-green and falling badly in the red. Modern alternatives include avalanche photodiodes, silicon photomultipliers and hybrid detectors, which combine a photocathode with a semiconductor amplification stage and reach much higher quantum efficiency.

## Specialized optical components

Everything so far is standard on a commercial microscope. The components in this section are what you add when you need to do something the catalogue does not offer, and they appear constantly in custom-built systems and in methods papers.

### Galvanometric mirrors

A **galvanometric scanner**, universally called a galvo, is a small mirror mounted on a limited-rotation motor. Apply a voltage and the shaft rotates by a proportional angle, with a position sensor providing feedback so the mirror lands accurately. The travel is only around 20 degrees mechanical, which doubles to 40 degrees optical, but that is more than enough to sweep a beam across a field of view.

Put two galvos in series with their axes perpendicular and you can steer a beam anywhere in a two-dimensional field, at kilohertz rates, without moving the sample at all. This is how confocal and multiphoton microscopes scan. A resonant scanner, which oscillates at a fixed frequency of 8 or 12 kHz rather than following an arbitrary command, is used when video-rate imaging is required.

```{figure} ../figures/chap7_galvo_scan.gif
---
width: 92%
name: chap7_galvo_mirrors
align: center
---
Galvanometric scanning with two mirrors. The fast mirror sweeps a whole line in x while the slow mirror steps once per line in y, and the scan lens and tube lens turn each deflection into a lateral displacement of the focus. The sample is drawn face-on so that both scan axes are visible; the y deflection is perpendicular to the page, which is why the drawn beam does not bend at that mirror.
```

```{tip}
**Why a scan lens is not just a lens.** Between the galvos and the objective you will always find a scan lens (often labelled f-theta) and a tube lens. They do two jobs. First, they make the position of the focused spot proportional to the scan _angle_ rather than to its tangent, so that equal voltage steps give equal spatial steps and the focal spot stays on a flat plane instead of curving away at the edges. Second, they image the galvo mirror onto the back focal plane of the objective, so that the beam pivots there rather than walking across the pupil. Without that conjugation the beam would clip the aperture and the intensity would fall off across the field.
```

### Digital micromirror devices

A **digital micromirror device** (DMD) is a chip carrying a million or more aluminium mirrors, each a few micrometres across, each mounted on a hinge and each individually switchable between two tilt positions, conventionally about ±12 degrees. One position sends light towards the sample; the other sends it off to the side, into an absorbing **beam blocker**. Load a binary image onto the chip and you have a programmable mask, switchable in tens of microseconds.

```{figure} ../figures/chap7_dmd_patterning.gif
---
width: 95%
name: chap7_dmd
align: center
---
A digital micromirror device in use. Illumination arrives at an angle; mirrors in the ON position reflect it straight up into the objective, while mirrors in the OFF position send it off to the side into a beam blocker. Loading a pattern therefore decides which parts of the field are ever excited. The objective then projects the pattern onto the sample, so what lands there is a demagnified copy of the chip. The animation runs from full-field illumination, through selecting two cells, to a membrane-only pattern, and the ON and OFF counts are for the whole two-dimensional chip.
```

This is enormously useful. Acquire a widefield image, select the cells or the structures you care about, compute which micromirrors correspond to them, and illuminate only those. Everything else in the field is never excited at all, so it neither bleaches nor contributes background. You improve signal-to-noise ratio and reduce phototoxicity in the same move. The same capability drives patterned optogenetic stimulation, targeted photobleaching for FRAP, and the structured illumination patterns of {ref}`Chapter 9 <chap9>`.

### Spatial light modulators

A **spatial light modulator** (SLM) does something a DMD cannot: it controls the _phase_ of the light, pixel by pixel, continuously rather than in binary.

The **liquid crystal** variety exploits the fact that the elongated, charged molecules of a liquid crystal reorient in an applied electric field, and that their refractive index depends on their orientation. Anchor the molecules at the boundaries, apply a voltage across a pixel, and the optical path through that pixel changes by a controllable amount, so light passing through acquires a programmable phase delay.

Being able to write an arbitrary phase pattern is remarkably powerful. Recall from {ref}`Chapter 6 <chap6_2>` that the field in the back focal plane is the Fourier transform of the field in the sample plane. Imposing a phase pattern in a pupil plane therefore lets you sculpt the focus: correct the aberrations a scattering sample introduces so a distorted focus becomes sharp again (**adaptive optics**), or split one beam into a dozen independently positioned foci in three dimensions (**holography**, which is how patterned optogenetics in a living brain is done).

The same device can also modulate amplitude. Because the liquid crystal changes the polarisation state as well as the phase, a polariser before the SLM and an analyser after it convert a polarisation rotation into a transmission change. With the analyser crossed, zero voltage gives full transmission and maximum voltage gives none, and you have a DMD-like intensity mask built out of phase.

```{figure} ../figures/chap7_slm_liquid_crystal.gif
---
width: 95%
name: chap7_slm_liquid_crystal
align: center
---
One pixel of a liquid crystal SLM as the applied voltage is ramped from its minimum to its maximum and back. The molecules tilt towards the field, the effective refractive index falls, and the emerging wave picks up a controllable phase delay. Add a polariser before the cell and a crossed analyser after it, and the same reorientation becomes a continuously variable transmission.
```

The other family of SLM is built from **microelectromechanical systems** (MEMS): deformable mirrors, used in reflection. An array of electrostatic actuators pushes a reflective membrane in and out by a fraction of a micrometre. A surface displacement $d$ produces an optical path difference of $2d$ in reflection, so very small movements produce a full wave of phase. Deformable mirrors come as **segmented** devices, where each pixel is an independent flat mirror, and **continuous** devices, where a single flexible membrane is deformed smoothly. Continuous membranes avoid the diffraction from inter-pixel gaps and are preferred for adaptive optics; segmented devices give more independent control.

```{figure} ../figures/chap7_mems_dm.png
---
width: 90%
name: chap7_mems_dm
align: center
---
Segmented and continuous MEMS deformable mirrors. Two rays reflecting from surfaces at different heights leave with a phase difference of twice the height difference.
```

## Specialized mechanical components

Optics get the attention, but a microscope that vibrates is worthless, and one that cannot move the sample reproducibly is not much better.

An **optical table** is a thick honeycomb-cored steel slab resting on pneumatic isolators, and the isolators are the point. A table sitting on the floor transmits every footstep, door slam and cleaning trolley in the corridor straight into your beam path. Floated on air, the assembly has a resonant frequency around 1 Hz, well below building vibration, so it simply does not follow it. Push down on one corner of a floated table and it drifts slowly back rather than bouncing. For super-resolution work, where the whole measurement rests on localising a molecule to a few nanometres over seconds, this is not a luxury.

```{figure} ../figures/chap7_optical_table.png
---
width: 85%
name: chap7_optical_table
align: center
---
An optical table on pneumatic isolators. The honeycomb core provides stiffness at low mass, and the air legs decouple the table from building vibration.
```

**Translation stages** move the sample in x and y. They can be manual, motorised, or piezoelectric, and the choice is a trade-off between range and precision: a motorised stage covers centimetres with micrometre steps, a piezo stage covers a hundred micrometres with nanometre steps. Stage scanning is much slower than galvo scanning, but it has no field-of-view limit, which is why tiled acquisitions of whole slides are done this way.

**Objective positioners** move the objective along z, and are the standard way to acquire a focal stack. A piezo objective collar settles in a few milliseconds and steps in tens of nanometres, comfortably finer than the axial resolution of any light microscope.

```{figure} ../figures/chap7_stages.png
---
width: 90%
name: chap7_stages
align: center
---
Translation stages for lateral (xy) sample positioning and a piezo objective positioner for axial (z) scanning.
```

## Putting it together

That is the catalogue. Sources that differ mainly in the shape of their spectrum, mirrors and filters that are all built from the same interference physics, objectives that encode their entire specification in a few engraved characters, detectors that differ mainly in how they read out, and a set of programmable and mechanical components for putting light exactly where you want it.

None of these parts is interesting on its own. What is interesting is the reasoning that assembles them, and that reasoning leaves visible traces. A PMT means scanning. A pulsed laser means nonlinear excitation. A cylindrical lens means a light sheet. Three LEDs and a set of dichroics mean multicolour imaging. In the next section we will use exactly these clues to read published instruments off the page.
