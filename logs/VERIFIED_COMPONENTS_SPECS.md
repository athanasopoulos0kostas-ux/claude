# Verified Component Specifications

**Source:** BOM v3 verification mission (November 4, 2025)

All dimensions verified from official datasheets.

---

## Major Components

| Component | Part Number | Package | Dimensions (mm) | Height (mm) | Price @ 1k | Notes |
|-----------|-------------|---------|-----------------|-------------|------------|-------|
| **Cellular** | BG95-M3 | LCC | 13 × 15.8 | 2.2 | €9.50 | LTE-M/NB-IoT, 2G fallback |
| **GPS** | MAX-M10S | LCC | 9.7 × 10 | 2.4 | €8.00 | u-blox M10 receiver |
| **MCU** | nRF52810-QFAA-R | QFN48 | 6 × 6 | 0.9 | €3.00 | Nordic BLE 5.0 |
| **Flash** | W25Q32JVSSIQ | SOIC-8 | 5.28 × 7.9 | 1.27 | €0.80 | 32Mbit |
| **eSIM** | ST4SIM-200M | MFF2 | 5 × 6 | 1.0 | €3.50 | Standard eSIM |

## Sensors

| Component | Part Number | Package | Dimensions (mm) | Height (mm) | Price @ 1k | Notes |
|-----------|-------------|---------|-----------------|-------------|------------|-------|
| **PPG** | MAX30102 | OLGA | 5.6 × 3.3 | 1.55 | €4.00 | Heart rate + SpO2 |
| **Temperature** | TMP102 | SOT563 | 1.6 × 1.2 | 0.6 | €0.80 | Body temp sensor |
| **Accelerometer** | ADXL372 | LGA | 3 × 3.25 | 1.0 | €2.50 | Motion detection |
| **NFC** | ST25DV04K-IER8C3 | UFDFPN8 | 2 × 3 | 0.85 | €1.20 | ISO 15693, 4Kbit |

## Power & Drivers

| Component | Part Number | Package | Dimensions (mm) | Height (mm) | Price @ 1k | Notes |
|-----------|-------------|---------|-----------------|-------------|------------|-------|
| **LDO** | MCP1700T-3302E/TT | SOT-23 | 2.9 × 1.3 | 1.1 | €0.30 | 3.3V regulator |
| **Haptic Driver** | DRV2605L | VQFN10 | 3 × 3 | 0.75 | €1.80 | TI haptic controller |
| **LRA Motor** | Jinlong G1040003D | Coin | Ø10 × 4.0 | 4.0 | €0.90 | 2.0 Grms (MAX vibration) |

## User Interface

| Component | Part Number | Package | Dimensions (mm) | Height (mm) | Price @ 1k | Notes |
|-----------|-------------|---------|-----------------|-------------|------------|-------|
| **RGB LED** | Everlight 19-337/R6GHBHC | 1616 | 1.6 × 1.6 | 0.8 | €0.15 | Common cathode |
| **Button** | Snaptron 4DT | Metal Dome | Ø4 | 0.3 | €0.10 | 180gf actuation |

## Batteries

| Component | Model | Dimensions (mm) | Capacity | Price @ 1k | Notes |
|-----------|-------|-----------------|----------|------------|-------|
| **Battery (2×)** | LP301020 | 3 × 10 × 20 | 50mAh each | €2.00 | 100mAh total, 3.7V LiPo |

---

## Component Placement Strategy

### TOP PCB Side (551mm², 99% utilization)
- **BG95-M3 cellular:** 13×15.8mm + 1mm clearance = 17×19.8mm zone
- **MAX-M10S GPS:** 9.7×10mm + 1mm clearance = 13.7×14mm zone
- **RGB LED:** 1.6×1.6mm (center)
- **Dome switch:** Ø4mm (center)
- **Passives:** Remaining space

### BOTTOM PCB Side (551mm², 30% utilization)

**<1mm tall (spread freely, ~73-83mm²):**
- TMP102 (0.6mm) - **on flex tail with PPG**
- DRV2605L (0.75mm)
- ST25DV04K (0.85mm)
- nRF52810 (0.9mm)
- Passives

**>1mm tall (10×11mm concentrated zone, 77.5% density):**
- W25Q32 (1.27mm) - 41.71mm²
- ST4SIM-200M (1.0mm) - 30.0mm²
- ADXL372 (1.0mm) - 9.75mm²
- MCP1700T (1.1mm) - 3.77mm²
- **Total:** 85.23mm² in 110mm² zone

**Flex tail (2.5mm below PCB):**
- MAX30102 (1.55mm) at 0.5mm from bottom (skin contact)
- TMP102 (0.6mm) at 0.5mm from bottom (body temp)

---

## Critical Component Notes

### ✅ Haptic Motor Isolation
- **G1040003D must NOT touch PCB**
- 2.0 Grms vibration will crack solder joints
- PCB has 11×11mm cutout for motor clearance
- Motor sits in 3mm layer, PCB at 5mm level

### ✅ PPG + Temperature Sensing
- Both on flex tail for direct skin contact
- Positioned 0.5mm from device bottom
- Through sapphire dome opening
- Flex tail: ~10×10mm, drops 2.5mm below main PCB

### ✅ RF Modules
- Built-in antennas (no external antenna routing)
- Require 1mm clearance around modules
- Sapphire windows provide RF transparency + IP67 seal
- No metal directly over antennas

### ✅ eSIM Correction
- Original BOM had STSAFE-J100 (WRONG - security chip, not eSIM!)
- Corrected to ST4SIM-200M (actual MFF2 eSIM)
- Enables carrier flexibility vs iSIM lock-in

---

## Rejected Alternatives

### BG770A-GL (iSIM combined module)
- ❌ Provider lock-in risk (unclear RSP support)
- ❌ Technology immaturity (2-3 years old)
- ❌ Unacceptable for life-saving medical device
- ✅ Would save €6/unit but too risky

### Capacitive Touch Button
- ❌ Fails when wet/gloves
- ❌ No tactile feedback
- ❌ Unacceptable for emergency medical device
- ✅ Dome switch chosen (waterproof, tactile, works with gloves)

### ST25DV04K UFDFPN12 (3×3mm)
- ❌ Larger footprint (9mm² vs 6.5mm² with resistor)
- ❌ More expensive
- ❌ Energy harvesting useless (NFC only during active scan)
- ✅ UFDFPN8 (2×3mm) chosen

---

## Total Component Footprint

**Absolute minimum (just ICs):** 552.7mm²
**With passives:** ~580mm²
**With routing overhead:** ~810mm²

**Available space:**
- Main PCB: 32×21mm = 672mm²
- Minus 11×11mm cutout = 551mm²
- Double-sided: 1102mm²

**Utilization: 815mm² / 1102mm² = 74% ✅**

---

**Last Verified:** November 4, 2025
**BOM Version:** v3
**Total Cost:** €78.65/unit @ 1000qty (electronics only)
