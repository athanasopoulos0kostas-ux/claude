# PCB Bottom Component Fit Verification

**Date:** November 10, 2025
**Purpose:** Verify ALL components fit in PCB bottom with height restrictions

---

## PCB Bottom Available Area Analysis

**Total PCB area:** 32×21mm = 672mm²

**Subtract BG600L-M3 footprint (occupies separate layer below):**
- BG600L-M3: 18.7×16mm = 299.2mm²
- **Remaining PCB bottom surface:** 672 - 299.2 = **372.8mm²**

---

## Height Zones on PCB Bottom

Due to components in the layer below PCB, height budget varies:

### Zone 1: Above Motor (100mm²)
- **Location:** 10×10mm area where motor sits below
- **Height available:** 1.0mm only
  - Motor intrudes 4mm into 3mm battery layer
  - Leaves only 1mm clearance in 2.4mm module layer
  - PCB bottom components here limited to ≤1mm tall

### Zone 2: Above BG600L-M3 Module (299mm²)
- **Location:** 18.7×16mm footprint
- **Height available:** 0mm (module occupies this)
- **NO COMPONENTS ALLOWED** (module in separate layer below)

### Zone 3: Remaining Area (~273mm²)
- **Location:** Rest of PCB bottom
- **Height available:** Full 2.4mm
- **Can place any component** up to 2.4mm tall

---

## Component Inventory - PCB BOTTOM ONLY

### Major ICs on PCB Bottom

| Component | Part Number | Dimensions (L×W×H mm) | Footprint (mm²) | Height (mm) | Zone Assignment |
|-----------|-------------|----------------------|-----------------|-------------|-----------------|
| MCU | nRF52810-QFAA-R | 6×6×0.85 | 36.0 | 0.85 | Zone 1 or 3 ✅ |
| eSIM | ST4SIM-200M | 5×6×0.75 | 30.0 | 0.75 | Zone 1 or 3 ✅ |
| Accelerometer | ADXL372 | 3×3.25×1.06 | 9.75 | 1.06 | **Zone 3 only** ⚠️ |
| LDO | MCP1700T-3302E/TT | 2.9×1.3×0.95 | 3.77 | 0.95 | Zone 1 or 3 ✅ |
| Charger | MCP73831T-2ACI/OT | 3.1×1.8×1.3 | 5.58 | 1.3 | **Zone 3 only** ⚠️ |
| NFC | ST25DV04K-IER8C3 | 2×3×0.6 | 6.0 | 0.6 | Zone 1 or 3 ✅ |
| Haptic Driver | DRV2605L | 3×3×0.75 | 9.0 | 0.75 | Zone 1 or 3 ✅ |
| Flash | W25Q32JVZPIG | 6×5×0.75 | 30.0 | 0.75 | Zone 1 or 3 ✅ |

**Subtotal ICs:** 130.1mm²

---

### Passives on PCB Bottom

| Component | Qty | Package | Dimensions (mm) | Footprint Each | Total Footprint | Height | Notes |
|-----------|-----|---------|-----------------|----------------|-----------------|--------|-------|
| Decoupling caps (0.1µF) | 8 | 0402 | 1.0×0.5×0.5 | 0.5mm² | 4.0mm² | 0.5mm | Near every IC VDD |
| Bulk caps (10µF) | 3 | 0805 | 2.0×1.25×0.6 | 2.5mm² | 7.5mm² | 0.6mm | Power supply |
| I2C pull-ups (4.7kΩ) | 2 | 0402 | 1.0×0.5×0.35 | 0.5mm² | 1.0mm² | 0.35mm | SDA/SCL |
| NFC pull-up (10kΩ) | 1 | 0402 | 1.0×0.5×0.35 | 0.5mm² | 0.5mm² | 0.35mm | GPO line |
| Misc resistors | 5 | 0402 | 1.0×0.5×0.35 | 0.5mm² | 2.5mm² | 0.35mm | Various |
| RTC crystal | 1 | 3215 | 3.2×1.5×0.8 | 4.8mm² | 4.8mm² | 0.8mm | 32.768kHz |
| Crystal load caps | 2 | 0402 | 1.0×0.5×0.5 | 0.5mm² | 1.0mm² | 0.5mm | Matching network |
| Schottky diode | 1 | SOD-323 | 1.7×1.25×1.17 | 2.125mm² | 2.125mm² | 1.17mm | **Zone 3 only** ⚠️ |
| RGB LED resistors | 3 | 0402 | 1.0×0.5×0.35 | 0.5mm² | 1.5mm² | 0.35mm | Current limiting |

**Subtotal Passives:** 24.925mm²

---

### Connectors on PCB Bottom

| Component | Qty | Type | Estimated Footprint Each | Total Footprint | Height | Notes |
|-----------|-----|------|-------------------------|-----------------|--------|-------|
| Battery connectors | 2 | JST SH 1.0mm 2-pin SMD | **~4.5×2.5mm = 11.25mm²** | **22.5mm²** | **~3.0mm** ⚠️ | **CRITICAL - CHECK THIS!** |
| Pogo pins (charging) | 2 | Mill-Max spring contacts | **~Ø2mm pads = 3.14mm²** | **6.28mm²** | **~5mm** ⚠️ | **Through-hole or SMD?** |

**Subtotal Connectors:** 28.78mm²

---

## 🔴 COMPONENTS NOT ON PCB BOTTOM (ACCOUNTED SEPARATELY)

- **MAX30102 (PPG):** On flex tail, not main PCB
- **TMP102 (temp):** On flex tail, not main PCB
- **RGB LED:** Side-mounted on housing edge
- **Button (dome switch):** Side-mounted on housing edge
- **BG600L-M3 module:** Separate layer below PCB
- **Haptic motor:** Separate layer, not mounted on PCB
- **Batteries (2×):** Separate layer

---

## Total Component Footprint - PCB Bottom

| Category | Footprint (mm²) |
|----------|-----------------|
| Major ICs | 130.1 |
| Passives | 24.9 |
| Connectors | 28.8 |
| **SUBTOTAL (bare minimum)** | **183.8mm²** |

---

## 🔴 MISSING FACTORS - WHAT WE HAVEN'T ACCOUNTED FOR

### 1. Routing Space Between Components
- **Traces:** Need space for SPI, I2C, UART, power rails
- **Vias:** Each via ~0.3mm diameter, need hundreds
- **Clearance:** Minimum 0.2mm between traces
- **Estimated routing overhead:** +30-50% of component footprint
- **Conservative estimate:** +55mm² (30% overhead)

### 2. Component Keepout Zones
- **nRF52810 antenna:** Needs ~5mm keepout for BLE antenna matching
- **ST25DV04K NFC:** Needs keepout for antenna coil area
- **Crystal oscillator:** Needs ground plane isolation
- **Estimated keepout overhead:** +15-20mm²

### 3. Decoupling Capacitor Placement
- **Requirement:** Decoupling caps must be VERY close to IC VDD pins
- **Reality:** Each 0402 cap needs ~1.5×1mm space (with trace approach)
- **8 caps × 1.5mm² = 12mm² actual usage** (vs 4mm² bare footprint)
- **Additional space needed:** +8mm²

### 4. Test Points & Debug Pads
- **SWDIO/SWCLK:** For nRF52810 programming (2× pads)
- **UART TX/RX:** For debugging (2× pads)
- **Power test points:** GND, 3.7V, 3.3V (3× pads)
- **Estimated:** +5-8mm²

### 5. Connector Actual Dimensions (CRITICAL UNKNOWN!)
- **JST SH connectors:** I estimated 4.5×2.5mm, but need verification
- **Pogo pins:** Need PCB pad + surrounding clearance
- **Potential error:** ±10-20mm² if connectors are larger

### 6. Manufacturing Tolerances
- **Component placement tolerance:** ±0.1mm
- **PCB edge clearance:** Need ~1mm from PCB edge
- **Screw holes (if any):** Need clearance zones
- **Estimated:** +10-15mm²

---

## Revised Total with Overhead

| Item | Footprint (mm²) |
|------|-----------------|
| Bare components | 183.8 |
| Routing overhead (+30%) | +55.0 |
| Keepout zones | +15.0 |
| Decoupling spacing | +8.0 |
| Test points | +6.0 |
| Manufacturing tolerance | +12.0 |
| **REVISED TOTAL** | **279.8mm²** |

**Available space:** 372.8mm²
**Needed space:** 279.8mm²
**Utilization:** 75%

---

## 🔴 CRITICAL UNKNOWNS THAT COULD BREAK THE FIT

### 1. JST SH Battery Connector Dimensions
- **Assumed:** 4.5×2.5mm SMD footprint
- **Need to verify:** Actual PCB footprint from datasheet
- **Risk:** Could be 6×4mm = 24mm² each → +14mm² total

### 2. Pogo Pin PCB Footprint
- **Assumed:** Ø2mm pads
- **Need to verify:** Mill-Max 0929-7-15-20-77-14-11-0 PCB mounting
- **Risk:** Through-hole could need larger clearance

### 3. Component Height in Zone 1 (1mm limit)
- **Components that MUST fit in Zone 1:**
  - Only components ≤1mm tall
- **Problem:** Only 100mm² available in Zone 1
- **Need in Zone 1:** All components ≤1mm (nRF52810, eSIM, Flash, NFC, Haptic Driver, LDO, most passives)
- **Calculation needed:** Do all ≤1mm components fit in 100mm²?

---

## 🔴 ZONE-SPECIFIC PLACEMENT CHECK

### Zone 1: Above Motor (100mm² available, 1mm height limit)

**Components ≤1mm tall:**
- nRF52810: 36mm² (0.85mm)
- ST4SIM-200M: 30mm² (0.75mm)
- Flash W25Q32: 30mm² (0.75mm)
- Haptic Driver: 9mm² (0.75mm)
- NFC: 6mm² (0.6mm)
- LDO: 3.77mm² (0.95mm)
- All passives except diode: ~23mm² (all <1mm)

**Subtotal ≤1mm components:** 137.77mm² **→ DOES NOT FIT IN 100mm²!** ❌

---

## 🚨 CRITICAL ISSUE IDENTIFIED

**PROBLEM:** We have 137.77mm² of components that are ≤1mm tall, but:
- Zone 1 (1mm height): Only 100mm² available
- Zone 3 (2.4mm height): 273mm² available

**SOLUTION NEEDED:**
- **Option 1:** Move motor to edge so it doesn't create 1mm restriction
- **Option 2:** Accept that some ≤1mm components go in Zone 3 (wastes height budget but works)
- **Option 3:** Shrink motor diameter or change motor placement

**USER'S CONCERN WAS VALID!** We missed the zone restriction conflict.

---

## What We Actually Missed

1. ✅ **Routing overhead:** ~30-50% additional space needed
2. ✅ **Connector dimensions:** JST SH and pogo pins need verification
3. ✅ **Decoupling cap placement:** Need space around ICs, not just bare footprint
4. ✅ **Zone 1 restriction:** 137.77mm² of ≤1mm components can't fit in 100mm² Zone 1
5. ⚠️ **Test points and debug pads:** Add ~6mm²
6. ⚠️ **Manufacturing tolerances:** Need edge clearance

---

## Recommendation

**WE NEED TO:**
1. Verify JST SH connector and pogo pin PCB footprints
2. Decide motor placement strategy to minimize Zone 1 restriction
3. Calculate exact routing space needed
4. Create detailed PCB layout plan with component placement priorities

**Current assessment:** Likely still fits, but with **75-80% utilization** (not 50% as initially calculated). Tight but feasible.

**USER WAS RIGHT TO BE SKEPTICAL!** ✅
