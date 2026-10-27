(chap8_2)=
# 8.2 - Molecular techniques

The three techniques in this section are performed on ordinary fluorescence microscopes, and none of them is primarily about making an image. They answer questions that an image cannot: how fast is this molecule moving, what fraction of it is stuck to something, and is it touching that other molecule. Two of them, FCS and FRAP, measure motion. The third, FRET, measures proximity. All three return a number with units, and a number with units is a different kind of scientific object from a picture.

There is a pleasing piece of history connecting the first two, and connecting both to Chapter 5. Fluorescence correlation spectroscopy was introduced in 1972 by Douglas Magde, Elliot Elson and Watt Webb at Cornell; the quantitative analysis of photobleaching recovery came from Webb's group a few years later; and in 1990 the same laboratory built the first two-photon microscope. Much of this chapter grew out of one corridor.

## Fluorescence correlation spectroscopy

### Listening to the noise

Take a confocal microscope, park the laser at one point, and stop scanning. The pinhole restricts what the detector sees to a small ellipsoid around the focus, the _detection volume_,

$$ V_{\rm eff} = \pi^{3/2}\,\omega_{xy}^2\,\omega_z, $$

where $\omega_{xy}$ and $\omega_z$ are its lateral and axial radii. For a diffraction-limited confocal spot this is a few tenths of a femtolitre, less than $10^{-15}$ litres. At nanomolar concentrations it contains, on average, a handful of molecules.

Now record the fluorescence over time. Molecules wander in and out of the volume by Brownian motion, and every arrival or departure makes the signal jump. What you record looks like noise, and in any other chapter of this book we would be trying to suppress it. Here it _is_ the measurement (_{numref}`Fig. {number} <chap8_fcs_principle>`_).

```{figure} ../figures/chap8_fcs_principle.png
---
width: 95%
name: chap8_fcs_principle
align: center
---
(a) The detection volume defined by the focus and the pinhole. Only molecules inside it contribute. (b) The signal fluctuates as molecules diffuse in and out. (c) Slower diffusion moves the autocorrelation decay to longer lag times. (d) The amplitude at short lag is the inverse of the average number of molecules in the volume, so a higher concentration gives a lower curve.
```

The way to extract information from a fluctuating signal is to compare it with itself a little later. The _autocorrelation function_ is

$$ G(\tau) = \frac{\langle \delta F(t)\,\delta F(t+\tau) \rangle}{\langle F(t) \rangle^{2}}, \qquad \delta F(t) = F(t) - \langle F(t) \rangle . $$

In words: take the deviation from the mean, multiply it by the deviation a time $\tau$ later, and average over the whole recording. If a molecule typically stays in the volume for a time $\tau_D$, then for lags much shorter than $\tau_D$ the signal still resembles itself and $G$ is large; for lags much longer, the molecule responsible for the fluctuation has left and the memory is gone, so $G$ falls to zero.

For free three-dimensional diffusion, with no binding, flow or photophysics, the expected shape is

$$ G(\tau) = \frac{1}{N}\left(1 + \frac{\tau}{\tau_D}\right)^{-1}\left(1 + \frac{\tau}{\kappa^{2}\tau_D}\right)^{-1/2}, $$

with $N$ the average number of molecules in the volume and $\kappa = \omega_z/\omega_{xy}$ the elongation of the volume. For molecules diffusing in a two-dimensional membrane the second bracket disappears. Fitting the measured curve returns two quantities:

$$ G(0) = \frac{1}{N} \;\Rightarrow\; C = \frac{N}{V_{\rm eff}N_A}, \qquad\qquad D = \frac{\omega_{xy}^{2}}{4\tau_D}. $$

The amplitude gives the concentration, the decay time gives the diffusion coefficient. Five molecules in a volume of 0.3 fL corresponds to about 28 nM, which is why FCS is at home at concentrations where a conventional image would be almost empty.

The inverse dependence on $N$ is the most counterintuitive feature, and worth dwelling on. More molecules mean a _smaller_ correlation amplitude, because the fluctuation caused by one molecule entering or leaving is a smaller fraction of the total signal. It is the same $1/\sqrt{N}$ statistics that governs shot noise. FCS therefore works best at low concentrations, and becomes progressively harder as the concentration rises.

### Try it yourself

The simulation below does what an FCS instrument does, from scratch. Molecules perform random walks in a two-dimensional patch of sample, as they would in a membrane. The detected signal is the sum of their contributions, weighted by a Gaussian detection spot of radius $\omega = 0.25$ μm. Real molecules cross a confocal spot in about a millisecond, far too fast to follow by eye, so the simulation starts in slow motion: watch individual molecules drift through the spot and produce bumps in the trace. Pressing **Measure** then fast-forwards through several seconds of real measurement time, computes the autocorrelation from the signal and fits it with the two-dimensional model. Nothing in the simulation knows the answer: the fitted values have to emerge from the noise.

```{raw} html
<div id="fcs-sim" class="almb-widget">
  <style>
    #fcs-sim.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:760px;margin:1.2em auto;padding:18px 22px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #fcs-sim .ctrls{display:flex;flex-direction:column;gap:10px;margin-bottom:14px;}
    #fcs-sim .row{display:grid;grid-template-columns:260px 1fr;align-items:center;gap:14px;}
    #fcs-sim .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #fcs-sim .lab b{color:#e05020;font-weight:600;}
    #fcs-sim input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #fcs-sim .stage{display:grid;grid-template-columns:240px 1fr;gap:14px;margin-bottom:14px;}
    #fcs-sim canvas{width:100%;height:auto;display:block;border-radius:6px;}
    #fcs-sim .cap{font-size:11.5px;color:#777;margin:3px 0 0 2px;}
    #fcs-sim .right{display:flex;flex-direction:column;gap:6px;}
    #fcs-sim .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:12px;}
    #fcs-sim .card{background:#f7f7f8;border:1px solid #ececec;border-radius:8px;padding:9px 10px;text-align:center;}
    #fcs-sim .card .k{font-size:11px;color:#777;line-height:1.25;min-height:26px;display:flex;align-items:center;justify-content:center;}
    #fcs-sim .card .v{font-size:18px;font-weight:600;color:#2a4494;margin-top:3px;font-variant-numeric:tabular-nums;}
    #fcs-sim .card .u{font-size:11px;color:#999;}
    #fcs-sim .status{border-radius:8px;padding:10px 14px;font-size:13.5px;line-height:1.45;}
    #fcs-sim .btns{display:flex;gap:8px;justify-content:flex-end;margin-top:10px;}
    #fcs-sim button{font:inherit;font-size:13px;padding:5px 12px;border-radius:6px;border:1px solid #d0d0d0;background:#fafafa;cursor:pointer;}
    #fcs-sim button.main{background:#e05020;border-color:#e05020;color:#fff;}
    #fcs-sim button:hover{filter:brightness(0.96);}
    @media (max-width:620px){#fcs-sim .stage{grid-template-columns:1fr;} #fcs-sim .grid{grid-template-columns:1fr;} #fcs-sim .row{grid-template-columns:1fr;gap:2px;}}
  </style>
  <div class="ctrls">
    <div class="row"><span class="lab" id="fcs-n-lab">Molecules in the spot <b>&lang;N&rang;</b> = 4</span><input type="range" id="fcs-n" min="1" max="15" step="1" value="4"></div>
    <div class="row"><span class="lab" id="fcs-d-lab">Diffusion coefficient <b>D</b> = 10 &mu;m&sup2;/s</span><input type="range" id="fcs-d" min="0" max="100" step="1" value="59"></div>
  </div>
  <div class="stage">
    <div><canvas id="fcs-box" width="480" height="480"></canvas><div class="cap">4 &times; 4 &mu;m of sample, slowed down several hundred times. The orange spot is the detection volume.</div></div>
    <div class="right">
      <canvas id="fcs-trace" width="900" height="250"></canvas>
      <div class="cap">Fluorescence from the spot (slow motion). Each bump is a molecule passing through.</div>
      <canvas id="fcs-g" width="900" height="380"></canvas>
      <div class="cap">Autocorrelation after pressing Measure: dots measured, solid line the fit, dashed line the true curve.</div>
    </div>
  </div>
  <div class="grid">
    <div class="card"><div class="k">Fitted &lang;N&rang;<br>from the amplitude</div><div class="v" id="fcs-fn">&ndash;</div><div class="u">molecules (true: <span id="fcs-tn">4</span>)</div></div>
    <div class="card"><div class="k">Fitted D<br>from the decay time</div><div class="v" id="fcs-fd">&ndash;</div><div class="u">&mu;m&sup2;/s (true: <span id="fcs-tdd">10</span>)</div></div>
    <div class="card"><div class="k">Simulated<br>measurement time</div><div class="v" id="fcs-t">0.0</div><div class="u">s</div></div>
  </div>
  <div class="status" id="fcs-status"></div>
  <div class="btns"><button id="fcs-pause">Pause</button><button class="main" id="fcs-measure">Measure</button></div>
  <script>
  (function(){
    var W0=0.25, L=4.0, AEFF=Math.PI*W0*W0, SUBM=150, SUBV=4, RING=4096, VIEWN=360, GOAL=8000;
    var sN=document.getElementById("fcs-n"), sD=document.getElementById("fcs-d");
    var lN=document.getElementById("fcs-n-lab"), lD=document.getElementById("fcs-d-lab");
    var cBox=document.getElementById("fcs-box"), cTr=document.getElementById("fcs-trace"), cG=document.getElementById("fcs-g");
    var xB=cBox.getContext("2d"), xT=cTr.getContext("2d"), xG=cG.getContext("2d");
    var oN=document.getElementById("fcs-fn"), oD=document.getElementById("fcs-fd"), oT=document.getElementById("fcs-t"), oS=document.getElementById("fcs-status");
    var oTN=document.getElementById("fcs-tn"), oTD=document.getElementById("fcs-tdd");
    var bP=document.getElementById("fcs-pause"), bM=document.getElementById("fcs-measure");
    var Ntrue, D, tauD, dtM, dtV, M, px, py, mode="watch", lastFit=null, lastG=[];
    var ring, head, count, sumI, lags, sumProd, nProd, tSim, view, vhead, vcount, running=true, visible=true, frameNo=0;
    function Dval(){return Math.pow(10, 1.7*(+sD.value)/100);}
    lags=[]; (function(){var k=1; while(k<=3000){lags.push(Math.round(k)); k=Math.max(k+1,k*1.22);} })();
    function resetCorr(){ring=new Float64Array(RING); head=0; count=0; sumI=0; sumProd=new Float64Array(lags.length); nProd=new Float64Array(lags.length); tSim=0; lastFit=null; lastG=[];}
    function init(rebuild){
      Ntrue=+sN.value; D=Dval(); tauD=W0*W0/(4*D); dtM=tauD/15; dtV=(W0*W0/40)/240;
      var Ds=(D<10?D.toFixed(1):String(Math.round(D)));
      lN.innerHTML="Molecules in the spot <b>&lang;N&rang;</b> = "+Ntrue;
      lD.innerHTML="Diffusion coefficient <b>D</b> = "+Ds+" &mu;m&sup2;/s";
      oTN.textContent=Ntrue; oTD.textContent=Ds;
      if(rebuild){ M=Math.max(1,Math.round(Ntrue/AEFF*L*L)); px=new Float64Array(M); py=new Float64Array(M);
        for(var i=0;i<M;i++){px[i]=Math.random()*L; py[i]=Math.random()*L;} }
      view=new Float64Array(VIEWN); vhead=0; vcount=0;
      resetCorr(); mode="watch"; bM.textContent="Measure";
      oN.textContent="\u2013"; oD.textContent="\u2013"; oT.textContent="0.0";
      drawG(); report();
    }
    function move(dt){
      var a=Math.sqrt(6*D*dt), I=0, c=L/2, r2max=9*W0*W0, k2=2/(W0*W0);
      for(var i=0;i<M;i++){
        var x=px[i]+(2*Math.random()-1)*a, y=py[i]+(2*Math.random()-1)*a;
        if(x<0)x+=L; else if(x>=L)x-=L; if(y<0)y+=L; else if(y>=L)y-=L;
        px[i]=x; py[i]=y;
        var dx=x-c, dy=y-c, r2=dx*dx+dy*dy;
        if(r2<r2max) I+=Math.exp(-k2*r2);
      }
      return I;
    }
    function stepMeasure(){
      var I=move(dtM);
      ring[head]=I;
      for(var j=0;j<lags.length;j++){var k=lags[j]; if(count>=k){sumProd[j]+=I*ring[(head-k+RING)%RING]; nProd[j]++;}}
      head=(head+1)%RING; count++; sumI+=I; tSim+=dtM;
    }
    function gEst(){
      var m=sumI/Math.max(count,1), out=[];
      for(var j=0;j<lags.length;j++){ if(nProd[j]>50 && m>0){ out.push([lags[j]*dtM, sumProd[j]/nProd[j]/(m*m)-1]); } }
      return out;
    }
    function fit(g){
      if(g.length<6) return null;
      var best=null;
      for(var q=0;q<160;q++){
        var td=tauD*Math.pow(10,-1.5+3*q/159), sgg=0, sGg=0;
        for(var i=0;i<g.length;i++){var mdl=1/(1+g[i][0]/td); sgg+=mdl*mdl; sGg+=g[i][1]*mdl;}
        var amp=sGg/sgg, res=0;
        for(var i2=0;i2<g.length;i2++){var e=g[i2][1]-amp/(1+g[i2][0]/td); res+=e*e;}
        if(best===null||res<best.res) best={res:res,amp:amp,td:td};
      }
      return best;
    }
    function drawBox(){
      var s=cBox.width/L, c=cBox.width/2;
      xB.fillStyle="#101010"; xB.fillRect(0,0,cBox.width,cBox.height);
      var grd=xB.createRadialGradient(c,c,0,c,c,W0*s*1.8);
      grd.addColorStop(0,"rgba(224,80,32,0.85)"); grd.addColorStop(0.55,"rgba(224,80,32,0.35)"); grd.addColorStop(1,"rgba(224,80,32,0)");
      xB.fillStyle=grd; xB.beginPath(); xB.arc(c,c,W0*s*1.8,0,2*Math.PI); xB.fill();
      var k2=2/(W0*W0);
      for(var i=0;i<M;i++){
        var dx=px[i]-L/2, dy=py[i]-L/2, w=Math.exp(-k2*(dx*dx+dy*dy));
        xB.fillStyle= w>0.05 ? "rgba(124,252,124,"+(0.45+0.55*w).toFixed(2)+")" : "#4d4d4d";
        xB.fillRect(px[i]*s-2,py[i]*s-2,4,4);
      }
      if(mode==="measure"){ xB.fillStyle="rgba(255,255,255,0.10)"; xB.fillRect(0,0,cBox.width,cBox.height); }
    }
    function drawTrace(){
      var Wd=cTr.width, H=cTr.height;
      xT.clearRect(0,0,Wd,H); xT.fillStyle="#fafafa"; xT.fillRect(0,0,Wd,H);
      if(mode==="measure"){
        var p=Math.min(1,(tSim/tauD)/GOAL);
        xT.fillStyle="#555"; xT.font="26px sans-serif"; xT.textAlign="center";
        xT.fillText("Fast-forwarding to collect statistics\u2026", Wd/2, H/2-22);
        xT.fillStyle="#e6e6e6"; xT.fillRect(120,H/2,Wd-240,18); xT.fillStyle="#e05020"; xT.fillRect(120,H/2,(Wd-240)*p,18);
        xT.textAlign="left"; return;
      }
      var n=Math.min(vcount,VIEWN); if(n<2) return;
      var mx=0.3; for(var i=0;i<n;i++){ var v=view[(vhead-n+i+VIEWN)%VIEWN]; if(v>mx) mx=v; }
      var top=Math.max(mx*1.15, 1.0);
      xT.strokeStyle="#0d5e22"; xT.lineWidth=2.4; xT.beginPath();
      for(var j=0;j<n;j++){ var v2=view[(vhead-n+j+VIEWN)%VIEWN], x=(VIEWN-n+j)/(VIEWN-1)*Wd, y=H-10-(H-20)*v2/top; if(j===0)xT.moveTo(x,y); else xT.lineTo(x,y); }
      xT.stroke();
    }
    function drawG(){
      var g=lastG, f=lastFit;
      var Wd=cG.width, H=cG.height, l=70, r=16, t=14, b=50;
      xG.clearRect(0,0,Wd,H); xG.fillStyle="#fff"; xG.fillRect(0,0,Wd,H);
      var tmin=0.01e-3, tmax=2000e-3, ymax=Math.max(1.35/Ntrue, 0.02);
      function X(tau){return l+(Wd-l-r)*(Math.log10(tau)-Math.log10(tmin))/(Math.log10(tmax)-Math.log10(tmin));}
      function Y(v){return H-b-(H-b-t)*Math.max(Math.min(v/ymax,1.05),-0.1);}
      xG.strokeStyle="#333"; xG.lineWidth=1.5; xG.beginPath(); xG.moveTo(l,t); xG.lineTo(l,H-b); xG.lineTo(Wd-r,H-b); xG.stroke();
      xG.fillStyle="#555"; xG.font="20px sans-serif"; xG.textAlign="center";
      [1e-5,1e-4,1e-3,1e-2,1e-1,1].forEach(function(tk){var v=tk*1000, lbl=(v>=1?String(v):String(v)); xG.fillText(lbl,X(tk),H-b+24); xG.strokeStyle="#eee"; xG.beginPath(); xG.moveTo(X(tk),t); xG.lineTo(X(tk),H-b); xG.stroke();});
      xG.fillText("lag time \u03c4 [ms]", (l+Wd-r)/2, H-6);
      xG.save(); xG.translate(20,(H-b+t)/2); xG.rotate(-Math.PI/2); xG.fillText("G(\u03c4)",0,0); xG.restore();
      xG.strokeStyle="#999"; xG.setLineDash([8,6]); xG.lineWidth=2; xG.beginPath();
      for(var q=0;q<=200;q++){var tau=tmin*Math.pow(tmax/tmin,q/200), x=X(tau), y=Y((1/Ntrue)/(1+tau/tauD)); if(q===0)xG.moveTo(x,y); else xG.lineTo(x,y);} xG.stroke(); xG.setLineDash([]);
      if(f){ xG.strokeStyle="#e05020"; xG.lineWidth=2.4; xG.beginPath();
        for(var q2=0;q2<=200;q2++){var tau2=tmin*Math.pow(tmax/tmin,q2/200), x2=X(tau2), y2=Y(f.amp/(1+tau2/f.td)); if(q2===0)xG.moveTo(x2,y2); else xG.lineTo(x2,y2);} xG.stroke(); }
      xG.fillStyle="#2a4494";
      for(var i=0;i<g.length;i++){ if(g[i][0]>=tmin && g[i][0]<=tmax){ xG.beginPath(); xG.arc(X(g[i][0]),Y(g[i][1]),4.5,0,2*Math.PI); xG.fill(); } }
    }
    function hexA(hex,al){var r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16);return "rgba("+r+","+g+","+b+","+al+")";}
    function report(){
      oT.textContent=tSim.toFixed(1);
      var col, txt, f=lastFit;
      if(f){ var Nf=1/f.amp, Df=W0*W0/(4*f.td); oN.textContent=Nf.toFixed(1); oD.textContent=(Df<10?Df.toFixed(1):String(Math.round(Df))); }
      if(mode==="measure"){ col="#b07000"; txt="<b>Measuring.</b> Thousands of molecules have to cross the spot before the dots settle onto the dashed curve."; }
      else if(!f){ col="#2a4494"; txt="<b>Slow motion.</b> Watch molecules drift through the orange spot: each bump in the trace is one of them. Press <b>Measure</b> to record long enough to compute the correlation."; }
      else { var eN=Math.abs(1/f.amp-Ntrue)/Ntrue, eD=Math.abs(W0*W0/(4*f.td)-D)/D;
        if(eN<0.2&&eD<0.25){ col="#0d5e22"; txt="<b>Done.</b> The fit recovers the true values from noise alone. Change one slider and measure again: concentration moves the curve up or down, diffusion moves it left or right."; }
        else { col="#e05020"; txt="<b>Not quite converged.</b> Press Measure again for a longer recording."; } }
      oS.style.background=hexA(col,0.10); oS.style.border="1px solid "+hexA(col,0.35); oS.innerHTML="<span style='color:"+col+"'>"+txt+"</span>";
    }
    function frame(){
      if(running&&visible){
        frameNo++;
        if(mode==="watch"){
          var acc=0; for(var s=0;s<SUBV;s++) acc+=move(dtV);
          view[vhead]=acc/SUBV; vhead=(vhead+1)%VIEWN; vcount++;
          drawBox(); drawTrace();
        } else {
          for(var s2=0;s2<SUBM;s2++) stepMeasure();
          if(frameNo%20===0){ drawBox(); drawTrace(); }
          if(frameNo%6===0){ lastG=gEst(); lastFit=fit(lastG); drawG(); report(); }
          if(tSim/tauD>=GOAL){ lastG=gEst(); lastFit=fit(lastG); mode="watch"; bM.textContent="Measure again"; drawG(); report(); }
        }
      }
      requestAnimationFrame(frame);
    }
    sN.addEventListener("input",function(){init(true);});
    sD.addEventListener("input",function(){init(false);});
    bM.addEventListener("click",function(){ resetCorr(); mode="measure"; bM.textContent="Measuring\u2026"; running=true; bP.textContent="Pause"; drawG(); report(); drawTrace(); });
    bP.addEventListener("click",function(){running=!running; bP.textContent=running?"Pause":"Resume";});
    if("IntersectionObserver" in window){ new IntersectionObserver(function(es){visible=es[0].isIntersecting;}).observe(document.getElementById("fcs-sim")); }
    init(true); requestAnimationFrame(frame);
  })();
  </script>
</div>
```

Play with it for a minute. With one or two molecules in the spot, the trace is a series of isolated bumps and the correlation is high. Add molecules and the bumps overlap into a signal that hovers around its mean, and $G(0)$ drops. Slow the diffusion and the molecules dawdle; measure again and the curve slides to the right without changing height. Notice also how long the measurement has to run before the dots settle: it only converges once thousands of molecules have crossed the spot, which is why real FCS measurements take tens of seconds per point.

### What it can tell you

```{figure} ../figures/chap8_ex_fcs_ago2.png
---
width: 95%
name: chap8_ex_fcs_ago2
align: center
---
FCS in HEK293 cells stably expressing GFP-tagged Ago2. Left: the two measurement positions, in the nucleus (red) and the cytoplasm (cyan). Middle: normalised autocorrelation curves; the cytoplasmic curve decays later. Right: the interpretation, with largely free Ago2 in the nucleus and Ago2 incorporated into large complexes in the cytoplasm. Copyright: PicoQuant, via picoquant.com.
```

```{tip}
**Worked example: weighing a complex with a microscope that cannot see it.**

In _{numref}`Fig. {number} <chap8_ex_fcs_ago2>`_ the fitted diffusion coefficients are about 13.7 μm²/s in the nucleus and 5.4 μm²/s in the cytoplasm, a ratio of 2.5. Is that consistent with the proposed explanation?

For a compact object, the Stokes-Einstein relation gives $D \propto 1/R$, and its radius scales with molecular mass as $R \propto M^{1/3}$, so $D \propto M^{-1/3}$. Free Ago2 is about 158 kDa; the RNA-induced silencing complexes it joins in the cytoplasm are around 3 MDa. Then

$$ \frac{D_{\rm nuc}}{D_{\rm cyt}} \approx \left(\frac{3 \times 10^{6}}{1.58 \times 10^{5}}\right)^{1/3} = 19^{1/3} \approx 2.7 . $$

Predicted 2.7, measured 2.5. Neither complex is anywhere near resolvable, yet the measurement constrains their size. The cube root also carries a warning: a twenty-fold change in mass produces less than a three-fold change in diffusion, so FCS is good at detecting large changes in complex size and poor at detecting small ones.
```

### Summary

- **Advantages**: sensitivity down to single molecules and nanomolar concentrations; absolute values of concentration and diffusion coefficient; temporal resolution limited only by the detector, from microseconds upward; extensions to two colours (cross-correlation) report directly on whether two species move together.
- **Drawbacks**: a single point, with no spatial context beyond the position you chose; the result is only as good as the model fitted, and the crowded, compartmentalised cytoplasm often violates the assumption of free diffusion; it needs low expression levels and bright, photostable probes; measurements are slow to converge.

## Fluorescence recovery after photobleaching

### Principle

FCS listens to a system at equilibrium. FRAP does the opposite: it kicks the system out of equilibrium and watches it recover.

Image a labelled sample, then deliver a brief, intense pulse of light to a defined region, bleaching every fluorophore inside it (Chapter 4.1). The region goes dark. Then keep imaging at low power. Bleached molecules diffuse out of the region and unbleached molecules diffuse in, so the region slowly brightens again. How fast it brightens reports on mobility; how bright it eventually becomes reports on what fraction of the molecules can move at all.

```{figure} ../figures/chap8_frap_principle.png
---
width: 95%
name: chap8_frap_principle
align: center
---
(a) A uniformly labelled region before bleaching, immediately after, and after recovery by diffusion. (b) The recovery curve. The pre-bleach level, the level immediately after bleaching $F_0$ and the plateau $F_\infty$ define the mobile and immobile fractions, and the half-time of recovery gives the diffusion coefficient.
```

The mobile fraction follows directly from the three levels in _{numref}`Fig. {number} <chap8_frap_principle>`_,

$$ f_{\rm mobile} = \frac{F_\infty - F_0}{F_{\rm pre} - F_0}, $$

and for a uniformly bleached circular spot of radius $w$, with simple two-dimensional diffusion, the half-time of recovery gives

$$ D \approx \frac{0.224\,w^{2}}{t_{1/2}}. $$

The prefactor depends on the bleach profile and the geometry assumed, and different papers use different ones, so treat it as part of a model rather than as a constant of nature.

The simulation below runs two experiments side by side. Both compartments contain the same diffusing molecules. In the left one, 10% of them are anchored in place; in the right one, 85% are. Bleached molecules are drawn in grey so that you can watch them mix out of the box, something you can never see in a real experiment.

```{figure} ../figures/chap8_frap_simulation.gif
---
width: 85%
name: chap8_frap_simulation
align: center
---
Simulated FRAP in two compartments that differ only in their immobile fraction. Fluorescent molecules are green, bleached ones grey. The recovery curves (bottom) share the same initial speed, set by the diffusion coefficient of the mobile molecules, but plateau at very different levels, set by the fraction of molecules that cannot move.
```

Two lessons are hidden in _{numref}`Fig. {number} <chap8_frap_simulation>`_. The first is that rate and extent are independent: the two curves rise at the same initial speed, because the mobile molecules diffuse identically in both, but they saturate at entirely different levels. The second is subtler. Even in the mostly mobile compartment the plateau settles noticeably below 0.9, the value you would expect from a 10% immobile fraction. The reason is that the compartment is finite, and the bleach pulse permanently destroyed a few percent of all the fluorophores it contains. If the bleached region is a large fraction of a small cell, this depletion can masquerade as an immobile fraction. The cure is either to keep the bleached region small compared with the compartment, or to measure the total fluorescence of the cell and correct for it.

### What it can tell you

FRAP was developed in the mid-1970s to measure how fast molecules move laterally in membranes, and it provided some of the first quantitative support for the idea that the membrane is a two-dimensional fluid. Its most characteristic use today is the comparison in _{numref}`Fig. {number} <chap8_ex_frap_lbr>`_: the same protein, two locations, one question.

```{figure} ../figures/chap8_ex_frap_lbr.jpg
---
width: 55%
name: chap8_ex_frap_lbr
align: center
---
FRAP of GFP-tagged lamin B receptor. Bleached in the endoplasmic reticulum (left column), the region recovers within minutes: the protein diffuses freely in the ER membrane. Bleached in the nuclear envelope (right column), it barely recovers at all, because there the receptor is anchored to the nuclear lamina. Copyright: Ellenberg et al. (1997), via The Journal of Cell Biology.
```

### Summary

- **Advantages**: possible on almost any confocal microscope, and with a digital micromirror device (Chapter 7.1) several regions of arbitrary shape can be bleached in one experiment; reports on a whole region rather than a single point, so it is far less noise-limited than FCS; answers the binary question "free or bound?" very directly.
- **Drawbacks**: destructive by construction; the bleach pulse itself can be phototoxic; spatial resolution limited by how small a region can usefully be bleached; quantitative interpretation depends on the model, and a finite pool of fluorophores must be corrected for.

## FRET at work

Chapter 4.1 introduced Förster resonance energy transfer, the non-radiative handoff of energy from an excited donor to a nearby acceptor, and ended by promising that we would see it at work in this chapter. Here it is.

The physics fits in a single equation, already met in Chapter 4,

$$ E = \frac{1}{1 + (r/R_0)^{6}}, $$

and the sixth power makes FRET simultaneously the most sensitive molecular ruler available to a light microscope and an unusually short one.

```{tip}
**Worked example: how long is the ruler?**

Invert the efficiency: $r = R_0\left[(1-E)/E\right]^{1/6}$. An efficiency of 0.9 corresponds to $r = 0.69\,R_0$, and an efficiency of 0.1 to $r = 1.44\,R_0$. Everything measurable lies within a factor of about two in distance.

For a pair with $R_0 = 5.4$ nm, the useful range runs from roughly 3.7 to 7.8 nm. Closer than that, every configuration reads as maximum transfer. Further than about 10 nm there is no signal, and no signal looks exactly the same as no interaction. A negative FRET result is therefore never proof that two proteins do not interact: they may be bound with the fluorophores simply pointing away from each other.
```

Applications fall into two families, shown in _{numref}`Fig. {number} <chap8_fret_applications>`_.

```{figure} ../figures/chap8_fret_applications.png
---
width: 85%
name: chap8_fret_applications
align: center
---
(a) Intermolecular FRET: donor and acceptor sit on two different proteins. While they are apart, the donor emits its own colour; when they bind, the energy passes to the acceptor, which emits instead. (b) Intramolecular FRET: both fluorophores sit on one sensing domain. A stimulus folds the domain and brings them close together, switching the emission from donor colour to acceptor colour.
```

**Intermolecular FRET** puts the donor on one molecule and the acceptor on another and asks whether they come together. It is the standard way to detect protein-protein interactions in living cells, and unlike a biochemical pull-down it tells you where and when the interaction happens. Quantified carefully, the efficiency also constrains the geometry of a complex, which is useful input for structural models.

**Intramolecular FRET** puts both fluorophores on a single construct, joined by a sensing domain that changes conformation in response to something. The result is a genetically encoded biosensor that turns a chemical or physical variable into a change in the ratio of acceptor to donor emission. The first widely used example, the cameleon calcium sensors of the late 1990s, sandwiched calmodulin and a calmodulin-binding peptide between two fluorescent proteins of different colours: calcium binding folds the peptide into calmodulin and brings the two fluorophores together. The same design principle now reports on kinase activity, small GTPase activation, pH, mechanical tension across a protein, and membrane voltage. This is the form in which most people meet FRET today.

The difficulties are worth stating plainly. Building a working sensor takes a pair with good spectral overlap but separable emission, a linker that converts the conformational change into a useful change in distance, and a construct that folds and behaves like the protein it reports on. Measuring the efficiency itself from intensities is harder still: some donor emission leaks into the acceptor channel, some acceptor is excited directly by the donor's excitation light, and the ratio of donors to acceptors in a given pixel is usually unknown. Even $R_0$ carries an assumption, because it depends on the relative orientation of the two dipoles, which is almost always assumed rather than measured. Most published FRET is therefore used comparatively, as a change between conditions, rather than as an absolute distance, and that is usually the honest way to use it.

Two experimental tricks help. In _acceptor photobleaching_, the acceptor is deliberately destroyed, a FRAP-like manoeuvre, and the donor is measured before and after: if it gets brighter, it was transferring energy, and $E = 1 - F_{D,\rm before}/F_{D,\rm after}$. The cleaner trick never touches the acceptor at all. A donor that transfers energy gains an extra route back to the ground state, so it leaves the excited state sooner: its _lifetime_ drops. Measure that lifetime and

$$ E = 1 - \frac{\tau_{DA}}{\tau_D}, $$

independent of how much sensor the cell expresses, of spectral bleedthrough, and of stoichiometry.

### Summary

- **Advantages**: sensitivity to separations of a few nanometres, far below the diffraction limit; works in living cells and animals; genetically encodable sensors turn almost any molecular event into an optical signal in real time.
- **Drawbacks**: a short and steep working range, so negative results are inconclusive; absolute efficiencies are difficult to obtain from intensities; sensors are laborious to design and validate; the orientation factor is usually assumed.

Measuring a lifetime at every pixel of an image requires counting photons with nanosecond timing, and that is the subject of the next section.
