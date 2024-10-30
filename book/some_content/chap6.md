# 6 - A gentle introduction to Fourier optics

When in physics we talk about frequencies, most people immediately think about _temporal_ frequencies, or in other words repetitive changes in time with a fixed rate. For example, a melody is composed of several musical notes, but at the very core each note corresponds to a simple sinusoid with a specific frequency: the note A4 (La) corresponds to 440 Hz, C5 (Do) to 523 Hz and so on. Most of us are somehow naturally able to tell the difference between a low and a high note, even in a complex song where multiple instruments play at the same time. That is because the cochlea in our ear performs an operation very similar to the Fourier transform, decomposing the sound in its costituent harmonics, and hair cells signal the brain accordingly.

However, since any function can be expressed as a combination of sinusoids, the same decomposition in _spatial_ frequencies is possible (and extremely useful) with images. When we look at rolling hills covered in grass we can say that the hill silhouette corresponds to low spatial frequencies, because they change slowly throughout the landscape, while the profile of grass blades corresponds to high spatial frequencies, because they change very "rapidly". You can see a computed example here below. Note that, because the view is two-dimensional, its transform in spatial frequencies will also be two-dimensional.

```{figure} ../figures/hills_FFT.png
---
height: 400px
name: hills_FFT
align: center
---
Adapted from "Rolling green hills in the East Bay Area, California" by Jon 'ShakataGaNai' Davis, CC-BY-SA-3.0
```

IMG
Adapted from iStockphoto

In the same way professional musicians and sound technicians have a deep understanding of spectra and filtering, we can get trained to 


But here’s the catch: our eyes don’t naturally see in terms of frequencies. They see shapes, colors, and contrasts. So to reveal these hidden layers, we use tools like Fourier transforms. They allow us to take an image and break it down, showing us details we’d never see otherwise. Microscopy uses this principle constantly, helping us push beyond the limitations of our eyes, our lenses, and even our instruments.
