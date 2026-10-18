# MISSION BRIEF — Autonomous Production CAD for the TMD Wrist Device

> Paste this whole file as the task prompt for the CLI agent, started in `D:\ai project`.
> It is meant to run start to finish with **no human input**.

---

## 0. Role

You are a **senior mechanical design engineer** working in a medical-device product team, with
hands-on experience in precision mechanisms, compliant flexures, DFM for CNC, FDM/SLA and sheet
metal, and in preparing patent drawings. You own this design end to end: physics, geometry,
tolerancing, manufacturing, sourcing and documentation. Work the way a professional would before
signing a drawing: **calculate, model, check, and only then release.**

You are fully autonomous. **Do not ask the user anything.** When a decision is needed, make the
engineering call, write it in the Decision Log (§9) with the reason, and keep going. You may use
**any method, tool, library or software on this machine**, and you may install packages, as long as
the deliverables in §5 are produced and verified.

---

## 1. The product (read first, then confirm against the sources)

**A Passive, Self-Tuning Vibration Absorber for Suppression of Pathological Hand Tremor**
(inventors Bhavesh A, Ashwin T E, Mithun Shankar M; VIT Chennai). This is a wrist-worn tuned mass damper with
no battery, sensor or controller. A brass proof mass sits at the tip of a spring-steel cantilever blade.
A fulcrum carriage on an MGN7 linear rail pinches the blade and sets its active length L, so
k₂ = 3EI/L³ and the tuned frequency ω₂ = √(k₂/m₂). An asymmetric-friction drag shoe ("walking"
mechanism) lets residual mistuned vibration move the carriage toward the position where ω₂
equals the tremor frequency (3–8 Hz). At that point the motion collapses and the carriage stops.

**Sources of truth, in priority order:**
1. `Inventive_Disclosure_Filled.docx`: the legal disclosure. Never contradict its inventive concept or claims.
2. `extracted_patent_text.txt`: a plain-text copy of (1), for quick reading.
3. `PATENT_CAD_DESIGN_REPORT.md` and `INVENTIVE_DISCLOSURE_CAD_ANNEXURE.md`: the intended part list, reference
   numerals (100–130), BOM, sizing table and figure list. **They contain errors (see §2), so verify every number.**
4. `cad_design/TMD_Wrist_Device.py` and `patent_drawings/generate_patent_drawings.py`: old attempts.
   Use them only as hints for layout intent. **Do not trust their geometry.**

Read all of the above in full before you model anything.

---

## 2. Audit of the current state (already verified — do not repeat; fix)

**No real CAD exists in this project.** The current outputs are placeholders:

| Item | Finding |
|---|---|
| `cad_design/TMD_Wrist_Device.py` | Fatal bug: `app = None` and `adsk.core.Application.get()` is never called, so it crashes at `app.activeProduct`. It has never produced a model, and no STEP file was ever exported. |
| `cad_design/parts_stl/*.stl`, `*.obj` | Axis-aligned **boxes** (12 triangles per part) from a pure-Python mesh writer. They are not B-rep, have no holes and no real profiles, and are not fit for manufacture. |
| `PATENT_CAD_DESIGN_REPORT.md` | Claims an "AST PASS" and "STEP ready" that never happened. Lists the rail mass as 28 g; a HIWIN MGN7 rail is about 0.22 kg/m, so 80 mm is about 18 g. Check it against the catalogue. |
| Damping ratio | The disclosure says ζ_opt ≈ 0.13 at μ = 0.1 and the report says 0.168. **The correct value is 0.168** (√(0.3/10.648)). Fix it everywhere it appears. |
| Assembly geometry in old script | The root clamp (z = 12.04) overlaps the blade (z = 12.0–12.4). The blade has nothing under it at the root (about 5 mm air gap to the spine). The carriage overlaps the rail. The fulcrum bracket body passes through the blade. The fulcrum has **one pin, not a pinch pair**. The damper puck touches nothing at its lower face, so it provides no damping. The rail span (x = 35–115 mm) does not cover the fulcrum positions the sizing table needs. |
| Orphan `~$*.SLDPRT` lock files | Already deleted. |

**Engineering problems you must solve, not just model:**

1. **Gravity sag.** Static deflection of any linear absorber is δ = g/ω₂², independent of mass:
   **27.6 mm at 3 Hz, 9.9 mm at 5 Hz, 3.9 mm at 8 Hz.** The old layout leaves about 8 mm under the mass
   and about 6 mm above it inside the shroud, so the mass would bottom out across most of the band. Choose and
   justify a solution: a pre-set (pre-bent) blade that is level under 1 g at mid-band, a larger clearance
   envelope, re-orienting the bending axis relative to the dominant tremor direction, or a combination. Add
   elastomer **bump stops** so the blade can never be overstressed when it hits the end of its travel.
2. **Boundary condition at the fulcrum.** k = 3EI/L³ assumes a *clamped* end. A pinch made of a single
   pin pair behaves closer to a pinned support, while the root clamp behind it adds a back-span. Model the
   real support: either two axially spaced pin pairs that approximate fixity, or derive or FEA the correct
   tip stiffness for the root-clamp + pinch + overhang beam. Then recompute the L(s) → f map and the rail
   stroke from that model.
3. **Fatigue.** At 5 Hz × 8 h/day the blade sees about 5×10⁷ cycles per year, so it needs infinite life. Static root
   stress is 165–317 MPa across the band. Add the alternating stress at the expected relative amplitude,
   apply Goodman with spring-steel endurance and Kt for any hole or clamp edge, and target a safety factor ≥ 1.5.
   Keep holes out of the high-moment zone, and give the clamp edge a lead-in radius.
4. **Damper force path.** A viscoelastic element only damps if it is attached to both bodies that move
   relative to each other (proof mass ↔ cuff, or blade ↔ carriage) and is loaded in shear or compression
   within its strain limit. Design a real attachment and size it to c₂ ≈ 2ζ√(k₂m₂) with ζ = 0.168.
5. **Walking mechanism force path.** State explicitly (with a free-body sketch in the report) how blade
   vibration produces a net force on the carriage, and how the drag shoe gives μ_fwd ≈ 0.08 against μ_rev ≈ 0.35
   on the friction strip (126). Make the geometry of the shoe, its preload spring and the strip buildable.
6. **Mass budget and claims.** Total device mass must stay within 50–300 g (claim range). Mass ratio μ
   is based on m₁ = 1.0 kg; keep that assumption stated.

---

## 3. Design rules (non-negotiable)

**Inventive concept.** Do not remove or change the function of any claimed element (cuff/band, proof mass,
compliant element, passive self-tuning carriage with asymmetric damping, 3–8 Hz band, no power,
sensor or controller). Keep reference numerals 100–130 and part IDs `PRT-001` … `PRT-010` stable. Any
dimension change from the disclosure or report goes into the **Design Change Log** with old value,
new value and reason, because the patent text cites these numbers.

**Standards to apply** (use the ISO set; mention ASME only where a vendor part uses it):
- Drawings: ISO 128 (lines/views), ISO 129-1 (dimensioning), first-angle projection, ISO 7200 title block.
- Tolerancing: ISO 2768-mK general; ISO 286 fits for pins and bores (e.g. H7/g6 sliding, H7/p6 press);
  ISO 1101 GD&T on functional surfaces (rail seat flatness, blade clamp faces, pin bores).
- Surface finish: ISO 1302 (Ra) on the rail seat, clamp faces and friction strip.
- Fasteners: ISO 4762 SHCS, ISO 10642 countersunk, ISO 7089 washers, metric coarse threads, and tap
  drill / clearance / counterbore sizes from ISO 273 (medium fit).
- Skin-contact parts: material must be suitable for intact-skin contact per ISO 10993 (state which grade).
  Edges that touch skin get radii of 1 mm or more, and there are no pinch points the user can reach.
- Risk: list the top hazards (pinch, blade fracture, strap failure, skin irritation) and the design control for each,
  in the style of ISO 14971.

**Units and model hygiene.** Use millimetres throughout. One body per part, one file per part. Name every
feature, sketch and part. Every sketch must be fully constrained. Make the assembly parametric from a single
driving table (blade b, h, E, m₂, L range, stroke). Set the tuned position as a configuration or parameter
so the assembly can be shown at 3 Hz, 5 Hz and 8 Hz.

---

## 4. Fabrication and availability (design for what can actually be bought and made)

Pick each part's process **first**, then model to that process's rules. Prefer catalogue (COTS) parts over custom ones.
The build team is in **Chennai, India**, so favour parts available from Indian distributors (e.g. Robu.in,
Amazon.in, local spring-steel shim and brass-bar suppliers, local CNC and 3D-print bureaus), with an
international fallback.

| Part | Default process / source | Model-to rules |
|---|---|---|
| PRT-001 Cuff base | FDM in PETG (prototype); SLA or PA12 MJF for the release version | wall ≥ 1.6 mm, hole compensation +0.2 mm, heat-set inserts (M2/M3) instead of tapped plastic, no unsupported overhang > 45°, print orientation noted on drawing |
| PRT-002 Blade | 0.40 mm hardened & tempered C75S / AISI 1095 shim stock; laser, wire EDM or photo-etch | corner radii ≥ 1 mm, no holes in the high-moment zone, deburr note, flat-pattern **DXF** |
| PRT-003 Root clamp, PRT-006 Fulcrum bracket | CNC 6061-T6, anodised | internal radii ≥ tool R (≥ 1 mm), standard drill sizes, ISO 286 bores for pins |
| PRT-004 Rail, PRT-005 Block | **Buy: HIWIN MGN7C (or interchangeable clone)** | model to the **catalogue** dimensions, M2 holes at 15 mm pitch, correct counterbores; cut rail length to suit stroke + block length + end margins |
| PRT-007 Drag unit | Brass CZ121 shoe + spring-steel leaf + felt/PTFE pad | buildable preload, replaceable pad |
| PRT-008 Proof mass | CNC brass CZ121 (8.5 g/cm³) | hit m₂ within ±1 g by geometry; tapped M2.5 holes; edges chamfered |
| PRT-009 Damper | Sorbothane sheet (import) — **local fallback: silicone or neoprene sheet, Shore A 20–30**; give both and re-size c₂ for each | bonded or captured, never floating |
| PRT-010 Shroud | Clear PETG (FDM) or clear SLA resin for prototype; PC vacuum-form for volume | wall ≥ 1.5 mm, clearance to moving parts ≥ (max sag + dynamic amplitude + 2 mm), snap-fit or M2 screws |
| 124 Pins | Buy ISO 8734 dowel pins Ø2.5 h6 | — |
| 120 Strap | Buy 20 mm medical hook-and-loop | slot 21 × 4 mm |

Write a **sourcing BOM** (CSV and XLSX) with: item, ref numeral, qty, material/spec, process, make/buy,
supplier (India + global), part number, est. unit cost (INR), lead time, mass (from CAD), and notes.

---

## 5. Deliverables

Use exactly this structure. Nothing else should be left in the project when you finish.

```
D:\ai project\
├── README.md                       ← index: what each folder holds, revision, how to open
├── CAD_AGENT_PROMPT.md             ← this brief (keep)
├── AGENTS.md, GEMINI.md, .agents\  ← user's tool config (DO NOT TOUCH)
├── 01_Source_Documents\
│   └── Inventive_Disclosure_Filled.docx
├── 02_Engineering\
│   ├── Design_Report.md            ← corrected PATENT_CAD_DESIGN_REPORT, now with real numbers from CAD
│   ├── Design_Calculations.md      ← sizing, BC model, sag, fatigue, damper, walking force path, tolerance stack
│   ├── Decision_and_Change_Log.md
│   └── images\                     ← iso / front / top / section renders at 3, 5, 8 Hz positions (PNG)
├── 03_CAD_Native\                  ← parametric native files (SLDPRT/SLDASM, or the chosen tool's native)
├── 04_CAD_STEP\                    ← one AP214/AP242 STEP per part + full assembly STEP
├── 05_Manufacturing\
│   ├── Drawings_PDF\               ← one ISO drawing per custom part + assembly drawing with balloons & BOM
│   ├── STL_Print\                  ← STL only for printed parts (001, 010), fine tessellation
│   └── DXF_Flat\                   ← blade + any laser/water-jet profiles
├── 06_Patent_Drawings\
│   ├── Set_A_Labeled\              ← FIG 1–5, PDF, A4
│   ├── Set_B_Unlabeled\            ← FIG 1–5, PDF, A4
│   └── INVENTIVE_DISCLOSURE_CAD_ANNEXURE.md  ← updated
└── 07_BOM_Sourcing\
    ├── BOM.xlsx
    └── BOM.csv
```

**Patent drawings** must be free of any educational-licence watermark (see §6), and must be generated **from the real 3D model** (projected views, an actual section cut through
the model, an exploded view), not drawn by hand in SVG. Format: A4 portrait, black lines on white,
no colour or shading other than hatching, uniform line weight, numerals ≥ 3.2 mm high with thin leader
lines, "Sheet n of N", and no descriptive text on Set B. Check the margins and format against the
**current Indian Patents Rules (Rule 15 / Third Schedule)** before releasing, and note the rule you followed.
FIG 5 (flowchart + FRF graph) is a diagram, not a CAD view; plot the FRF from the 2-DOF equation with
the final m₂, k₂ and c₂ values.

---

## 6. Toolchain: choose, probe, fall back

Installed on this machine (verified): **SOLIDWORKS 2026 (v34), Student/Educational licence**, **Autodesk Fusion 360** (needs a signed-in
GUI session; the Fusion MCP bridge was *not* reachable), **Blender 5.2**, Python 3.12, and `uv`. Python has **no**
CAD libraries yet. You may install anything.

Run a 2-minute probe of each path, then pick:

1. **Preferred — SOLIDWORKS API** (via `pywin32` COM, `SldWorks.Application`): gives native parametric
   SLDPRT/SLDASM/SLDDRW, real ISO drawings, mass properties, interference detection, and STEP/DXF/PDF export.
   Use it if a licence is active and the COM object starts.

   **The user's SOLIDWORKS is a STUDENT (educational) licence.** This changes how you use it:
   - **Activation can block automation.** Student seats often need an online sign-in (3DEXPERIENCE ID) or
     periodic re-activation, which shows a dialog no script can answer. Start SolidWorks with a 120 s
     timeout, poll whether `ISldWorks` responds and whether a part document can be created, and check for
     any modal licence window. If it is blocked, **do not wait or retry in a loop.** Log it and switch to path 2.
   - **Watermark.** Drawings, prints and PDF/DXF exports from SLDDRW files carry the
     *"SOLIDWORKS Educational Product — For Instructional Use Only"* stamp. **Patent drawings (§5,
     `06_Patent_Drawings`) must never carry it.** Generate all patent figures through path 2 from the exported
     STEP geometry. Open every final PDF, render it, and confirm that the watermark text is absent. Manufacturing
     drawings from SOLIDWORKS may keep the stamp, but say so in the README.
   - **Native files are "tainted".** Educational SLDPRT/SLDASM files open with a watermark in any commercial
     SOLIDWORKS seat. So **STEP AP242 (`04_CAD_STEP`) is the official hand-off format** for fabricators and the
     patent agent, and native files are kept for the inventors' own editing only.
   - **Add-ins.** Which add-ins you get depends on the student package. Probe for SOLIDWORKS Simulation and
     Motion, and load them if they are present; if they are absent, do gate 6 analytically or with an open-source
     FEA (e.g. CalculiX via `uv`).
   - **Licence scope.** An educational licence is for non-commercial / instructional use. Record in the open-risks
     list that commercial manufacture or licensing (Disclosure §22) needs the CAD re-saved or re-checked
     on a commercial seat, and that the neutral STEP files are the transferable asset.
2. **Fallback — build123d or CadQuery (OpenCascade)** in a `uv` venv: exact B-rep STEP, STL, DXF and section
   projections, fully headless. If you use this, the STEP files are the "native" deliverable and drawings are
   produced from model projections (e.g. via build123d's `ExportSVG` → PDF). Then lay out ISO title
   blocks and dimensions programmatically.
3. Fusion 360 only if both of the above fail.

Whatever you pick: **all scripts, venvs and scratch files live outside the project** in
`%TEMP%\tmd_cad_work\`. The project receives only finished outputs.

---

## 7. Verification gates (all must pass before release)

Do not mark anything done on assertion alone. Produce evidence (numbers, logs, images) and put it in the report.

1. **Geometry validity.** Every STEP re-imports as a closed, valid solid (no free edges, volume > 0).
2. **Interference.** Zero interference in the assembly at the 3 Hz, 5 Hz and 8 Hz carriage positions, *and* with the
   blade at max sag ± dynamic amplitude. Report the minimum clearances.
3. **Kinematics.** The carriage reaches both ends of the required stroke without hitting any other part.
4. **Mass.** Mass properties from CAD match the BOM within ±3%. m₂ (proof mass + effective blade mass, ≈ 0.24·m_blade)
   is within ±1 g of target. The total is within 50–300 g.
5. **Physics.** Recompute f at 3/5/8 Hz positions from the *as-modelled* geometry and your stiffness model; error ≤ 2%
   against the target. Present a table.
6. **Strength.** The fatigue SF ≥ 1.5 at the worst case is shown with numbers. Run a simple FEA (SOLIDWORKS Simulation or
   an analytic check) on the blade and fulcrum pins.
7. **Fasteners and fits.** Every hole matches its fastener and standard (clearance, tap drill, counterbore depth),
   and thread engagement is at least 1.5×d in aluminium or the insert length in plastic.
8. **Drawings.** Each custom part has a fully dimensioned drawing that a machinist could quote from without
   asking a question (material, finish, tolerances, general tolerance note, units, projection symbol,
   revision, mass).
9. **Visual check.** Render each part and the assembly and *look at the images*. Fix anything that looks wrong.
10. **Docs consistency.** Every number in the report, annexure and BOM traces to the CAD or the calculations,
    and nothing contradicts the disclosure except entries listed in the Change Log.

If a gate fails, fix it and re-run **all** gates. Loop until every gate is green.

---

## 8. Storage clean-up (do this LAST, only after §7 is green)

**Principle:** the user needs the product files, not the means of making them. Remove anything that is
generated, duplicated, superseded or only useful to the automation.

**Delete:**
- `cad_design\TMD_Wrist_Device.py`, `cad_design\fusion_cli_runner.py`, `cad_design\generate_3d_cad_models.py`,
  `cad_design\TMD_Wrist_Device.manifest`
- `cad_design\TMD_Wrist_Device_Assembly.obj`, `.mtl`, the whole `cad_design\parts_stl\` folder (placeholder boxes)
- `cad_design\CAD_AND_PATENT_VIEWER.html` (it points at the deleted meshes)
- `patent_drawings\generate_patent_drawings.py` and all old `FIG_*.svg` files (superseded by §5)
- `extracted_patent_text.txt` (duplicate of the .docx)
- the broken Fusion script copy at `%APPDATA%\Autodesk\Autodesk Fusion 360\API\Scripts\TMD_Wrist_Device\`
  (that folder only; leave the other scripts there alone)
- empty `cad_design\` and `patent_drawings\` folders, any `__pycache__`, `*.bak`, `*.log`, `~$*` and temp files
- `%TEMP%\tmd_cad_work\` once the outputs are copied

**Move** (do not copy): `Inventive_Disclosure_Filled.docx` → `01_Source_Documents\`; the two `.md` reports → their
§5 locations after updating them.

**Never touch:** `AGENTS.md`, `GEMINI.md`, `.agents\`, `CAD_AGENT_PROMPT.md`, or anything outside
`D:\ai project` except the two paths named above.

Before deleting, list each file with its size, confirm that it is on the list above, then delete it. At the end, print
the final tree with sizes, and confirm that no `.py`, `.svg` draft, `.obj` or temp file remains in the project.

---

## 9. Working method and final report

1. **Plan.** Read the sources, then write `Design_Calculations.md` sections 1–4 (sizing, boundary-condition model,
   sag, fatigue). Decide the layout before you open the CAD tool.
2. **Skeleton.** Build the driving parameters and the assembly layout sketch (rail datum, blade line, mass envelope,
   shroud envelope).
3. **Parts.** Model COTS parts from the catalogue first (rail, block, pins, screws), then the custom parts around them.
4. **Assemble.** Add mates or joints, with the carriage position driven by a parameter.
5. **Verify** (§7) → **Drawings** (§5) → **Patent figures** → **BOM** → **Docs** → **Clean-up** (§8).

Keep `Decision_and_Change_Log.md` up to date as you go (date, decision, options considered, reason).

**When you finish, reply with:**
- the final folder tree;
- a gate table (§7), each gate PASS with its key number;
- the Design Change Log summary (what changed from the disclosure and why);
- open risks the inventors must act on (e.g. walking-mechanism efficacy is still unproven until the bench
  test in Disclosure §14 is run; patent-agent review of the changed numbers).

Do not report success for anything you did not verify. If something cannot be done on this machine
(e.g. no SOLIDWORKS licence), say exactly what, use the fallback, and carry on.
