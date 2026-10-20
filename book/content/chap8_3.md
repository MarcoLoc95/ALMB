(chap8_3)=
# 8.3 - Lifetime imaging

Every fluorescence image so far in this book measures the same thing: how many photons arrived. Brightness is the observable, and contrast is built from differences in brightness. This section is about replacing that observable with a better one.

## The trouble with brightness

Suppose you express a genetically encoded sensor whose fluorescence increases when the membrane potential rises. You image a neuron, you see a flash, and you conclude that something happened. Now try to say _what_ happened: was the membrane at $-50$ mV or at $-20$ mV?

You cannot, because intensity depends on far too many things that have nothing to do with the quantity you want.

Go through the possibilities. Intensity scales with the local concentration of the probe, which for a genetically encoded sensor means with its expression level, which varies from cell to cell and drifts over a developmental time course. It scales with the excitation power, so a drifting laser looks like biology. It falls as the sample bleaches, monotonically and irreversibly. And it depends on how much tissue lies above the plane of interest, because scattering and absorption attenuate both the excitation and the emission, so the same structure looks dimmer when it is deeper.

Each of these can be partly controlled, and none can be eliminated. Ratiometric sensors help by adding a reference channel, but they solve the problem by measuring two intensities rather than by measuring something better.

## Lifetime is a property of the molecule

{ref}`Chapter 4.1 <chap4_1>` defined the fluorescence lifetime as the average time a molecule spends in the excited state,

$$ \tau = \frac{1}{\Gamma_r + \Gamma_{nr}}, $$

set by the competition between the radiative rate $\Gamma_r$ and all the non-radiative routes $\Gamma_{nr}$. After a short excitation pulse, a population of identical molecules therefore emits with an exponentially decaying intensity, $I(t) = I_0\,e^{-t/\tau}$, and for typical fluorescent proteins and dyes $\tau$ is between 1 and 10 ns.

The crucial point is what does _not_ appear in that equation. The lifetime describes how a single molecule decays, so it does not care how many molecules there are: concentration and expression level drop out. It does not care how they were excited: laser power drops out. It does not care that some molecules have already been destroyed, because the survivors decay exactly as before: photobleaching drops out. And it does not care what fraction of the emitted light reaches the detector: depth, absorption and collection efficiency drop out. If you like the language of thermodynamics, intensity is _extensive_, scaling with the amount of stuff, while lifetime is _intensive_, like a temperature.

What the lifetime _does_ depend on is anything that opens or closes a non-radiative escape route from the excited state. That list includes the local pH, the concentration of quenching ions such as chloride, viscosity, oxygen, temperature, and the presence of a FRET acceptor. The last one is worth writing out. Energy transfer is simply one more way of leaving the excited state, with its own rate $\Gamma_{\rm FRET}$, so the donor lifetime falls from $\tau_D = 1/(\Gamma_r + \Gamma_{nr})$ to

$$ \tau_{DA} = \frac{1}{\Gamma_r + \Gamma_{nr} + \Gamma_{\rm FRET}}, \qquad E = \frac{\Gamma_{\rm FRET}}{\Gamma_r + \Gamma_{nr} + \Gamma_{\rm FRET}} = 1 - \frac{\tau_{DA}}{\tau_D}. $$

This is the relation promised at the end of {ref}`Section 8.2 <chap8_2>`, and it is why FLIM is regarded as the most reliable way to measure FRET.

Once the relationship between lifetime and, say, pH has been characterised for a given probe, every subsequent measurement returns an absolute pH in every pixel, without calibrating anything about the microscope. That is what makes **fluorescence lifetime imaging microscopy**, FLIM, quantitative in a way that intensity imaging is not.

## Counting photons one at a time

Measuring a nanosecond decay at every pixel sounds as though it should require an impossibly fast camera. The standard solution sidesteps the problem elegantly.

```{figure} ../figures/chap8_flim_tcspc.png
---
width: 95%
name: chap8_flim_tcspc
align: center
---
(a) In each excitation cycle, the laser pulse starts a clock and the first detected photon stops it, giving one arrival delay. Because emission is random, every cycle gives a different value, and most cycles give none. (b) Accumulated over many cycles, the delays build a histogram whose decay constant is the lifetime. (c) Repeating this at every pixel produces a lifetime map.
```

The method is **time-correlated single-photon counting**, TCSPC, and it runs on a scanning confocal or multiphoton microscope with three additions: a pulsed laser ({ref}`Chapter 7.1 <chap7_1>`), a detector fast enough to register individual photons with picosecond timing, and an electronics module that times the interval between each laser pulse and the next detected photon. One such interval tells you almost nothing, since emission is a random process. But tens of thousands of them, sorted into a histogram, trace out the exponential decay itself, as in _{numref}`Fig. {number} <chap8_flim_tcspc>`_, and fitting it gives $\tau$ for that pixel.

There is one constraint that governs everything about how FLIM feels to use. The electronics can time only the _first_ photon after each pulse. If a pulse happens to produce two detected photons, the second is lost, and because the first of two random arrivals is on average earlier than either one alone, the histogram becomes biased towards short delays. The fitted lifetime comes out too short. This is called **pile-up**, and the only cure is to keep the photon rate low enough that pulses producing two photons are rare. The usual rule is that no more than 1 to 5% of laser pulses should produce a detected photon, which in practice means attenuating the excitation, typically with neutral density filters.

The simulation below lets you run a TCSPC measurement and feel both constraints: the statistical one, that precision improves only with the square root of the number of photons, and the systematic one, pile-up.

```{raw} html
<div id="tc-sim" class="almb-widget">
  <style>
    #tc-sim.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:720px;margin:1.2em auto;padding:18px 22px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #tc-sim .ctrls{display:flex;flex-direction:column;gap:10px;margin-bottom:14px;}
    #tc-sim .row{display:grid;grid-template-columns:300px 1fr;align-items:center;gap:14px;}
    #tc-sim .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #tc-sim .lab b{color:#e05020;font-weight:600;}
    #tc-sim input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #tc-sim canvas{width:100%;height:auto;display:block;}
    #tc-sim .cap{font-size:11.5px;color:#777;margin:3px 0 12px 2px;}
    #tc-sim .grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-bottom:12px;}
    #tc-sim .card{background:#f7f7f8;border:1px solid #ececec;border-radius:8px;padding:9px 10px;text-align:center;}
    #tc-sim .card .k{font-size:11.5px;color:#777;}
    #tc-sim .card .v{font-size:20px;font-weight:600;color:#2a4494;margin-top:3px;font-variant-numeric:tabular-nums;}
    #tc-sim .card .u{font-size:11px;color:#999;}
    #tc-sim .status{border-radius:8px;padding:10px 14px;font-size:13.5px;line-height:1.45;}
    #tc-sim .btns{display:flex;gap:8px;justify-content:flex-end;margin-top:10px;}
    #tc-sim button{font:inherit;font-size:13px;padding:5px 12px;border-radius:6px;border:1px solid #d0d0d0;background:#fafafa;cursor:pointer;}
    #tc-sim button:hover{background:#f0f0f0;}
    @media (max-width:620px){#tc-sim .row{grid-template-columns:1fr;gap:2px;}}
  </style>
  <div class="ctrls">
    <div class="row"><span class="lab" id="tc-tau-lab">True lifetime <b>&tau;</b> = 2.5 ns</span><input type="range" id="tc-tau" min="0.5" max="5" step="0.1" value="2.5"></div>
    <div class="row"><span class="lab" id="tc-mu-lab">Laser pulses that give a photon: <b>1 %</b></span><input type="range" id="tc-mu" min="0" max="100" step="1" value="37"></div>
  </div>
  <canvas id="tc-h" width="1100" height="440"></canvas>
  <div class="cap">Each detected photon adds one count at its arrival time after the laser pulse. Solid line: fit. Dashed line: the true decay.</div>
  <div class="grid">
    <div class="card"><div class="k">Photons collected</div><div class="v" id="tc-n">0</div></div>
    <div class="card"><div class="k">Fitted lifetime</div><div class="v" id="tc-fit">&ndash;</div><div class="u" id="tc-true">true value: 2.5 ns</div></div>
  </div>
  <div class="status" id="tc-status"></div>
  <div class="btns"><button id="tc-pause">Pause</button><button id="tc-reset">Start again</button></div>
  <script>
  (function(){
    var T=12.5, NB=100, NMAX=20000, RMAX=35, GROW=1.015;
    var sTau=document.getElementById("tc-tau"), sMu=document.getElementById("tc-mu");
    var lTau=document.getElementById("tc-tau-lab"), lMu=document.getElementById("tc-mu-lab");
    var cv=document.getElementById("tc-h"), cx=cv.getContext("2d");
    var oN=document.getElementById("tc-n"), oF=document.getElementById("tc-fit"), oTr=document.getElementById("tc-true"), oS=document.getElementById("tc-status");
    var bP=document.getElementById("tc-pause"), bR=document.getElementById("tc-reset");
    var tau, p, mu, hist, n, sumT, rate, credit, running=true, visible=true, frameNo=0;
    function pFrom(v){return 0.001*Math.pow(10, 2.7*(+v)/100);}
    function init(){
      tau=+sTau.value; p=pFrom(sMu.value); mu=-Math.log(1-p);
      var pc=p*100, ps=pc<1?pc.toFixed(1):(pc<10?pc.toFixed(1):pc.toFixed(0));
      lTau.innerHTML="True lifetime <b>&tau;</b> = "+tau.toFixed(1)+" ns";
      lMu.innerHTML="Laser pulses that give a photon: <b>"+ps+" %</b>";
      oTr.textContent="true value: "+tau.toFixed(1)+" ns";
      hist=new Float64Array(NB); n=0; sumT=0; rate=0.4; credit=0;
      draw(null); report(null);
    }
    function zeroTruncPoisson(){
      var u=Math.random()*(1-Math.exp(-mu)), k=1, pk=Math.exp(-mu)*mu, c=pk;
      while(c<u && k<60){ k++; pk*=mu/k; c+=pk; }
      return k;
    }
    function detect(){
      credit+=rate; rate=Math.min(RMAX, rate*GROW);
      while(credit>=1 && n<NMAX){
        credit-=1;
        var k=zeroTruncPoisson(), t=-tau/k*Math.log(1-Math.random());
        if(t>=T) continue;
        hist[Math.floor(t/T*NB)]++; n++; sumT+=t;
      }
    }
    function meanTrunc(tt){ return tt - T/(Math.exp(T/tt)-1); }
    function fitTau(){
      if(n<30) return null;
      var m=sumT/n, lo=0.02, hi=60;
      for(var it=0;it<60;it++){ var mid=0.5*(lo+hi); if(meanTrunc(mid)<m) lo=mid; else hi=mid; }
      return 0.5*(lo+hi);
    }
    function draw(tf){
      var W=cv.width, H=cv.height, l=60, r=20, t=18, b=62;
      cx.clearRect(0,0,W,H); cx.fillStyle="#fff"; cx.fillRect(0,0,W,H);
      var hmax=5; for(var i=0;i<NB;i++) if(hist[i]>hmax) hmax=hist[i];
      var ymax=hmax*1.12;
      function X(tt){return l+(W-l-r)*tt/T;}
      function Y(v){return H-b-(H-b-t)*v/ymax;}
      cx.strokeStyle="#333"; cx.lineWidth=1.5; cx.beginPath(); cx.moveTo(l,t); cx.lineTo(l,H-b); cx.lineTo(W-r,H-b); cx.stroke();
      cx.fillStyle="#555"; cx.font="22px sans-serif"; cx.textAlign="center";
      for(var tk=0;tk<=12;tk+=2){ cx.fillText(tk, X(tk), H-b+28); }
      cx.fillText("arrival time after the laser pulse [ns]", (l+W-r)/2, H-8);
      cx.save(); cx.translate(24,(H-b+t)/2); cx.rotate(-Math.PI/2); cx.fillText("counts",0,0); cx.restore();
      var bw=(W-l-r)/NB;
      cx.fillStyle="rgba(42,68,148,0.35)";
      for(var j=0;j<NB;j++){ if(hist[j]>0){ var y=Y(hist[j]); cx.fillRect(l+j*bw, y, bw-0.5, H-b-y); } }
      if(n>=30){
        var binw=T/NB;
        var curve=function(tt,col,dash){ var norm=n*binw/(tt*(1-Math.exp(-T/tt)));
          cx.strokeStyle=col; cx.lineWidth=2.6; cx.setLineDash(dash); cx.beginPath();
          for(var q=0;q<=200;q++){ var s=q/200*T, yy=Y(norm*Math.exp(-(s+binw/2)/tt)); if(q===0) cx.moveTo(X(s),yy); else cx.lineTo(X(s),yy); }
          cx.stroke(); cx.setLineDash([]); };
        curve(tau,"#888888",[9,7]);
        if(tf) curve(tf,"#e05020",[]);
      }
    }
    function hexA(hex,al){var r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16);return "rgba("+r+","+g+","+b+","+al+")";}
    function report(tf){
      oN.textContent=n.toLocaleString("en-US");
      var col, txt;
      if(!tf){ oF.textContent="\u2013"; col="#2a4494"; txt="Photons arrive one at a time. Watch the histogram take the shape of the decay."; }
      else{
        oF.textContent=tf.toFixed(2)+" ns";
        var se=tf/Math.sqrt(n), off=Math.abs(tf-tau)>2.5*se;
        if(p>0.05 || (off && p>0.01 && n>3000)){ col="#e05020"; txt="<b>Pile-up.</b> At this rate some pulses give two photons, but only the first one is timed. Early arrivals are over-counted, so the fitted lifetime is too short, and collecting more photons does not fix it."; }
        else if(n<3000){ col="#b07000"; txt="<b>Still collecting.</b> With few photons the fit wanders; its precision improves only with the square root of the photon count."; }
        else if(!off){ col="#0d5e22"; txt="<b>Good measurement.</b> The fit matches the true lifetime."+(n>=NMAX?" Now try raising the count rate.":""); }
        else { col="#b07000"; txt="<b>Close.</b> The remaining difference is statistical."; }
      }
      oS.style.background=hexA(col,0.10); oS.style.border="1px solid "+hexA(col,0.35); oS.innerHTML="<span style='color:"+col+"'>"+txt+"</span>";
    }
    function frame(){
      if(running&&visible&&n<NMAX){ detect(); frameNo++; if(frameNo%2===0){ var tf=fitTau(); draw(tf); report(tf);} }
      requestAnimationFrame(frame);
    }
    sTau.addEventListener("input",init); sMu.addEventListener("input",init); bR.addEventListener("click",init);
    bP.addEventListener("click",function(){running=!running; bP.textContent=running?"Pause":"Resume";});
    if("IntersectionObserver" in window){ new IntersectionObserver(function(es){visible=es[0].isIntersecting;}).observe(document.getElementById("tc-sim")); }
    init(); requestAnimationFrame(frame);
  })();
  </script>
</div>
```

Start at 1% and watch the histogram take shape: at first the fit wanders, then it settles onto the dashed line. Then push the rate up and start again. At high rates the fitted lifetime comes out too short, and it stays too short no matter how many photons you add: more photons cannot fix a systematic error. In a real instrument, a higher rate would also have filled the histogram faster, which is exactly why pile-up is a temptation.

```{tip}
**Worked example: why a FLIM image takes minutes.**

Take a laser at 80 MHz and keep the detection rate at 1% of pulses to avoid pile-up. The maximum detected photon rate is

$$ 80 \times 10^{6}\ \text{s}^{-1} \times 0.01 = 8 \times 10^{5}\ \text{photons/s}. $$

A reliable single-exponential fit needs on the order of $10^4$ photons per pixel (the relative precision is roughly $1/\sqrt{N}$, so 1% needs $10^4$), giving a minimum dwell time per pixel of

$$ \frac{10^{4}}{8 \times 10^{5}\ \text{s}^{-1}} = 12.5\ \text{ms}. $$

A $256 \times 256$ image therefore takes $65\,536 \times 12.5$ ms $\approx 820$ s, about fourteen minutes, and that assumes a bright probe and a perfect detector. If two populations of the probe coexist, as they do in any FLIM-FRET experiment where some sensors are bound and some are not, the decay is bi-exponential and you need many more photons still. This is the photon budget of {ref}`Chapter 7.3 <chap7_3>` in its starkest form.
```

TCSPC is not the only option. _Frequency-domain_ FLIM modulates the excitation sinusoidally and measures the phase shift and the loss of modulation depth of the emission, from which the lifetime follows. It can be faster, and is easier to combine with cameras, but copes less gracefully with mixtures of lifetimes. Increasingly common, whichever way the data were acquired, is _phasor analysis_: each pixel's decay is transformed into a single point on a two-dimensional plot, without fitting any model. A pure single-exponential species falls on a semicircle, and a mixture of two species falls on the straight line joining them, at a position that gives their proportions. If you read FLIM papers, you will meet phasor plots.

## What people measure with it

**Absolute pH.** The chromophore of enhanced yellow fluorescent protein can be protonated, and the protonated and deprotonated forms decay at different rates. Across the range from pH 4.5 to 9.0, its lifetime moves from about 1.8 to 3.2 ns. In _{numref}`Fig. {number} <chap8_ex_flim_ph>`_ the intensity images across that range are essentially uninformative; the lifetime images read out the pH directly, pixel by pixel.

```{figure} ../figures/chap8_ex_flim_ph.png
---
width: 95%
name: chap8_ex_flim_ph
align: center
---
Cells expressing EYFP in buffers of known pH. Top: intensity images, which vary from cell to cell for reasons unrelated to pH. Bottom: lifetime images, which change systematically from about 1.8 ns at pH 4.5 to 3.2 ns at pH 9.0. Source: [to be added].
```

**Temperature.** A BODIPY dye carrying a phenyl ring that can twist relative to the rest of the molecule makes a molecular thermometer. The twisting motion is a non-radiative escape route, and it speeds up as the temperature rises, so the lifetime falls from about 5.5 ns at 23 °C to about 4.5 ns at 55 °C. One nanosecond of range may sound small, but TCSPC resolves lifetimes to a few tens of picoseconds, so the sensor distinguishes changes of a few degrees. The image in _{numref}`Fig. {number} <chap8_ex_flim_temperature>`_ also shows a common display convention: brightness from the intensity, which shows where the cells are, and colour from the lifetime, which shows how warm they are.

```{figure} ../figures/chap8_ex_flim_temperature.png
---
width: 85%
name: chap8_ex_flim_temperature
align: center
---
A fluorescent molecular thermometer in living cells imaged at temperatures from 23 to 55 °C. Intensity sets the brightness of each pixel and lifetime its colour. Right: the structure of the dye, with the arrow marking the rotation that provides the temperature-dependent non-radiative pathway. Source: [to be added].
```

**Membrane voltage, through FRET.** The Ace2N-mNeon sensor fuses the bright green fluorescent protein mNeonGreen to Ace2N, a rhodopsin domain whose retinal chromophore absorbs differently depending on the membrane voltage. The rhodopsin is the FRET acceptor. When the voltage changes, its absorption spectrum changes, the spectral overlap with mNeonGreen changes, and so $R_0$ and the transfer efficiency change, even though the distance between the two does not. The donor lifetime follows. In the zebrafish embryo of _{numref}`Fig. {number} <chap8_ex_flim_voltage>`_, different tissues sit at visibly different lifetimes. Turning those into millivolts requires calibration and controls, for instance for autofluorescence, but because the readout is a lifetime, the same calibration holds in every cell regardless of how much sensor it expresses. Bioelectric signalling during development, outside the nervous system, is still poorly understood, and this kind of measurement is one of the few ways to study it quantitatively in an intact animal.

```{figure} ../figures/chap8_ex_flim_voltage.png
---
width: 60%
name: chap8_ex_flim_voltage
align: center
---
Lifetime image of a zebrafish embryo expressing the voltage sensor Ace2N-mNeon. The colour scale spans 2.5 to 3.1 ns. Source: [to be added].
```

## Summary

- **Advantages**: quantitative and absolute, once the probe has been calibrated; independent of concentration, excitation power, photobleaching and depth; sensitive to the local chemical and physical environment in ways no intensity measurement can match; the most robust readout of FRET, needing only the donor.
- **Drawbacks**: slow, for the photon-budget and pile-up reasons above, which puts fast dynamics largely out of reach; analysis is genuinely complicated, especially for mixtures of lifetimes; the hardware, pulsed lasers, single-photon detectors and timing electronics, is expensive.

One observation sets up the next section. Cells contain molecules that fluoresce without any label, among them the metabolic cofactors NADH and NADPH that {ref}`Chapter 4.1 <chap4_1>` introduced as a source of autofluorescence. Their lifetime is around 0.4 ns when they are free in solution and two to three nanoseconds when they are bound to enzymes, so the lifetime of unlabelled tissue reports on its metabolic state. That is already a label-free measurement, and it points towards a family of techniques that do away with fluorophores altogether.
