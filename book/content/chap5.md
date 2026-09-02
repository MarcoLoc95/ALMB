(chap5)=
# 5 - Optical sectioning

In {ref}`Chapter 4 <chap4>` we gained something that no amount of clever optics had given us before: molecular specificity. Attach a fluorophore to a protein, choose the right filter set, and that protein alone lights up against a black background. It feels like the problem of imaging biology has been solved.

Point the same microscope at a thick specimen and the feeling evaporates. A monolayer of cultured cells looks superb. A 30 µm slice of brain tissue looks like a photograph taken through frosted glass: the structures are there somewhere, but they are buried under a bright, shapeless haze.

The reason is not a failure of the labelling. It is a consequence of a fact we established in {ref}`Chapter 3 <chap3_2>`: the point spread function of an objective is stretched along the optical axis, typically by a factor of two to three relative to its width. What matters here is a stronger and less obvious version of that statement. In a widefield fluorescence microscope, every fluorophore in the illuminated cone is excited, whether or not it sits in the focal plane, and every one of them sends light back into the objective.

It is worth doing the arithmetic, because the result is worse than most people expect. Consider a uniformly labelled specimen and ask how much light reaches the detector from a plane at distance $z$ from the focus. Far from the focus, the illumination is spread over an area growing as $z^2$, so each fluorophore is excited $z^2$ times more weakly. But that same plane contains $z^2$ times more excited fluorophores, because the cone is $z^2$ times wider. The two factors cancel exactly. Every plane in the specimen, in focus or not, contributes roughly the same amount of light.

That is the whole problem in one sentence. Focus on a plane inside a 30 µm specimen with a section thickness of half a micrometre, and you collect one plane worth of signal on top of about sixty planes worth of background. The signal is still there. It is simply drowned.

Notice that this is not a resolution problem. The objective still resolves 200 nm laterally, and the information about the focal plane is still present in the recorded image. What has collapsed is the **contrast**: the difference between a labelled structure and its surroundings, measured against the noise. No amount of magnification, and no amount of contrast stretching in software, will bring it back, because the background carries its own shot noise.

**Optical sectioning** is the name for any technique that solves this: a way of recording light from one thin plane of a thick specimen while rejecting, or better still never generating, the light from everywhere else. Stack the sections and you have a three-dimensional image of the specimen, acquired without ever cutting it.

There are only two honest strategies, and this chapter covers both. The first is to illuminate everything as before and then throw away the out-of-focus light on the detection side, which is what a confocal pinhole does. The second, and the more elegant, is to arrange the illumination so that the out-of-focus light is never produced in the first place. Total internal reflection, light-sheet illumination and two-photon excitation are three very different ways of doing exactly that (_{numref}`Fig. {number} <chap5_sectioning_overview>`_).

```{figure} ../figures/chap5_sectioning_overview.png
---
width: 100%
name: chap5_sectioning_overview
align: center
---
Five ways of dealing with out-of-focus light, with the excited fluorophores drawn bright and the rest faint. Widefield illuminates the whole depth of the specimen, so every plane contributes. Confocal microscopy concentrates the excitation into a double cone, which still lights up everything it passes through, and then uses a pinhole below the objective to admit light from the focus alone, marked in green. TIRF confines the excitation to a shell roughly 100 nm thick against the coverslip. Light-sheet microscopy illuminates only the plane being imaged, using a second objective placed at right angles to the detection objective. Multiphoton excitation sends the same cone through the specimen but makes fluorescence so improbable outside the focus that only the focal volume glows. Widefield and confocal are the two that generate light they will have to throw away.
```

Each of the four occupies a different corner of the same trade space, defined by four quantities you will meet again and again: how thin a section you get, how fast you get it, how deep into the specimen you can reach, and how much damage you do to the sample along the way. No technique wins on all four, and the point of this chapter is to make the compromises explicit enough that you can choose sensibly at the microscope.

At the end of this chapter you should be able to:

- Explain why a widefield fluorescence image of a thick specimen loses contrast, and argue why this is a problem of background rather than of lateral resolution.
- Describe how a confocal pinhole rejects out-of-focus light, and calculate the Airy unit for a given objective and emission wavelength.
- Justify a choice of pinhole diameter for a given specimen and photon budget, using the trade-off between optical section thickness and collected signal.
- Distinguish point-scanning from spinning-disk confocal microscopy, and select the appropriate one for a stated experiment.
- Calculate the critical angle and the evanescent penetration depth at a glass-sample interface, and explain why objective-type TIRF requires an objective whose numerical aperture exceeds the refractive index of the specimen.
- Relate the Gaussian beam waist and Rayleigh range to the trade-off between light-sheet thickness and usable field of view, and explain what a Bessel beam buys and what it costs.
- Describe two-photon excitation, and explain why the quadratic dependence on intensity confines fluorescence to the focal volume without any pinhole.
- Compare the four techniques in terms of sectioning strength, speed, penetration depth and phototoxicity, and defend a choice of technique for a given biological question.
