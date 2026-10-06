# ⚫ Gargantua — Kerr Black Hole Simulation

Real-time relativistic visualization of a rotating **Kerr black hole** with a volumetric accretion disk, ray-marched entirely on the GPU.

**[▶ Live demo](https://YOUR-USERNAME.github.io/gargantua/)**

![Preview](preview.png)

---

## ✨ Features

- **True Kerr metric** — event horizon, ISCO, photon sphere
- **RK4 photon geodesics** — 4th-order Runge-Kutta integration of `d²u/dφ² = 1.5·Rs·u² − u`
- **Volumetric accretion disk** — Shakura–Sunyaev temperature profile
- **Relativistic Doppler beaming** + gravitational redshift (`I_obs = g³·μ_e·I_emit`)
- **Planck-color emission** — physical black-body colors from Tanner Helland approximation
- **Photon ring** — thin bright circle on the shadow's edge, asymmetric from spin
- **Relativistic jets** with magnetic spiral structure
- **Procedural starfield** with gravitational lensing
- **ACES filmic tonemapping** + UnrealBloom + chromatic aberration
- **Live controls** — spin, speed, brightness, exposure, lensing, tilt, Doppler, swirl, jets, density, quality, waves, shadow, ring
- **5 presets** — Cinema, Science, Kerr, EHT, Performance
- **URL parameters** for sharing views: `?spin=0.998&tilt=0.3&shadow=1.2`
- **LocalStorage** — your settings persist between sessions
- **Screenshot** with a single key (`S`)
- **Fully mobile-adaptive** — works on phones, tablets, and desktops

---

## 🚀 Quick Start

### Option 1 — Open directly

Download `index.html` and open it in a modern browser (Chrome, Firefox, Edge, Safari). Internet connection is required — Three.js is loaded from a CDN.

### Option 2 — GitHub Pages

1. Fork or clone this repository.
2. Go to **Settings → Pages**.
3. Under "Source", select **Deploy from a branch** → `main` / `root`.
4. Save. Your site will be live at `https://YOUR-USERNAME.github.io/gargantua/`.

### Option 3 — Local server

```bash
python -m http.server 8000
# or
npx serve
```

Then open `http://localhost:8000`.

---

## ⌨ Controls

| Action | Input |
|---|---|
| Rotate camera | Drag (mouse or finger) |
| Zoom | Scroll or pinch |
| Pause / resume | `Space` |
| Reset camera | `R` |
| Hide UI | `H` |
| Screenshot (PNG) | `S` |
| Info panel | `i` button or `?` |

---

## 🎛 Parameters

| Slider | Range | Description |
|---|---|---|
| **Spin a\*** | 0 – 0.998 | Black hole angular momentum (0 = Schwarzschild) |
| **Speed** | 0 – 5 | Time-scale of disk rotation |
| **Brightness** | 0.2 – 2.5 | Disk emission brightness |
| **Exposure** | 0.4 – 2.2 | HDR exposure before ACES tonemap |
| **Lensing** | 0 – 2.5 | Gravitational deflection strength |
| **Tilt** | −1.2 – 1.2 | Observation angle above disk plane |
| **Doppler** | 0 – 2.5 | Relativistic beaming intensity |
| **Swirl** | 0 – 3 | Differential rotation speed |
| **Jets** | 0 – 2 | Relativistic jet power |
| **Density** | 0.3 – 3.0 | Disk volumetric density |
| **Quality** | 0.4 – 1.6 | Ray-marching steps + AA |
| **Waves** | 0 – 2 | Gravitational-wave ripple in lensing |
| **Shadow** | 0 – 2 | Shadow darkness |
| **Ring** | 0 – 2 | Photon ring brightness |

---

## 🔬 Physics Reference

### Kerr Metric — Key Radii

**Event horizon:**
```
r₊ = 1 + √(1 − a*²)
```

**ISCO** (Bardeen–Press–Teukolsky):
```
Z₁ = 1 + (1−a²)^(1/3) · [(1+a)^(1/3) + (1−a)^(1/3)]
Z₂ = √(3a² + Z₁²)
r_ISCO = 3 + Z₂ − √((3−Z₁)(3+Z₁+2Z₂))
```

**Photon sphere** (approximate): `r_ph ≈ 1.5 − 0.25·a*`

### Photon Geodesics

Equation of motion in the orbital plane:

```
d²u/dφ² = (3/2)·Rs·u² − u,   u = 1/r
```

Integrated with RK4:

```
u_{n+1} = u_n + (h/6)·(k₁ᵤ + 2k₂ᵤ + 2k₃ᵤ + k₄ᵤ)
```

### Shakura–Sunyaev Temperature Profile

```
T(r) ∝ r^(−3/4) · (1 − √(r_in/r))^(1/4)
```

### Relativistic Doppler + Redshift

```
D = 1 / [γ·(1 − β·cos θ)]      (Doppler factor)
g_grav = √(1 − Rs/r)            (gravitational redshift)
g = D · g_grav                  (combined)
I_obs = g³ · μ_e · I_emit       (observed intensity)
```

### Planck Color

Observed black-body temperature `T_obs = T_emit · g`, converted to RGB via Tanner Helland's piecewise approximation of Planck's law.

---

## 🏗 Technical Stack

- **[Three.js](https://threejs.org/)** r160 — WebGL rendering
- **Custom GLSL shaders** — full-screen ray-marching with geodesic integration
- **[UnrealBloomPass](https://threejs.org/docs/#examples/en/postprocessing/UnrealBloomPass)** — bloom post-processing
- **ACES filmic tonemapping** — cinematic dynamic range
- Vanilla JS, no build step, no dependencies beyond Three.js

---

## 📱 Mobile Support

The interface automatically adapts to small screens:

- Compact top bar on phones
- Sliders shrink and stack vertically
- Info panel becomes scrollable fullscreen
- Touch controls: drag to rotate, pinch to zoom
- Landscape mode has special layout

---

## 📄 License

MIT — see [LICENSE](LICENSE).

---

## 🙏 Credits

- Physics: Kerr (1963), Bardeen–Press–Teukolsky (1972), Shakura–Sunyaev (1973)
- Planck color approximation: Tanner Helland
- Inspired by *Interstellar*'s Gargantua (Kip Thorne / Double Negative)
- Reference: Event Horizon Telescope observations of M87* and Sgr A*
