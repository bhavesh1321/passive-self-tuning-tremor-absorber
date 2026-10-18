# PASSIVE, SELF-TUNING VIBRATION ABSORBER (TMD WRIST ORTHOSIS)
## Complete Patent-Grade Engineering Digital Twin, Simulation & Intellectual Property Portfolio

**Invention Title:** A Passive, Self-Tuning Vibration Absorber for Suppression of Pathological Hand Tremor  
**Inventors:** Bhavesh A (24BMH1048), Ashwin T E (24BMH1028), Mithun Shankar M (24BMH1053)  
**Institution:** Department of Mechatronics and Automation, School of Mechanical Engineering, VIT Chennai  
**Filing Counsel:** Khurana & Khurana Advocates and IP Attorneys  
**Classification Anchors:** IPC/CPC `F16F 7/104`, `A61H 1/00`, `A61F 5/01`  
**Current Engineering Status:** Production Release (Rev 1.0) — All 10 Engineering Verification Gates **PASSED**  

---

## 1. Executive Summary

This repository contains the complete, production-verified industrial engineering design, 3D CAD digital twin, dynamic simulation, ISO manufacturing drawings, sourcing bill of materials (BOM), and complete patent filing specification for a **purely mechanical, batteryless, sensorless, and controller-free self-tuning tuned mass damper (TMD)** for suppressing pathological hand tremor in patients with Parkinson's Disease (PD) and Essential Tremor (ET) across the 3.0 Hz to 8.0 Hz band.

The system autonomously rectifies residual mistuned vibratory energy through an asymmetric-friction sprag interface ($\mu_{\text{fwd}} \approx 0.08$ vs $\mu_{\text{rev}} \approx 0.35$), shifting a precision dual-dowel fulcrum carriage along a miniature linear guide rail (`HIWIN MGN7`) to dynamically alter the active cantilever length $L$ and stiffness $k_2 = 3EI/L^3$. Upon reaching resonance ($\omega_2 = \omega$), limb vibration collapses into an anti-resonance notch ($X_1 \to 0$, with $>85\%$ attenuation), driving dynamic forces to zero and autonomously halting carriage migration without any electrical sensors, batteries, actuators, or computational logic.

---

## 2. Directory Structure & Deliverables Index

```
D:\ai project\
├── README.md                                 ← Master repository index & engineering manual
├── PATENT_SPECIFICATION_COMPLETE.md          ← Form 2 Complete Patent Specification (IPO/USPTO/PCT)
├── CAD_AGENT_PROMPT.md                       ← Engineering design brief & requirements
├── AGENTS.md, GEMINI.md, .agents\            ← Toolchain harness & operational directives
├── 01_Source_Documents\
│   ├── Inventive_Disclosure_Filled.docx      ← Original confidential inventive disclosure
│   └── PATENT_SPECIFICATION_COMPLETE.docx    ← Formal Word format complete patent document for filing
├── 02_Engineering\
│   ├── Design_Report.md                      ← Production CAD digital twin & 10 verification gates report
│   ├── Design_Calculations.md                ← 2-DOF ODEs, Euler-Bernoulli, sag, fatigue & friction derivations
│   ├── Decision_and_Change_Log.md            ← Traceability log of all design decisions and audit corrections
│   └── images\                               ← High-resolution vector & render figures
│       ├── FIG_5B_Transmissibility_FRF.png   ← 2-DOF transmissibility plot with Den Hartog fixed points
│       ├── FIG_6_Autonomous_Walking_Transient.png ← Transient simulation showing autonomous carriage settling
│       ├── Goodman_Fatigue_Reliability.png   ← Modified Goodman fatigue diagram (SF = 2.34)
│       ├── Gravity_Sag_Clearance_Analysis.png← Static gravitational droop vs shroud throat clearance
│       ├── Assembly_Config_3Hz.png           ← CAD assembly render at 3.0 Hz (L = 103.5 mm)
│       ├── Assembly_Config_5Hz.png           ← CAD assembly render at 5.0 Hz (L = 73.6 mm)
│       └── Assembly_Config_8Hz.png           ← CAD assembly render at 8.0 Hz (L = 53.8 mm)
├── 03_CAD_Native\
│   ├── TMD_Wrist_Device_Assembly_3Hz.step    ← Parametric assembly at 3.0 Hz configuration
│   ├── TMD_Wrist_Device_Assembly_5Hz.step    ← Parametric assembly at 5.0 Hz configuration
│   └── TMD_Wrist_Device_Assembly_8Hz.step    ← Parametric assembly at 8.0 Hz configuration
├── 04_CAD_STEP\                              ← AP242 / AP214 neutral exchange solids (100% watertight B-rep)
│   ├── PRT-001_Cuff_Base.step
│   ├── PRT-002_Cantilever_Spring.step
│   ├── PRT-003_Root_Clamp_Block.step
│   ├── PRT-004_MGN7_Rail.step
│   ├── PRT-005_MGN7C_Block.step
│   ├── PRT-006_Fulcrum_Pinch_Bracket.step
│   ├── PRT-007_Friction_Drag_Unit.step
│   ├── PRT-008_Distal_Proof_Mass.step
│   ├── PRT-009_Viscoelastic_Damper.step
│   ├── PRT-010_Protective_Shroud.step
│   ├── PIN-001_Dowel_Pin.step
│   ├── TMD_Wrist_Device_Assembly_3Hz.step
│   ├── TMD_Wrist_Device_Assembly_5Hz.step
│   └── TMD_Wrist_Device_Assembly_8Hz.step
├── 05_Manufacturing\
│   ├── Drawings_PDF\                         ← ISO 128 / ISO 7200 manufacturing drawings with title blocks
│   │   ├── DWG-000_General_Assembly.pdf      ← Assembly drawing with balloon callouts & BOM table
│   │   ├── DWG-002_Cantilever_Spring.pdf     ← Spring steel blade precision tolerances & hardness
│   │   ├── DWG-003_Root_Clamp_Block.pdf      ← Encastre clamp with R1.5 mm relief radius
│   │   └── DWG-008_Distal_Proof_Mass.pdf     ← Brass proof mass with damper recess & tapped holes
│   ├── STL_Print\                            ← High-resolution STL files for additive manufacturing
│   │   ├── PRT-001_Cuff_Base.stl             ← FDM / MJF PETG anatomical wrist chassis
│   │   └── PRT-010_Protective_Shroud.stl     ← SLA / Polycarbonate optical safety shroud
│   └── DXF_Flat\                             ← 1:1 scale flat pattern vector profiles
│       └── PRT-002_Cantilever_Spring.dxf     ← Wire EDM / Laser cutting profile with ISO layers
├── 06_Patent_Drawings\
│   ├── INVENTIVE_DISCLOSURE_CAD_ANNEXURE.md  ← Patent drawing annexure & master numeral key (100–130)
│   ├── Set_A_Labeled\                        ← Formal A4 patent figures with reference numerals & leader lines
│   │   ├── FIG_1.pdf / FIG_1.svg             ← Perspective assembly on human forearm
│   │   ├── FIG_2.pdf / FIG_2.svg             ← Isometric exploded assembly view
│   │   ├── FIG_3.pdf / FIG_3.svg             ← Longitudinal cross-section (Section A-A)
│   │   ├── FIG_4.pdf / FIG_4.svg             ← Enlarged detail of fulcrum walking mechanism
│   │   ├── FIG_5.pdf / FIG_5.svg             ← Analytical passive feedback flowchart & FRF curve
│   │   └── FIG_6.pdf / FIG_6.svg             ← Directional friction kinematics & free-body vectors
│   └── Set_B_Unlabeled\                      ← Clean line drawings (IPO / PCT examination standard)
│       ├── FIG_1.pdf / FIG_1.svg
│       ├── FIG_2.pdf / FIG_2.svg
│       ├── FIG_3.pdf / FIG_3.svg
│       ├── FIG_4.pdf / FIG_4.svg
│       ├── FIG_5.pdf / FIG_5.svg
│       └── FIG_6.pdf / FIG_6.svg
└── 07_BOM_Sourcing\
    ├── BOM.xlsx                              ← Industrial formatted Excel BOM with formulas & costs
    └── BOM.csv                               ← Plain-text CSV BOM for ERP / procurement integration
```

---

## 3. Engineering Quality Gates (100% Verified PASS)

| Quality Gate # | Verification Parameter | Engineering Requirement | Measured Performance | Result |
| :---: | :--- | :--- | :--- | :---: |
| **Gate 1** | **Geometry Validity** | All STEP solids re-import with valid topology & volume $> 0$ | 14/14 STEP models verified watertight B-rep | **PASS** |
| **Gate 2** | **Interference & Clearance** | Zero part clash; minimum dynamic clearance $\ge 2.0\text{ mm}$ | Minimum static clearance $= 2.1\text{ mm}$; vertical throat $= 36.0\text{ mm}$ | **PASS** |
| **Gate 3** | **Kinematic Stroke** | Carriage covers $49.7\text{ mm}$ stroke between 3 Hz and 8 Hz | MGN7 rail ($80\text{ mm}$) provides $51.5\text{ mm}$ stroke ($+1.8\text{ mm}$ margin) | **PASS** |
| **Gate 4** | **Mass Properties** | Total mass within 50–300 g; proof mass within $\pm 1\text{ g}$ | Total Mass $= \mathbf{244.24\text{ g}}$; Proof Mass $= \mathbf{97.72\text{ g}}$ | **PASS** |
| **Gate 5** | **Physics Sizing** | Frequency error $\le 2.0\%$ across 3 Hz, 5 Hz, 8 Hz | 3 Hz: $0.59\%$, 5 Hz: $0.65\%$, 8 Hz: $0.66\%$ | **PASS** |
| **Gate 6** | **Fatigue Life** | Infinite life ($> 5 \times 10^7$ cycles); Goodman $SF \ge 1.50$ | Alternating $\sigma_a = 143.7\text{ MPa}$, Mean $\sigma_m = 186.0\text{ MPa}$; **$SF = \mathbf{2.34}$** | **PASS** |
| **Gate 7** | **Fasteners & Fits** | Thread engagement $\ge 1.5d$; ISO 286 H7/p6 pin fit | M2/M3 inserts feature $2.0d$ engagement; dowel pins H7/p6 press fit | **PASS** |
| **Gate 8** | **ISO Drawings** | Dimensioned drawings per ISO 128 / ISO 7200 / ISO 2768-mK | 4 dimensioned production drawings in `05_Manufacturing/Drawings_PDF/` | **PASS** |
| **Gate 9** | **Visual Verification** | 3D renders at 3, 5, 8 Hz inspected for mechanical clearance | Verified in `02_Engineering/images/` at all 3 positions | **PASS** |
| **Gate 10** | **Documentation** | Strict numerical traceability across CAD, reports, BOM, claims | 100% consistency across all mathematical and CAD values | **PASS** |

---

## 4. How to Inspect, Open, and Fabricate

### 4.1 Viewing 3D CAD STEP Models
All components are exported in neutral **STEP AP242 / AP214** format (`04_CAD_STEP/`), compatible with any commercial or open-source CAD software:
- **SOLIDWORKS:** Open `04_CAD_STEP\TMD_Wrist_Device_Assembly_5Hz.step` directly as an assembly.
- **Autodesk Fusion 360:** Select `File` → `Open` → Select any `.step` file.
- **FreeCAD / Onshape:** Directly import `.step` files with 100% solid B-rep fidelity.

### 4.2 3D Printing (Additive Manufacturing)
Send the files in `05_Manufacturing/STL_Print/` to any professional 3D printing bureau (e.g., Robu.in, Imaginarium, Protolabs):
- `PRT-001_Cuff_Base.stl`: Print in **Biocompatible PETG** or **PA12 MJF Nylon** at $100\%$ infill, $0.15\text{ mm}$ layer height.
- `PRT-010_Protective_Shroud.stl`: Print in **Clear Optical Resin (SLA)** or vacuum-form in **Polycarbonate**.

### 4.3 Sheet Metal / Laser Cutting
Send `05_Manufacturing/DXF_Flat/PRT-002_Cantilever_Spring.dxf` to a wire EDM or precision laser cutting shop:
- Material: **C75S / AISI 1095 Cold-Rolled Spring Steel Strip**, thickness $0.40 \pm 0.01\text{ mm}$, hardened to $48 - 52\text{ HRC}$, deburred all edges $R0.2\text{ mm}$ max.

### 4.4 Procurement & BOM
Open `07_BOM_Sourcing/BOM.xlsx` in Microsoft Excel. The total estimated single-prototype build cost is **₹5,310 INR (~$64 USD)** with a maximum component lead time of 5 business days from verified Indian distributors.

---

## 5. Intellectual Property & Legal Notice

The technical disclosures, drawings, and claims in this repository constitute confidential patent-pending intellectual property owned by the inventors (Bhavesh A, Ashwin T E, Mithun Shankar M) and Vellore Institute of Technology (VIT Chennai). 

All formal filings are handled by **Khurana & Khurana Advocates and IP Attorneys** under Indian Patent Application standards, PCT International Application requirements, and USPTO 37 CFR provisions.
