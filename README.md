# K1-Series-CFS-Nozzle-Wiper
Creality K1 Series CFS Nozzle Wiper Upgrade 

# Creality K1 Series CFS Nozzle Wiper Upgrade (K1 Max Fork)

This repository is a fork of [supernovaBvS/K1-Series-CFS-Nozzle-Wiper](https://github.com/supernovaBvS/K1-Series-CFS-Nozzle-Wiper), updated and configured with verified **Creality K1 Max** dimensions and coordinate values.

---

## 📌 Overview & Fork Changes

When retrofitting or running the **Creality Filament System (CFS)** on K1-series machines, the stock nozzle wiping routine often defaults to bed-mounted wipe sequences rather than utilizing the external rear purge chute wiper. 

This macro replaces the standard wiping behavior with an optimized, variable-width scrubbing motion inside the CFS purge chute.

### 🌟 What's Updated in This Fork:
- **Calibrated for K1 Max:** Adjusted X, Y, and Z travel limits, park locations, and wipe centers specifically tailored to the larger 300 × 300 mm bed volume of the K1 Max.
- **Chute Clearance Safety:** Tuned stroke bounds to prevent toolhead or nozzle collisions with the metal casing of the K1 Max purge chute assembly.
- **Ready-to-use Configurations:** Eliminates the guesswork of recalculating coordinates when running this macro on a K1 Max.

---

## 🚀 Key Advantages

* **Reclaim Full Build Plate Area:** Frees up build plate real estate by utilizing the external chute silicone wiper instead of bed-mounted brushes.
* **Universal Bed Compatibility:** Use textured PEI, smooth plates, or aftermarket build surfaces without worrying about clip clearance or wiper collisions.
* **Variable-Width Scrubbing:** Utilizes a wider, alternating X-axis wiping path to prevent prematurely cutting a deep trench into the silicone wiper.
* **Collision Protection:** Incorporates safe Z-hop clearances and conditional homing logic before maneuvering into the rear purge chute.

---

## 🛠️ K1 Max Macro Configuration

Below are the calibrated baseline values for the K1 Max. Adjust within your `printer.cfg` or included macro file as needed:

```ini
# Example wiper coordinates calibrated for K1 Max:
variable_wiper_x: 204          # Wiper center on K1 Max (tune between 203 - 205 depending on chute tolerance)
variable_wiper_y: 305          # Rear Y position for wiper engagement
variable_wipe_dist: 6          # Wipe stroke width (6mm safe; 8mm considered safe; up to 10-12mm if chute tab is trimmed)
variable_wipe_qty: 6           # Number of wipe passes
variable_safe_z: 10            # Safe Z clearance before moving to rear chute

> **Note on Mechanical Clearance:** On some K1 Max units, variations in the chute mounting bracket can cause slight interference on wide strokes. Start with a 6 mm stroke (`variable_wipe_dist: 6`) around `X=204` to `X=205`. If you have trimmed the chute bracket tab, you can extend the stroke up to 10–12 mm.
```
---

## 📥 Installation

1. **Add Macro File:**  
   Copy `cfs_nozzle_clear.cfg` (or the contents of the macro) into your Klipper configuration directory (e.g., alongside `printer.cfg`).

2. **Include in `printer.cfg`:**
   ```ini
   [include cfs_nozzle_clear.cfg]
   ```
3. **Restart Klipper**

4. **Slicer Integration:**  
   Call the macro (e.g., CFS_NOZZLE_CLEAR or override BOX_NOZZLE_CLEAN) in your filament change / toolchange G-code routines in Creality Print, OrcaSlicer, or PrusaSlicer.

6. **Dry Run:**  
   Before printing, run a manual test via the Klipper console (Fluidd/Mainsail) with the toolhead elevated to verify that the nozzle centers cleanly on your silicone wiper pad.

---

## ⚙️ Slicer Setup & Integration

* To trigger the wiping routine during filament changes and purge events, integrate the macro call into your slicer's custom G-code sections (OrcaSlicer, PrusaSlicer, or Creality Print).

* **OrcaSlicer / PrusaSlicer**
  * Change Filament G-code:   
    ```ini
    ; Retract slightly to prevent oozing before move
    M83
    G1 E-1.5 F2400

    ; Call the K1 Max calibrated wipe routine
    CFS_NOZZLE_CLEAR

    ; Resume relative/absolute positioning defaults
    G90
    ```

  * Machine Start G-code (Optional Clean before Bed Mesh)
    ```ini
    ; Heat nozzle to soft temperature (140-150C) to avoid burning bed/wiper
    M104 S150
    M190 S[bed_temperature_initial_layer_single]
    M109 S150

    ; Clear any cold ooze before homing/meshing
    CFS_NOZZLE_CLEAR
    ```

---

## 🔧 Step-by-Step Calibration & Dry Run
* Because assembly tolerances on the rear chute and bracket can vary by 1–2 mm between machines, follow these steps before initiating your first multi-color print:
  1. **Home All Axes:**
     ```ini
     G28
     ```
  2. **Raise Z for Visibility:**
     ```ini
     G1 Z50 F1200
     ```
  3. **Align the X/Y Position:**
     Move the printhead directly over your chute wiper center
     ```ini
     G1 X204 Y305 F6000
     ```
     * Inspect the nozzle position relative to the silicone tab.
     * If the nozzle is biased left, adjust variable_wiper_x upward (e.g., 205).
     * If biased right, reduce variable_wiper_x (e.g., 203).
  4. **Verify Wipe Bounds:**
     Simulate a test wipe stroke manually at reduced speed to check clearance against the chute walls:
     ```ini
     ; Test left bound
     G1 X200 Y305 F3000
     ; Test right bound
     G1 X208 Y305 F3000
     ```
  5. **Test Macro Execution:**
     Run the full macro via the Klipper web console (Fluidd/Mainsail):
     ```ini
     CFS_NOZZLE_CLEAR
     ```
---

## 🧩 Hardware Prerequisites & Notes
* **Chute Assembly:** Designed for K1 series equipped with the CFS purge chute and silicone wipe flap assembly.
* **Silicone Flap Wear:** Keep an eye on silicone wear during high-volume filament change prints. The alternating stroke width (variable_wipe_dist) minimizes central grooving, but periodic inspection is recommended.
* **K1 / K1C Compatibility:** If adapting this configuration back to an original K1 or K1C, note that travel limits and chute centerlines differ due to the smaller 220 × 220 mm bed footprint. Refer to the upstream repository for original K1 values.

---

## 🤝 Credits & Upstream
* Original implementation and logic by supernovaBvS.
* K1 Max coordinate testing and fork maintenance by thewolfman56.

---

## 📄 License
* This configuration and macro repository is distributed under the terms of the original project repository. Refer to the LICENSE file for complete details.
