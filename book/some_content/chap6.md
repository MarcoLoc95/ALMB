# 6 - A gentle introduction to Fourier optics

When in physics we talk about frequencies, most people immediately think about _temporal_ frequencies, or in other words repetitive changes in time with a fixed rate. For example, a melody is composed of several musical notes, but at the very core each note corresponds to a simple harmonic wave with a specific frequency: the note A4 (La) corresponds to 440 Hz, C5 (Do) to 523 Hz and so on. Most of us are somehow naturally able to tell the difference between a low and a high note, even in a complex song where multiple instruments are played at the same time. That is because the cochlea in our ear performs an operation very similar to the Fourier transform, decomposing the sound in its costituent harmonics, with hair cells signaling the brain accordingly.

However, since any function can be expressed as a combination of sinusoids, the decomposition of images in _spatial_ frequencies should also be possible. Why does it feel hard to imagine and not intuitive? There are two reasons: first, our eyes see shapes, colors and contrasts, in other words the "real" image, not its frequencies; second, images impressed on our retina are two-dimensional, therefore recognizing underlying geometrical patterns is just harder for our brains. Here's good news for the reader: in the same way professional musicians and sound technicians can get a deep understanding of spectra and filtering, you can be trained to think of images in terms of spatial frequencies and evaluate the consequences for microscopy. Luckily, we have access to a multitude of computational tools that make visualizing the frequency space very easy, so you do not have to appeal to your imagination too much.

To get a first intuition, we can look at the below picture of rolling hills covered in grass. We see that the hill silhouette changes "slowly" throughout the landscape, while the profile of grass blades changes very "rapidly". They correspond, respectively, to low and high spatial frequencies. One can even notice that the sky forms a single horizontal band that is fairly uniform from left to right: this feature corresponds to the lowest spatial frequencies in the image. We will learn how to interpret the spatial Fourier transforms later on, but you can try to see if you can already recognize what features might be linked to each other, knowing that the closer to the center of the Fourier transform, the lower the frequencies.

```{figure} ../figures/hills_FFT.png
---
height: 50%
name: hills_FFT
align: center
---
Adapted from "Rolling green hills in the East Bay Area, California" by ShakataGaNai, CC-BY-SA-3.0
```

Why are spatial frequencies so important in microscopy? First and foremost, spatial filtering is the reason why the resolution of any microscope is inherently limited. Understanding this physical principle can lead to deep insights into image formation and suggest techniques to enhance image quality. Second, Fourier transforms have the power to reveal hidden patterns within an image, such as symmetries, repeating structures or textural features that directly relate to the sample’s structure and may be difficult to notice with the naked eye.

At the end of this chapter you should be able to:
- Describe the Huygens-Fresnel principle and its role in understanding diffraction
- Explain why we measure the Fourier transform of an object in the far field
- Explain why a converging lens acts as a Fourier transformer
- Illustrate the relationship between the Fourier transform and the resolution limit
- Discuss the implications of deconvolution and pixel reassignment in image reconstruction
- Calculate the Fourier transform of simple 1D functions
- Visualize the Fourier transform of 2D functions and images using Python
