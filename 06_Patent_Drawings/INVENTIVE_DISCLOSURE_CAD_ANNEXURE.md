# ANNEXURE TO INVENTIVE DISCLOSURE: CAD DRAWINGS & DESCRIPTIONS
**For Complete Patent Application with Khurana & Khurana Advocates and IP Attorneys**

**Invention Title:** A Passive, Self-Tuning Vibration Absorber for Suppression of Pathological Hand Tremor  
**Inventors:** Bhavesh A, Ashwin T E, Mithun Shankar M  
**Institution:** Department of Mechatronics and Automation, School of Mechanical Engineering, VIT Chennai  
**Filing Format Compliance:** Indian Patents Rules 2003 (Rule 15 / Third Schedule), PCT Rule 11, USPTO 37 CFR §1.84  

---

## 12. Final CAD Images / Line Diagrams (Section 12 Response)

The formal patent drawings are provided in two complete, watermark-free vector sets conforming to Rule 15 of the Indian Patents Rules (A4 portrait format, 40 mm top/left margins, 30 mm right/bottom margins, uniform black line weights, numerals $\ge 3.2\text{ mm}$ with leader lines, "Sheet n of N" headers):
- **Set A (Fully Labeled):** Includes formal reference numerals (100–130) and thin leader lines. Located in:
  `06_Patent_Drawings/Set_A_Labeled/`
- **Set B (Unlabeled Line Diagrams):** Identical view geometry with reference numerals omitted for patent office examination standard. Located in:
  `06_Patent_Drawings/Set_B_Unlabeled/`

Both sets are available in vector PDF and SVG formats:

| Figure # | View Description & Mechanical Focus | Set A (Labeled) File | Set B (Unlabeled) File |
| :---: | :--- | :--- | :--- |
| **FIG. 1** | **Perspective Dorsal Assembly View** showing the TMD wrist device worn on the dorsal aspect of a human forearm, depicting cuff base, straps, rail, carriage, blade, proof mass, and shroud. | `FIG_1.pdf`<br>`FIG_1.svg` | `FIG_1.pdf`<br>`FIG_1.svg` |
| **FIG. 2** | **Isometric Exploded Assembly View** illustrating all ten discrete sub-assemblies and fasteners aligned along vertical assembly axes. | `FIG_2.pdf`<br>`FIG_2.svg` | `FIG_2.pdf`<br>`FIG_2.svg` |
| **FIG. 3** | **Longitudinal Centerline Cross-Section (Section A-A)** detailing the active vibrating cantilever length $L(s)$, carriage raceways, throat clearance, and damper pocket. | `FIG_3.pdf`<br>`FIG_3.svg` | `FIG_3.pdf`<br>`FIG_3.svg` |
| **FIG. 4** | **Enlarged Detail View of Walking Fulcrum Interface** showing upper/lower precision dowel pins pinching the spring blade and the inclined sprag drag unit engaging the friction strip. | `FIG_4.pdf`<br>`FIG_4.svg` | `FIG_4.pdf`<br>`FIG_4.svg` |
| **FIG. 5** | **Dual Analytical Representation:** (Left) Autonomous 5-stage mechanical closed-loop feedback flowchart; (Right) 2-DOF Transmissibility / FRF curve showing anti-resonance notch. | `FIG_5.pdf`<br>`FIG_5.svg` | `FIG_5.pdf`<br>`FIG_5.svg` |
| **FIG. 6** | **Directional Friction Free-Body Kinematics & Force Rectification** depicting normal load fluctuation $N(t)$, dynamic reaction moment $M(t)$, and net carriage migration force. | `FIG_6.pdf`<br>`FIG_6.svg` | `FIG_6.pdf`<br>`FIG_6.svg` |

---

## 13. Brief Description of the Accompanying Drawings (Section 13 Response)

**FIG. 1** is a perspective dorsal view of the passive self-tuning vibration absorber worn on the dorsal forearm of a user, illustrating the ergonomic cuff base (**100**) secured via lateral retention straps (**120**), supporting a miniature linear guide rail (**106**), a fixed root clamp block (**104**) retaining a compliant cantilever spring blade (**102**), a translatable variable-stiffness fulcrum pinch carriage (**108/110**) incorporating an asymmetric friction drag unit (**112**), a distal tuned proof mass (**114**) capturing a viscoelastic secondary damper puck (**116**), and an outer protective shroud (**118**) having an upper frequency calibration inspection window (**122**).

**FIG. 2** is an exploded perspective view of the apparatus of FIG. 1, depicting the ten discrete physical components and standard fasteners separated along vertical assembly alignment axes, showing the relationship between the base mounting bosses, linear rail fastener locations, carriage mounting interface, upper and lower fulcrum pinch dowels (**124**), root clamping fasteners (**128**), and proof mass retention fasteners (**130**).

**FIG. 3** is a longitudinal cross-sectional view taken along the longitudinal system centerline (Section A-A of FIG. 1), illustrating the variable active vibrating cantilever length $L(s)$ defined between the fulcrum contact pins (**124**) and the center of mass of the distal proof mass (**114**), the internal ball raceways of carriage block (**108**), the relief lead-in radius at root clamp (**104**), and the vertical throat clearance cavity accommodating static gravity sag $\delta_{\text{sag}}$ and dynamic vibratory deflection.

**FIG. 4** is an enlarged detailed schematic cross-section of the self-tuning fulcrum carriage interface, depicting the bifurcated yoke bracket (**110**) housing upper and lower precision-ground dowel contact pins (**124**) pinching the cantilever spring blade (**102**) with calibrated operating clearance, and an inclined sprag drag leaf (**112**) engaging a micro-toothed friction strip (**126**) with directionally asymmetric friction coefficients ($\mu_{\text{fwd}} \approx 0.08$ vs $\mu_{\text{rev}} \approx 0.35$).

**FIG. 5** is a dual analytical diagram comprising:
- (Left Panel) A closed-loop control flow diagram illustrating the autonomous 5-stage mechanical feedback cycle whereby residual mistuned tremor drives asymmetric carriage migration until anti-resonance settling occurs; and
- (Right Panel) A 2-DOF frequency response plot comparing the uncontrolled primary limb resonance peak at 5 Hz against the controlled twin Den Hartog invariant peaks ($P, Q$) and deep anti-resonance attenuation notch ($X_1 \to 0$), demonstrating in excess of 85% vibration attenuation across the 3–8 Hz pathological tremor band.

**FIG. 6** is a free-body kinematic and dynamic force diagram of the fulcrum carriage, illustrating the dynamic normal load fluctuation $N(t) = N_0 + \Delta N \sin(\omega t)$ and dynamic moment $M(t)$ induced by blade oscillation, the resulting cycle-averaged rectifying force driving linear carriage translation $\dot{s}$, and the autonomous cessation of migration upon reaching anti-resonance.

---

## Master Reference Numerals Key (For Patent Specification & Claims)

| Ref # | Component Name | Production CAD Part Identifier | Material & Process Specification | Functional Role |
| :---: | :--- | :--- | :--- | :--- |
| **100** | Ergonomic Cuff Base | `PRT-001_Cuff_Base` | Biocompatible PETG (ISO 10993) | Anatomical forearm chassis; mounting spine; R35 curvature |
| **102** | Cantilever Spring Blade | `PRT-002_Cantilever_Spring` | C75S / 1095 Spring Steel (0.40 mm) | Compliant beam; variable dynamic stiffness $k_2 = 35.5 - 252.7\text{ N/m}$ |
| **104** | Root Clamp Block | `PRT-003_Root_Clamp_Block` | Aluminum Alloy 6061-T6 (Anodized) | Fixed encastre clamp; R1.5 mm fatigue relief radius |
| **106** | Miniature Linear Rail | `PRT-004_MGN7_Rail` | High-Carbon Bearing Steel (SUJ2) | Precision ground MGN7 linear rail; 80 mm length |
| **108** | Linear Carriage Block | `PRT-005_MGN7C_Block` | Stainless Steel 440C | Recirculating ball carriage; 51.5 mm stroke |
| **110** | Fulcrum Pinch Bracket | `PRT-006_Fulcrum_Pinch_Bracket`| Aluminum Alloy 6061-T6 | Bifurcated yoke housing dual contact dowel pins (**124**) |
| **112** | Asymmetric Drag Unit | `PRT-007_Friction_Drag_Unit` | Brass CZ121 + Phosphor Bronze | 35° inclined sprag leaf producing $\mu_{\text{fwd}} \approx 0.08$ vs $\mu_{\text{rev}} \approx 0.35$ |
| **114** | Distal Proof Mass | `PRT-008_Distal_Proof_Mass` | Precision Brass CZ121 ($97.7\text{ g}$) | Secondary tuned inertia member ($m_2 = 0.100\text{ kg}$ effective) |
| **116** | Viscoelastic Damper | `PRT-009_Viscoelastic_Damper` | Sorbothane OO-50 Polyurethane | Captured shear puck; Den Hartog optimal damping $\zeta = 0.168$ |
| **118** | Protective Shroud | `PRT-010_Protective_Shroud` | Optical Polycarbonate / Clear PETG | Safety cover; 36 mm vertical clearance throat |
| **120** | Lateral Retention Straps | Standard COTS Part | Medical Hook-and-Loop (20 mm) | Dorsal limb fixation; breathable non-slip backing |
| **122** | Calibration Window | Inspection Window Feature | Laser-Etched 3–8 Hz Scale | Visual indicator of instantaneous tuned tremor frequency |
| **124** | Fulcrum Dowel Pins | `PIN-001_Dowel_Pins` | Hardened Tool Steel (Ø2.5 h6 x 14) | Upper & lower precision pinch pins establishing moving boundary node |
| **126** | Friction Base Track | Chassis Surface Feature | Micro-Toothed / Textured Strip | Contact track generating directional frictional asymmetry |
| **128** | Encastre Clamping Screws| Fastener COTS Part | Stainless Steel A2-70 (ISO 4762 M3)| M3 x 12 mm socket head cap screws for root clamp |
| **130** | Mass Retention Screws | Fastener COTS Part | Stainless Steel A2-70 (ISO 10642 M2.5)| M2.5 x 8 mm countersunk flat head screws |

---
**Prepared by:** Department of Mechatronics and Automation, VIT Chennai  
**Date of Release:** 18 October 2026
