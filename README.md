# 🌬️ Wind Tunnel Simulator — Vehicle + Forces

An interactive, browser-based 2D wind tunnel simulation built with vanilla HTML5 Canvas and JavaScript. Visualize airflow around aerodynamic bodies in real time, complete with empirical drag/lift force calculations and pressure coefficient mapping.

> **Educational tool** — uses inviscid potential flow visuals with empirical Cd/Cl models.

---

## ✨ Features

- **Real-time streamline visualization** — hundreds of animated particle traces render live airflow around the body
- **Three body types** — Sphere/Cylinder, Race Car, and Bus, each with its own geometry and aerodynamic model
- **Physics-accurate force readouts** — drag (D), lift (L), dynamic pressure (q), and non-dimensional coefficients Cd and Cl updated live
- **Circulation control (Γ)** — add a vortex to induce lift via the Kutta–Joukowski theorem
- **Pressure coefficient (Cp) heatmap** — toggle a colour overlay showing high/low pressure regions across the flow field
- **Velocity vector field** — overlay arrows showing local flow direction and speed at a grid of points
- **Interactive flow probe** — hover anywhere on the canvas to read local |V|, Cp, and flow angle θ
- **Best-efficiency sweep** — automatically scans U ∈ [0.2, 3.0] m/s and reports the speed U\* that minimises Cd
- **Fully responsive** — canvas resizes to fill the viewport on any screen

---

## 🖥️ Demo

Open `index.html` directly in any modern browser — no build step, no dependencies, no server required.

```bash
# Clone and open
git clone https://github.com/eashankgiriTL/PhysProject_WindTunnelSim.git
cd PhysProject_WindTunnelSim
open index.html   # macOS
# or just double-click index.html on Windows/Linux
```

---

## 🔧 Controls

### Flow & Geometry

| Control | Range | Description |
|---|---|---|
| **Free-stream speed U** | 0.20 – 3.00 m/s | Upstream airflow velocity |
| **Circulation Γ** | −1500 – 1500 px²/s | Vortex strength; generates lift via Kutta–Joukowski |
| **Body type** | Cylinder / Race Car / Bus | Shape of the aerodynamic body |
| **Body scale** | 0.6× – 1.8× | Scales the body size relative to the reference radius |
| **Reference radius / chord** | 24 – 140 px | Sets the characteristic length (1 px ≈ 1 cm) |

### Visualization

| Control | Description |
|---|---|
| **Seed rows** | Number of particle rows seeded upstream |
| **Trail fade (damping)** | How quickly old trails fade; lower = longer streaks |
| **Velocity pixel scale** | Scales how fast particles move on screen |
| **Show Cp heatmap** | Overlays a red-blue pressure coefficient map |
| **Show velocity vectors** | Overlays a green vector field grid |

### Playback

- **Reset seeds** — re-seeds all particles from scratch
- **Pause / Resume** — freezes or continues the animation

---

## 📐 Physics & Modelling

### Velocity Fields

- **Cylinder** — exact 2D potential flow solution (uniform flow + doublet + free vortex):

$$V_r = U\left(1 - \frac{a^2}{r^2}\right)\cos\theta, \quad V_\theta = -U\left(1 + \frac{a^2}{r^2}\right)\sin\theta + \frac{\Gamma}{2\pi r}$$

- **Race Car / Bus** — free stream + point vortex at centroid + normal-direction repulsion from the polygon boundary, producing realistic streamline wrapping

### Aerodynamic Coefficients

| Body | Cd model | Cl model |
|---|---|---|
| **Cylinder** | Empirical Re-based: Stokes (Re < 1), transitional, subcritical bluff (Cd ≈ 1.2), drag crisis (Re > 2×10⁵) | Kutta–Joukowski: CL = 2Γ / (U·c) |
| **Bus** | Bluff-body fit: ~0.8 with mild log Re trend | Kutta–Joukowski |
| **Race Car** | Polar drag: CD = CD0 + k·CL² (CD0 = 0.32, k = 0.07) | Kutta–Joukowski |

### Reference Values

```
ρ = 1.225 kg/m³   (ISA sea-level air density)
μ = 1.81 × 10⁻⁵ Pa·s   (dynamic viscosity)
1 px ≈ 1 cm   (spatial scale)
```

Forces are reported **per metre of span** (2D assumption).

---

## 🗂️ Project Structure

```
index.html          # Entire simulation — self-contained single file
README.md
```

---

## 🚀 Possible Extensions

- Add an airfoil (NACA profile) body type with angle-of-attack control
- Export force vs. speed sweep as a CSV
- Add a Reynolds number display and laminar/turbulent boundary annotation
- Implement proper panel-method or vortex-panel aerodynamics for the polygon bodies
- Mobile touch support for the flow probe

---

## 📄 License

MIT — free to use, modify, and distribute for educational or personal projects.

---

*Built as a physics project by [Eashan K Giri](https://github.com/eashankgiriTL).*
