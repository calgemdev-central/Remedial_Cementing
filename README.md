[Remedial_Cementing_Simulator_README.md](https://github.com/user-attachments/files/34159816/Remedial_Cementing_Simulator_README.md)
# Remedial Cementing Simulator | S. Siddhu | SOGE | Central

> **DISCLAIMER:** For educational purposes only. Simplified model; not a certified hydraulics or engineering program and not for operational, design, or regulatory decisions. Does not represent official CalGEM guidance. Verify all inputs and results independently.

## Remedial Cementing Simulator — README

*User guide for version 12 · October 2026*

## Overview

**Remedial Cementing Simulator** is a single-file, browser-based training tool that animates two remedial cementing jobs on a to-scale wellbore schematic: a **Balanced Plug** and a **Squeeze** through perforations. Every input updates the calculations, the schematic and the readouts live.

Current version: **v12** (`Balanced_Plug_Sqzv12.html`). A separate prototype, `MultiZone_Perf_Squeeze_Model_v2.html`, models squeezing through three perforation zones and is not yet merged into this tool.

## Getting Started

- Open `Balanced_Plug_Sqzv12.html` in any modern desktop browser (Chrome, Edge, Firefox, Safari). No installation, server or internet connection is needed.
- Pick **Balanced Plug** or **Squeeze Mode** with the toggle at the top of the input panel.
- Choose casing and tubing/workstring from the drop-downs (OD, weight and ID load automatically), then edit the job inputs.
- Run the numbered animation steps in order. Each step unlocks the next. Changing any input resets the animation.

## Balanced Plug Mode

| Input | Default | Notes |
|---|---|---|
| Casing OD / weight; casing ID | 7.000" 26 lb/ft; 6.276" | ID can be overridden; capacity recalculates |
| Well total depth (TD) | 4,000 ft | Sets the vertical scale of the schematic |
| Tubing OD / weight | 2.875" 6.5 lb/ft | Gives tubing capacity and tubing-by-casing annulus capacity |
| Tubing tail depth | 3,500 ft | Where the plug is spotted |
| Cement volume | 50 bbl |  |
| Spacer ahead (annulus) | 20 bbl | Spacer behind is sized to match the same height |
| Cut displacement short by | 2.0 bbl | 0 = perfectly balanced; greater than 0 leaves cement higher inside the pipe and lower in the annulus |
| Pull-up distance | 500 ft | Distance the tubing is pulled during step 6 |

### Animation steps

1. Run in hole (tubing string).
2. Pump spacer ahead.
3. Spot cement slurry (cement passes the tail and rises in the annulus).
4. Pump spacer behind.
5. Pump fresh-water displacement (balance).
6. Pull out of hole to the settled top of cement (TOC).

The Calculations Engine panel reports plug length and TOC with pipe in, required spacer behind, theoretical and actual displacement, the inside-pipe cement top with the cut applied, and the final plug length and TOC after pulling out.

## Squeeze Mode

| Input | Default | Notes |
|---|---|---|
| Casing OD / weight; casing ID | 7.000" 26 lb/ft; 6.276" | Casing OD also feeds the open-hole annulus calculation |
| Open hole size | 8.500" | Hole diameter behind the casing |
| Open hole annular capacity | calculated | bbl/ft between casing OD and the hole wall |
| Linear ft of cement in annulus | 100 ft | Cement volume in the annulus is calculated from it |
| Workstring OD / weight | 2.875" 6.5 lb/ft | Inside and annulus capacities calculated |
| Initial tubing tail depth; TD | 3,500 ft; 4,000 ft |  |
| Squeeze bottom depth; gun length; shot density | 3,500 ft; 5 ft; 4 spf | Perforation top and hole count are calculated |
| Total spotted volume; squeeze slurry volume | 50 bbl; 20 bbl | Residual is spotted minus squeezed |
| Cement density; water/flush density | 15.5 ppg; 8.33 ppg | Used for hydrostatic and MASP |
| Fracture gradient | 0.70 psi/ft | Applied at the squeeze bottom depth |

### Animation steps

1. Pressure test the casing string.
2. Run the wireline perforation gun and shoot.
3. Run the tubing string and spot the slurry block.
4. Displace slurry down the tubing string.
5. Pull tubing clear of the TOC.
6. Reverse circulate the tubing tail clean.
7. Apply the surface squeeze pressure profile (slurry leaves through the perforations, residual cement stays in the casing, and the open-hole annulus cement fills).

## Reading the Schematic

| Element | Meaning |
|---|---|
| Cement (grey, stippled) | Cement slurry |
| Spacer (amber) | Spacer ahead and behind (Balanced Plug) |
| Fresh water (light blue) | Displacement or flush water |
| Mud / brine (light grey) | Wellbore fluid before and between jobs |
| Perforations (red) and squeeze flow (orange dashes) | Open perforations and slurry leaving through them during step 7 |
| Tubing valve dot | Green when open, red when closed (step 7) |
| Tubing gauge (blue line) | Teed off the top of the wellhead stack at the tubing valve |
| Casing MASP gauge (red line) | Plumbed to the casing spool side outlet |
| Callout labels and depth ruler | Surface, TD, tubing tail, TOC, perforation interval and open-hole cement volume; the ruler is to scale vertically |
| Readout panel | Live numbers for the current step, anchored to the bottom of the schematic |
| MASP chart (Squeeze Mode) | Surface pressure buildup across the pump schedule, with a marker that tracks the animation |

The schematic is to scale vertically only; widths are exaggerated for legibility.

## Key Calculations

| Quantity | Expression |
|---|---|
| Capacity (bbl/ft) | ID² / 1029.4 |
| Annular capacity (bbl/ft) | (outer ID² − inner OD²) / 1029.4 |
| Open-hole annular capacity | (hole size² − casing OD²) / 1029.4; cement volume = capacity × linear ft |
| Plug length, pipe in (Balanced) | cement volume / (tubing capacity + annulus capacity) |
| TOC, pipe in | tubing tail depth − plug length |
| Spacer behind volume | (spacer ahead / annulus capacity) × tubing capacity |
| Theoretical displacement | (TOC pipe in − spacer behind height) × tubing capacity |
| Actual displacement | theoretical − cut displacement; inside TOC = TOC − cut / tubing capacity; annulus TOC = TOC + cut / annulus capacity |
| Final plug and TOC, pipe out | plug = cement volume / casing capacity; TOC = tubing tail depth − plug |
| Perforation top; hole count (Squeeze) | squeeze bottom − gun length; gun length × shots per ft |
| Residual cement and final TOC | spotted − squeezed; final TOC = TD − residual / casing capacity |
| Hydrostatic (psi) | 0.052 × density (ppg) × depth (ft) |
| Formation frac limit at perfs | fracture gradient × squeeze bottom depth |
| Initial MASP | frac limit − (slurry column + water column hydrostatic), slurry height = spotted volume / casing capacity |

## Assumptions and Limitations

- The MASP curve adds an illustrative **28 psi per increment** (30 increments across the spotted volume) to the starting MASP. It is a visual buildup, not a modeled formation response.
- No friction, pump rate, temperature, fluid compressibility, U-tube effects or cement lock-up are modeled in this tool. The multi-zone prototype adds friction, pump rate and lock-up.
- Open-hole annulus cement is displayed and its volume is calculated, but it is not part of the squeeze pressure or volume balance.
- The casing test (1,000 psi), the workstring pull to 600 ft above the cement top, and the tubing-gauge reading of 0 psi in step 7 are fixed animation values. A closed-in tubing string would be expected to follow casing pressure; this has not been changed.
- A single fracture gradient applies across the job; casing and tubing are concentric and vertical.
- Treat all absolute numbers as order-of-magnitude until compared against known job data.

## Version Notes (v12)

- Renamed Remedial Cementing Simulator; header band with author name and disclaimer.
- Rebuilt engineered-cutaway schematic: hatched formation, steel casing and tubing, wellhead, depth ruler, callout labels.
- Schematic height fits the panel so no empty space remains at the bottom; readouts added for every Squeeze step.
- Open-hole size, annular capacity and linear-feet-of-cement inputs added to Squeeze Mode, with animated annulus fill.
- Tubing gauge teed off the top of the stack with a live open/closed valve indicator; casing and tubing gauges colour-coded.
- Lighter cement colour; MASP chart moved to its own bordered chart.

---

**Disclaimer:** For educational purposes only. Simplified model; not a certified hydraulics or engineering program and not for operational, design, or regulatory decisions. Does not represent official CalGEM guidance. Verify all inputs and results independently.

*S. Siddhu | SOGE | Central*
