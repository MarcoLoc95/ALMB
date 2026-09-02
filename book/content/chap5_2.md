(chap5_2)=
# TIRF microscopy

## When 850 nm is still far too thick

The confocal microscope we just built gives an optical section of a bit under a micrometre. For most of cell biology that is excellent. For one particular class of question it is hopeless.

Suppose you want to watch a secretory vesicle fuse with the plasma membrane. The plasma membrane is about 5 nm thick. The interesting part of the event, the approach, docking and fusion, plays out within perhaps 100 nm of it. A 850 nm confocal section contains all of that, plus roughly eight times as much cytoplasm, full of vesicles that are not fusing and of freely diffusing labelled protein. The signal you want is a small perturbation on top of a large fluctuating background.

The same problem appears whenever the biology lives at the coverslip: focal adhesions, receptor clustering and diffusion in the membrane, cell-substrate contacts, single-molecule assays with proteins bound to a functionalised glass surface. What is needed is not a thinner slice through the specimen but a way of exciting a shell only a hundred nanometres deep, sitting exactly on the glass.

**Total internal reflection fluorescence** microscopy does this, and it does it using nothing more exotic than Snell's law.

## Total internal reflection

Recall from {ref}`Chapter 1 <chap1_3>` that at an interface between two media, light obeys

$$
n_1 \sin\theta_i = n_2 \sin\theta_t
$$

When light travels from a denser medium into a less dense one ($n_1 > n_2$), the transmitted ray bends *away* from the normal, so $\theta_t > \theta_i$. Increase the angle of incidence and $\theta_t$ grows faster than $\theta_i$ does. At some point it reaches 90°, the transmitted ray lies flat along the interface, and beyond that angle Snell's law has no real solution at all. The condition $\sin\theta_t = 1$ defines the **critical angle**:

$$
\theta_c = \arcsin\!\left(\frac{n_2}{n_1}\right)
$$

It is worth seeing why the failure is total rather than gradual. Rearranging Snell's law gives $\sin\theta_t = (n_1/n_2)\sin\theta_i$, and for $\theta_i > \theta_c$ the right-hand side exceeds one. There is no angle whose sine is greater than one, so there is no transmitted ray. Not a weak one: none. All of the energy is reflected back into the dense medium. This is **total internal reflection**, and you have seen it many times without naming it. It is what guides light along an optical fibre. It is why the sea near the horizon turns into a sheet of white glare, the sun reflecting off a surface you are viewing at a very shallow angle. And it is why, from underwater, the surface above you stops being a window and becomes a mirror once you look far enough from the vertical.

### Simulation: crossing the critical angle

Sweep the angle and watch where the energy goes. The opacity of each ray is the fraction of the power it carries, computed from the Fresnel equations. Below the critical angle almost everything is transmitted and the refracted ray bends steadily away from the normal. As you approach $\theta_c$ the transmitted ray swings towards the interface and fades while the reflected ray brightens, and past $\theta_c$ it vanishes entirely. The second slider changes the refractive index of the sample, which moves $\theta_c$: try setting it to 1.38, a realistic value for cytoplasm, and see how much steeper you have to go.

```{raw} html
<div id="tir-widget" class="almb-widget">
  <style>
    #tir-widget.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:640px;margin:1.2em auto;padding:18px 22px 16px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #tir-widget .row{display:grid;grid-template-columns:250px 1fr;align-items:center;gap:14px;margin-bottom:10px;}
    #tir-widget .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #tir-widget .lab b{color:#e05020;font-weight:600;}
    #tir-widget input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #tir-widget svg{width:100%;height:auto;display:block;margin-top:6px;}
    #tir-widget .readout{margin-top:10px;font-size:13.5px;color:#333;text-align:center;line-height:1.7;}
    #tir-widget .readout b{font-weight:650;}
    #tir-widget .hint{font-size:12.5px;color:#777;margin-top:8px;line-height:1.45;text-align:center;}
    @media (max-width:470px){#tir-widget .row{grid-template-columns:1fr;gap:2px;}}
  </style>

  <div class="row">
    <span class="lab" id="tir-a-lab">Angle of incidence = <b>45.0°</b></span>
    <input type="range" id="tir-a" min="0" max="88" step="0.5" value="45">
  </div>
  <div class="row">
    <span class="lab" id="tir-n-lab">Sample refractive index <b>n<sub>2</sub></b> = 1.33</span>
    <input type="range" id="tir-n" min="1.30" max="1.45" step="0.005" value="1.33">
  </div>

  <svg id="tir-svg" viewBox="0 0 560 330" xmlns="http://www.w3.org/2000/svg"></svg>
  <div class="readout" id="tir-out"></div>
  <div class="hint">Cover glass and immersion oil are fixed at n<sub>1</sub> = 1.518. Ray opacity shows how much of the energy goes each way.</div>

  <script>
  (function(){
    var el = document.getElementById("tir-widget");
    if (!el || el.dataset.init) return;
    el.dataset.init = "1";

    var N1 = 1.518;
    var svg = document.getElementById("tir-svg");
    var sA = document.getElementById("tir-a"), sN = document.getElementById("tir-n");
    var labA = document.getElementById("tir-a-lab"), labN = document.getElementById("tir-n-lab");
    var out = document.getElementById("tir-out");

    var W = 560, H = 330, OX = 280, OY = 178, L = 152;

    function fresnel(th, n2){
      var si = Math.sin(th), ci = Math.cos(th);
      var s2 = (N1/n2)*si;
      if (s2 >= 1) return 1;
      var ct = Math.sqrt(1 - s2*s2);
      var rs = (N1*ci - n2*ct)/(N1*ci + n2*ct);
      var rp = (n2*ci - N1*ct)/(n2*ci + N1*ct);
      return 0.5*(rs*rs + rp*rp);
    }

    function arrow(x1,y1,x2,y2,col,op,w){
      var dx = x2-x1, dy = y2-y1, len = Math.sqrt(dx*dx+dy*dy);
      if (len < 1e-6) return "";
      dx /= len; dy /= len;
      var b = 10, hw = 5;
      var bx = x2 - dx*b, by = y2 - dy*b;
      var p1x = bx - dy*hw, p1y = by + dx*hw;
      var p2x = bx + dy*hw, p2y = by - dx*hw;
      return '<line x1="'+x1.toFixed(1)+'" y1="'+y1.toFixed(1)+'" x2="'+bx.toFixed(1)+
             '" y2="'+by.toFixed(1)+'" stroke="'+col+'" stroke-opacity="'+op.toFixed(3)+
             '" stroke-width="'+w+'" stroke-linecap="round"/>' +
             '<polygon points="'+x2.toFixed(1)+','+y2.toFixed(1)+' '+p1x.toFixed(1)+','+
             p1y.toFixed(1)+' '+p2x.toFixed(1)+','+p2y.toFixed(1)+
             '" fill="'+col+'" fill-opacity="'+op.toFixed(3)+'"/>';
    }

    function update(){
      var thd = parseFloat(sA.value), n2 = parseFloat(sN.value);
      var th = thd*Math.PI/180;
      var thc = Math.asin(n2/N1), thcd = thc*180/Math.PI;
      var R = fresnel(th, n2), T = 1 - R;
      var tir = thd >= thcd;

      labA.innerHTML = "Angle of incidence = <b>" + thd.toFixed(1) + "&deg;</b>";
      labN.innerHTML = "Sample refractive index <b>n<sub>2</sub></b> = " + n2.toFixed(3);

      var s = '<defs>' +
              '<linearGradient id="tir-ev" x1="0" y1="1" x2="0" y2="0">' +
              '<stop offset="0%" stop-color="#e05020" stop-opacity="0.55"/>' +
              '<stop offset="100%" stop-color="#e05020" stop-opacity="0"/></linearGradient></defs>';

      // media
      s += '<rect x="0" y="'+OY+'" width="'+W+'" height="'+(H-OY)+'" fill="#dbe6ef"/>';
      s += '<rect x="0" y="0" width="'+W+'" height="'+OY+'" fill="#f6fafd"/>';
      if (tir){
        s += '<rect x="0" y="'+(OY-34)+'" width="'+W+'" height="34" fill="url(#tir-ev)"/>';
      }
      s += '<line x1="0" y1="'+OY+'" x2="'+W+'" y2="'+OY+'" stroke="#7f97a8" stroke-width="2"/>';
      s += '<line x1="'+OX+'" y1="14" x2="'+OX+'" y2="'+(H-10)+'" stroke="#aaa" stroke-width="1" stroke-dasharray="5 5"/>';
      s += '<text x="10" y="'+(H-12)+'" font-size="12.5" fill="#3a5b73">glass, n<tspan baseline-shift="sub" font-size="9">1</tspan> = 1.518</text>';
      s += '<text x="10" y="20" font-size="12.5" fill="#3a5b73">sample, n<tspan baseline-shift="sub" font-size="9">2</tspan> = '+n2.toFixed(3)+'</text>';

      // incident ray (from lower left, up to the origin)
      var ix = OX - L*Math.sin(th), iy = OY + L*Math.cos(th);
      s += arrow(ix, iy, OX, OY, "#e05020", 1.0, 3);

      // reflected ray (down to the right)
      var rx = OX + L*Math.sin(th), ry = OY + L*Math.cos(th);
      s += arrow(OX, OY, rx, ry, "#e05020", Math.max(R, 0.06), 3);

      // transmitted ray (up into the sample)
      if (!tir){
        var st = (N1/n2)*Math.sin(th), tt = Math.asin(st);
        var tx = OX + L*Math.sin(tt), ty = OY - L*Math.cos(tt);
        s += arrow(OX, OY, tx, ty, "#0072B2", Math.max(T, 0.06), 3);
        s += '<text x="'+(tx+6)+'" y="'+(ty-2)+'" font-size="12" fill="#0072B2">' +
             (tt*180/Math.PI).toFixed(1)+'&deg;</text>';
      }

      // angle arc and label
      var arc = "";
      for (var k=0; k<=24; k++){
        var a = th*k/24;
        var px = OX - 46*Math.sin(a), py = OY + 46*Math.cos(a);
        arc += (k? "L":"M") + px.toFixed(1) + " " + py.toFixed(1) + " ";
      }
      s += '<path d="'+arc+'" fill="none" stroke="#666" stroke-width="1.2"/>';
      s += '<text x="'+(OX - 62*Math.sin(th/2) - 6)+'" y="'+(OY + 62*Math.cos(th/2) + 4)+
           '" font-size="12.5" fill="#444" text-anchor="middle">&#952;</text>';

      s += '<text x="'+(W-10)+'" y="'+(H-12)+'" font-size="12.5" fill="'+(tir?"#D55E00":"#888")+
           '" text-anchor="end">&#952;'+'<tspan baseline-shift="sub" font-size="9">c</tspan> = '+
           thcd.toFixed(1)+'&deg;</text>';
      if (tir){
        s += '<text x="'+(W-10)+'" y="24" font-size="13" fill="#D55E00" text-anchor="end">total internal reflection</text>';
      }
      svg.innerHTML = s;

      out.innerHTML = tir
        ? '<b style="color:#D55E00">100% reflected, nothing transmitted.</b> An evanescent field remains in the first ~100 nm of the sample.'
        : '<b style="color:#0072B2">' + (100*T).toFixed(1) + '%</b> transmitted &nbsp;|&nbsp; <b style="color:#e05020">' +
          (100*R).toFixed(1) + '%</b> reflected';
    }

    sA.addEventListener("input", update);
    sN.addEventListener("input", update);
    update();
  })();
  </script>
</div>
```

The numbers for a microscope are as follows. Standard immersion oil and cover glass are matched at $n_1$ = 1.518. The aqueous medium above is around $n_2$ = 1.33, and the interior of a cell is a little higher, roughly 1.36 to 1.38. So

$$
\theta_c = \arcsin\!\left(\frac{1.33}{1.518}\right) = 61.2° \qquad \text{(buffer)}
$$

and about 65° for the cytoplasm. These are large angles, and that turns out to be the whole engineering challenge of TIRF.

## The evanescent field

Here is the part that makes the technique possible. "No light is transmitted" is a statement about energy flow, not about the electromagnetic field. The field cannot simply stop at the interface, because Maxwell's equations require the tangential components to be continuous across it, and nothing in nature jumps discontinuously from a finite value to zero. What happens instead is that a field does exist in the second medium, but it carries no net energy away: it oscillates in place and dies off exponentially with distance from the surface.

The result is worth deriving rather than quoting, because every term in the final formula can be traced back to a step in the argument. You will not be asked to reproduce it, but you should be able to follow where each piece comes from.

Write the transmitted wave in complex form, as we did in {ref}`Chapter 1 <chap1_2>`:

$$
\vec{E}_t = \vec{E}_{t,0}\,e^{\,i\left(\vec{k}_t \cdot \vec{r} - \omega t\right)}
$$

Put the origin where the beam meets the interface, let $x$ run along the interface and $z$ perpendicular to it, pointing into the sample. Then $\vec{k}_t \cdot \vec{r} = k_x x + k_z z$, and simple trigonometry on the wave vector gives its two components:

$$
k_x = k_t \sin\theta_t, \qquad k_z = k_t \cos\theta_t
$$

We know Snell's law for the sine, so the first component is immediate:

$$
k_x = k_t \sin\theta_t = k_t\,\frac{n_1}{n_2}\sin\theta_i
$$

We have no Snell's law for the cosine, but we have trigonometry. Writing $\cos\theta_t = \sqrt{1 - \sin^2\theta_t}$ and substituting again,

$$
k_z = k_t\sqrt{1 - \left(\frac{n_1}{n_2}\right)^{2}\sin^{2}\theta_i}
$$

Now look at what happens beyond the critical angle. There, by definition, $(n_1/n_2)\sin\theta_i > 1$, so the quantity under the square root is _negative_. Rather than declaring the situation impossible, factor out the minus sign:

$$
k_z = k_t\sqrt{-1}\,\sqrt{\left(\frac{n_1}{n_2}\right)^{2}\sin^{2}\theta_i - 1} = i\,\beta,
\qquad \beta \equiv k_t\sqrt{\left(\frac{n_1}{n_2}\right)^{2}\sin^{2}\theta_i - 1}
$$

The perpendicular component of the wave vector has become purely imaginary, and $\beta$, which is a perfectly ordinary positive real number, is called the **attenuation coefficient**. Substituting back into the wave and splitting the exponential into its $x$ and $z$ parts:

$$
\vec{E}_t = \vec{E}_{t,0}\,e^{\,i\left(k_x x - \omega t\right)}\,e^{\,i(i\beta)z}
= \vec{E}_{t,0}\,\underbrace{e^{\,i\left(k_x x - \omega t\right)}}_{\text{travels along } x}\,\underbrace{e^{-\beta z}}_{\text{decays along } z}
$$

because $i \times i = -1$. This is the whole result in one line. There _is_ a field in the sample. It propagates along the surface, in the $x$ direction, exactly as an ordinary wave would. Perpendicular to the surface it does not propagate at all: it simply decays. A wave that fades away instead of travelling is called **evanescent**, from the Latin for vanishing.

Intensity is the squared modulus of the field. The travelling factor has modulus one, so only the decaying factor survives, and it survives squared:

$$
I(z) = I_0\,e^{-2\beta z} \equiv I_0\,e^{-z/d}, \qquad d \equiv \frac{1}{2\beta}
$$

The length $d$ is the **penetration depth**: the distance over which the excitation intensity falls by a factor $e$. Substituting $k_t = 2\pi n_2/\lambda_0$ into the definition of $\beta$, the refractive index $n_2$ cancels neatly out of the bracket and leaves

$$
d = \frac{\lambda_0}{4\pi\sqrt{n_1^2\sin^2\theta_i - n_2^2}}
$$

where $\lambda_0$ is the vacuum wavelength. Everything on the right is something you know or can set: the two refractive indices, the colour of your laser and the angle you dial in. Two features of this expression matter. First, $d$ is a fraction of a wavelength, typically 60 to 200 nm, which is exactly the scale we wanted. Second, the square root goes to zero as $\theta$ approaches $\theta_c$, so $d$ diverges there: just above the critical angle the field reaches deep into the sample, and the sectioning is poor. Push to steeper angles and it tightens quickly.

### Simulation: how deep the light reaches

The slider sets the angle of incidence, starting just above the critical angle. Watch what happens in the first fraction of a degree: at 61.5° the field still reaches several hundred nanometres into the sample, and by 65° it is down to about 110 nm. This is why setting the TIRF angle is a real skill rather than a switch, and why an angle that is almost critical gives you a bright image that is not really TIRF at all. The second slider changes the excitation wavelength, which matters less but is not negligible.

```{raw} html
<div id="ev-widget" class="almb-widget">
  <style>
    #ev-widget.almb-widget{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;max-width:620px;margin:1.2em auto;padding:18px 22px 16px;background:#fff;border:1px solid #e6e6e6;border-radius:10px;box-shadow:0 1px 3px rgba(0,0,0,.05);color:#222;box-sizing:border-box;}
    #ev-widget .row{display:grid;grid-template-columns:250px 1fr;align-items:center;gap:14px;margin-bottom:10px;}
    #ev-widget .lab{font-size:14px;font-variant-numeric:tabular-nums;color:#333;white-space:nowrap;}
    #ev-widget .lab b{color:#e05020;font-weight:600;}
    #ev-widget input[type=range]{width:100%;accent-color:#e05020;height:22px;cursor:pointer;}
    #ev-widget svg{width:100%;height:auto;display:block;margin-top:6px;}
    #ev-widget .readout{margin-top:10px;font-size:13.5px;color:#333;text-align:center;}
    #ev-widget .readout b{color:#e05020;font-weight:650;}
    #ev-widget .hint{font-size:12.5px;color:#777;margin-top:8px;line-height:1.45;text-align:center;}
    @media (max-width:470px){#ev-widget .row{grid-template-columns:1fr;gap:2px;}}
  </style>

  <div class="row">
    <span class="lab" id="ev-a-lab">Angle of incidence = <b>65.0°</b></span>
    <input type="range" id="ev-a" min="61.5" max="80" step="0.1" value="65">
  </div>
  <div class="row">
    <span class="lab" id="ev-l-lab">Excitation wavelength <b>&lambda;</b> = 488 nm</span>
    <input type="range" id="ev-l" min="400" max="680" step="1" value="488">
  </div>

  <svg id="ev-svg" viewBox="0 0 560 300" xmlns="http://www.w3.org/2000/svg"></svg>
  <div class="readout" id="ev-out"></div>
  <div class="hint">Cover glass n<sub>1</sub> = 1.518, aqueous sample n<sub>2</sub> = 1.33, so the critical angle is 61.2&deg;.</div>

  <script>
  (function(){
    var el = document.getElementById("ev-widget");
    if (!el || el.dataset.init) return;
    el.dataset.init = "1";

    var N1 = 1.518, N2 = 1.33;
    var THC = Math.asin(N2/N1)*180/Math.PI;
    var svg = document.getElementById("ev-svg");
    var sA = document.getElementById("ev-a"), sL = document.getElementById("ev-l");
    var labA = document.getElementById("ev-a-lab"), labL = document.getElementById("ev-l-lab");
    var out = document.getElementById("ev-out");

    var W = 560, H = 300, PAD = {l:56, r:120, t:16, b:44};
    var ZMAX = 400;
    function X(z){ return PAD.l + (z/ZMAX)*(W-PAD.l-PAD.r); }
    function Y(i){ return H-PAD.b - i*(H-PAD.t-PAD.b); }

    function depth(thd, lam){
      var s = Math.sin(thd*Math.PI/180);
      return lam/(4*Math.PI*Math.sqrt(N1*N1*s*s - N2*N2));
    }

    function update(){
      var thd = parseFloat(sA.value), lam = parseFloat(sL.value);
      var d = depth(thd, lam);
      labA.innerHTML = "Angle of incidence = <b>" + thd.toFixed(1) + "&deg;</b>";
      labL.innerHTML = "Excitation wavelength <b>&lambda;</b> = " + lam.toFixed(0) + " nm";

      var s = "";
      // grid
      [0, 0.25, 0.5, 0.75, 1].forEach(function(v){
        s += '<line x1="'+PAD.l+'" y1="'+Y(v)+'" x2="'+(W-PAD.r)+'" y2="'+Y(v)+
             '" stroke="#eee" stroke-width="1"/>' +
             '<text x="'+(PAD.l-8)+'" y="'+(Y(v)+4)+'" font-size="11" fill="#888" text-anchor="end">'+
             (v*100)+'</text>';
      });
      [0,100,200,300,400].forEach(function(z){
        s += '<text x="'+X(z)+'" y="'+(H-PAD.b+17)+'" font-size="11" fill="#888" text-anchor="middle">'+z+'</text>';
      });

      // the coverslip surface at z = 0
      s += '<rect x="'+(PAD.l-9)+'" y="'+PAD.t+'" width="9" height="'+(H-PAD.t-PAD.b)+
           '" fill="#dbe6ef" stroke="#9fb4c4" stroke-width="1"/>';

      // decay curve and filled area
      var path = "", area = "M " + X(0) + " " + Y(0) + " ";
      for (var k=0; k<=200; k++){
        var z = ZMAX*k/200, I = Math.exp(-z/d);
        path += (k? "L":"M") + X(z).toFixed(1) + " " + Y(I).toFixed(1) + " ";
        area += "L " + X(z).toFixed(1) + " " + Y(I).toFixed(1) + " ";
      }
      area += "L " + X(ZMAX) + " " + Y(0) + " Z";
      s += '<path d="'+area+'" fill="#e05020" fill-opacity="0.16"/>';
      s += '<path d="'+path+'" fill="none" stroke="#e05020" stroke-width="2.6"/>';

      // 1/e marker
      var ie = Math.exp(-1);
      s += '<line x1="'+PAD.l+'" y1="'+Y(ie)+'" x2="'+X(Math.min(d,ZMAX))+'" y2="'+Y(ie)+
           '" stroke="#666" stroke-width="1.2" stroke-dasharray="4 3"/>';
      if (d <= ZMAX){
        s += '<line x1="'+X(d)+'" y1="'+Y(ie)+'" x2="'+X(d)+'" y2="'+Y(0)+
             '" stroke="#666" stroke-width="1.2" stroke-dasharray="4 3"/>';
        s += '<circle cx="'+X(d)+'" cy="'+Y(ie)+'" r="5" fill="#e05020"/>';
        s += '<text x="'+(X(d)+8)+'" y="'+(Y(ie)-8)+'" font-size="12.5" fill="#e05020">d = '+
             d.toFixed(0)+' nm</text>';
      }

      // axes and labels
      s += '<line x1="'+PAD.l+'" y1="'+(H-PAD.b)+'" x2="'+(W-PAD.r)+'" y2="'+(H-PAD.b)+'" stroke="#999" stroke-width="1"/>';
      s += '<line x1="'+PAD.l+'" y1="'+PAD.t+'" x2="'+PAD.l+'" y2="'+(H-PAD.b)+'" stroke="#999" stroke-width="1"/>';
      s += '<text x="'+((PAD.l+W-PAD.r)/2)+'" y="'+(H-8)+'" font-size="12" fill="#555" text-anchor="middle">Distance from the coverslip, z [nm]</text>';
      s += '<text x="16" y="'+((PAD.t+H-PAD.b)/2)+'" font-size="12" fill="#555" text-anchor="middle" transform="rotate(-90 16 '+((PAD.t+H-PAD.b)/2)+')">Excitation intensity [%]</text>';

      // a cell sitting on the glass, shaded by how much it is excited
      var bx = W - PAD.r + 26;
      s += '<text x="'+(bx+22)+'" y="'+(PAD.t+12)+'" font-size="11.5" fill="#777" text-anchor="middle">what is lit</text>';
      s += '<rect x="'+(bx-8)+'" y="'+(H-PAD.b)+'" width="60" height="9" fill="#dbe6ef" stroke="#9fb4c4" stroke-width="1"/>';
      for (var j=0; j<9; j++){
        var zz = 18 + j*42;                       // nm above the glass
        var yy = H - PAD.b - 8 - (zz/ZMAX)*(H-PAD.t-PAD.b);
        var a = Math.exp(-zz/d);
        s += '<circle cx="'+(bx + 8 + (j%2)*26)+'" cy="'+yy.toFixed(1)+
             '" r="7" fill="rgb(13,140,38)" fill-opacity="'+(0.07+0.9*a).toFixed(3)+'"/>';
      }
      svg.innerHTML = s;

      out.innerHTML = "Penetration depth <b>d = " + d.toFixed(0) +
                      " nm</b>. A fluorophore that far from the glass is excited " +
                      "at 37% of the rate of one touching it.";
    }
    sA.addEventListener("input", update);
    sL.addEventListener("input", update);
    update();
  })();
  </script>
</div>
```

```{tip}
**Worked example.** Excitation at 488 nm, cover glass at $n_1$ = 1.518, buffer at $n_2$ = 1.33, angle of incidence 65°:

$$
d = \frac{488\ \text{nm}}{4\pi\sqrt{(1.518 \times 0.9063)^2 - 1.33^2}} = \frac{488}{4\pi \times 0.352} = 110\ \text{nm}
$$

Compare with the 850 nm confocal section from the previous subsection. TIRF is roughly eight times thinner, and it achieves this without discarding a single photon at a pinhole, because the out-of-focus fluorophores were never excited.
```

```{tip}
A fair objection, and one that is raised in every lecture on this topic: if all the energy is reflected, how can there be any intensity in the sample at all? And why should that intensity follow the _decay_ rather than the oscillation?

Take the second half first. The intensity is the time-averaged squared modulus of the field. Averaging over time removes the oscillation entirely, since a wave swinging between $-1$ and $+1$ has a mean square that does not depend on where you are along $x$. What is left is the only factor that varies with position without oscillating, which is $e^{-2\beta z}$. So the intensity is a function of depth alone: maximum at the interface, where $e^{0} = 1$, and falling from there.

Now the first half. There is genuinely energy in the sample, and there is genuinely no net energy flow into it. Both are true because the energy is in transit: it crosses the interface, spends a moment in a shell a hundred nanometres thick, and returns. Averaged over a cycle, nothing is lost. What the fluorophores do is intercept a little of that borrowed energy while it is passing through, which is also why TIRF illumination is not quite lossless in a real sample. The deeper reason there is any field at all is the continuity requirement we started from: an electric field cannot be finite on one side of a surface and exactly zero on the other, so it has to go to zero somehow, and the fastest way nature has of doing that is exponentially.
```

Note also what the exponential means for quantitative work. A fluorophore at 110 nm emits $1/e$, about 37%, of what an identical fluorophore emits at the glass surface. In a TIRF image, brightness is a proxy for axial position. This is a nuisance if you want to compare intensities between molecules, and a gift if you want to measure how far a vesicle is from the membrane, which is the basis of several elegant assays.

## Getting a steep enough angle

Making light arrive at the coverslip beyond 61° is not trivial. There are two ways.

**Prism-type TIRF** is the straightforward one: glue a prism to the slide, send the laser in through it, and collect the fluorescence with an ordinary objective from the other side. It gives a clean, uniform evanescent field and works with any objective. It also puts a prism where the condenser should be, restricts you to a sandwich geometry, and makes the sample very hard to access. It survives mostly in single-molecule biophysics.

**Objective-type TIRF** is what almost everyone uses, and it exploits the same conjugate-plane logic we met with the confocal pinhole. Recall that the back focal plane of an objective is a Fourier plane: a point there corresponds to a direction in the specimen. Focus the laser onto the centre of the back focal plane and it emerges as a collimated beam travelling straight up the axis, which is ordinary epi-illumination. Move that focused spot laterally and the emergent beam tilts. Move it far enough out towards the edge of the pupil and the beam strikes the coverslip beyond the critical angle, is totally reflected, and comes back down through the objective to reappear on the opposite side of the back focal plane (_{numref}`Fig. {number} <chap5_objective_tirf>`_).

```{figure} ../figures/chap5_objective_tirf.png
---
width: 100%
name: chap5_objective_tirf
align: center
---
Objective-type TIRF, drawn as a thin lens for clarity. (a) With the laser focused on the axis of the back focal plane, the beam emerges parallel to the optical axis and excites the full depth of the specimen. (b) Displacing the focus towards the edge of the pupil tilts the emergent beam past the critical angle. Nothing is transmitted, the beam returns through the objective on the opposite side of the pupil, and only the evanescent shell is excited. Turning one knob takes you from (a) to (b).
```

This puts a hard requirement on the objective. The angle it can deliver is limited by its numerical aperture through $\text{NA} = n_1\sin\theta$, and total internal reflection requires $n_1 \sin\theta > n_2$. Combining the two:

$$
\text{NA} > n_2
$$

The numerical aperture must exceed the refractive index of the *specimen*. For a cell at $n_2 \approx 1.38$, an NA 1.4 objective only just reaches the critical angle, which as we saw is exactly where the sectioning is worthless. You need headroom, and that is why dedicated TIRF objectives are sold at NA 1.45, 1.49 and occasionally 1.7. They are among the most expensive objectives in the catalogue, they demand a matched immersion oil and, at NA 1.7, special high-index cover glass.

```{tip}
Two failure modes account for most disappointing TIRF images.

The first is a **dirty or scratched coverslip**. The evanescent field samples 100 nm above the glass, so every speck of debris on it is imaged at full contrast. TIRF is the technique that punishes bad coverslip cleaning most severely.

The second is an angle that is **almost but not quite** critical. The resulting image looks like TIRF, is noticeably brighter than TIRF, and has a penetration depth of several hundred nanometres. If your background looks higher than it should, the angle is the first thing to check.
```

## What it is used for, and what it cannot do

TIRF is the natural tool for anything that happens at or near the plasma membrane on the coverslip side:

- **Vesicle fusion and exocytosis.** A vesicle approaching the membrane brightens as it enters the evanescent field, then flashes and disperses on fusion. The whole sequence is visible with a signal-to-background ratio that no other technique matches.
- **Single-molecule imaging.** With almost no out-of-focus background, individual fluorophores are readily detected. Most single-molecule fluorescence assays, including in vitro reconstitutions of motor proteins and microtubule dynamics, are done in TIRF.
- **Membrane organisation and dynamics.** Receptor clustering, diffusion measurements, and the assembly and turnover of focal adhesions.

Its limitations follow directly from the physics and are not negotiable:

- **Advantages**: excitation is confined to a single ~100 nm shell, so out-of-focus fluorescence is never generated; axial confinement roughly eight times better than confocal; the detector is a camera, so acquisition is as fast as widefield; photobleaching and phototoxicity are confined to the illuminated shell, leaving the rest of the cell untouched.
- **Drawbacks**: you can only image what is against the coverslip, so anything deeper is simply invisible; the high-NA objectives required are expensive and unforgiving about immersion media and coverslip thickness; the illumination field is often uneven, which complicates quantification; intensity and axial position are entangled.

That last set of drawbacks is really one drawback stated four times: TIRF is a surface technique. If your biology is 40 µm inside an embryo, none of this helps.

```{tip}
There is a useful halfway house. Set the angle just *below* critical and the beam is refracted rather than reflected, entering the specimen as a steeply inclined sheet a few micrometres thick. This is called **HILO** (highly inclined and laminated optical sheet) or oblique illumination, it reaches a few micrometres deep instead of 100 nm, and it is often the right compromise for imaging inside a cell rather than on its underside. Notice that it is already a light-sheet technique in disguise, which is where we go next.
```

