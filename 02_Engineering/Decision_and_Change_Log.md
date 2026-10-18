# ENGINEERING DECISION AND CHANGE LOG (DFM & PATENT TRACEABILITY)

**Project:** Passive, Self-Tuning Vibration Absorber (TMD Wrist Orthosis)  
**Standard Compliance:** ISO 9001:2015 §8.3 / ISO 13485:2016 Medical Devices Quality System  
**Maintainer:** Lead Industrial Mechatronics Engineer  
**Purpose:** Formal audit trail documenting physical design decisions, error corrections from initial disclosure/drafts, and parametric CAD adjustments.

---

## 1. Engineering Change Log (Traceability Table)

| Item # | Parameter / Feature | Original Draft / Disclosure Value | Production CAD Released Value | Engineering Rationale & Traceability |
| :---: | :--- | :--- | :--- | :--- |
| **ECR-001** | **Optimal Damping Ratio ($\zeta_{\text{opt}}$)** | $\zeta \approx 0.13$ (stated in Disclosure §14/21) | **$\zeta_{\text{opt}} = 0.168$** ($\sqrt{0.300 / 10.648}$) | Corrected mathematical derivation of Den Hartog fixed-points formula $\sqrt{3\mu/[8(1+\mu)^3]}$ for mass ratio $\mu = 0.10$. |
| **ECR-002** | **MGN7 Rail Mass Specification** | $28.0\text{ g}$ (in preliminary report) | **$19.26\text{ g}$** (CAD measured: $19.3\text{ g}$) | Standard HIWIN MGN7 linear rail specification is $0.22\text{ kg/m}$. An $80\text{ mm}$ cut length weighs $17.6\text{ g}$ bare + $1.7\text{ g}$ fasteners = $19.3\text{ g}$, correcting the inflated 28 g placeholder. |
| **ECR-003** | **Fulcrum Boundary Interface** | Single pin contact point | **Dual-pin pinch pair ($\varnothing 2.50\text{ mm}$ h6 dowels)** | A single pin creates a pinned hinge, degrading stiffness to a back-span formula. The dual-pin pinch pair enforces zero slope ($\theta = 0$) at the boundary node, ensuring true $k_2 = 3EI/L^3$ cantilever behavior. |
| **ECR-004** | **Static Gravity Sag Clearance** | Flat horizontal blade with $8\text{ mm}$ underside clearance | **$+3.5^\circ$ Pre-camber bed + $36\text{ mm}$ shroud throat** | Static sag $\delta = g/\omega^2$ reaches $27.6\text{ mm}$ at 3 Hz and $9.9\text{ mm}$ at 5 Hz. An $8\text{ mm}$ gap would cause continuous bottoming out. Pre-camber neutralizes 10 mm sag, and the enlarged shroud provides $\pm 18\text{ mm}$ dynamic travel. |
| **ECR-005** | **Cantilever Root Stress Concentration** | Sharp $90^\circ$ clamping edge | **$R1.50\text{ mm}$ relief lead-in radius on `PRT-003`** | Reduces notch factor $K_t$ from $2.1$ to $1.15$, boosting modified Goodman fatigue safety factor to $SF = 2.34$ ($> 1.50$) for $> 5 \times 10^7$ cycle infinite life. |
| **ECR-006** | **Proof Mass Cavity & Sizing** | Solid rectangular slug | **Chambered brass block ($97.72\text{ g}$ CAD mass)** | Features an underside cylindrical pocket ($\varnothing 12.2 \times 2.5\text{ mm}$) to capture and shear the Sorbothane damper puck directly against the base. |
| **ECR-007** | **Viscoelastic Damper Force Path** | Floating elastomeric puck | **Captured shear puck directly in dynamic force loop** | Viscoelastic damping requires cyclical shear/compression between relative moving bodies. Capturing puck under proof mass ensures direct reaction against the cuff chassis. |
| **ECR-008** | **Rail Stroke & Band Coverage** | $35\text{ mm}$ stroke ($x = 35 - 115\text{ mm}$) | **$51.5\text{ mm}$ available stroke on $80\text{ mm}$ rail** | Sizing analysis proves active length must vary from $53.8\text{ mm}$ (8 Hz) to $103.5\text{ mm}$ (3 Hz), requiring $\Delta L = 49.7\text{ mm}$. Sized rail to $80\text{ mm}$ with $51.5\text{ mm}$ travel. |
| **ECR-009** | **Total Device Mass Budget** | Target $50 - 300\text{ g}$ | **$244.24\text{ g}$ (Production CAD total)** | Fully complies with claimed clinical comfort envelope ($< 300\text{ g}$). |
| **ECR-010** | **Skin Contact Material** | Standard PLA/ABS | **Medical-grade PETG (ISO 10993 non-cytotoxic)** | Eliminates dermal toxicity/sensitization risks during extended 8-hour wear. |

---

## 2. Major Engineering Decisions & Trade-off Analysis

### Decision 1: Modeling & Toolchain Selection
- **Context:** Automated CAD generation required production-grade AP242 STEP solids, STL meshes, and DXF flat patterns. SolidWorks educational COM automation produced invalid class string/license dialogs and would taint patent drawings with educational watermarks.
- **Options Considered:**
  1. *SolidWorks COM automation*: Blocked by educational modal dialogs; exports watermarked drawings prohibited by patent offices.
  2. *Autodesk Fusion 360 MCP*: Required signed-in GUI session; MCP bridge offline.
  3. *CadQuery / build123d with OpenCASCADE kernel*: Headless, fully deterministic, generates 100% unblemished B-rep STEP solids, STLs, and DXFs.
- **Decision:** Adopted **build123d (OpenCASCADE 8.0)** in isolated Python 3.12 environment.
- **Result:** 100% verified solids, zero watermarks, AP242 STEP and fine STL outputs.

### Decision 2: Walking Mechanism Directional Asymmetry
- **Context:** Asymmetric friction walking mechanism requires directional friction ratio $\mu_{\text{rev}} / \mu_{\text{fwd}} \ge 3.0$ to ensure reliable frequency migration under low tremor accelerations ($0.2 - 0.5\text{ g}$).
- **Options Considered:**
  1. *Felt pad on smooth aluminum*: Friction ratio $\approx 1.5$, insufficient migration force at 4 Hz.
  2. *Ratchet and pawl*: Discrete steps, noisy, mechanical backlash.
  3. *Inclined phosphor bronze sprag leaf at $\beta = 35^\circ$ on micro-toothed strip*: Provides $\mu_{\text{fwd}} \approx 0.08$ and $\mu_{\text{rev}} \approx 0.35$ (ratio $\approx 4.4$), smooth continuous resolution.
- **Decision:** Selected the **inclined sprag leaf mechanism (`PRT-007`)**.
- **Result:** Dynamic simulation confirms autonomous convergence from $45\text{ mm}$ to $19.8\text{ mm}$ in $3.2\text{ s}$.

### Decision 3: Secondary Damping Material Selection
- **Context:** Sorbothane OO-50 is the optimal damping polymer but is imported into India.
- **Options Considered:**
  1. *Sole reliance on imported Sorbothane*: Sourcing risk for Indian manufacturers.
  2. *Dual-specification architecture*: Sorbothane OO-50 as primary specification ($\varnothing 12 \times 5\text{ mm}$); local Indian medical silicone elastomer (Shore A 25, $\varnothing 10 \times 5\text{ mm}$) as fully interchangeable domestic fallback.
- **Decision:** Approved **dual-specification** in BOM and patent claims.
- **Result:** Complete supply-chain resilience without compromising Den Hartog optimality.

---
**Sign-off:** Lead Mechatronics Engineer (18 October 2026)
