(chap7_2)=
# 7.2 - Reading a schematic

Open almost any methods paper in microscopy and you will find, usually as Figure 1, a line drawing full of ellipses, rectangles and diagonal bars, labelled with a dense fog of acronyms. It looks forbidding. It is not. A schematic is a story with a fixed plot: light is born, it travels to the sample, it comes back changed, and it is counted. Your job is to follow it.

This section gives you a procedure and then applies it to real published instruments. The procedure is not the only one possible, and experienced people stop using it consciously, but it works every time and it is what you should fall back on when a figure looks impenetrable.

## The procedure

```{figure} ../figures/chap7_schematic_recipe.png
---
width: 95%
name: chap7_schematic_recipe
align: center
---
The five steps applied to a generic epifluorescence microscope. Find the ends of the story first, then fill in the middle.
```

**1. Find the light source or sources.** Look for a laser box, an LED, a lamp, or a beam entering the figure from off-page. There may be more than one, and if there are, that fact alone is informative: multiple sources usually means multiple colours, and therefore multiple labels in the sample.

**2. Find the sample.** It is almost always labelled, and it is almost always at the focus of an objective. In a schematic drawn with the optical axis vertical, it will be at the top (an inverted microscope) or in the middle (a light-sheet or a horizontal custom build).

**3. Find the detector or detectors.** A camera is drawn as a rectangle, a PMT as a cylinder with a cable. Again, more than one detector tells you something: either two colours recorded simultaneously, or two different measurement modes.

**4. Follow the optical path from source to detector, through the sample.** Light travels in straight lines until something bends it. Trace the beam. If the figure is drawn well, the beam itself is shaded, and you can simply follow the shading.

**5. Identify each component you cross, and ask what it is for.** This is where the previous section pays off. Every component you cross is a decision somebody made, and each one narrows down what the instrument is for.

Then step back and read the whole thing as a sentence. If you have crossed a pulsed laser, two scanning mirrors and a PMT, you are looking at a multiphoton microscope, and you knew that before reading the caption.

```{tip}
When you meet a component you do not recognise, do not stop. Note where it sits (illumination path or detection path, before or after the objective, in a pupil plane or an image plane) and keep going. Its position usually tells you more than its name, and you can look the name up afterwards. Outside an exam you always can look it up, and everybody does.
```

## Worked example 1: two ways to build a light sheet

Our first example comes from a review of light-sheet fluorescence microscopy {cite}`stelzer2021lightsheet`, and it is a gift, because it shows two implementations side by side that differ in exactly one respect.

```{figure} ../figures/chap7_schematic_lightsheet_spim_dslm.png
---
width: 95%
name: chap7_schematic_spim_dslm
align: center
---
Two implementations of light-sheet illumination. (a) A static sheet formed by a cylindrical lens (SPIM). (b) A dynamic sheet swept out by a scanning mirror (DSLM). The detection arm is identical in both. Reproduced from Stelzer et al. (2021), Nature Reviews Methods Primers.
```

**Panel a.** Step one: the beam enters from the left, so the source is off-page, and given that it is drawn as a thin collimated line it is a laser. Step two: the sample sits in the middle, and here it is helpfully drawn as a small larva. Step three: the detector is a camera at the top right. Step four: follow the path.

The beam first passes two lenses in succession. Two lenses in a row acting on a collimated beam, both drawn as simple singlets, and with the beam visibly wider after them than before, is a **beam expander**: a short-focal-length lens diverges the beam and a longer-focal-length lens recollimates it, magnifying the diameter by the ratio of the focal lengths. Why expand the beam? Because the beam has to fill the back aperture of the illumination objective. An underfilled pupil means a lower effective numerical aperture, which means a thicker, less confined sheet.

Then comes a **cylindrical lens**, and this is the component that defines the whole instrument. A cylindrical lens has optical power in one axis only, so it focuses the beam to a line rather than a point. The illumination objective relays this line into the sample, where it becomes a thin sheet of light spanning the field of view.

The sample is illuminated by that sheet. Fluorescence is emitted in all directions, and the detection arm sits **perpendicular** to the illumination. This orthogonal geometry is the definition of light-sheet microscopy ({ref}`Chapter 5 <chap5_3>`): only the plane you are imaging is ever excited, so out-of-focus fluorophores neither bleach nor contribute background, and you get optical sectioning for free without a pinhole.

The detection path is a detection objective, then a **fluorescence filter**, then a **tube lens**, then the camera. Note the order and what it tells you. The filter sits between the objective and the tube lens, which means it sits in infinity space, which means the detection objective is infinity-corrected. This is exactly the practical advantage described in the previous section: parallel rays let you insert a filter of any thickness without disturbing the focus.

Verdict: a fluorescence light-sheet microscope illuminating a single static plane. There is no scanning anywhere, so a three-dimensional stack would require moving the sample.

**Panel b.** The detection arm is identical, so all the information is in the illumination path. The cylindrical lens is gone. In its place there is a **scanning mirror**, followed by an **f-theta lens** and a **tube lens**.

The sheet is now made in time rather than in space. The beam stays a focused point, and the scanning mirror sweeps it rapidly across the field during a single camera exposure. Averaged over the exposure, the sample sees a sheet. The f-theta lens is the scan lens: it keeps the focused spot on a flat plane and makes its position proportional to the mirror angle, so the sweep is uniform.

Why go to this trouble? Because a static sheet made by a cylindrical lens is illuminated coherently across its whole width, so scattering objects in the sample produce interference stripes across the field. A scanned sheet illuminates one point at a time, and the striping largely disappears. You also gain control: the sheet height, and therefore the trade-off between field of view and sheet thickness, becomes a software parameter rather than a choice of lens.

```{tip}
This pair of panels is a perfect illustration of the general principle that a schematic encodes a set of decisions. Both instruments produce a light sheet. One does it with a passive optic and no moving parts; the other with an active component, extra electronics and extra alignment. Knowing which one you are looking at tells you what compromises the authors were willing to make.
```

## Worked example 2: patterned illumination with a spatial light modulator

The second example is an open-source structured illumination add-on {cite}`hannebelle2024opensim`, designed to bolt onto the illumination port of an ordinary inverted microscope.

```{figure} ../figures/chap7_schematic_opensim.png
---
width: 90%
name: chap7_schematic_opensim
align: center
---
Optical layout of the openSIM add-on. Three LEDs are combined, polarised, patterned by a reflective SLM and relayed into the illumination port of a commercial inverted microscope. Reproduced from Hannebelle et al. (2024), Nature Communications.
```

Step one: the sources are three **LEDs**, drawn as small coloured squares at the bottom right, in blue, green and red. Three sources, three colours, so this instrument does multicolour fluorescence. Step two: the sample is at the top, above the objective. Step three: the detector is a camera at the bottom. Step four and five: walk the path.

Each LED is followed by a pair of **collimator lenses**. LEDs emit into a wide solid angle, so unlike a laser they must be collimated before anything else can be done with them.

The three collimated beams then meet a **mirror** and two **dichroic mirrors**, arranged in a staircase. This is a standard beam-combining arrangement, and it is worth understanding as a pattern because you will see it constantly. The red beam reflects off the plain mirror. The first dichroic transmits red and reflects green, so after it the two travel together. The second dichroic transmits red and green and reflects blue. Three beams enter from three directions and one beam leaves, carrying all three colours on a common axis. The dichroic used in reverse is a beam combiner.

Next is a **linear polariser**, and shortly afterwards a **polarising beam splitter** and an **SLM**. That grouping is a signature. The polariser makes the light linearly polarised. The polarising beam splitter reflects that polarisation state towards the SLM. The SLM, which here is a reflective liquid-crystal device, rotates the polarisation pixel by pixel. On the way back, the polarising beam splitter transmits only the rotated component. The result is that the pattern written on the SLM becomes a pattern of intensity in the beam. This is the amplitude-modulation trick from the previous section: phase control plus polarisation optics equals amplitude control.

The patterned beam then passes a **tube lens** into the infinity space of the microscope, through the **filter cube** (excitation filter, dichroic, emission filter), up through the objective and onto the sample. The inset in the original figure shows what arrives: a set of fine stripes at several orientations and phases.

Emission returns through the objective, transmits through the dichroic and emission filter of the cube, passes a second tube lens, and lands on the camera.

Verdict: a multicolour widefield fluorescence microscope in which the illumination is a programmable striped pattern. That is **structured illumination microscopy** ({ref}`Chapter 9 <chap9>`), which recovers spatial frequencies beyond the diffraction limit by encoding them into the moiré pattern between the sample and a known illumination grid. The camera records a series of raw frames at different stripe phases and orientations, and the resolution improvement is computed afterwards.

Notice how much you extracted without any knowledge of SIM theory. Three LEDs meant multicolour. A polariser plus polarising beam splitter plus SLM meant programmable amplitude patterning. A filter cube plus a single objective meant epifluorescence. The technique name is the only thing you needed the caption for.

## Worked example 3: one instrument, four modes

The third example {cite}`meng2022octoscope` is different in character: rather than one optical path, it shows four configurations of the same hardware.

```{figure} ../figures/chap7_schematic_octoscope.png
---
width: 95%
name: chap7_schematic_octoscope
align: center
---
Four measurement configurations of a single modular microscope, with the inactive elements greyed out in each panel. Camera or PMT detection, under one-photon or two-photon excitation. Reproduced from Meng et al. (2022), Journal of Optics.
```

The greying-out is the key to reading this figure. In each panel the active path is drawn solid and everything else is faded, so the four panels are really four states of one machine.

**Panel a.** Excitation enters from the right as a broad blue beam, reflects off a dichroic, and passes through the objective onto the sample. Emission returns, transmits through the dichroic, passes a **tube lens** and an **emission filter**, and reaches a **camera**. Blue excitation and a camera: this is one-photon widefield fluorescence imaging.

**Panel d.** The excitation path is identical. The difference is downstream: a small mirror has been inserted in the detection path, folding the light sideways through a lens and onto a **PMT**, while the camera is greyed out. Same excitation, different detector.

Ask what changes. A PMT has no pixels, so the instrument is no longer forming an image; it is measuring total emitted intensity as a function of time, with single-photon sensitivity and nanosecond response. That is the right detector for photon counting, for fluorescence correlation spectroscopy, or for lifetime measurements ({ref}`Chapter 8 <chap8>`), and the wrong one for morphology.

**Panel f.** Now the excitation beam is drawn in red and enters along a different path, and the detection is again the PMT. A red or near-infrared excitation beam paired with a point detector is the signature of **two-photon excitation**. Two photons at, say, 800 nm are absorbed simultaneously to drive a transition that one 400 nm photon would drive. Because the process depends on the square of the intensity, it only happens in the tiny volume at the focus, which is why no pinhole is needed and why a single-element detector suffices: all the light that arrives came from the focal spot.

**Panel i.** Two-photon excitation again, but detected on the camera.

```{tip}
**What the four panels are really for.** Two excitation modes multiplied by two detection modes gives four experiments on one optical table. One-photon plus camera gives fast morphology over a field of view. One-photon plus PMT gives quantitative photon counting from a point. Two-photon plus PMT gives deep, optically sectioned scanning. Two-photon plus camera gives a spatially resolved record of a two-photon excited volume. The whole design philosophy is modularity, and you can read it straight off the figure by noticing that only two components ever move: the excitation input and one flip mirror.
```

## Your turn

Here is a schematic to work through yourself before reading the answer. It is an affordable, easy-to-build light-sheet microscope for cleared tissue {cite}`otomo2024descspim`.

```{figure} ../figures/chap7_schematic_descspim.png
---
width: 90%
name: chap7_schematic_descspim
align: center
---
System overview of descSPIM. Work through the five steps before opening the solution below. Reproduced from Otomo et al. (2024), Nature Communications.
```

Apply the procedure. Where is the light source, and what kind is it? Where is the sample, and what is unusual about how it is mounted? Where is the detector, and what does the choice of detector suggest? What does each component in the illumination path do, and why are there two cylindrical lenses rather than one? What is the black block on the far side of the sample for?

```{admonition} Solution
:class: tip, dropdown

**Source.** A laser, coupled into a single-mode optical fibre. The fibre is doing something worth noticing: it transports light from a laser box that can sit anywhere on the bench, and it delivers a clean, diverging beam with a well-defined mode from a small, easily mounted output. Fibre coupling is a common way to keep a build simple.

**Sample.** Bottom right, mounted on a stage that moves in x, y, z and $\theta$. Rotation is the giveaway: this is a sample you want to view from several directions, which in light-sheet microscopy means a thick, three-dimensional specimen. The caption confirms it is cleared tissue in a cuvette.

**Detector.** A CMOS camera at the top right, on its own z stage. A plain CMOS rather than an sCMOS is a budget decision, consistent with the entire point of the instrument, and it is acceptable here because cleared and well-labelled tissue is bright.

**Illumination path.** A collimating lens turns the diverging fibre output into a parallel beam, and it is achromatic, meaning it is corrected for two wavelengths and therefore intended for use with more than one laser line. Three mirrors follow. Two would be enough to redirect a beam in a plane; the third is there because two mirrors in series are the standard way of gaining independent control of beam position and angle during alignment.

**Two cylindrical lenses.** Both form a sheet, but with different focal lengths, 500 mm and 150 mm. A longer focal length gives a weaker focus: a thicker sheet that stays thin over a longer distance. A shorter focal length gives a thinner sheet over a shorter distance. The two lenses are therefore two operating modes: wide field of view with modest axial resolution, or better axial resolution over a narrower region. The second one is mounted on a translation stage so its waist can be positioned within the sample.

**Beam block.** The illumination beam does not stop at the sample; it continues out the other side. Left alone it would hit the wall of the enclosure and scatter light back into the detection path. The block absorbs it. This is unglamorous and it is in the figure because it matters.

**Verdict.** A one-sided, static light-sheet microscope for cleared tissue, built from stock catalogue parts, with two selectable sheet geometries and a rotatable sample. Optical sectioning comes from the sheet; three-dimensional stacks come from translating the sample and the camera together.
```

## A note on what schematics do not tell you

Two cautions before we move on.

First, schematics are drawn to explain, not to build from. Distances are not to scale, relay lenses are often omitted, and mounts, apertures and beam dumps are usually invisible. The descSPIM figure is unusually honest in drawing its beam block. Do not conclude that a component is absent just because it is not drawn.

Second, the caption is part of the figure. Authors put focal lengths, numerical apertures, model numbers and the meanings of their acronyms there, and reading it will answer most of the questions the drawing raises. The exercise of reading a schematic cold is a good way to learn, but in real life you read the caption too.

With that, we have the skill in one direction: from a drawing to a function. The last section runs it the other way, and asks how you would arrive at such a drawing in the first place.
