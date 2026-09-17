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
variable_wipe_dist: 6          # Wipe stroke width (8mm safe; up to 10-12mm if chute tab is trimmed)
variable_wipe_qty: 4           # Number of wipe passes
variable_safe_z: 10            # Safe Z clearance before moving to rear chute
