# 6 - A gentle introduction to Fourier optics

When in physics we talk about frequencies, most people immediately think about _temporal_ frequencies, or in other words repetitive changes in time with a fixed rate. For example, a melody is composed of several musical notes, but at the very core each note corresponds to a simple sinusoid with a specific frequency: the note A4 (La) corresponds to 440 Hz, C5 (Do) to 523 Hz and so on. Most of us are somehow naturally able to tell the difference between a low and a high note, even in a complex song where multiple instruments play at the same time. That is because the cochlea in our ear performs an operation very similar to the Fourier transform, decomposing the sound in its costituent harmonics, and hair cells signal the brain accordingly.

However, since any function can be expressed as a combination of sinusoids, the decomposition of images in _spatial_ frequencies is possible (and extremely useful). Why does it not feel intuitive? There are two reasons: first, our eyes see shapes, colors and contrasts, not frequencies; second, images impressed on our retina are two-dimensional, therefore recognizing underlying geometrical patterns is just harder for our brains. Here's good news for the reader: in the same way professional musicians and sound technicians can get a deep understanding of spectra and filtering, you can be trained to think of images in terms of spatial frequencies and the consequences of filtering in microscopy. Luckily, we have access to a multitude of computational tools that make the conversion to the frequency space very easy and will be useful throughout the whole chapter.

To get a first intuition, we can look at the below picture of rolling hills covered in grass. We see that the hill silhouette changes "slowly" throughout the landscape, while the profile of grass blades changes very "rapidly". They correspond, respectively, to low and high spatial frequencies. One can even notice that the sky forms a single horizontal band that is fairly uniform from left to right: this feature corresponds to the lowest spatial frequencies in the image. We will learn how to interpret the Fourier transforms of images later on, but you can try to see if you recognize  

```{figure} ../figures/hills_FFT.png
---
height: 50%
name: hills_FFT
align: center
---
Adapted from "Rolling green hills in the East Bay Area, California" by ShakataGaNai, CC-BY-SA-3.0
```
We will delve into the details later, but as a quick introduction

```{figure} ../figures/waves_FFT.png
---
height: 50%
name: waves_FFT
align: center
---
Adapted from iStockphoto
```
