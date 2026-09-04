(chap7_3)=
# 7.3 - From function to design

Reading a schematic is reverse engineering. You are reconstructing somebody else's reasoning from the traces it left. This section runs the arrow forwards: you have a biological question, and you need an instrument.

This is not a course in optical design, and nobody expects you to compute a lens prescription. But you will very likely find yourself choosing a microscope, whether that means picking one from the facility booking system, specifying a purchase, or building something on a bench. In all three cases the reasoning is the same, and it is worth having it explicitly rather than by osmosis.

## Start with the sample, always

Every design decision cascades from the specimen. Before anything else, answer these:

- **What is the sample?** Fixed cells on a coverslip, a living monolayer, an organoid, a cleared brain, a whole developing embryo, a mouse under anaesthesia? The answer sets the geometry of everything.
- **How thick is it, and how far in do you need to see?** A monolayer is 5 µm and sits against the glass. A zebrafish embryo is a millimetre of scattering tissue.
- **Is it alive?** If yes, you have a photon budget, a temperature requirement, a medium, and a clock.
- **What do you need to resolve?** Whole cells at 5 µm, organelles at 500 nm, or protein clusters at 30 nm?
- **How fast does it move?** Nothing at all, minutes for cell migration, milliseconds for a calcium transient.

```{figure} ../figures/chap7_design_cascade.png
---
width: 95%
name: chap7_design_cascade
align: center
---
The design cascade. Each choice constrains the next, and the arrows run mostly in one direction: the sample determines the label, the label determines the source and filters, and the required resolution and speed determine the objective and the detector. Budget acts on every stage at once.
```

## The cascade

### Sample to label

What can you actually attach a signal to? Genetically encoded fluorescent proteins are the standard for live imaging because they are expressed by the cell itself and are usually well tolerated, but they are dimmer and bleach faster than good synthetic dyes. Organic dyes are brighter and more photostable but often need to be loaded, and many are cytotoxic. Quantum dots are extremely bright and essentially do not bleach, but they are large, they blink, and delivering them into a cell is a project in itself. Immunolabelling gives you exquisite specificity and requires you to kill and permeabilise the sample first.

And how many labels? Each additional colour costs you a laser line or an LED, a filter set, and a share of the spectrum. Beyond three or four channels in the visible range you begin fighting spectral overlap ({ref}`Chapter 4 <chap4_2>`).

### Label to source and filters

Once the fluorophore is fixed, its excitation spectrum fixes the wavelength you need, and the rest follows. An LED engine is cheap, stable and adequate for most fluorescent proteins in a widefield system. A laser is required whenever you need to focus into a diffraction-limited spot (any scanning technique), whenever you need coherence (interference-based methods), or whenever you simply need more power than a lamp can deliver. A pulsed laser is required for multiphoton excitation, and for nothing else in this course.

The filter set follows mechanically from the fluorophore: an excitation band inside the absorption peak, a dichroic edge in the Stokes gap, and an emission band over the emission peak. Buy them as a matched cube unless you have a specific reason not to.

### Resolution and field of view to objective

Here you meet the first genuinely hard trade-off, and it is worth being blunt about it: you cannot have high resolution and a large field of view at the same time.

Resolution is set by the numerical aperture, $d = \lambda / 2\mathrm{NA}$, so fine detail demands high NA. But high NA objectives have short working distances, high magnification, and therefore small fields of view. A 100x/1.45 oil objective resolves 180 nm over a field of about 130 µm; a 10x/0.3 air objective resolves 900 nm over 1.3 mm. There is no objective that does both, because the number of resolvable points in an image is limited by the sensor and by the design of the optics, and you are choosing how to spend them.

The other constraints on the objective are physical:

- **Immersion medium.** Air caps you at NA < 1. Water ($n = 1.33$) reaches about 1.2 and matches the refractive index of living tissue, so it is the right choice for imaging deep into an aqueous sample without spherical aberration. Oil ($n = 1.518$) reaches 1.4 to 1.5 and matches glass, so it is the right choice for anything within a few micrometres of the coverslip. Silicone oil ($n = 1.41$) is a compromise aimed at live tissue.
- **Working distance.** If your sample sits in a dish under 500 µm of medium, an objective with a 170 µm working distance cannot reach it, whatever its NA.
- **Corrections.** Multicolour quantitative work needs apochromatic correction; large fields need a plan correction. Both cost money.

### Speed, sensitivity and photon budget to detector

If you need speed, you need parallel readout, so CMOS or sCMOS. If you need to detect a handful of photons, you need an EMCCD, or a PMT if you are scanning anyway. If you need fidelity across a wide dynamic range and you have time, a cooled CCD is still excellent. If you have a scanning system, the question of a camera does not arise at all: you need a point detector.

The single most useful concept for thinking about this is the **photon budget**. Your sample can only emit a certain number of photons before it bleaches or dies. That number is fixed by the labelling and the biology, not by your equipment. Everything you ask for spends from the same account:

- More resolution means dividing the same photons among more, smaller pixels.
- More speed means fewer photons per frame.
- A larger field of view means spreading photons over more area.
- A longer experiment means the photons have to last longer.

You cannot improve one of these without paying for it somewhere else, and the currency is always signal-to-noise ratio. This is why "what is the best microscope" is not a question with an answer, and why the honest answer to "can I have higher resolution" is usually "yes, and here is what it will cost you."

```{tip}
**Worked example: matching the camera to the objective.**

You have chosen a 60x/1.30 objective and you are imaging green emission at 520 nm. The optical resolution is

$$d = \frac{\lambda}{2\mathrm{NA}} = \frac{520}{2 \times 1.30} = 200 \ \text{nm}$$

To record that resolution without losing it, the Nyquist criterion requires at least two pixels across the smallest resolvable distance, so the pixel size projected back into the sample must be no larger than 100 nm. Projected into the camera plane, that is

$$100 \ \text{nm} \times 60 = 6.0 \ \mu\text{m}$$

A typical sCMOS has 6.5 µm pixels. Projected back, that is 108 nm per pixel: slightly undersampled. Options are to add a 1.5x magnification changer (giving 72 nm per pixel, comfortably Nyquist-sampled), to move to a 100x objective, or to accept a small loss of resolution in exchange for a larger field of view and more photons per pixel.

Note that the last option is a real option. Oversampling costs you signal per pixel and field of view, and if your sample is dim, deliberately sampling at the Nyquist limit rather than beyond it is the right call. This is the same trade-off explored interactively in the sampling section of this chapter.
```

## Two worked designs

### A live zebrafish embryo over 24 hours

**Sample.** A whole embryo, roughly 1 mm across, alive, developing, and needing to stay that way for a day. Fluorescent protein expressed in a tissue of interest.

**Immediate consequences.** Photodamage is the binding constraint. Any technique that illuminates the whole volume in order to image one plane will bleach and cook the embryo long before 24 hours are up, which rules out widefield and makes confocal marginal at best. The sample is thick, so you need optical sectioning. It is alive, so you need speed and a controlled environment.

**Design.** Light-sheet fluorescence microscopy ({ref}`Chapter 5 <chap5_3>`). Illuminating only the imaged plane means the photon budget is spent almost entirely on photons you actually detect, and the dose per plane is orders of magnitude lower than in a confocal.

- **Source:** a CW laser matching the fluorescent protein, fibre-coupled for a clean mode.
- **Illumination optics:** beam expander, then either a cylindrical lens for a static sheet or a galvo for a scanned one. Given a live, scattering, three-dimensional embryo, the scanned sheet is worth the extra complexity because it suppresses the striping that scattering produces in a coherently illuminated static sheet.
- **Detection objective:** water dipping, low to moderate magnification, moderate NA. Something like 20x/1.0 W. Resolution of about 260 nm is plenty for tissue-scale development, and the large field of view and long working distance are essential.
- **Detector:** sCMOS. You need speed to capture a whole volume before the embryo moves, a large field of view to hold the embryo, and low noise because the per-plane dose is deliberately small.
- **Mechanics:** a sample holder that can rotate, because a millimetre of tissue is opaque enough that you will want to image from more than one side and fuse the views.

### Calcium transients 400 µm deep in a mouse cortex

**Sample.** Living brain, in an anaesthetised or head-fixed animal, with a genetically encoded calcium indicator. You need to resolve individual neurons and catch transients lasting tens of milliseconds, several hundred micrometres below the surface.

**Immediate consequences.** Depth is the binding constraint. Brain tissue scatters visible light heavily, and by 400 µm a one-photon focus is hopeless. Scattering falls off steeply with wavelength, so the answer is to excite in the near infrared.

**Design.** Two-photon laser scanning microscopy ({ref}`Chapter 8 <chap8>`).

- **Source:** a femtosecond pulsed laser near 920 nm. As computed in {ref}`Chapter 7.1 <chap7_1>`, the pulse structure delivers the peak intensity needed for two-photon absorption at a tolerable average power.
- **Scanning:** a resonant galvo for the fast axis and a conventional galvo for the slow axis, giving video-rate frames, plus a scan lens and tube lens conjugating the mirrors to the objective pupil.
- **Objective:** water immersion, long working distance, moderate NA and low magnification, for example 16x/0.8 W with a 3 mm working distance. High NA would help collection, but you need the working distance and the field of view more.
- **Detector:** a PMT, and specifically a GaAsP PMT for the higher quantum efficiency. There is no pinhole and no camera: because two-photon excitation only occurs at the focus, every emitted photon that reaches the detector, however scattered, came from the right place and should be collected. This is a genuinely elegant consequence of the nonlinearity, and it is why the detector sits as close to the objective as the designer can manage.
- **Mechanics:** a stable, heavy frame and a piezo objective positioner for fast axial jumps between imaging planes.

Notice that the two designs share almost nothing. Same fluorescence, same physics, entirely different instrument, because the samples asked different questions.

## Sampling diffraction-limited objects

The diffraction limit sets the size of the smallest object an optical system can render: anything finer is blurred out to that size. Since the limit depends only on the numerical aperture and the wavelength, it is tempting to assume that every image is automatically diffraction-limited. It is not, because whether we actually _record_ that finest detail depends on the camera, through the pixel size and the magnification.

The total magnification $M$ makes objects in the sample appear $M$ times larger at the camera, which means each pixel samples a region of the sample $M$ times smaller than its physical size. Consider a camera with $2000 \times 2000$ pixels, each $6.5\ \mu\text{m}$ across. Behind a $10\times$ objective, one pixel covers $650\ \text{nm}$ of the sample; behind a $100\times$ objective, the same pixel covers only $65\ \text{nm}$. The optics have not changed, but what the pixel grid can capture has.

The rule for matching the two comes straight from the frequency picture. The microscope band-limits the image: it passes no spatial frequency above its cutoff, so the image contains no period finer than the resolution $d$. The sampling theorem then says we must place at least two samples across the finest period, so the pixel spacing at the sample must be no larger than half the resolution. In practice a small safety margin is added, and a common convention is to make the pixel about $1/2.3 \approx 0.44$ times the smallest feature. Sampling more coarsely than this loses real information, an error called **undersampling** that shows up as a pixelated, aliased image; sampling much more finely, **oversampling**, adds no new information and only spreads the same photons over more pixels.

To make it concrete, a diffraction-limited resolution of $320\ \text{nm}$ calls for samples every $140\ \text{nm}$ or so across the image. With a $6.5\ \mu\text{m}$ pixel, that requires a magnification of roughly $45$ to $50\times$. The lesson is worth stating plainly: magnification does nothing for the optical blur of the microscope, but it is what lets the detector sample finely enough to record all the detail the optics did transmit.

### Interactive resolution calculator

The two ideas of this section, the diffraction-limited resolution and the sampling it demands, come together in a small calculator. Enter the wavelength, the numerical aperture, your camera's pixel size and the total magnification, and it reports the Abbe and Rayleigh resolutions, the effective pixel size projected back onto the sample, the sampling that the resolution requires, and whether your current setup is undersampled, well sampled or oversampled.

```{raw} html
<div id="res-calc" class="almb-widget">
  <style>
    #res-calc.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:640px;margin:1.2em auto;padding:18px 22px 18px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #res-calc .ctrls{display:flex;flex-direction:column;gap:11px;margin-bottom:16px;}
    #res-calc .row{display:grid;grid-template-columns:220px 1fr;align-items:center;gap:14px;}
    #res-calc .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #res-calc .lab b{color:#e05020;font-weight:600;}
    #res-calc input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #res-calc .grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:14px;}
    #res-calc .card{background:#f7f7f8;border:1px solid #ececec;border-radius:8px;padding:10px 12px;text-align:center;}
    #res-calc .card .k{font-size:11px;color:#777;line-height:1.25;min-height:26px;display:flex;align-items:center;justify-content:center;}
    #res-calc .card .v{font-size:19px;font-weight:600;color:#2a4494;margin-top:3px;font-variant-numeric:tabular-nums;}
    #res-calc .card .u{font-size:11px;color:#999;}
    #res-calc .status{border-radius:8px;padding:11px 14px;font-size:13.5px;line-height:1.45;}
    #res-calc .status b{font-weight:700;}
    @media (max-width:520px){#res-calc .grid{grid-template-columns:repeat(2,1fr);} #res-calc .row{grid-template-columns:1fr;gap:2px;}}
  </style>
  <div class="ctrls">
    <div class="row"><span class="lab" id="rc-l-lab">Wavelength <b>&lambda;</b> = 500 nm</span><input type="range" id="rc-l" min="380" max="750" step="5" value="500"></div>
    <div class="row"><span class="lab" id="rc-na-lab">Numerical aperture <b>NA</b> = 0.95</span><input type="range" id="rc-na" min="0.1" max="1.49" step="0.01" value="0.95"></div>
    <div class="row"><span class="lab" id="rc-px-lab">Camera pixel <b>p</b> = 6.5 &mu;m</span><input type="range" id="rc-px" min="1" max="20" step="0.1" value="6.5"></div>
    <div class="row"><span class="lab" id="rc-m-lab">Total magnification <b>M</b> = 40&times;</span><input type="range" id="rc-m" min="1" max="150" step="1" value="40"></div>
  </div>
  <div class="grid">
    <div class="card"><div class="k">Abbe resolution<br>&lambda;/(2&middot;NA)</div><div class="v" id="rc-abbe">&hellip;</div><div class="u">nm</div></div>
    <div class="card"><div class="k">Rayleigh resolution<br>0.61&middot;&lambda;/NA</div><div class="v" id="rc-ray">&hellip;</div><div class="u">nm</div></div>
    <div class="card"><div class="k">Effective pixel<br>at the sample</div><div class="v" id="rc-eff">&hellip;</div><div class="u">nm</div></div>
    <div class="card"><div class="k">Required sampling<br>(Nyquist, &divide;2.3)</div><div class="v" id="rc-req">&hellip;</div><div class="u">nm</div></div>
  </div>
  <div class="status" id="rc-status"></div>
  <script>
  (function(){
    var sL=document.getElementById("rc-l"),sNA=document.getElementById("rc-na"),sP=document.getElementById("rc-px"),sM=document.getElementById("rc-m");
    var lL=document.getElementById("rc-l-lab"),lNA=document.getElementById("rc-na-lab"),lP=document.getElementById("rc-px-lab"),lM=document.getElementById("rc-m-lab");
    var oAb=document.getElementById("rc-abbe"),oRa=document.getElementById("rc-ray"),oEf=document.getElementById("rc-eff"),oRq=document.getElementById("rc-req"),oSt=document.getElementById("rc-status");
    function update(){
      var lam=+sL.value, NA=+sNA.value, p=+sP.value, M=+sM.value;
      lL.innerHTML="Wavelength <b>&lambda;</b> = "+lam+" nm";
      lNA.innerHTML="Numerical aperture <b>NA</b> = "+NA.toFixed(2);
      lP.innerHTML="Camera pixel <b>p</b> = "+p.toFixed(1)+" &mu;m";
      lM.innerHTML="Total magnification <b>M</b> = "+M+"&times;";
      var abbe=lam/(2*NA), ray=0.61*lam/NA, eff=p*1000/M, req=ray/2.3;
      oAb.textContent=Math.round(abbe);
      oRa.textContent=Math.round(ray);
      oEf.textContent=Math.round(eff);
      oRq.textContent=Math.round(req);
      var col,txt;
      if(eff>req){ col="#e05020";
        txt="<b>Undersampled.</b> Each pixel covers "+Math.round(eff)+"&nbsp;nm at the sample, coarser than the "+Math.round(req)+"&nbsp;nm the optics require. Fine detail is being lost. Increase the magnification or use a smaller pixel.";
      } else if(eff>=0.5*req){ col="#0d5e22";
        txt="<b>Well sampled.</b> A pixel covers "+Math.round(eff)+"&nbsp;nm, finer than the "+Math.round(req)+"&nbsp;nm requirement, so the resolution the optics deliver is captured without waste.";
      } else { col="#b07000";
        txt="<b>Oversampled.</b> A pixel covers only "+Math.round(eff)+"&nbsp;nm, far below the "+Math.round(req)+"&nbsp;nm needed. No extra detail is gained; the same light is just spread over more pixels, lowering the signal per pixel.";
      }
      oSt.style.background=hexA(col,0.10);
      oSt.style.color="#333";
      oSt.style.border="1px solid "+hexA(col,0.35);
      oSt.innerHTML="<span style='color:"+col+"'>"+txt+"</span>";
    }
    function hexA(hex,a){var r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16);return "rgba("+r+","+g+","+b+","+a+")";}
    [sL,sNA,sP,sM].forEach(function(s){s.addEventListener("input",update);});
    update();
  })();
  </script>
</div>
```

For a fuller tool that includes a large library of real objectives and immersion media, Nikon provides an online resolution calculator at [this link](https://www.microscope.healthcare.nikon.com/microtools/resolution-calculator/).

## Being critical

The reason to learn this reasoning is not only so you can build things. It is so you can read the literature properly.

Once you can go from function to design, you can look at a published instrument and ask whether the choices were good ones. Why an EMCCD when an sCMOS would have been faster and quieter? Probably because the paper predates the widespread availability of sCMOS, and the date of publication is right there. Why a 1.4 NA oil objective on a sample that is 80 µm thick? That is a genuine question, since oil immersion introduces severe spherical aberration when you focus more than a few micrometres into an aqueous sample. Why only two colours when the biology involves three proteins? Perhaps the third label was not available, perhaps the spectra overlapped, perhaps the budget ran out.

Some of these questions have good answers and some expose real limitations. Either way, the ability to ask them is what separates reading a methods section from understanding it.

```{tip}
Budget is a design constraint, not an embarrassment. A very large fraction of published microscopy is done on instruments that were affordable rather than optimal, and papers like the descSPIM design in the previous section exist precisely to make good imaging accessible. When you look at a schematic and think "why did they not use a better camera", the answer is often simply the price, and the interesting question becomes whether the compromise was well chosen.
```

## Where this leads

You now have the two skills that the rest of the course assumes. You can look at an instrument and work out what it does, and you can start from a biological question and reason towards the instrument that answers it.

Everything that follows is an application of this. The advanced techniques of {ref}`Chapter 8 <chap8>` are, almost without exception, rearrangements of components you have now met: a pulsed laser and a PMT for multiphoton, a fast detector and timing electronics for lifetime imaging, a high-NA objective and an oblique beam for TIRF. The super-resolution methods of {ref}`Chapter 9 <chap9>` add a DMD or an SLM to pattern the illumination, or a very sensitive camera and a lot of frames, or both. And {ref}`Chapter 10 <chap10>` deals with what happens after the detector, where the choices made on the optical table show up as the properties of the data you have to analyse.

The parts do not change very much. What changes is the reasoning that arranges them.
