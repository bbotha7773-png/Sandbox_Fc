# FC Tactical Broadcast Sandbox — Unified CV Workspace

A high-performance, lightweight, zero-dependency tactical tracking simulation playground. This environment projects a 2D football pitch matrix into a 3D perspective-corrected space using a custom HTML5 Canvas engine. It is engineered to simulate clean broadcast feeds for downstream computer vision (CV) automation, coordinate projection, and target-tracking pipelines.

---

## 🛠️ Core Architecture & Mechanics

### 1. 3D Perspective Projection Engine
The field renders using a manual camera transformation matrix (`CAMERA`) that calculates spatial depth without relying on heavy external WebGL frameworks. 
* **Dynamic FOV Matrix:** Real-time adjustments change pixel-to-meter scaling factors on the fly.
* **Camera Tracking:** The virtual camera automatically tracks the ball's $X$-axis velocity vector with smooth interpolation, mimicking standard broadcast tracking cameras.

### 2. Inverse Spatial Coordinates Matrix
Every entity on the pitch has its physical world coordinates ($X, Z$ in pixels) mapped directly to a real-time ground truth coordinate system:
* **Macro Sectors:** Divides the pitch into an $18 \times 6$ high-contrast operational layout (e.g., sector `A1` to `R6`).
* **Sub-Cell Precision:** Translates localized pixel bounds into discrete $(X, Y)$ micro-matrix cells.
* **Metric Registration:** Computes precise player positions relative to the center circle in standard metric meters ($105\text{m} \times 68\text{m}$ scale).

### 3. Absolute Clean Mode (Pristine Frame Capture)
Designed specifically for automated image processing, shape contour detection, and color segmentation pipelines. Any UI elements or text layouts will contaminate contour generation.
* **UI Isolation:** Double-tapping or double-touching the canvas instantly purges the menu buttons, sidebar controllers, and telemetry registers from the DOM (`opacity: 0`).
* **Artifact-Free Execution:** Downstream automation scripts can capture raw, pixel-perfect frames of the field and player objects without any UI pollution.

---

## 🎛️ Control System & Shortcuts

* **Toggle Engineering Sidebar:** Tap the floating `MENU / CLOSE` button to hide or reveal the configuration panel.
* **Toggle Pristine Capture Mode:** Double-click (desktop) or double-tap (mobile device/automation layer) anywhere inside the main canvas field to completely vanish the user interface. Double-tap again to restore the dashboard workspace.
* **Live Parameters Matrix:**
  * **Transmission Speed:** Adjusts ball transfer velocity across vectors.
  * **Decision Latency:** Injects customized frame-delay thresholds into the AI decision loop before passing.
  * **Projection FOV:** Modifies focal length to test CV threshold boundaries under varying perspective compressions.
  * **Profile Shifts:** Instantly swap team color hex profiles to test tracking robustness against dynamic lighting or jersey alterations.

---

## 🚀 Quick Start via Termux

To host and test this engine locally directly on your device:

1. **Fire up the lightweight web server:**
   ```bash
   python -m http.server 8080
