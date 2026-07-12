# Appendix: The math of Fourier transforms 

Having built the intuition, we gather here the quantitative tools that make Fourier optics usable in practice. We first list the handful of general properties that let us manipulate transforms without recomputing integrals, then catalogue the transforms of the simple functions that keep reappearing in microscopy, in one and two dimensions. We close by connecting the resolution limit to the very concrete question of how finely a camera must sample an image, and to the idea of imaging as an inverse problem.

Throughout, we use the convention introduced earlier in the chapter,

$$
F(k) = \mathcal{F}\{f\}(k) = \int_{-\infty}^{+\infty} f(x)\, e^{-ikx}\, dx, \qquad f(x) = \frac{1}{2\pi}\int_{-\infty}^{+\infty} F(k)\, e^{ikx}\, dk,
$$

and write transform pairs as $f(x) \leftrightarrow F(k)$. The factors of $2\pi$ that appear below are a consequence of this particular convention; other textbooks distribute them differently, so it is the shapes and the reciprocal relationships that matter, not the exact constants.

## General properties of Fourier transforms

### Linearity

$$
a\,f(x) + b\,g(x) \;\leftrightarrow\; a\,F(k) + b\,G(k)
$$

The transform of a sum is the sum of the transforms, and scaling a function scales its transform. This is the property that licenses the whole picture of an image as a sum of independent gratings: we can analyze each frequency on its own and add the results back together.

### Shift

$$
f(x - x_0) \;\leftrightarrow\; e^{-ikx_0}\,F(k)
$$

Shifting a function in space multiplies its spectrum by a linear phase ramp, while leaving the magnitude $|F(k)|$ untouched. This is exactly why the position (phase) of a grating appears as the phase of its Fourier points, without changing where those points sit or how bright they are.

### Convolution

$$
(f \ast g)(x) \;\leftrightarrow\; F(k)\,G(k)
$$

Convolution in space becomes ordinary multiplication in frequency. This is the single most useful property for microscopy: the imaging relation $i = o \ast \text{PSF}$ turns into $\hat i = \hat o \cdot \text{OTF}$, which is what made deconvolution and spatial filtering possible in the previous section.

### Multiplication

$$
f(x)\,g(x) \;\leftrightarrow\; \frac{1}{2\pi}\,(F \ast G)(k)
$$

The dual of the convolution property: multiplying two functions in space convolves their spectra in frequency. This explains, for example, why cutting off a wave with a finite aperture, that is multiplying it by a rectangular window, smears its spectrum by convolving it with a sinc, which is the frequency-space face of diffraction from a finite lens.

### Duality

$$
\text{if } f(x) \leftrightarrow F(k), \quad \text{then } F(x) \leftrightarrow 2\pi\, f(-k)
$$

The two domains play symmetric roles, up to a reflection and a constant. A transform pair read backwards is essentially a transform pair again. This symmetry is why a rectangle and a sinc are partners whichever way round we take them, and why, as we will see, a Gaussian is its own partner.

## 1D Fourier transforms

For each pair we begin from the definition, $F(k) = \int_{-\infty}^{+\infty} f(x)\, e^{-ikx}\, dx$, and carry the integral through. Several of the results lean on a single identity, so we derive that one first.

### Dirac delta

The delta function is fixed by its sifting property, $\int f(x)\,\delta(x - x_0)\,dx = f(x_0)$. Taking $f(x) = e^{-ikx}$ and $x_0 = 0$ evaluates the transform at once:

$$
F(k) = \int_{-\infty}^{+\infty} \delta(x)\, e^{-ikx}\, dx = e^{-ik\cdot 0} = 1,
$$

so $\delta(x) \leftrightarrow 1$. A point in space contains every spatial frequency, all with equal weight and in phase; a displaced point only acquires a phase, $\delta(x - x_0) \leftrightarrow e^{-ikx_0}$. This is the formal reason a point source excites the entire frequency response of a system, and why imaging a tiny bead reveals the point spread function.

Inverting this pair gives an identity we will reuse below, the integral representation of the delta function:

$$
\int_{-\infty}^{+\infty} e^{-i(k - a)x}\, dx = 2\pi\, \delta(k - a).
$$ (deltarep)

### Constant

The integral $\int 1 \cdot e^{-ikx}\,dx$ does not converge in the ordinary sense, but {eq}`deltarep` evaluates it directly at $a = 0$:

$$
F(k) = \int_{-\infty}^{+\infty} 1 \cdot e^{-ikx}\, dx = 2\pi\, \delta(k),
$$

so $1 \leftrightarrow 2\pi\,\delta(k)$. A perfectly uniform field has only the zero-frequency, or DC, component. This is the background brightness that a high-pass filter removes, leaving edges behind.

### Sine

Writing the sine through Euler's formula, $\sin(k_0 x) = \tfrac{1}{2i}\big(e^{ik_0 x} - e^{-ik_0 x}\big)$, and applying {eq}`deltarep` to each term,

$$
F(k) = \frac{1}{2i}\int_{-\infty}^{+\infty}\big(e^{ik_0 x} - e^{-ik_0 x}\big)e^{-ikx}\, dx = \frac{1}{2i}\Big[2\pi\,\delta(k - k_0) - 2\pi\,\delta(k + k_0)\Big].
$$

Using $1/i = -i$ and tidying the signs,

$$
\sin(k_0 x) \;\leftrightarrow\; i\pi\big[\delta(k + k_0) - \delta(k - k_0)\big].
$$

A pure sine is two opposite, purely imaginary spikes at $\pm k_0$: a single frequency, with the imaginary sign carrying the odd symmetry of the sine.

### Cosine

The cosine follows identically from $\cos(k_0 x) = \tfrac{1}{2}\big(e^{ik_0 x} + e^{-ik_0 x}\big)$:

$$
F(k) = \frac{1}{2}\Big[2\pi\,\delta(k - k_0) + 2\pi\,\delta(k + k_0)\Big] = \pi\big[\delta(k - k_0) + \delta(k + k_0)\big].
$$

A pure cosine is two real spikes at $\pm k_0$, the one-dimensional version of the grating that produces a symmetric pair of Fourier points, sitting farther from the center the finer the grating.

### Square wave

The square wave is periodic, so instead of integrating over the whole line we expand it in a Fourier series. Any function of period $L$, with fundamental frequency $k_0 = 2\pi/L$, can be written as $f(x) = \sum_{n=-\infty}^{\infty} c_n\, e^{ink_0 x}$, and transforming term by term with {eq}`deltarep` gives a result worth remembering in its own right: the spectrum of any periodic signal is a train of spikes at the harmonics,

$$
F(k) = \sum_{n=-\infty}^{\infty} c_n \int_{-\infty}^{+\infty} e^{ink_0 x}\, e^{-ikx}\, dx = 2\pi \sum_{n=-\infty}^{\infty} c_n\, \delta(k - n k_0).
$$

For the wave that alternates between $+1$ and $-1$ each half period, the coefficients come from one short integral over a single period:

$$
c_n = \frac{1}{L}\int_{-L/2}^{L/2} f(x)\, e^{-ink_0 x}\, dx = \frac{1}{L}\left[\int_{0}^{L/2} e^{-ink_0 x}\, dx - \int_{-L/2}^{0} e^{-ink_0 x}\, dx\right] = \frac{2\big(1 - (-1)^n\big)}{i\, L n k_0}.
$$

Because $1 - (-1)^n$ is zero for even $n$ and equal to $2$ for odd $n$, and $L k_0 = 2\pi$, the coefficients collapse to $c_n = -2i/(\pi n)$ for odd $n$ and vanish otherwise. The transform is therefore a ladder of spikes at the odd harmonics alone, with heights falling off as $1/n$:

$$
F(k) = 4i \sum_{n = 1, 3, 5, \dots}^{\infty} \frac{1}{n}\big[\delta(k + n k_0) - \delta(k - n k_0)\big].
$$

Reading the same coefficients back as a series recovers the familiar form $f(x) = \tfrac{4}{\pi}\big(\sin k_0 x + \tfrac{1}{3}\sin 3k_0 x + \tfrac{1}{5}\sin 5k_0 x + \cdots\big)$. The sharp corners of the wave are exactly what demand this infinite ladder of ever-higher harmonics, and a microscope that truncates the ladder at its cutoff frequency is what rounds those corners off. A single, isolated pulse is not periodic and behaves differently: its transform is the continuous sinc, $\text{rect}(x/d) \leftrightarrow d\,\sin(kd/2)/(kd/2)$, that we derived for the diffraction from one slit.

### Gaussian

Substituting the Gaussian into the definition, the two exponents combine into one and we complete the square,

$$
-\frac{x^2}{2\sigma^2} - ikx = -\frac{1}{2\sigma^2}\big(x + i\sigma^2 k\big)^2 - \frac{\sigma^2 k^2}{2},
$$

which pulls the $k$-dependent factor outside the integral:

$$
F(k) = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2}\, e^{-ikx}\, dx = e^{-\sigma^2 k^2/2}\int_{-\infty}^{+\infty} e^{-\frac{1}{2\sigma^2}(x + i\sigma^2 k)^2}\, dx.
$$

The remaining integral is the standard Gaussian integral, equal to $\sigma\sqrt{2\pi}$ (shifting the integration variable by the imaginary constant leaves its value unchanged), so

$$
e^{-x^2/2\sigma^2} \;\leftrightarrow\; \sigma\sqrt{2\pi}\; e^{-\sigma^2 k^2/2}.
$$

A Gaussian transforms into another Gaussian, and the two widths are reciprocal: a function that is narrow in space is broad in frequency, and vice versa. This reciprocity is the seed of both the resolution limit and the uncertainty principle, since one cannot be compact in both domains at once.

## 2D Fourier transforms

In two dimensions the definition reads $F(\vec k) = \int f(\vec r)\, e^{-i\vec k \cdot \vec r}\, d^2 r$, with $\vec k \cdot \vec r = k_x x + k_y y$. Whenever a function factorises as $f(x, y) = g(x)\, h(y)$ its transform factorises too, $F(\vec k) = G(k_x)\, H(k_y)$, which settles most of the cases below immediately.

### Dirac delta

Since $\delta(x, y) = \delta(x)\, \delta(y)$ is separable, the transform is the product of two one-dimensional delta transforms,

$$
\delta(x, y) \;\leftrightarrow\; 1,
$$

a completely flat two-dimensional spectrum: a single point contains all frequencies in every direction with equal weight.

### Constant

Equally, $1 = 1 \cdot 1$ separates, so the transform is the product of two one-dimensional constant transforms,

$$
1 \;\leftrightarrow\; (2\pi)^2\, \delta(k_x)\, \delta(k_y).
$$

A uniform image is pure DC, a single point at the very center of the spectrum.

### Sine

A sine grating $\sin(\vec k_0 \cdot \vec r)$ does not separate, but the two-dimensional version of {eq}`deltarep`, $\int e^{-i(\vec k - \vec k_0)\cdot \vec r}\, d^2 r = (2\pi)^2\, \delta(\vec k - \vec k_0)$, dispatches it through Euler's formula exactly as in one dimension:

$$
\sin(\vec k_0 \cdot \vec r) \;\leftrightarrow\; 2\pi^2 i\big[\delta(\vec k + \vec k_0) - \delta(\vec k - \vec k_0)\big],
$$

an antisymmetric, imaginary pair of points at $\pm \vec k_0$. The points lie along the direction in which the grating varies, perpendicular to the stripes themselves.

### Cosine

The cosine grating gives the same pair of points, now real and symmetric,

$$
\cos(\vec k_0 \cdot \vec r) \;\leftrightarrow\; 2\pi^2\big[\delta(\vec k - \vec k_0) + \delta(\vec k + \vec k_0)\big].
$$

Together, sine and cosine make explicit the mapping from the previous section: the direction of $\vec k_0$ fixes the orientation of the pair, its magnitude fixes the distance of the points from the center, and a shift of the grating shows up as a phase on the points, sine and cosine being simply two phases of the same thing.

### Square wave

A square grating of bars that varies only along $x$ is separable, $f(x, y) = \mathrm{sq}(x) \cdot 1$, so its transform is the one-dimensional ladder of odd harmonics in $k_x$ multiplied by $2\pi\, \delta(k_y)$:

$$
F(\vec k) = 2\pi\, \delta(k_y)\cdot 4i \sum_{n = 1, 3, 5, \dots}^{\infty} \frac{1}{n}\big[\delta(k_x + n k_0) - \delta(k_x - n k_0)\big].
$$

The spikes sit in a single row along the direction of variation, confined to $k_y = 0$: the two-dimensional grating is just the one-dimensional ladder laid along one axis. A checkerboard is the product of two perpendicular square waves, and since multiplying in space convolves the spectra, its transform is the convolution of two such rows, that is a full grid of spikes.

### Gaussian

The circular Gaussian separates, $e^{-(x^2 + y^2)/2\sigma^2} = e^{-x^2/2\sigma^2}\, e^{-y^2/2\sigma^2}$, so its transform is the product of two one-dimensional Gaussian transforms,

$$
e^{-(x^2 + y^2)/2\sigma^2} \;\leftrightarrow\; 2\pi\sigma^2\, e^{-\sigma^2(k_x^2 + k_y^2)/2}.
$$

A circular Gaussian blob transforms into a circular Gaussian, once again with reciprocal width. This is the standard soft model of a point spread function and its transfer function: a broad PSF (poor resolution) corresponds to a narrow OTF (little high-frequency content), tying the two-dimensional picture straight back to resolution.
