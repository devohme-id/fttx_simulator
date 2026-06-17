# FTTH Attenuation Simulator

An interactive, premium web-based simulator designed to model Fiber-to-the-Home (FTTH) network topologies and estimate optical propagation loss in real-time. Built entirely client-side with native web technologies (**HTML5, CSS3, and Vanilla JavaScript**), it provides telecommunication engineers, students, and network designers with a visual and educational environment to calculate optical link budgets and verify signal margins.

👉 **Live Demo:** [https://devohme-id.github.io/fttx_simulator/](https://devohme-id.github.io/fttx_simulator/)

---

## 🚀 Key Features

### 1. Interactive Workspace (Pan & Zoom)
* **Smooth Panning:** Click and drag the empty canvas grid space to navigate an infinite canvas.
* **Focal Zooming:** Zoom in and out (from 30% up to 200%) using your mouse scroll wheel or trackpad pinch-to-zoom. Perbesaran/perkecilan mengikuti koordinat kursor mouse Anda secara dinamis.
* **Grid Alignment:** Dot-grid background adapts to Light/Dark themes for comfortable editing.

### 2. Realistic Hardware Casings & Theme Sync
Every equipment card is custom-styled to mimic real-world hardware, adapting visual gradients according to the active theme:
* **OLT (Optical Line Terminal):** Styled as a dark brushed-metal 1U rackmount chassis with mounting ears, screws, and air vents.
* **SFP Module (Transceiver):** Zinc-alloy metallic silver transceiver casing with copper/gold contact fingers and colored latch levers. Designed to remain silver/white metallic across both Light and Dark themes to preserve its signature physical look.
* **ONT (Optical Network Terminal):** Residential desktop router housing with dual rear antennas (that rotate dynamically on hover) and top heat vents.
* **Splitter & ODP:** Transparent fiber cassette trays with internal fiber routing for Splitters, and gray double-lock cabinet boxes with hinges for ODPs.
* **Fiber Spool & Adapters:** Wooden flanges winding yellow fiber cable, and standard SC connectors.
* **Adaptive Sidebar:** Equipment palette cards in the sidebar dynamically match the active theme's background and border variables.

### 3. Active Status Indicators (Live LEDs)
Nodes feature live indicators that react to the simulation's current state:
* **OLT:** 
  * `ACT` (Activity) flashes green when there is an active downstream path connected.
* **ONT:**
  * `PWR` (Power) glows solid green.
  * `PON` (Passive Optical Network) glows green if the received power is good (>= -24 dBm) or yellow under warning/marginal signal conditions.
  * `LOS` (Loss of Signal) flashes red rapidly if the connection is cut or the signal drops below the sensitivity threshold (< -27 dBm).
  * `LAN` flashes green to simulate active local traffic when a path is functional.

### 4. Smart Visual Ports & SC Color-Coding
* **Square SC Adapters:** Connector sockets are designed as square flanges representing actual SC adapter sleeves.
* **Core Glowing:** Port cores emit a bright glowing teal/cyan dot when a cable is connected.
* **Adapter Classification:** Input ports use a blue flange representing **SC/UPC** (Ultra Physical Contact, flat polish), while output ports use a green flange representing **SC/APC** (Angled Physical Contact, 8° polish).

### 5. Floating Selected Actions Overlay
* **Prevent Name Truncation:** Contextual buttons (Info, Settings, Delete) are hidden by default to keep the card headers tidy and prevent equipment name labels (`eq-node-name`) from being cut off.
* **Spring Bounce Animation:** Click once on any node to select it, and a larger actions menu (24px buttons with 14px SVGs) slides up from the bottom of the card body with a spring scale-up bounce.

### 6. Attenuation Logic & Real-time Calculations
As you modify properties or connect lines, the simulation calculates path loss recursively from OLT to ONT:
* **Connection Path:** Uses smooth SVG Bezier curves showing signal flow animations. Curves turn Green (Good), Yellow (Warning), or Red (Critical) depending on local power level.
* **Short Connections:** Enhanced Bezier algorithms prevent overshooting or visual looping on closely positioned nodes.
* **Loss Sheet (Rincian Kalkulasi):** Clicking the Info (ℹ️) button on any node details the mathematical loss budget (cable attenuation, splitter ratios, connector/splicing insertion loss) step-by-step.
* **Landscape PDF Report:** Generates an A4 Landscape layout report compiling the network diagram, symbol legend, and a structured link budget table ready to print or save.

---

## 📐 Standard Loss & Calculation Parameters

The calculator evaluates propagation losses using standard international ITU-T G.984 (GPON), IEEE 802.3ah (EPON), and G.652 Single Mode Fiber values:

| Component | Parameter / Type | Standard Loss (dB) |
| :--- | :--- | :--- |
| **SM Fiber Cable (1490nm)** | Attenuation per km | `0.25 dB / km` |
| **SM Fiber Cable (1310nm)** | Attenuation per km | `0.35 dB / km` |
| **Splicing (Fusion Joint)** | Per point / las fiber | `0.10 dB` |
| **SC/APC Connector** | Angled Polish (Green) | `0.30 dB` |
| **SC/UPC Connector** | Flat Polish (Blue) | `0.50 dB` |
| **Adapter Connector Loss** | Air-gap connection | `0.20 dB` |
| **Passive Splitter 1:2** | Power Split Loss | `3.50 dB` |
| **Passive Splitter 1:4** | Power Split Loss | `7.00 dB` |
| **Passive Splitter 1:8** | Power Split Loss | `10.50 dB` |
| **Passive Splitter 1:16** | Power Split Loss | `14.00 dB` |
| **Passive Splitter 1:32** | Power Split Loss | `17.50 dB` |
| **Passive Splitter 1:64** | Power Split Loss | `21.00 dB` |

### ONT Sensitivity Signal Margins:
* **Good Signal (Hijau):** `Rx Power >= -24.00 dBm` (PON LED solid green, LAN flashing).
* **Warning / Marginal (Kuning):** `Rx Power between -24.01 dBm and -27.00 dBm` (PON LED solid yellow).
* **Critical / No Signal (Merah):** `Rx Power < -27.00 dBm` (LOS LED flashes red rapidly).

---

## ⌨️ Interactive Mouse & Keyboard Shortcuts

| Action | Control / Key | Description |
| :--- | :--- | :--- |
| **Add Equipment** | **Drag & Drop** | Drag a device card from the sidebar list and drop it on the canvas |
| **Move Equipment** | **Left-Click + Drag** | Drag cards around the canvas at any time |
| **Select Node** | **Single Click** | Highlights the node border and slides up the actions overlay panel |
| **Connect Cables** | **Click OUT → Click IN** | Click a green port (*OUT*), then click a yellow port (*IN*) to link them |
| **Configure Properties** | **Double-Click** / Click ⚙️ | Opens the configurations properties modal (or select node and click Gear) |
| **Delete Node** | **Delete / Backspace** | Press while a node is selected (or click 🗑️ in the floating actions overlay) |
| **Delete Connection** | **Double-Click** on line | Instantly disconnects the cable |
| **Delete Connection (Alt)**| **Click + Delete** | Click the line until it glows blue, then press Delete/Backspace |
| **Canvas Pan** | **Click & Hold empty canvas + Drag** | Move around the workspace canvas |
| **Canvas Zoom** | **Scroll Wheel / Pinch** | Zoom in/out focusing on the cursor coordinates |

---

## 📁 Project Structure

The project has a modular client-side layout:

```text
├── index.html            # Main markup page and modal layouts
├── css/
│   ├── index.css         # Design system tokens, variables, reset styles
│   ├── layout.css        # Core layout (Header, Sidebar, Workspace)
│   ├── sidebar.css       # Sidebar equipment palette styles
│   ├── canvas.css        # Equipment casing designs, LEDs, actions bar, ports
│   ├── tooltip.css       # Floating hover statistics tooltips
│   └── modal.css         # Glassmorphism overlay dialogs (Confirm, Settings, Loss Sheet)
└── js/
    ├── app.js            # Main orchestrator, modal controls, and active indicators
    ├── equipment-data.js # Source-of-truth default parameters and properties form fields
    ├── calculator.js     # Path attenuation propagation engine (recursive tree traversal)
    ├── canvas.js         # Canvas rendering, coordinate transformations, and selection
    ├── connections.js    # Bezier curve SVG connection drawing and flow line styling
    ├── drag-drop.js      # Pointer API drag and drop canvas handlers
    └── tooltip.js        # Attenuation estimations tooltip positioning
```

---

## 💻 Running Locally

Since the app has no compilation or compilation build steps, you can run it directly:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/devohme-id/fttx_simulator.git
   cd fttx_simulator
   ```
2. **Launch a local server:**
   You can open `index.html` directly in a browser, or run a quick local server:
   * **Node.js (npx):** `npx serve .`
   * **Python:** `python3 -m http.server 8080`
3. Open `http://localhost:8080` in your web browser.

---

## 📝 License

This project is open-source and available under the **MIT License**.
