(chap5_1)=
# Confocal microscopy

## A very good idea, thirty years too early

In 1957, a 30-year-old junior fellow at Harvard filed a patent for a microscope. His name was **Marvin Minsky**, and he is remembered today as one of the founders of artificial intelligence, not as a microscopist. That is exactly the point: he was not trying to invent an instrument. He was trying to trace the wiring of the brain, and he could not, because every slice of nervous tissue he looked at dissolved into the same milky haze we described in the chapter introduction.

His solution, sketched in {ref}`Chapter 1 <chap1_1>` and worth stating precisely here, has two halves that must be used together. First, do not spread the illumination across the whole field. Focus it to a single diffraction-limited spot, so that almost all of the excitation power lands in one tiny volume. Second, do not image the whole field either. Place an aperture in front of the detector, positioned so that the only light which can pass through it is light that came from that same spot.

Either half alone helps a little. Together they are transformative, because the two constraints are multiplicative: to reach the detector, a photon must have been emitted in the illuminated volume *and* have come from a point that the aperture accepts. The illuminated point and the detected point are the same point, which is where the name comes from: the illumination focus and the detection focus are _confocal_.

Minsky built the instrument. It worked. Nobody cared. He had no laser, so he used a zirconium arc lamp and threw away almost all of its light in order to make a point source. He had no fast scanner, so he moved the specimen instead of the beam, at a stately few frames per second. He had no computer, so he displayed the result on the long-persistence screen of a military radar oscilloscope and looked at it before it faded, with no way of recording it other than photographing the screen. The idea had to wait for lasers, photomultipliers, galvanometers and digital storage to catch up. By the late 1980s all four existed, and the confocal microscope went from curiosity to the standard workhorse of cell biology in about a decade.

## What the pinhole actually does

Consider a fluorophore sitting exactly in the focal plane. The objective collects its light, the tube lens focuses it, and it converges to a diffraction-limited spot in the image plane. Now consider a fluorophore a few micrometres above the focal plane. Its light also enters the objective, but because it was not at the front focal plane, the bundle leaving the objective is not collimated. The tube lens therefore focuses it somewhere else along the axis, and in the image plane it forms not a spot but a broad, dim disc.

Put a small aperture in the image plane and the consequences are asymmetric in exactly the way we want (_{numref}`Fig. {number} <chap5_widefield_vs_confocal>`_). The in-focus light is already concentrated into a spot smaller than the aperture, so essentially all of it gets through. The out-of-focus light is spread over an area hundreds of times larger, so only the tiny fraction that happens to fall on the aperture survives. The rejection is not perfect, and it becomes weaker as the defocus becomes small, but it is dramatic.

```{figure} ../figures/chap5_widefield_vs_confocal.png
---
width: 100%
name: chap5_widefield_vs_confocal
align: center
---
Ray trace through an objective and a tube lens for three fluorophores: one in the focal plane (green) and two displaced along the axis (orange). The in-focus light converges to a point in the image plane. The defocused light comes to a focus before or after it, and by the time it reaches the image plane it is spread out. A pinhole placed at the image plane transmits the first and blocks almost all of the second.
```

```{tip}
The pinhole sits in a plane that is conjugate to the focal plane, which is another way of saying that it sits where the camera sensor would sit. This is why a confocal image and a widefield image of the same specimen are in perfect register: the light takes the same path, and the only difference is what happens at the very end of it.
```

There is a second consequence that is easy to miss. Because the detector now sees light from one point at a time, it does not need to be a camera. Knowing *where* the light came from is not the detector's job, since the scanner already knows where it pointed the beam. All the detector has to do is count photons, and for that the right device is a photomultiplier tube or an avalanche photodiode: a single, extremely sensitive element with no spatial resolution whatsoever. The image is not recorded. It is assembled, pixel by pixel, from a sequence of intensity measurements.

## A cone instead of a column

So far we have changed only the detection side, and in principle that is enough: a pinhole in front of the detector sections a specimen no matter how it was illuminated. In practice every confocal instrument also changes the illumination, and it is worth seeing why.

In the widefield microscope of {ref}`Chapter 4 <chap4_1>`, the excitation beam arrives at the back of the objective collimated, so it leaves the front of the objective as a broad, roughly parallel **column** of light passing straight through the specimen. Remove the lens that collimates it, let the beam converge into the back aperture instead, and the objective focuses it to a diffraction-limited spot. The illuminated region becomes a **cone**, or rather a double cone: narrow at the focus and widening above and below it.

Be careful about what this does and does not achieve. It does *not* stop the other planes from being excited. The double cone still passes through the entire depth of the specimen, and every fluorophore it touches absorbs and emits, just as before. What changes is the distribution of power. The same total energy that was spread across a wide column is now concentrated into a tiny volume at the focus, so the plane we care about is excited far more intensely than any other, and the point we are measuring gives back much more signal. The out-of-focus light is still generated; the pinhole is still doing the work of removing it.

There is usually a second pinhole as well, on the excitation side, placed in a plane conjugate to the first. Its job is not sectioning but beam cleanup: it trims the laser to a clean spot, so that the illuminated point and the detected point really are the same point. The two pinholes and the focal spot in the specimen are all conjugate to one another, which is the geometric content of the word _confocal_.

```{tip}
A question that comes up every year: does the pinhole reduce the numerical aperture?

It does not. The numerical aperture is a property of the objective and the immersion medium, $\text{NA} = n\sin\theta$, fixed by the widest cone of light the front lens can accept. The pinhole sits far downstream, in the image plane, long after that cone has been collected. What it does is discard part of the Airy pattern that the objective has already formed, which changes the shape of the effective point spread function slightly, but not the angular acceptance that produced it. If you replaced the detector with a screen, the spot you would see just before the pinhole and just after it would be the same spot, only dimmer.
```

## How wide should the pinhole be?

This is the one setting on a confocal microscope that you will change constantly, so it is worth understanding rather than memorising.

Closing the pinhole rejects more out-of-focus light and gives a thinner optical section. It also throws away signal, because even a perfectly in-focus point source is not a point in the image plane: it is an Airy pattern, with a finite width set by diffraction. Close the pinhole below the size of the Airy disk and you start cutting into the very light you are trying to collect.

The natural unit is therefore the Airy pattern itself. One **Airy unit** (AU) is defined as the diameter of the Airy disk, that is, the diameter of the first dark ring:

$$
1\ \text{AU} = \frac{1.22\,\lambda_{\text{em}}}{\text{NA}}
$$

Note carefully what a 1 AU pinhole does and does not admit. It passes the central disc of the Airy pattern and nothing else: the rings fall outside it. That central disc happens to contain about 84% of the energy, so that is what gets through, and the remaining 16% sitting in the rings is discarded. Opening the pinhole to recover it is a poor bargain, as the simulation below makes clear: going from 1 AU to 3 AU buys another ten percentage points of signal while tripling the width of the region you accept light from.

### Simulation: sizing the pinhole

Drag the slider and watch two things at once. On the left, the white circle is the pinhole drawn on the Airy pattern, and everything it rejects is dimmed. On the right, the curve is the fraction of the light from an in-focus point source that survives, with the current setting marked. Notice how flat the curve becomes past 1 AU, and how steeply it falls below it.

```{raw} html
<div id="ph-widget" class="almb-widget">
  <style>
    #ph-widget.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:680px;margin:1.2em auto;padding:18px 22px 16px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #ph-widget .row{display:grid;grid-template-columns:230px 1fr;align-items:center;gap:14px;margin-bottom:12px;}
    #ph-widget .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #ph-widget .lab b{color:#e05020;font-weight:600;}
    #ph-widget input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #ph-widget .panels{display:flex;flex-wrap:wrap;gap:20px;justify-content:center;align-items:flex-start;}
    #ph-widget .panel{flex:1 1 250px;max-width:290px;}
    #ph-widget .ptitle{font-size:13px;color:#444;text-align:center;margin-bottom:6px;font-weight:600;}
    #ph-widget canvas{width:100%;height:auto;display:block;border-radius:3px;background:#000;}
    #ph-widget svg{width:100%;height:auto;display:block;}
    #ph-widget .readout{margin-top:12px;font-size:13.5px;color:#333;text-align:center;line-height:1.6;}
    #ph-widget .readout b{color:#e05020;}
    #ph-widget .hint{font-size:12.5px;color:#777;margin-top:10px;line-height:1.45;text-align:center;}
    @media (max-width:470px){#ph-widget .row{grid-template-columns:1fr;gap:2px;}}
  </style>

  <div class="row">
    <span class="lab" id="ph-lab">Pinhole diameter = <b>1.00</b> AU</span>
    <input type="range" id="ph-slider" min="0.10" max="3.00" step="0.02" value="1.00">
  </div>

  <div class="panels">
    <div class="panel">
      <div class="ptitle">Airy pattern at the pinhole</div>
      <canvas id="ph-can" width="260" height="260"></canvas>
    </div>
    <div class="panel">
      <div class="ptitle">Light passing the pinhole</div>
      <svg id="ph-svg" viewBox="0 0 260 260" xmlns="http://www.w3.org/2000/svg"></svg>
    </div>
  </div>

  <div class="readout" id="ph-out"></div>
  <div class="hint">Numbers assume a 63&times;/1.40 oil objective and an emission wavelength of 520&nbsp;nm.</div>

  <script>
  (function(){
    var el = document.getElementById("ph-widget");
    if (!el || el.dataset.init) return;
    el.dataset.init = "1";

    // --- Bessel functions of the first kind (Abramowitz & Stegun 9.4)
    function J0(x){
      x = Math.abs(x);
      if (x < 3){
        var t = (x/3)*(x/3);
        return 1 - 2.2499997*t + 1.2656208*t*t - 0.3163866*t*t*t
                 + 0.0444479*Math.pow(t,4) - 0.0039444*Math.pow(t,5)
                 + 0.00021*Math.pow(t,6);
      }
      var u = 3/x;
      var f = 0.79788456 - 0.00000077*u - 0.00552740*u*u - 0.00009512*u*u*u
            + 0.00137237*Math.pow(u,4) - 0.00072805*Math.pow(u,5)
            + 0.00014476*Math.pow(u,6);
      var th = x - 0.78539816 - 0.04166397*u - 0.00003954*u*u
             + 0.00262573*u*u*u - 0.00054125*Math.pow(u,4)
             - 0.00029333*Math.pow(u,5) + 0.00013558*Math.pow(u,6);
      return f/Math.sqrt(x)*Math.cos(th);
    }
    function J1(x){
      var s = x < 0 ? -1 : 1; x = Math.abs(x);
      if (x < 3){
        var t = (x/3)*(x/3);
        return s*x*(0.5 - 0.56249985*t + 0.21093573*t*t - 0.03954289*t*t*t
              + 0.00443319*Math.pow(t,4) - 0.00031761*Math.pow(t,5)
              + 0.00001109*Math.pow(t,6));
      }
      var u = 3/x;
      var f = 0.79788456 + 0.00000156*u + 0.01659667*u*u + 0.00017105*u*u*u
            - 0.00249511*Math.pow(u,4) + 0.00113653*Math.pow(u,5)
            - 0.00020033*Math.pow(u,6);
      var th = x - 2.35619449 + 0.12499612*u + 0.00005650*u*u
             - 0.00637879*u*u*u + 0.00074348*Math.pow(u,4)
             + 0.00079824*Math.pow(u,5) - 0.00029166*Math.pow(u,6);
      return s*f/Math.sqrt(x)*Math.cos(th);
    }
    var V1 = 3.8317059;                       // first zero of J1
    function encircled(ph){ var v = V1*ph; return 1 - J0(v)*J0(v) - J1(v)*J1(v); }

    // --- inferno-like colour ramp
    var RAMP = [[0,0,4],[40,11,84],[101,21,110],[159,42,99],[212,72,66],
                [245,125,21],[250,193,39],[252,255,164]];
    function ramp(t, out){
      t = t < 0 ? 0 : (t > 1 ? 1 : t);
      var f = t*(RAMP.length-1), i = Math.floor(f), g = f - i;
      if (i >= RAMP.length-1){ i = RAMP.length-2; g = 1; }
      out[0] = RAMP[i][0] + g*(RAMP[i+1][0]-RAMP[i][0]);
      out[1] = RAMP[i][1] + g*(RAMP[i+1][1]-RAMP[i][1]);
      out[2] = RAMP[i][2] + g*(RAMP[i+1][2]-RAMP[i][2]);
    }

    var can = document.getElementById("ph-can");
    var g = can.getContext("2d");
    var Wp = can.width, Hp = can.height;
    var img = g.createImageData(Wp, Hp), data = img.data;
    var EXT = 1.75;                            // half-width of the view, in AU

    (function paint(){
      var cx = (Wp-1)/2, cy = (Hp-1)/2, sx = 2*EXT/(Wp-1), col = [0,0,0], k = 0;
      for (var py=0; py<Hp; py++){
        var Y = (py-cy)*sx;
        for (var px=0; px<Wp; px++){
          var X = (px-cx)*sx, r = Math.sqrt(X*X+Y*Y);
          var v = 2*V1*r, I;
          if (v < 1e-8){ I = 1; } else { var b = 2*J1(v)/v; I = b*b; }
          ramp(Math.pow(I, 0.35), col);
          data[k]=col[0]; data[k+1]=col[1]; data[k+2]=col[2]; data[k+3]=255;
          k += 4;
        }
      }
      g.putImageData(img, 0, 0);
    })();
    var base = g.getImageData(0, 0, Wp, Hp);

    // --- encircled-energy curve, pre-computed
    var svg = document.getElementById("ph-svg");
    var PAD = {l:44, r:12, t:14, b:38}, SW = 260, SH = 260;
    function X(ph){ return PAD.l + (ph/3)*(SW-PAD.l-PAD.r); }
    function Y(e){ return SH-PAD.b - e*(SH-PAD.t-PAD.b); }
    var curve = "";
    for (var i=0; i<=180; i++){
      var p = 0.02 + (3-0.02)*i/180;
      curve += (i? "L":"M") + X(p).toFixed(1) + " " + Y(encircled(p)).toFixed(1) + " ";
    }
    var axes = "";
    [0, 0.25, 0.5, 0.75, 1].forEach(function(e){
      axes += '<line x1="'+PAD.l+'" y1="'+Y(e)+'" x2="'+(SW-PAD.r)+'" y2="'+Y(e)+
              '" stroke="#eee" stroke-width="1"/>' +
              '<text x="'+(PAD.l-6)+'" y="'+(Y(e)+4)+'" font-size="10" fill="#888" text-anchor="end">'+
              (e*100)+'</text>';
    });
    [0,1,2,3].forEach(function(p){
      axes += '<text x="'+X(p)+'" y="'+(SH-PAD.b+15)+'" font-size="10" fill="#888" text-anchor="middle">'+p+'</text>';
    });
    svg.innerHTML = axes +
      '<path d="'+curve+'" fill="none" stroke="#0072B2" stroke-width="2.2"/>' +
      '<line id="ph-vline" x1="0" y1="'+PAD.t+'" x2="0" y2="'+(SH-PAD.b)+'" stroke="#e05020" stroke-width="1.4" stroke-dasharray="4 3"/>' +
      '<circle id="ph-dot" r="4.5" fill="#e05020"/>' +
      '<line x1="'+PAD.l+'" y1="'+(SH-PAD.b)+'" x2="'+(SW-PAD.r)+'" y2="'+(SH-PAD.b)+'" stroke="#999" stroke-width="1"/>' +
      '<line x1="'+PAD.l+'" y1="'+PAD.t+'" x2="'+PAD.l+'" y2="'+(SH-PAD.b)+'" stroke="#999" stroke-width="1"/>' +
      '<text x="'+((PAD.l+SW-PAD.r)/2)+'" y="'+(SH-6)+'" font-size="11" fill="#555" text-anchor="middle">Pinhole diameter [AU]</text>' +
      '<text x="13" y="'+((PAD.t+SH-PAD.b)/2)+'" font-size="11" fill="#555" text-anchor="middle" transform="rotate(-90 13 '+((PAD.t+SH-PAD.b)/2)+')">Light collected [%]</text>';
    var vline = document.getElementById("ph-vline"), dot = document.getElementById("ph-dot");

    var slider = document.getElementById("ph-slider");
    var lab = document.getElementById("ph-lab");
    var out = document.getElementById("ph-out");

    function update(){
      var ph = parseFloat(slider.value);
      lab.innerHTML = "Pinhole diameter = <b>" + ph.toFixed(2) + "</b> AU";

      g.putImageData(base, 0, 0);
      var rpix = (ph/2)/EXT * (Wp-1)/2;
      g.save();
      // dim everything the pinhole rejects
      g.globalCompositeOperation = "source-over";
      g.beginPath();
      g.rect(0, 0, Wp, Hp);
      g.arc(Wp/2, Hp/2, rpix, 0, 2*Math.PI, true);
      g.fillStyle = "rgba(0,0,0,0.62)";
      g.fill("evenodd");
      g.beginPath();
      g.arc(Wp/2, Hp/2, rpix, 0, 2*Math.PI);
      g.strokeStyle = "#ffffff"; g.lineWidth = 1.8; g.stroke();
      g.restore();

      var e = encircled(ph);
      vline.setAttribute("x1", X(ph)); vline.setAttribute("x2", X(ph));
      dot.setAttribute("cx", X(ph)); dot.setAttribute("cy", Y(e));

      var au_um = 1.22*0.520/1.40;            // one Airy unit in the specimen [um]
      out.innerHTML = "<b>" + (100*e).toFixed(1) + "%</b> of the light from an in-focus point gets through &nbsp;|&nbsp; " +
                      (ph*au_um).toFixed(2) + " µm in the specimen &nbsp;|&nbsp; " +
                      (ph*au_um*63).toFixed(0) + " µm at the physical pinhole";
    }
    slider.addEventListener("input", update);
    update();
  })();
  </script>
</div>
```

```{tip}
**Worked example.** A 63×/1.40 oil objective, imaging GFP at $\lambda_{\text{em}}$ = 520 nm:

$$
1\ \text{AU} = \frac{1.22 \times 0.520\ \text{µm}}{1.40} = 0.45\ \text{µm}
$$

That is the size of the Airy disk _in the specimen_. The physical pinhole sits in the image plane, so its diameter must be multiplied by the magnification: $0.45 \times 63 \approx 28$ µm. This is why the pinhole in a real instrument is a visible hole rather than a microscopic one, and it is also why the same setting in micrometres means different things on different objectives. Always set the pinhole in Airy units and let the software do the conversion.
```

Now the trade-off itself (_{numref}`Fig. {number} <chap5_pinhole_tradeoff>`_). Two things happen as the pinhole closes, and they happen on different schedules.

The **lateral** resolution improves, but only in the last stretch. Down to about 1 AU almost nothing changes, because the pinhole is still larger than the diffraction spot and is not shaping it. Below roughly 0.5 AU the pinhole starts to act as a genuine spatial filter, and in the limit of a vanishingly small pinhole the effective point spread function becomes the *product* of the excitation and detection point spread functions. Multiplying two similar bell shapes gives a narrower bell: the width shrinks by a factor of $\sqrt{2}$, about 40%. That is the entire theoretical resolution gain of confocal microscopy over widefield, and it is available only at a pinhole size that transmits a few percent of your photons. In practice nobody uses it.

The **axial** behaviour is completely different, and it is the real reason to own a confocal microscope. Here the improvement continues all the way down, because the axial extent of the detected volume is set directly by how much defocused light the aperture admits.

```{figure} ../figures/chap5_pinhole_tradeoff.png
---
width: 85%
name: chap5_pinhole_tradeoff
align: center
---
Effect of the pinhole diameter, computed from the scalar diffraction theory of the confocal point spread function. The lateral width (dashed) saturates around 1 AU: closing further gains little until the pinhole becomes very small, where it approaches the $\sqrt{2}$ limit. The axial width (solid) keeps improving all the way down. The collected signal (dotted, right axis) does the opposite. One Airy unit sits close to where the three curves make the best compromise, which is why it is the default on every instrument.
```

A useful working estimate for the thickness of the optical section, and one you may meet in the manual of your microscope, is

$$
\text{FWHM}_{\text{axial}} = \sqrt{\left(\frac{0.88\,\lambda_{\text{em}}}{n - \sqrt{n^2 - \text{NA}^2}}\right)^{2} + \left(\frac{\sqrt{2}\,n\,\text{PH}}{\text{NA}}\right)^{2}}
$$

where PH is the pinhole diameter referred back to the specimen (that is, the physical diameter divided by the magnification) and $n$ is the refractive index of the immersion medium. The structure of the formula tells the story on its own: the first term is what diffraction gives you even with an infinitely small pinhole, and the second is the penalty for opening it. When the second term is small compared to the first, closing the pinhole further buys you nothing.

```{tip}
**Worked example, continued.** For the same 63×/1.40 oil objective ($n$ = 1.518, $\lambda_{\text{em}}$ = 520 nm):

- at 1 AU (PH = 0.45 µm): section thickness 0.85 µm, 84% of the signal
- at 0.5 AU (PH = 0.23 µm): section thickness 0.60 µm, 58% of the signal

Halving the pinhole buys a 30% thinner section and costs 30% of your photons. Whether that is a good deal depends entirely on how bright your sample is, and on whether the structure you care about is limited by sectioning or by noise. For a fixed, brightly stained sample, close it. For a dim live cell that you need to image two hundred times, do not.
```

```{tip}
For readers who have already been through {ref}`Chapter 6 <chap6_3>`, there is a much deeper way to say all of this. The optical transfer function of a widefield microscope is exactly zero in a cone-shaped region around the $k_z$ axis, the so-called _missing cone_. Those frequencies describe structures that vary along $z$ but not laterally, which is precisely what a uniform out-of-focus haze looks like. A widefield microscope therefore cannot distinguish such a haze from a constant offset, no matter how good the deconvolution. The confocal pinhole fills in the missing cone, which is why confocal sectioning is a genuine gain of information and not a cosmetic improvement.
```

## Getting the beam to move: two answers

We now have a way of measuring one point of the specimen very cleanly. To produce an image we need several hundred thousand of them, and how you get them defines the two families of confocal instrument (_{numref}`Fig. {number} <chap5_scanning_vs_spinning>`_).

```{figure} ../figures/chap5_scanning_vs_spinning.gif
---
width: 100%
name: chap5_scanning_vs_spinning
align: center
---
How the two instruments build an image. On the left, a point-scanning confocal sweeps a single focused spot across the field in a raster and reads out one pixel at a time. On the right, a spinning disk sweeps hundreds of spots at once, so the image fills in everywhere simultaneously and is complete after a fraction of a turn of the disk. Both are slowed down enormously here, and the difference between them is compressed even further: a real spinning disk completes a frame in well under a millisecond, roughly a thousand times faster than a point scanner, which is a ratio no animation can show side by side. Read the two counters rather than the clock.
```

The obvious approach, and the one Minsky used, is to leave the optics alone and **move the specimen**. It is mechanically simple and cheap, and it guarantees that every point is imaged through the exact centre of the field, with no off-axis aberration at all. It is also almost never done today, for a reason that will be familiar to anyone who has aligned a microscope: moving a stage means accelerating a physical object back and forth a few hundred times per image, and a microscope is precisely the instrument you least want to shake. Vibrations degrade the alignment, and positioning a stage repeatably to a fraction of the resolution limit is far harder than steering a beam.

**Laser scanning confocal microscopy** therefore does it the other way and moves the light. Two galvanometer mirrors, one for $x$ and one for $y$, are mounted on shafts that rotate through small angles in response to a voltage from the controller. Tilting them deflects the beam, so the focus traces a raster across the specimen while the specimen itself sits still. The emitted light travels back along the same path and off the same mirrors, which cancels the scan motion and delivers a stationary beam to a stationary pinhole. This trick is called **descanning**, and it is what makes a single fixed pinhole possible at all. To build a $z$-stack you then move the objective or the stage in $z$ alone, one slow step per plane rather than hundreds of fast ones per image.

The cost is time. Each pixel gets the detector's attention for a **dwell time** of typically 1 to 10 µs, and a 512 × 512 image therefore takes somewhere between a quarter of a second and several seconds. Faster is possible with a resonant scanner, which oscillates at a fixed frequency of about 8 kHz and reaches video rate, but the dwell time falls in proportion and the images become noisier.

**Spinning-disk confocal microscopy** attacks the problem by parallelising it. The idea goes back to the **Nipkow disk**, patented by Paul Nipkow in 1884 for mechanical television and repurposed for microscopy by Mojmír Petráň and Milan Hadravský in the 1960s. A disk carrying about a thousand pinholes, laid out along interleaved Archimedean spirals so that a partial rotation sweeps every point of the field exactly once, spins in a conjugate image plane. Hundreds of confocal spots are illuminated and detected at the same time, and because there are now hundreds of positions to keep track of, the detector has to be a camera again.

The modern implementation, due to Yokogawa, adds a second disk carrying one microlens per pinhole, mounted on the same shaft. Without it, the disk blocks upwards of 95% of the laser light; the microlenses focus the light into the pinholes instead of onto the metal between them, and recover most of it. The gain in speed is enormous: the spiral is laid out so that roughly a thirtieth of a turn is enough to sweep every point of the field exactly once, and at a few thousand revolutions per minute that means a complete confocal image in a fraction of a millisecond. A spinning disk delivers hundreds to a thousand frames per second, roughly three orders of magnitude faster than point scanning.

The disk speed is not free to choose. It has to be **synchronised with the camera exposure**, so that each frame contains a whole number of complete sweeps. Get this wrong and the exposure ends part way through a sweep, some parts of the field having been visited once more than others, and the pinhole pattern itself shows up in the image as a stationary grid or a set of moving stripes. If you ever stop the disk while the laser is on, you see the raw truth of the technique: not an image but a field of separated bright dots, one per pinhole.

Nothing else is free either. The pinholes must be far enough apart that light from one does not leak into its neighbours, and in a thick or highly scattering specimen this **pinhole crosstalk** is exactly what happens. A spinning disk is therefore measurably less confocal than a point scanner, and its advantage evaporates in thick tissue. The pinhole size is also fixed by the manufacturer, so you cannot trade sectioning against signal. And there is a subtler loss: a point scanner can linger. If a region is dim, you raise the dwell time and collect photons for longer before moving on. A spinning disk gives every point the same brief visit, over and over, so a dim sample simply produces a dim image and your only remaining lever is the camera exposure, which costs you the speed you bought the instrument for.

The choice between them is not subtle:

- **Fixed, thick, densely labelled tissue**, where you want the thinnest possible section and have all the time in the world: point scanning.
- **Live cells and fast subcellular dynamics**, where the specimen will bleach or move or die before a point scanner finishes: spinning disk.

## What confocal costs

The pinhole is a filter, and filters throw things away. Even at 1 AU you discard about 16% of the in-focus light before any detector inefficiency, and everything below 1 AU costs more.

Worse, and this is the criticism that motivates the rest of the chapter: the pinhole is on the *detection* side. The excitation is still a full double cone passing right through the specimen, so every plane above and below the focus is being illuminated, excited, bleached and stressed at full power, for every single plane of your $z$-stack. Acquire fifty planes and you have illuminated the whole specimen fifty times over in order to keep fifty thin slices of it. Confocal microscopy solves the contrast problem and does nothing at all about the photodamage problem. Indeed it makes it worse, because the light you throw away at the pinhole was paid for in photobleaching, in the sense of {ref}`Chapter 4 <chap4_1>`.

To summarise:

- **Advantages**: genuine optical sectioning of thick specimens; sharper, higher-contrast images; a modest lateral resolution gain; multi-channel and spectral detection are straightforward; the technique is mature and available almost everywhere.
- **Drawbacks**: scanning is slow; the whole depth of the specimen is illuminated for every plane, causing photobleaching and phototoxicity out of proportion to the data collected; the pinholes must be well aligned; signal is discarded by design.

```{tip}
A word on cost, since it shapes what you will actually find in a facility. A good commercial confocal starts somewhere around twenty thousand euros and climbs steeply from there, which is expensive but an order of magnitude below the super-resolution instruments of {ref}`Chapter 9 <chap9>`. Much of what you are paying for is alignment. The optical principle is simple enough that confocals were once routinely home-built, but the scanner, the pinhole and the detection path have to stay aligned to a fraction of the Airy disk while mirrors oscillate a few thousand times a second, and that is engineering rather than optics. Almost nobody builds their own any more.

The practical consequence of the photodamage problem is worth stating plainly too: point-scanning confocal is mostly a technique for fixed specimens, or for small fields imaged occasionally. For a fast live process, a plain widefield microscope will often beat it outright, because widefield captures the whole field in one exposure and confocal has to visit it a quarter of a million times.
```

The next three sections all take the same view of the problem. If the trouble is that we generate light we then have to throw away, the answer is to stop generating it.

