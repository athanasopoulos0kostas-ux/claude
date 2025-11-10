# Component Verification Checklist

**Date:** November 10, 2025
**Status:** VERIFICATION IN PROGRESS
**Method:** Manual datasheet verification (web access blocked)

---

## Verification Status Summary

| Component | Part Number | Verification Status | Priority |
|-----------|-------------|-------------------|----------|
| Cellular+GPS Module | BG600L-M3 | ❌ NOT VERIFIED | 🔴 CRITICAL |
| MCU | nRF52810-QFAA-R | ❌ NOT VERIFIED | 🔴 CRITICAL |
| PPG Sensor | MAX30102 | ❌ NOT VERIFIED | 🔴 CRITICAL |
| Battery | LP301020 | ❌ NOT VERIFIED | 🔴 CRITICAL |
| Temperature Sensor | TMP102 | ❌ NOT VERIFIED | 🟡 HIGH |
| Accelerometer | ADXL372 | ❌ NOT VERIFIED | 🟡 HIGH |
| Flash Memory | W25Q32JVZPIG | ❌ NOT VERIFIED | 🟡 HIGH |
| NFC Chip | ST25DV04K-IER8C3 | ❌ NOT VERIFIED | 🟡 HIGH |
| eSIM | ST4SIM-200M | ❌ NOT VERIFIED | 🟡 HIGH |
| Haptic Driver | DRV2605L | ❌ NOT VERIFIED | 🟢 MEDIUM |
| LDO Regulator | MCP1700T-3302E/TT | ❌ NOT VERIFIED | 🟢 MEDIUM |
| Charging IC | MCP73831T-2ACI/OT | ❌ NOT VERIFIED | 🟢 MEDIUM |
| Haptic Motor | Jinlong G1040003D | ❌ NOT VERIFIED | 🔴 CRITICAL |
| RGB LED | Everlight 19-337/R6GHBHC | ❌ NOT VERIFIED | 🟢 MEDIUM |
| Button | Snaptron 4DT | ❌ NOT VERIFIED | 🟢 MEDIUM |

---

## CRITICAL COMPONENTS (Must Verify First)

### 1. BG600L-M3 (Cellular + GPS Module)

**BOM Claims:**
- Dimensions: Unknown (NEEDS VERIFICATION)
- Features: LTE-M/NB-IoT + integrated GPS + 2G fallback
- Package: LCC (Land Grid Array)
- Power: Unknown

**What to Verify:**
- [ ] Exact dimensions: Length × Width × Height (mm)
- [ ] Package type and pin count
- [ ] **CRITICAL:** Does it actually have integrated GPS?
- [ ] **CRITICAL:** Does it support 2G/EGPRS fallback?
- [ ] Power consumption:
  - [ ] Peak TX (mA at 3.7V)
  - [ ] RX typical (mA)
  - [ ] PSM (Power Save Mode) current (µA)
  - [ ] GPS active current (mA)
- [ ] Operating voltage range
- [ ] Temperature range

**Where to Find:**
- Manufacturer: Quectel (quectel.com)
- Datasheet name: "BG600L-M3_Hardware_Design_V1.0.pdf" (typical naming)
- Look for: Section 1.3 (Product Overview), Section 2.1 (Dimensions)

**Critical Questions:**
1. **Does BG600L-M3 exist?** (or is it BG600L vs BG600L-M3 variant confusion?)
2. **Does it have integrated GPS or separate GPS module required?**
3. **Is 2G fallback actually supported in this variant?**

**Datasheet Pages to Check:**
- Page 1-5: Product overview and feature list
- Mechanical dimensions section: Exact L×W×H
- Power consumption section: All operating modes

---

### 2. nRF52810-QFAA-R (MCU)

**BOM Claims:**
- Dimensions: 6 × 6 × 0.85 mm
- Package: QFN48
- Flash: 192KB
- Previous BOM error: Was listed as 4×4mm (CORRECTED)

**What to Verify:**
- [ ] Exact dimensions: 6mm × 6mm × 0.85mm height?
- [ ] Package: QFN48 (48-pin QFN)?
- [ ] Flash: 192KB correct?
- [ ] RAM: ? KB
- [ ] Power consumption:
  - [ ] Active mode (CPU running) @ 3V
  - [ ] Sleep mode (all peripherals off)
  - [ ] Deep sleep
  - [ ] BLE TX/RX current
- [ ] Operating voltage: 1.7V - 3.6V?
- [ ] Temperature range: -40°C to +85°C?

**Where to Find:**
- Manufacturer: Nordic Semiconductor (nordicsemi.com)
- Datasheet: "nRF52810_PS_v1.4.pdf" (Product Specification)
- Look for: Section 6 (Electrical Specifications), Package drawings

**Critical Questions:**
1. **Is QFN48 package 6×6mm or different size?** (QFN packages vary!)
2. **Does it have sufficient Flash/RAM for our firmware?**

---

### 3. MAX30102 (PPG Sensor)

**BOM Claims:**
- Dimensions: 5.6 × 3.3 × 1.55 mm
- Package: OLGA14 (Optical LGA, 14-pin)
- Features: Heart rate + SpO2

**What to Verify:**
- [ ] Exact dimensions: 5.6 × 3.3 × 1.55 mm?
- [ ] Package: OLGA14 correct?
- [ ] Power consumption:
  - [ ] Active measurement (LED on) typical/max
  - [ ] Standby current
  - [ ] Shutdown current
- [ ] Operating voltage: 1.8V (I/O) + 3.3V (LED)?
- [ ] LED drive current capability
- [ ] Sample rate capabilities

**Where to Find:**
- Manufacturer: Maxim Integrated (now Analog Devices)
- Datasheet: "MAX30102.pdf"
- Look for: Package Information, Electrical Characteristics (Table 1)

**Critical Questions:**
1. **Power consumption at 20mA LED current** (affects battery life!)
2. **Dimensions correct?** (Previous BOM had errors)

---

### 4. LP301020 (Battery)

**BOM Claims:**
- Dimensions: 20 × 10 × 3.0 mm thick
- Capacity: 50mAh @ 3.7V
- Chemistry: Li-Po with PCM
- Quantity: 2× (100mAh total)
- **Previous error:** Was claimed 2mm thick (doesn't exist!)

**What to Verify:**
- [ ] **CRITICAL:** Does 3.0mm thick version exist at 50mAh?
- [ ] Actual dimensions: 20 × 10 × ? mm
- [ ] Capacity: 50mAh or different?
- [ ] With or without PCM (Protection Circuit Module)?
- [ ] Connector type: JST, solder pads, or wire leads?
- [ ] UN38.3 certification (required for shipping)
- [ ] Discharge rate: Continuous / Peak current

**Where to Find:**
- Multiple manufacturers make this form factor:
  - Search: "LP301020" on Alibaba, AliExpress
  - Battery Space, Power Stream, Shenzhen suppliers
- Look for: Product specification sheet, dimensions drawing

**Critical Questions:**
1. **Does 3mm thick battery exist, or is it 3.2mm, 3.5mm, etc?**
2. **Is 50mAh achievable at 3.0mm thickness?** (capacity vs thickness relationship)
3. **Are these readily available or custom order?**

**Alternative batteries to research:**
- LP321020 (3.2mm × 10 × 20mm) - might be more common
- LP351020 (3.5mm × 10 × 20mm)
- LP301030 (3.0mm × 10 × 30mm) - longer but same thickness

---

### 5. Jinlong G1040003D (Haptic Motor)

**BOM Claims:**
- Dimensions: Ø10mm × 4.0mm height
- Type: Coin LRA (Linear Resonant Actuator)
- Vibration: 2.0 Grms (maximum strength)
- **Previous error:** Part Z4LC1B0001781 didn't exist

**What to Verify:**
- [ ] Part number G1040003D actually exists?
- [ ] Dimensions: Ø10mm diameter × 4.0mm height?
- [ ] Vibration strength: 2.0 Grms confirmed?
- [ ] Operating voltage: 3.0V typical?
- [ ] Current draw: Peak / Typical (mA)
- [ ] Resonant frequency: ~175 Hz?
- [ ] Connection: Wire leads length and type

**Where to Find:**
- Manufacturer: Jinlong Machinery & Electronics
- Alternatives: Vybronics, Precision Microdrives
- Look for: Product catalog, specification sheet

**Critical Questions:**
1. **Does this specific part number exist?** (Last motor part didn't!)
2. **Is 2.0 Grms the actual rating?**
3. **Availability and lead time?**

---

## HIGH PRIORITY COMPONENTS

### 6. TMP102 (Temperature Sensor)

**BOM Claims:**
- Dimensions: 1.6 × 1.2 × 0.5 mm
- Package: SOT563
- Accuracy: ±0.5°C
- **Previous error:** Was listed as DSBGA package

**What to Verify:**
- [ ] Package SOT563: 1.6 × 1.2mm footprint correct?
- [ ] Height: 0.5mm or 0.6mm? (SOT563 typical height)
- [ ] Power consumption:
  - [ ] Active conversion current
  - [ ] Shutdown current (< 1µA?)
- [ ] I2C address options
- [ ] Conversion time

**Where to Find:**
- Manufacturer: Texas Instruments (ti.com)
- Datasheet: "TMP102.pdf"

---

### 7. ADXL372 (Accelerometer)

**BOM Claims:**
- Dimensions: 3 × 3.25 × 1.06 mm
- Package: LGA16 (16-pin Land Grid Array)
- Range: ±200g (high-g for fall detection)

**What to Verify:**
- [ ] Dimensions: 3 × 3.25 × 1.06 mm?
- [ ] Package: LGA16 correct?
- [ ] Measurement range: ±200g?
- [ ] Power consumption:
  - [ ] Active measurement
  - [ ] Standby
- [ ] Sample rate capabilities
- [ ] Interface: SPI or I2C?

**Where to Find:**
- Manufacturer: Analog Devices (analog.com)
- Datasheet: "ADXL372.pdf"

---

### 8. W25Q32JVZPIG (Flash Memory)

**BOM Claims:**
- Dimensions: 6 × 5 × 0.75 mm
- Package: WSON-8
- Capacity: 4MB (32Mbit)
- **Previous error:** Was SOIC-8 (1.75mm tall) → WSON-8 (0.75mm)

**What to Verify:**
- [ ] Package WSON-8: 6 × 5mm footprint?
- [ ] Height: 0.75mm correct?
- [ ] Capacity: 32Mbit / 4MB?
- [ ] Interface: SPI
- [ ] Power consumption:
  - [ ] Active read (mA)
  - [ ] Deep power-down (µA)
- [ ] Operating voltage: 2.7V - 3.6V?

**Where to Find:**
- Manufacturer: Winbond (winbond.com)
- Datasheet: "W25Q32JV.pdf"
- Look for: Package drawings (WSON-8 6x5mm section)

**Critical Questions:**
1. **Is WSON-8 actually 0.75mm tall?** (Package height critical for our 1mm budget!)

---

### 9. ST25DV04K-IER8C3 (NFC Chip)

**BOM Claims:**
- Dimensions: 2 × 3 × 0.6 mm
- Package: UFDFPN8 (8-pin, ultra-thin)
- Capacity: 4Kbit EEPROM
- **Previous error:** Was UFDFPN12 (3×3mm) variant

**What to Verify:**
- [ ] Package UFDFPN8: 2 × 3mm correct?
- [ ] Height: 0.6mm or 0.85mm? (Different sources show different)
- [ ] Part number suffix "-IER8C3" correct?
- [ ] Features: I2C + NFC + GPO pin
- [ ] GPO output type: Open-drain (needs pull-up resistor)
- [ ] Power consumption

**Where to Find:**
- Manufacturer: STMicroelectronics (st.com)
- Datasheet: "ST25DV04K.pdf"
- Look for: Package information (UFDFPN8 vs UFDFPN12)

---

### 10. ST4SIM-200M (eSIM Chip)

**BOM Claims:**
- Dimensions: 5 × 6 × 0.75 mm
- Package: MFF2 (Machine Form Factor 2)
- Type: eUICC eSIM
- **Previous error:** BOM had STSAFE-J100 (security chip, NOT eSIM!)

**What to Verify:**
- [ ] Part number ST4SIM-200M correct?
- [ ] Package MFF2: 5 × 6mm?
- [ ] Height: 0.75mm or 1.0mm?
- [ ] Is this an eSIM or eUICC chip?
- [ ] GSMA RSP (Remote SIM Provisioning) support?
- [ ] Carrier compatibility
- [ ] Interface: SPI, I2C, or ISO 7816?

**Where to Find:**
- Manufacturer: STMicroelectronics (st.com)
- Datasheet: "ST4SIM-200M.pdf"

**Critical Questions:**
1. **Does ST4SIM-200M exist?** (STM makes secure elements, but is this an actual eSIM chip?)
2. **Is this the correct part for eSIM functionality?**

**Alternative eSIM chips to research:**
- Infineon SLM97
- G+D eUICC
- Thales/Gemalto eSIM solutions

---

## MEDIUM PRIORITY COMPONENTS

### 11. DRV2605L (Haptic Driver)

**BOM Claims:**
- Dimensions: 3 × 3 × 0.75 mm
- Package: VQFN10

**What to Verify:**
- [ ] Dimensions correct?
- [ ] Power consumption
- [ ] Drive capabilities for 2.0 Grms motor

**Where to Find:**
- Manufacturer: Texas Instruments
- Datasheet: "DRV2605L.pdf"

---

### 12. MCP1700T-3302E/TT (LDO Regulator)

**BOM Claims:**
- Dimensions: 2.9 × 1.3 × 0.95 mm
- Package: SOT-23 (3-pin)
- Output: 3.3V, 250mA
- **Previous error:** Was /TO variant (through-hole)

**What to Verify:**
- [ ] Package SOT-23: Dimensions correct?
- [ ] Suffix "/TT" = SOT-23 SMD variant?
- [ ] Output: 3.3V ±2%?
- [ ] Max current: 250mA?
- [ ] Dropout voltage
- [ ] Quiescent current

**Where to Find:**
- Manufacturer: Microchip
- Datasheet: "MCP1700.pdf"

---

### 13. MCP73831T-2ACI/OT (Charging IC)

**BOM Claims:**
- Dimensions: 3.1 × 1.8 × 1.3 mm
- Package: SOT-23-5 (5-pin)
- Charge current: 500mA

**What to Verify:**
- [ ] Dimensions correct?
- [ ] Package SOT-23-5?
- [ ] Max charge current: 500mA?
- [ ] Termination voltage: 4.2V?
- [ ] Power consumption

**Where to Find:**
- Manufacturer: Microchip
- Datasheet: "MCP73831.pdf"

---

### 14. Everlight 19-337/R6GHBHC-M01/2T (RGB LED)

**BOM Claims:**
- Dimensions: 1.6 × 1.6 × 0.8 mm
- Package: 1616 (0603 metric)
- Type: Common cathode RGB

**What to Verify:**
- [ ] Part number correct?
- [ ] Dimensions: 1.6 × 1.6 × 0.8mm?
- [ ] Common cathode configuration?
- [ ] Forward voltage: R/G/B channels
- [ ] Forward current: Max per channel
- [ ] Wavelengths: R (~620nm), G (~515nm), B (~455nm)?

**Where to Find:**
- Manufacturer: Everlight
- Datasheet: Search "19-337/R6GHBHC-M01/2T"

---

### 15. Snaptron 4DT (Metal Dome Switch)

**BOM Claims:**
- Dimensions: Ø4mm × 0.3mm height
- Type: Metal dome (tactile)
- Actuation force: 180gf

**What to Verify:**
- [ ] Part series "4DT" correct?
- [ ] Diameter: 4mm?
- [ ] Height/travel: 0.3mm?
- [ ] Actuation force: 180gf?
- [ ] Life cycles: Millions of actuations?
- [ ] Contact resistance

**Where to Find:**
- Manufacturer: Snaptron
- Datasheet/Catalog: "Snaptron 4DT Series.pdf"

---

## VERIFICATION PROCEDURE

### For Each Component:

1. **Find Official Datasheet**
   - Manufacturer website
   - Distributor sites (Mouser, DigiKey, Arrow)
   - Component databases

2. **Extract Critical Specs:**
   - Dimensions (L × W × H in mm) - from mechanical drawing
   - Package type - from package section
   - Electrical specs - from electrical characteristics table
   - Power consumption - from typical/max current tables

3. **Cross-Reference:**
   - Compare datasheet specs against BOM claims
   - Flag any discrepancies
   - Note if dimension differs by >0.1mm
   - Note if power consumption significantly different

4. **Document Results:**
   - Mark component as ✅ VERIFIED or ❌ DISCREPANCY FOUND
   - Note datasheet version/date
   - Add comments for any concerns

5. **Update Verification Status Table** (at top of this document)

---

## KNOWN ISSUES FROM PREVIOUS BOM VERSIONS

These were already caught and corrected, but verify the corrections are accurate:

1. ❌ **nRF52810:** Was 4×4mm → Corrected to 6×6mm (QFN48)
2. ❌ **MAX-M10S GPS:** Was 12×16mm → Corrected to 9.7×10mm
   **(NOTE: MAX-M10S removed in favor of BG600L-M3 integrated GPS!)**
3. ❌ **TMP102:** Was DSBGA → Corrected to SOT563
4. ❌ **W25Q32:** Was SOIC-8 (1.75mm tall) → WSON-8 (0.75mm)
5. ❌ **LP301020 Battery:** Was 2mm thick → Corrected to 3mm
6. ❌ **STSAFE-J100:** Was eSIM chip → Corrected to ST4SIM-200M (actual eSIM)
7. ❌ **MCP1700-3302E/TO:** Was through-hole → Corrected to /TT (SMD)
8. ❌ **Jinlong Z4LC1B0001781:** Part didn't exist → G1040003D
9. ❌ **ST25DV04K:** Was UFDFPN12 (3×3mm) → UFDFPN8 (2×3mm)

**Verify these corrections are actually accurate!**

---

## CRITICAL VERIFICATION QUESTIONS

Answer these after completing verification:

### Module Selection:
- [ ] Does BG600L-M3 actually integrate GPS + Cellular + 2G fallback?
- [ ] Or do we need BG95-M3 + MAX-M10S (separate modules)?
- [ ] What is the ACTUAL size of chosen module(s)?

### Height Budget:
- [ ] W25Q32 WSON-8: Is it really 0.75mm tall? (Critical for 1mm budget!)
- [ ] ST25DV04K UFDFPN8: Is it 0.6mm or 0.85mm tall?
- [ ] All components under 1mm confirmed?

### Battery Reality:
- [ ] LP301020 at 3.0mm thick: Does it exist?
- [ ] If not, what alternatives at 3.0-3.2mm thick?

### Power Budget:
- [ ] MAX30102 PPG: Actual current at 20mA LED drive?
- [ ] BG600L-M3: Power consumption in all modes?
- [ ] Total system current: Does 100mAh give 7-10 days?

### Part Availability:
- [ ] Are all parts actually purchasable?
- [ ] Lead times acceptable?
- [ ] Any obsolescence issues?

---

## NEXT STEPS AFTER VERIFICATION

1. **Update BOM v3** with verified specs
2. **Create discrepancy report** if dimensions differ
3. **Recalculate PCB layout** with verified dimensions
4. **Recalculate power budget** with verified consumption
5. **Recalculate device height** with verified component heights
6. **Flag any components that need alternatives**

---

**Verification Started:** 2025-11-10
**Verification Completed:** TBD
**Verified By:** Manual datasheet review
**Reviewed By:** TBD
