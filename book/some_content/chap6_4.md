# Quantitative approaches

1D Fourier transforms
---
aa


2D Fourier transforms
---
aa

Immersion objectives
---
A perfect air lens, meaning the gap between the front element of the objective and the sample is filled with air, can have a maximum NA of around 1.0 due to the refractive index of air. To achieve higher NA, it is necessary to fill the space between the objective and the sample with immersion media with n greater than 1.0, such as water (n=1.33), glycerol (n=1.46) or immersion oil (n=1.51).

When light travels between mediums with different refractive indexes at an angle, the light slows and is bent, this is refraction. Typically this occurs when light emitted from the sample hits a glass-air interface. As illustrated in Fig.3, when air fills the interface gap between sample and objective, the higher angles are bent at the interface and fail to be collected by the objective. In contrast, when oil (much higher refractive index) fills the gap, light is bent less and is all collected by the objective.
Resolution and Numerical Aperture_image-3.png
Figure 3: Refractive index matching fluid allows better angular collection efficiency for samples mounted in mediums other than air. In the left image, the collection angles of the objective are diminished because of refraction at the glass-air interface. In contrast, matching the refractive index of the glass with immersion oil, as illustrated in the right panel, allows a larger range of angles of light from the sample to enter the lens.

For thin samples mounted with index-matching medium, the glass and sample can be considered to have the same refractive index. When sample thickness increases, or where no index-matching medium can be used (live cell imaging), choosing immersion objectives that use water or glycerol as index matching fluids, being similar to the sample, can be more effective

Sampling Diffraction-Limited Objects
---
(https://www.teledynevisionsolutions.com/learn/learning-center/scientific-imaging/resolution-and-numerical-aperture/)

Diffraction-limited imaging defines the size of the smallest objects in the image. Anything smaller will be blurred by the microscope to the diffraction-limited size. Since the diffraction limit is set by the NA of the objective and the wavelength of light used, it may be mistakenly assumed that we are always performing diffraction-limited imaging. However, this is not necessarily true depending on the size of the camera's pixel and the magnification of the system.

The total magnification (M) of the optical system makes objects in the sample appear M times larger at the camera. For example, a microscope camera might have 2000×2000 pixels with each pixel measuring 6.5 µm by 6.5 µm. Depending on the magnification, the pixel will sample different regions in the sample. Using a 10x lens, one 6.5 µm by 6.5 µm pixel would sample 650 nm by 650 nm of the sample. In contrast, using a 100x lens that same pixel would sample 65 nm by 65 nm.

Camera pixel size should be matched to the diffraction-limited blur. In order to differentiate between two objects, one must make a measurement in between them. By convention, the pixel size needs to be 1÷2.3 (~0.44) as large as the smallest object to be imaged. If the smallest object in a sample is 1 µm, the pixel size should be at least 0.44 µm in order to best image the sample. Pixel sizes larger than this will lose information, known as undersampling, while pixel sizes smaller than this provide no extra information, known as oversampling.

Fig.4 illustrates a case where the sensor's large pixels undersample the spatial information in the neuron. Using smaller pixels or increasing the magnification solves the problem.
Resolution and Numerical Aperture_image-4.png
Figure 4: Illustration of the effect of pixel size and magnification on sampling spatial information in the final image. Large pixels under-sample the possible spatial information leading to a 'pixelated' appearance (left) but using smaller pixel sensor (middle) or magnifying more (right) allows optimal sampling.

For the example given earlier of a diffraction-limited resolution of 320 nm, one would need pixels sampling every 140 nm in the image to truly achieve this resolution. With a 6.5 µm pixel, 45-50x magnification would provide pixels of an appropriate size. Magnification has no influence on the optical blur of the microscope but does allow appropriate sampling to recover all the information transmitted by the microscope.

Smallest feature measurable: an inverse problem
---

The maximum resolving power of an optical system is defined by the following: how close together can two small features be such that the blurring of their images doesn't lead to them appearing as one feature? This is a loose definition that depends on the wavelength of light used.

In general, the larger the back aperture the wider the angles we can collect, the larger the NA, and the higher the resolution. The theoretical maximum angle that light can be collected by a lens is 180 (it would have to be a huge lens), making the maximum half-angle 90. Realistically, half-angles above 72 cannot currently be achieved. For an air lens with half-angle 72, the NA would then be 0.95 and the maximum resolution (the smallest object that could be observed) of the image would be 320 nm. Two objects closer than 320 nm would not be resolved and would appear as one object, and anything smaller than 320 nm would appear as a blurry blob 320 nm in size. This is the diffraction limit to imaging.


Interactive resolution calculator
---
https://www.microscope.healthcare.nikon.com/microtools/resolution-calculator/
