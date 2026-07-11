# 7 - Imaging system design

a


To add to subsection about cameras:
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