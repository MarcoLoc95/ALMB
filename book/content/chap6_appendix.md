# Appendix: The math of Fourier transforms

This appendix is optional, and nothing in Chapter 6 depends on it. Every result the chapter actually uses is derived at the point where it is used. What follows is for readers who are mathematically inclined and want to see the transforms worked out from the definition, and it doubles as a table to look things up in.

Throughout we use the convention of Chapter 6,

$$
F(k) = \mathcal{F}\{f\}(k) = \int_{-\infty}^{+\infty} f(x)\, e^{-ikx}\, dx, \qquad f(x) = \frac{1}{2\pi}\int_{-\infty}^{+\infty} F(k)\, e^{ikx}\, dk,
$$

and write transform pairs as $f(x) \leftrightarrow F(k)$. The factors of $2\pi$ below are a consequence of this particular convention; other textbooks distribute them differently, so it is the shapes and the reciprocal relationships that matter, not the exact constants.

## Summary

| property | $f(x)$ | $F(k)$ |
| :--- | :--- | :--- |
| linearity | $a\,f(x) + b\,g(x)$ | $a\,F(k) + b\,G(k)$ |
| shift | $f(x - x_0)$ | $e^{-ikx_0}\,F(k)$ |
| scaling | $f(ax)$ | $\dfrac{1}{\lvert a \rvert}\,F\!\left(\dfrac{k}{a}\right)$ |
| convolution | $(f \ast g)(x)$ | $F(k)\,G(k)$ |
| multiplication | $f(x)\,g(x)$ | $\dfrac{1}{2\pi}\,(F \ast G)(k)$ |
| duality | $F(x)$ | $2\pi\, f(-k)$ |

| 1D pair | $f(x)$ | $F(k)$ |
| :--- | :--- | :--- |
| Dirac delta | $\delta(x)$ | $1$ |
| constant | $1$ | $2\pi\,\delta(k)$ |
| sine | $\sin(k_0 x)$ | $i\pi\big[\delta(k + k_0) - \delta(k - k_0)\big]$ |
| cosine | $\cos(k_0 x)$ | $\pi\big[\delta(k - k_0) + \delta(k + k_0)\big]$ |
| square wave, period $L = 2\pi/k_0$ | $\mathrm{sq}(x)$ | $4i \displaystyle\sum_{n = 1, 3, 5, \dots} \frac{1}{n}\big[\delta(k + n k_0) - \delta(k - n k_0)\big]$ |
| single slit | $\mathrm{rect}(x/d)$ | $d\,\dfrac{\sin(kd/2)}{kd/2}$ |
| Gaussian | $e^{-x^2/2\sigma^2}$ | $\sigma\sqrt{2\pi}\; e^{-\sigma^2 k^2/2}$ |

| 2D pair | $f(\vec r)$ | $F(\vec k)$ |
| :--- | :--- | :--- |
| Dirac delta | $\delta(x, y)$ | $1$ |
| constant | $1$ | $(2\pi)^2\, \delta(k_x)\,\delta(k_y)$ |
| sine grating | $\sin(\vec k_0 \cdot \vec r)$ | $2\pi^2 i\big[\delta(\vec k + \vec k_0) - \delta(\vec k - \vec k_0)\big]$ |
| cosine grating | $\cos(\vec k_0 \cdot \vec r)$ | $2\pi^2\big[\delta(\vec k - \vec k_0) + \delta(\vec k + \vec k_0)\big]$ |
| bar grating along $x$ | $\mathrm{sq}(x)$ | $2\pi\,\delta(k_y) \cdot 4i \displaystyle\sum_{n = 1, 3, 5, \dots} \frac{1}{n}\big[\delta(k_x + n k_0) - \delta(k_x - n k_0)\big]$ |
| Gaussian | $e^{-(x^2 + y^2)/2\sigma^2}$ | $2\pi\sigma^2\, e^{-\sigma^2(k_x^2 + k_y^2)/2}$ |

The derivations follow.

## General properties of Fourier transforms

Each property follows from the definition by a change of variables, or by exchanging the order of two integrals. In this section every integral runs over the whole real line, and we drop the limits to keep the expressions readable. Exchanging the order of integration is legitimate for the well-behaved (absolutely integrable) functions of physical interest; for the delta functions and plane waves of the later sections, the same manipulations hold in the sense of distributions.

### Linearity

$$
a\,f(x) + b\,g(x) \;\leftrightarrow\; a\,F(k) + b\,G(k)
$$

The integral of a sum is the sum of the integrals, and constants can be taken outside:

$$
\int \big[a\,f(x) + b\,g(x)\big]\, e^{-ikx}\, dx = a\int f(x)\, e^{-ikx}\, dx + b\int g(x)\, e^{-ikx}\, dx = a\,F(k) + b\,G(k).
$$

The transform of a sum is the sum of the transforms. This is what licenses the whole picture of an image as a sum of independent gratings: each frequency can be analyzed on its own and the results added back together.

### Shift

$$
f(x - x_0) \;\leftrightarrow\; e^{-ikx_0}\,F(k)
$$

Substitute $u = x - x_0$, so that $x = u + x_0$ and $dx = du$. Shifting the whole real line by $x_0$ gives the whole real line again, so the limits do not change:

$$
\int f(x - x_0)\, e^{-ikx}\, dx = \int f(u)\, e^{-ik(u + x_0)}\, du = e^{-ikx_0} \int f(u)\, e^{-iku}\, du = e^{-ikx_0}\, F(k).
$$

The factor $e^{-ikx_0}$ has modulus $1$ for every $k$, so $\big|e^{-ikx_0} F(k)\big| = |F(k)|$.

Shifting a function in space multiplies its spectrum by a linear phase ramp and leaves the magnitude $|F(k)|$ untouched. This is why moving a grating changes the phase of its two Fourier points without changing where they sit or how bright they are.

### Scaling

$$
f(ax) \;\leftrightarrow\; \frac{1}{|a|}\,F\!\left(\frac{k}{a}\right)
$$

Substitute $u = ax$, so that $x = u/a$ and $dx = du/a$. The sign of $a$ matters, because it decides whether the limits keep their order.

If $a > 0$, then $u$ runs from $-\infty$ to $+\infty$ as $x$ does:

$$
\int_{-\infty}^{+\infty} f(ax)\, e^{-ikx}\, dx = \frac{1}{a}\int_{-\infty}^{+\infty} f(u)\, e^{-i(k/a)u}\, du = \frac{1}{a}\, F\!\left(\frac{k}{a}\right).
$$

If $a < 0$, then $u$ runs from $+\infty$ down to $-\infty$, and putting the limits back in the usual order costs a minus sign:

$$
\int_{-\infty}^{+\infty} f(ax)\, e^{-ikx}\, dx = \frac{1}{a}\int_{+\infty}^{-\infty} f(u)\, e^{-i(k/a)u}\, du = -\frac{1}{a}\int_{-\infty}^{+\infty} f(u)\, e^{-i(k/a)u}\, du = -\frac{1}{a}\, F\!\left(\frac{k}{a}\right).
$$

Since $|a| = a$ in the first case and $|a| = -a$ in the second, both are covered by the single prefactor $1/|a|$.

Squeeze a function in space and its spectrum spreads out, by exactly the same factor. Everything narrow is broadband. This single line is the reciprocity behind the resolution limit: a compact point spread function demands a wide transfer function, and a microscope with a narrow passband cannot produce a sharp point.

### Convolution

$$
(f \ast g)(x) \;\leftrightarrow\; F(k)\,G(k)
$$

The convolution is defined as $(f \ast g)(x) = \int f(x')\, g(x - x')\, dx'$. Insert this into the definition of the transform and exchange the order of the two integrals:

$$
\mathcal{F}\{f \ast g\}(k) = \int \left[\int f(x')\, g(x - x')\, dx'\right] e^{-ikx}\, dx = \int f(x') \left[\int g(x - x')\, e^{-ikx}\, dx\right] dx'.
$$

The inner bracket is the transform of $g$ shifted by $x'$, which by the shift property equals $e^{-ikx'}\, G(k)$. Since $G(k)$ does not depend on $x'$, it comes out of the remaining integral:

$$
\mathcal{F}\{f \ast g\}(k) = \int f(x')\, e^{-ikx'}\, G(k)\, dx' = G(k) \int f(x')\, e^{-ikx'}\, dx' = F(k)\, G(k).
$$

Convolution in space becomes ordinary multiplication in frequency. This is the most useful property in the whole chapter: the imaging relation $i = o \ast \text{PSF}$ turns into $\hat i = \hat o \cdot \text{OTF}$, which is what makes deconvolution and spatial filtering possible.

### Multiplication

$$
f(x)\,g(x) \;\leftrightarrow\; \frac{1}{2\pi}\,(F \ast G)(k)
$$

Write $f$ through its inverse transform, calling the integration variable $k'$ to keep it distinct from $k$:

$$
f(x) = \frac{1}{2\pi}\int F(k')\, e^{ik'x}\, dk'.
$$

Insert this into the transform of the product and exchange the order of integration:

$$
\mathcal{F}\{f g\}(k) = \int \left[\frac{1}{2\pi}\int F(k')\, e^{ik'x}\, dk'\right] g(x)\, e^{-ikx}\, dx = \frac{1}{2\pi}\int F(k') \left[\int g(x)\, e^{-i(k - k')x}\, dx\right] dk'.
$$

The inner bracket is the definition of $G$, evaluated at $k - k'$ instead of $k$. Hence

$$
\mathcal{F}\{f g\}(k) = \frac{1}{2\pi}\int F(k')\, G(k - k')\, dk' = \frac{1}{2\pi}\,(F \ast G)(k).
$$

The factor $1/2\pi$ comes from the inverse transform, and it is the one place where the asymmetry of our convention shows up in the properties.

The multiplication property is the dual of the convolution property. It explains why cutting a wave off with a finite aperture, that is multiplying it by a rectangular window, smears its spectrum by convolving it with a sinc, and it is also what widens the passband of a scanning microscope, whose effective PSF is a product.

### Duality

$$
\text{if } f(x) \leftrightarrow F(k), \quad \text{then } F(x) \leftrightarrow 2\pi\, f(-k)
$$

Start from the inverse formula and replace $x$ by $-x$ everywhere:

$$
f(-x) = \frac{1}{2\pi}\int F(k)\, e^{-ikx}\, dk, \qquad \text{that is} \qquad \int F(k)\, e^{-ikx}\, dk = 2\pi\, f(-x).
$$

The letters $x$ and $k$ are only labels, so we may swap them, calling the integration variable $x$ and the free variable $k$:

$$
\int F(x)\, e^{-ikx}\, dx = 2\pi\, f(-k).
$$

The left-hand side is, by definition, the Fourier transform of the function $F(x)$, which proves the property.

The two domains play symmetric roles, up to a reflection and a constant, so a transform pair read backwards is a transform pair again. For example, applying duality to the single-slit pair derived below gives

$$
d\,\frac{\sin(xd/2)}{xd/2} \;\leftrightarrow\; 2\pi\,\mathrm{rect}\!\left(\frac{-k}{d}\right) = 2\pi\,\mathrm{rect}\!\left(\frac{k}{d}\right),
$$

so a rectangle and a sinc are partners whichever way round they are taken, and a Gaussian is its own partner.

### Parseval's theorem

$$
\int_{-\infty}^{+\infty} |f(x)|^2\, dx = \frac{1}{2\pi}\int_{-\infty}^{+\infty} |F(k)|^2\, dk
$$

Write $|f(x)|^2 = f(x)\, f^*(x)$. Taking the complex conjugate of the inverse formula flips the sign in the exponent:

$$
f^*(x) = \frac{1}{2\pi}\int F^*(k)\, e^{-ikx}\, dk.
$$

Insert this and exchange the order of integration:

$$
\int |f(x)|^2\, dx = \int f(x) \left[\frac{1}{2\pi}\int F^*(k)\, e^{-ikx}\, dk\right] dx = \frac{1}{2\pi}\int F^*(k) \left[\int f(x)\, e^{-ikx}\, dx\right] dk.
$$

The inner bracket is $F(k)$, and $F^*(k)\,F(k) = |F(k)|^2$, which is the theorem.

Total power is the same whether it is counted in space or in frequency. This is why signal and noise can be weighed entirely in frequency space, as the Fourier Ring Correlation does.

## 1D Fourier transforms

Each pair starts from the definition, $F(k) = \int_{-\infty}^{+\infty} f(x)\, e^{-ikx}\, dx$. Several of them lean on one identity, the integral representation of the delta function, which we derive right after the first pair.

### Dirac delta

The delta function is fixed by its sifting property, $\int f(x)\,\delta(x - x_0)\,dx = f(x_0)$. Taking $f(x) = e^{-ikx}$ and $x_0 = 0$ evaluates the transform at once:

$$
F(k) = \int_{-\infty}^{+\infty} \delta(x)\, e^{-ikx}\, dx = e^{-ik\cdot 0} = 1,
$$

that is,

$$
\delta(x) \;\leftrightarrow\; 1.
$$

A point in space contains every spatial frequency, all with equal weight and in phase, which is the formal reason that imaging a tiny bead reveals the point spread function.

#### The integral representation of the delta function

Applying the inverse formula to the pair $\delta(x) \leftrightarrow 1$ gives

$$
\delta(x) = \frac{1}{2\pi}\int_{-\infty}^{+\infty} e^{ikx}\, dk.
$$

We want this in the form that appears inside forward transforms. First swap the names of the two letters, which changes nothing: $\delta(k) = \frac{1}{2\pi}\int e^{ixk}\, dx$. Then substitute $x \to -x$, which maps the real line onto itself, to get $\delta(k) = \frac{1}{2\pi}\int e^{-ikx}\, dx$. Finally replace $k$ by $k - a$:

$$
\int_{-\infty}^{+\infty} e^{-i(k - a)x}\, dx = 2\pi\, \delta(k - a).
$$ (deltarep)

Since this identity carries most of what follows, it is worth checking directly rather than only through the inverse formula. Write $q = k - a$ and cut the integral off at $\pm L$:

$$
\int_{-L}^{L} e^{-iqx}\, dx = \left[\frac{e^{-iqx}}{-iq}\right]_{-L}^{L} = \frac{e^{-iqL} - e^{iqL}}{-iq} = \frac{e^{iqL} - e^{-iqL}}{iq} = \frac{2\sin(qL)}{q},
$$

using $e^{i\theta} - e^{-i\theta} = 2i\sin\theta$ in the last step. Now watch what happens as $L \to \infty$. At $q = 0$ the function equals $2L$, so its peak grows without bound. Its first zeros sit at $q = \pm\pi/L$, so the peak becomes ever narrower. Its area stays fixed: substituting $u = qL$ and using the classical result $\int_{-\infty}^{+\infty} \frac{\sin u}{u}\, du = \pi$,

$$
\int_{-\infty}^{+\infty} \frac{2\sin(qL)}{q}\, dq = 2\int_{-\infty}^{+\infty} \frac{\sin u}{u}\, du = 2\pi.
$$

Away from $q = 0$ the function oscillates ever faster, so when it multiplies any smooth function $\varphi(q)$ under an integral those oscillations cancel, and only the neighbourhood of $q = 0$ survives, contributing $2\pi\,\varphi(0)$. That is exactly the action of $2\pi\,\delta(q)$, which confirms {eq}`deltarep`.

The same identity is in fact what makes the inverse formula work. Substituting the definition of $F$ into the inverse formula and exchanging the integrals,

$$
\frac{1}{2\pi}\int F(k)\, e^{ikx}\, dk = \int f(x') \left[\frac{1}{2\pi}\int e^{-ik(x' - x)}\, dk\right] dx' = \int f(x')\, \delta(x' - x)\, dx' = f(x),
$$

where the bracket is {eq}`deltarep` with the roles of the letters exchanged.

### Constant

The integral $\int 1 \cdot e^{-ikx}\,dx$ does not converge in the ordinary sense, but {eq}`deltarep` evaluates it directly at $a = 0$:

$$
F(k) = \int_{-\infty}^{+\infty} 1 \cdot e^{-ikx}\, dx = 2\pi\, \delta(k),
$$

that is,

$$
1 \;\leftrightarrow\; 2\pi\,\delta(k).
$$

Duality gives the same result from the delta pair: $\delta(x) \leftrightarrow 1$ implies $1 \leftrightarrow 2\pi\,\delta(-k)$, and $\delta(-k) = \delta(k)$ because the delta function is even.

A perfectly uniform field has only the zero-frequency, or DC, component: the background brightness that a high-pass filter removes.

### Sine

Write the sine through Euler's formula,

$$
\sin(k_0 x) = \frac{1}{2i}\big(e^{ik_0 x} - e^{-ik_0 x}\big),
$$

and insert it into the definition, combining the exponentials in each term:

$$
F(k) = \frac{1}{2i}\left[\int_{-\infty}^{+\infty} e^{-i(k - k_0)x}\, dx - \int_{-\infty}^{+\infty} e^{-i(k + k_0)x}\, dx\right].
$$

The first integral is {eq}`deltarep` with $a = k_0$, and the second is {eq}`deltarep` with $a = -k_0$:

$$
F(k) = \frac{1}{2i}\Big[2\pi\,\delta(k - k_0) - 2\pi\,\delta(k + k_0)\Big] = \frac{\pi}{i}\Big[\delta(k - k_0) - \delta(k + k_0)\Big].
$$

Since $1/i = i/i^2 = -i$, the prefactor is $-i\pi$, and absorbing the minus sign by swapping the two terms in the bracket gives

$$
\sin(k_0 x) \;\leftrightarrow\; i\pi\big[\delta(k + k_0) - \delta(k - k_0)\big].
$$

A pure sine is two opposite, purely imaginary spikes at $\pm k_0$, the imaginary sign carrying its odd symmetry.

### Cosine

The cosine follows in the same way from

$$
\cos(k_0 x) = \frac{1}{2}\big(e^{ik_0 x} + e^{-ik_0 x}\big).
$$

Inserting it into the definition and applying {eq}`deltarep` with $a = k_0$ and $a = -k_0$,

$$
F(k) = \frac{1}{2}\left[\int_{-\infty}^{+\infty} e^{-i(k - k_0)x}\, dx + \int_{-\infty}^{+\infty} e^{-i(k + k_0)x}\, dx\right] = \frac{1}{2}\Big[2\pi\,\delta(k - k_0) + 2\pi\,\delta(k + k_0)\Big],
$$

that is,

$$
\cos(k_0 x) \;\leftrightarrow\; \pi\big[\delta(k - k_0) + \delta(k + k_0)\big].
$$

A pure cosine is two real spikes at $\pm k_0$, the one-dimensional version of the grating that produces a symmetric pair of Fourier points, sitting farther from the center the finer the grating.

### Square wave

The square wave is periodic, so instead of integrating over the whole line we expand it in a Fourier series. Any function of period $L$, with fundamental frequency $k_0 = 2\pi/L$, can be written as

$$
f(x) = \sum_{n=-\infty}^{\infty} c_n\, e^{ink_0 x}, \qquad c_n = \frac{1}{L}\int_{-L/2}^{L/2} f(x)\, e^{-ink_0 x}\, dx.
$$

The formula for $c_n$ comes from multiplying the series by $e^{-imk_0 x}$ and integrating over one period. Every term with $n \neq m$ drops out, because

$$
\int_{-L/2}^{L/2} e^{i(n - m)k_0 x}\, dx = \frac{e^{i(n-m)\pi} - e^{-i(n-m)\pi}}{i(n - m)k_0} = \frac{2\sin\big((n - m)\pi\big)}{(n - m)k_0} = 0,
$$

using $k_0 L/2 = \pi$, while the term with $n = m$ integrates to $L$.

**Transforming the series.** Transforming term by term, each exponential is handled by {eq}`deltarep` with $a = nk_0$:

$$
F(k) = \sum_{n=-\infty}^{\infty} c_n \int_{-\infty}^{+\infty} e^{-i(k - nk_0)x}\, dx = 2\pi \sum_{n=-\infty}^{\infty} c_n\, \delta(k - n k_0).
$$

This is a result worth remembering in its own right: the spectrum of any periodic signal is a train of spikes at the harmonics $nk_0$, with weights $2\pi c_n$.

**The coefficients.** Take the wave that equals $-1$ for $-L/2 < x < 0$ and $+1$ for $0 < x < L/2$. The case $n = 0$ is the average over a period, which vanishes because the two halves cancel:

$$
c_0 = \frac{1}{L}\left[\int_0^{L/2} 1\, dx - \int_{-L/2}^{0} 1\, dx\right] = \frac{1}{L}\left[\frac{L}{2} - \frac{L}{2}\right] = 0.
$$

For $n \neq 0$ we split the integral at $x = 0$:

$$
c_n = \frac{1}{L}\left[\int_{0}^{L/2} e^{-ink_0 x}\, dx - \int_{-L/2}^{0} e^{-ink_0 x}\, dx\right].
$$

Each piece is elementary. Using $k_0 L/2 = \pi$ and $e^{\pm in\pi} = (-1)^n$,

$$
\int_{0}^{L/2} e^{-ink_0 x}\, dx = \left[\frac{e^{-ink_0 x}}{-ink_0}\right]_0^{L/2} = \frac{e^{-in\pi} - 1}{-ink_0} = \frac{1 - (-1)^n}{ink_0},
$$

$$
\int_{-L/2}^{0} e^{-ink_0 x}\, dx = \left[\frac{e^{-ink_0 x}}{-ink_0}\right]_{-L/2}^{0} = \frac{1 - e^{in\pi}}{-ink_0} = -\frac{1 - (-1)^n}{ink_0}.
$$

Subtracting the second from the first doubles the result:

$$
c_n = \frac{1}{L}\cdot\frac{2\big(1 - (-1)^n\big)}{ink_0} = \frac{2\big(1 - (-1)^n\big)}{i\, L n k_0}.
$$

Now $1 - (-1)^n$ is zero for even $n$ and equal to $2$ for odd $n$, and $L k_0 = 2\pi$. So the even coefficients vanish, and for odd $n$, positive or negative,

$$
c_n = \frac{4}{2\pi i n} = \frac{2}{i\pi n} = -\frac{2i}{\pi n}.
$$

**Collecting the spikes.** Only odd $n$ survive in $F(k)$. Group each positive odd $n$ with its partner $-n$, noting that $c_{-n} = -c_n = 2i/(\pi n)$:

$$
2\pi\big[c_n\,\delta(k - nk_0) + c_{-n}\,\delta(k + nk_0)\big] = 2\pi\cdot\frac{2i}{\pi n}\big[\delta(k + nk_0) - \delta(k - nk_0)\big] = \frac{4i}{n}\big[\delta(k + nk_0) - \delta(k - nk_0)\big].
$$

Summing over the positive odd $n$ gives a ladder of spikes at the odd harmonics alone, with heights falling off as $1/n$:

$$
\mathrm{sq}(x) \;\leftrightarrow\; 4i \sum_{n = 1, 3, 5, \dots}^{\infty} \frac{1}{n}\big[\delta(k + n k_0) - \delta(k - n k_0)\big].
$$

**Back to the series.** Reading the same coefficients back into the series, with the same pairing of $n$ and $-n$ and the identity $e^{-i\theta} - e^{i\theta} = -2i\sin\theta$,

$$
f(x) = \sum_{n = 1, 3, 5, \dots} \frac{2i}{\pi n}\big(e^{-ink_0 x} - e^{ink_0 x}\big) = \sum_{n = 1, 3, 5, \dots} \frac{2i}{\pi n}\big(-2i\sin nk_0 x\big) = \frac{4}{\pi}\sum_{n = 1, 3, 5, \dots} \frac{\sin nk_0 x}{n},
$$

which is the familiar form $f(x) = \tfrac{4}{\pi}\big(\sin k_0 x + \tfrac{1}{3}\sin 3k_0 x + \tfrac{1}{5}\sin 5k_0 x + \cdots\big)$. Each term is a sine of the kind derived above, and transforming $\tfrac{4}{\pi n}\sin(nk_0 x)$ with the sine pair gives $\tfrac{4}{\pi n}\cdot i\pi\big[\delta(k + nk_0) - \delta(k - nk_0)\big]$, the same spike pair as before, which is a useful cross-check.

The sharp corners of the wave are what demand this infinite ladder of ever-higher harmonics, and a microscope that truncates the ladder at its cut-off is what rounds those corners off.

### Rectangular pulse (single slit)

A single, isolated pulse is not periodic and behaves differently. Define

$$
\mathrm{rect}\!\left(\frac{x}{d}\right) = \begin{cases} 1, & |x| < d/2, \\ 0, & |x| > d/2. \end{cases}
$$

The function vanishes outside the slit, so the integral only runs over its width:

$$
F(k) = \int_{-d/2}^{d/2} e^{-ikx}\, dx = \left[\frac{e^{-ikx}}{-ik}\right]_{-d/2}^{d/2} = \frac{e^{-ikd/2} - e^{ikd/2}}{-ik} = \frac{e^{ikd/2} - e^{-ikd/2}}{ik}.
$$

Using $e^{i\theta} - e^{-i\theta} = 2i\sin\theta$ with $\theta = kd/2$,

$$
F(k) = \frac{2i\sin(kd/2)}{ik} = \frac{2\sin(kd/2)}{k}.
$$

Multiplying numerator and denominator by $d/2$ puts it in the standard sinc form:

$$
\mathrm{rect}\!\left(\frac{x}{d}\right) \;\leftrightarrow\; d\,\frac{\sin(kd/2)}{kd/2}.
$$

At $k = 0$ the division by $k$ above is not allowed, but there the integral is simply the width of the slit, $\int_{-d/2}^{d/2} dx = d$, which agrees with the limit $\sin u / u \to 1$. The zeros sit at $kd/2 = m\pi$, that is at $k = 2\pi m/d$ for nonzero integers $m$, so a narrower slit gives a wider central lobe: the scaling property again. This is the continuous sinc of single-slit diffraction in Chapter 6. Where the periodic square wave has a discrete ladder of spikes, the isolated pulse has a continuous spectrum.

### Gaussian

**Combining the exponents.** Substituting the Gaussian into the definition, the two exponentials merge into one:

$$
F(k) = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2}\, e^{-ikx}\, dx = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2 - ikx}\, dx.
$$

**Completing the square.** We look for constants $b$ and $c$ such that the exponent equals $-\frac{1}{2\sigma^2}(x + b)^2 + c$. Expanding,

$$
-\frac{1}{2\sigma^2}(x + b)^2 + c = -\frac{x^2}{2\sigma^2} - \frac{b}{\sigma^2}\,x - \frac{b^2}{2\sigma^2} + c.
$$

Matching the term linear in $x$ with $-ikx$ requires $b/\sigma^2 = ik$, so $b = i\sigma^2 k$. The constant terms must cancel, so $c = b^2/2\sigma^2 = (i\sigma^2 k)^2/2\sigma^2 = -\sigma^2 k^2/2$. Therefore

$$
-\frac{x^2}{2\sigma^2} - ikx = -\frac{1}{2\sigma^2}\big(x + i\sigma^2 k\big)^2 - \frac{\sigma^2 k^2}{2},
$$

and the factor that depends only on $k$ comes out of the integral:

$$
F(k) = e^{-\sigma^2 k^2/2}\int_{-\infty}^{+\infty} e^{-\frac{1}{2\sigma^2}(x + i\sigma^2 k)^2}\, dx.
$$

**The imaginary shift.** If $\sigma^2 k$ were a real number, the substitution $u = x + \sigma^2 k$ would simply slide the real line along itself, and the integral would equal the plain Gaussian integral. But the shift here is imaginary, so the substitution moves the integration path off the real axis, onto the horizontal line $\mathrm{Im}\, z = c$ in the complex plane, with $c = \sigma^2 k$. We need to show that the integral along that line is the same as along the real axis.

Let $g(z) = e^{-z^2/2\sigma^2}$. This function has no singularities anywhere in the complex plane, so by Cauchy's theorem its integral around any closed path vanishes. Take the rectangle with corners $-R$, $R$, $R + ic$, $-R + ic$, traversed in that order:

$$
\int_{-R}^{R} g(x)\, dx + \int_{0}^{c} g(R + iy)\, i\, dy - \int_{-R}^{R} g(x + ic)\, dx - \int_{0}^{c} g(-R + iy)\, i\, dy = 0.
$$

On the two vertical sides $z = \pm R + iy$ with $y$ between $0$ and $c$, so $z^2 = R^2 - y^2 \pm 2iRy$ and

$$
|g(z)| = e^{-(R^2 - y^2)/2\sigma^2} \le e^{-(R^2 - c^2)/2\sigma^2}.
$$

Each vertical side has length $|c|$, so each of those two integrals is at most $|c|\, e^{-(R^2 - c^2)/2\sigma^2}$ in absolute value, which tends to zero as $R \to \infty$. In that limit only the two horizontal integrals remain, and they must be equal:

$$
\int_{-\infty}^{+\infty} e^{-\frac{1}{2\sigma^2}(x + i\sigma^2 k)^2}\, dx = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2}\, dx.
$$

The argument works for either sign of $c$, that is for every $k$.

**The Gaussian integral.** It remains to evaluate $I = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2}\, dx$. The classic trick is to square it, writing the second copy with $y$ as the integration variable, so that it becomes an integral over the whole plane:

$$
I^2 = \int_{-\infty}^{+\infty} e^{-x^2/2\sigma^2}\, dx \int_{-\infty}^{+\infty} e^{-y^2/2\sigma^2}\, dy = \iint e^{-(x^2 + y^2)/2\sigma^2}\, dx\, dy.
$$

In polar coordinates $x^2 + y^2 = r^2$ and $dx\, dy = r\, dr\, d\theta$, and the extra factor of $r$ makes the radial integral elementary:

$$
I^2 = \int_0^{2\pi} d\theta \int_0^{\infty} e^{-r^2/2\sigma^2}\, r\, dr = 2\pi\left[-\sigma^2 e^{-r^2/2\sigma^2}\right]_0^{\infty} = 2\pi\sigma^2.
$$

Since $I > 0$, $I = \sigma\sqrt{2\pi}$. Putting the pieces together,

$$
e^{-x^2/2\sigma^2} \;\leftrightarrow\; \sigma\sqrt{2\pi}\; e^{-\sigma^2 k^2/2}.
$$

A Gaussian transforms into another Gaussian with reciprocal width: the original has width $\sigma$ in $x$, and its transform has width $1/\sigma$ in $k$, so the product of the two widths is fixed at $1$. This is the scaling property made concrete, and the seed of both the resolution limit and the uncertainty principle.

## 2D Fourier transforms

In two dimensions the definition reads $F(\vec k) = \int f(\vec r)\, e^{-i\vec k \cdot \vec r}\, d^2 r$, with $\vec k \cdot \vec r = k_x x + k_y y$ and $d^2 r = dx\, dy$.

**Separable functions.** Whenever a function factorises as $f(x, y) = g(x)\, h(y)$, its transform factorises too. Split the exponential with $e^{-i(k_x x + k_y y)} = e^{-ik_x x}\, e^{-ik_y y}$, and the double integral separates into a product of two single ones:

$$
F(\vec k) = \iint g(x)\, h(y)\, e^{-ik_x x}\, e^{-ik_y y}\, dx\, dy = \left[\int g(x)\, e^{-ik_x x}\, dx\right]\left[\int h(y)\, e^{-ik_y y}\, dy\right] = G(k_x)\, H(k_y).
$$

This settles most of the cases below immediately.

**The delta identity in 2D.** The plane wave $e^{-i(\vec k - \vec k_0)\cdot \vec r}$ is separable, so applying {eq}`deltarep` once in each direction,

$$
\iint e^{-i(\vec k - \vec k_0)\cdot \vec r}\, d^2 r = \int e^{-i(k_x - k_{0x})x}\, dx \int e^{-i(k_y - k_{0y})y}\, dy = 2\pi\,\delta(k_x - k_{0x}) \cdot 2\pi\,\delta(k_y - k_{0y}) = (2\pi)^2\, \delta(\vec k - \vec k_0),
$$ (deltarep2d)

where $\delta(\vec k - \vec k_0)$ stands for the product of the two one-dimensional deltas.

### Dirac delta

Since $\delta(x, y) = \delta(x)\, \delta(y)$ is separable, the transform is the product of two one-dimensional delta transforms, each equal to $1$:

$$
\delta(x, y) \;\leftrightarrow\; 1 \cdot 1 = 1.
$$

A single point contains all frequencies in every direction with equal weight: a completely flat two-dimensional spectrum.

### Constant

Equally, $1 = 1 \cdot 1$ separates, so the transform is the product of two one-dimensional constant transforms:

$$
1 \;\leftrightarrow\; 2\pi\,\delta(k_x) \cdot 2\pi\,\delta(k_y) = (2\pi)^2\, \delta(k_x)\,\delta(k_y).
$$

A uniform image is pure DC, a single point at the very center of the spectrum.

### Sine

A sine grating with a general direction $\vec k_0$ does not separate, but Euler's formula works exactly as in one dimension:

$$
\sin(\vec k_0 \cdot \vec r) = \frac{1}{2i}\big(e^{i\vec k_0 \cdot \vec r} - e^{-i\vec k_0 \cdot \vec r}\big).
$$

Inserting this into the definition and applying {eq}`deltarep2d` with $\vec k_0$ and with $-\vec k_0$,

$$
F(\vec k) = \frac{1}{2i}\left[\iint e^{-i(\vec k - \vec k_0)\cdot \vec r}\, d^2 r - \iint e^{-i(\vec k + \vec k_0)\cdot \vec r}\, d^2 r\right] = \frac{(2\pi)^2}{2i}\big[\delta(\vec k - \vec k_0) - \delta(\vec k + \vec k_0)\big].
$$

The prefactor is $4\pi^2/2i = -2\pi^2 i$, and swapping the two terms to absorb the minus sign gives

$$
\sin(\vec k_0 \cdot \vec r) \;\leftrightarrow\; 2\pi^2 i\big[\delta(\vec k + \vec k_0) - \delta(\vec k - \vec k_0)\big].
$$

This is an antisymmetric, imaginary pair of points at $\pm \vec k_0$. They lie along the direction in which the grating varies, which is perpendicular to the stripes themselves: the stripes are the lines on which $\vec k_0 \cdot \vec r$ is constant, and those lines are perpendicular to $\vec k_0$.

### Cosine

With $\cos(\vec k_0 \cdot \vec r) = \tfrac{1}{2}\big(e^{i\vec k_0 \cdot \vec r} + e^{-i\vec k_0 \cdot \vec r}\big)$ the same steps give $\tfrac{1}{2}(2\pi)^2 = 2\pi^2$ in front and a plus sign inside:

$$
\cos(\vec k_0 \cdot \vec r) \;\leftrightarrow\; 2\pi^2\big[\delta(\vec k - \vec k_0) + \delta(\vec k + \vec k_0)\big].
$$

The same pair of points as for the sine, now real and symmetric.

**Sine and cosine as two phases.** Both results are special cases of a grating with an arbitrary phase $\varphi$. Writing

$$
\cos(\vec k_0 \cdot \vec r - \varphi) = \frac{1}{2}\big(e^{-i\varphi}\, e^{i\vec k_0 \cdot \vec r} + e^{i\varphi}\, e^{-i\vec k_0 \cdot \vec r}\big)
$$

and transforming each term with {eq}`deltarep2d`,

$$
\cos(\vec k_0 \cdot \vec r - \varphi) \;\leftrightarrow\; 2\pi^2\big[e^{-i\varphi}\,\delta(\vec k - \vec k_0) + e^{i\varphi}\,\delta(\vec k + \vec k_0)\big].
$$

For $\varphi = 0$ this is the cosine. For $\varphi = \pi/2$ the grating is $\sin(\vec k_0 \cdot \vec r)$, and with $e^{\mp i\pi/2} = \mp i$ the bracket becomes $-i\,\delta(\vec k - \vec k_0) + i\,\delta(\vec k + \vec k_0)$, which is the sine result. Shifting a cosine grating by $\vec r_0$ gives $\cos\big(\vec k_0 \cdot (\vec r - \vec r_0)\big)$, which is the case $\varphi = \vec k_0 \cdot \vec r_0$.

This makes the mapping of Chapter 6 explicit: the direction of $\vec k_0$ fixes the orientation of the pair, its magnitude fixes the distance of the points from the center, and a shift of the grating shows up only as a phase on the points, sine and cosine being two phases of the same thing.

### Square wave

A square grating of bars that varies only along $x$ is separable, $f(x, y) = \mathrm{sq}(x) \cdot 1$. Its transform is therefore the one-dimensional ladder of odd harmonics in $k_x$, times the one-dimensional transform of the constant in $k_y$, which is $2\pi\,\delta(k_y)$:

$$
\mathrm{sq}(x) \;\leftrightarrow\; 2\pi\, \delta(k_y)\cdot 4i \sum_{n = 1, 3, 5, \dots}^{\infty} \frac{1}{n}\big[\delta(k_x + n k_0) - \delta(k_x - n k_0)\big].
$$

The spikes sit in a single row along the direction of variation, confined to $k_y = 0$: the two-dimensional grating is just the one-dimensional ladder laid along one axis.

**Checkerboard.** A checkerboard is the product of two perpendicular square waves, $\mathrm{sq}(x)\,\mathrm{sq}(y)$. Write $\mathrm{SQ}(k)$ for the one-dimensional square-wave spectrum above. The checkerboard is separable, so its transform is simply

$$
\mathrm{sq}(x)\,\mathrm{sq}(y) \;\leftrightarrow\; \mathrm{SQ}(k_x)\,\mathrm{SQ}(k_y) = -16 \sum_{n = 1, 3, \dots}\;\sum_{m = 1, 3, \dots} \frac{1}{nm}\big[\delta(k_x + nk_0) - \delta(k_x - nk_0)\big]\big[\delta(k_y + mk_0) - \delta(k_y - mk_0)\big],
$$

using $(4i)^2 = -16$. Expanding the two brackets places spikes at $(\pm nk_0, \pm mk_0)$ with $n$ and $m$ both odd: a full grid, with nothing on the axes, and the four strongest spikes at $(\pm k_0, \pm k_0)$ on the diagonals.

The same answer follows from the multiplication property. In two dimensions it carries $1/(2\pi)^2$, one factor of $1/2\pi$ per dimension, and it convolves the spectra of the two bar gratings, $2\pi\,\delta(k_y)\,\mathrm{SQ}(k_x)$ and $2\pi\,\delta(k_x)\,\mathrm{SQ}(k_y)$:

$$
\frac{1}{(2\pi)^2}\iint 2\pi\,\delta(k_y')\,\mathrm{SQ}(k_x') \cdot 2\pi\,\delta(k_x - k_x')\,\mathrm{SQ}(k_y - k_y')\, dk_x'\, dk_y' = \mathrm{SQ}(k_x)\,\mathrm{SQ}(k_y),
$$

since the two deltas set $k_x' = k_x$ and $k_y' = 0$. The convolution of two perpendicular rows of spikes is a full grid.

### Gaussian

The circular Gaussian separates, $e^{-(x^2 + y^2)/2\sigma^2} = e^{-x^2/2\sigma^2}\, e^{-y^2/2\sigma^2}$, so its transform is the product of two one-dimensional Gaussian transforms:

$$
F(\vec k) = \sigma\sqrt{2\pi}\, e^{-\sigma^2 k_x^2/2} \cdot \sigma\sqrt{2\pi}\, e^{-\sigma^2 k_y^2/2} = 2\pi\sigma^2\, e^{-\sigma^2(k_x^2 + k_y^2)/2},
$$

that is,

$$
e^{-(x^2 + y^2)/2\sigma^2} \;\leftrightarrow\; 2\pi\sigma^2\, e^{-\sigma^2(k_x^2 + k_y^2)/2}.
$$

The result depends only on $k_x^2 + k_y^2 = |\vec k|^2$, so a circular Gaussian blob transforms into a circular Gaussian, again with reciprocal width. This is the standard soft model of a point spread function and its transfer function: a broad PSF, meaning poor resolution, corresponds to a narrow OTF, meaning little high-frequency content.