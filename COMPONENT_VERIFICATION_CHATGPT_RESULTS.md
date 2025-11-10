# Component Verification Report - ChatGPT Deep Search Results

**Date:** November 10, 2025
**Source:** ChatGPT deep search (aggregated from manufacturer datasheets and distributor pages)
**Confidence Level:** ⚠️ PRELIMINARY - Awaiting direct datasheet confirmation
**Status:** 15 components researched, multiple critical issues identified

---

## Executive Summary

### 🚨 CRITICAL FINDINGS:

1. **BG600L-M3 EXISTS** ✅ - Module confirmed: 18.7 × 16 × 2.1mm
2. **HEIGHT CRISIS** 🔴 - Multiple components exceed 1mm budget:
   - BG600L-M3: 2.1mm (110% over budget!)
   - MAX30102: 1.55mm (55% over)
   - ADXL372: 1.06mm (6% over)
   - MCP73831: 1.3mm (30% over)
3. **Battery thickness variance** ⚠️ - LP301020: 3.0-3.2mm depending on PCM/wires
4. **Package variant confusion** ⚠️ - Multiple parts have variant suffixes that matter

---

## MAJOR ICs - VERIFIED SPECIFICATIONS

### 1. nRF52810-QFAA-R (MCU/BLE)

**Verification Status:** ✅ CONFIRMED from Mouser/Nordic

**Verified Dimensions:**
- Length × Width: 6.0 × 6.0mm
- Height: Variable (QFN body thickness vendor-dependent)
- **Package:** QFN48 (48-pin, surface mount)

**Critical Notes:**
- ⚠️ Nordic also offers CSP variants with different PN - don't confuse QFN (QFAA-R) with CSP
- ⚠️ QFN body + solder + PCB stack needs clearance check for 1mm budget
- ✅ Package type confirmed: QFN, not CSP

**Height Budget Impact:**
- Typical QFN48 body: ~0.85-0.9mm
- With solder joints: ~1.0mm total
- **Status:** ⚠️ MARGINAL - Right at 1mm limit

**Source:** Mouser product page + Nordic Semiconductor product docs

---

### 2. Quectel BG600L-M3 (Cellular + GPS Module)

**Verification Status:** ✅ CONFIRMED from Quectel datasheets

**Verified Dimensions:**
- Length × Width × Height: **18.7 × 16.0 × 2.1mm**
- **Package:** SMT module with castellated pads (not bare die)

**Critical Notes:**
- ✅ **Module EXISTS** (not a phantom part!)
- ✅ **Integrated GNSS confirmed** (Quectel spec mentions GNSS)
- ✅ **LTE-M / NB-IoT + EGPRS fallback confirmed**
- 🚨 **HEIGHT PROBLEM:** 2.1mm will NOT fit 1mm budget (110% over!)
- ⚠️ Requires antenna clearance and keepouts
- ⚠️ Module is thicker than bare ICs - includes antenna matching

**Height Budget Impact:**
- Module height: 2.1mm
- **Status:** 🔴 CRITICAL FAILURE - Exceeds budget by 1.1mm

**Design Implications:**
- Cannot place on same layer as components with 1mm budget
- Needs dedicated recess or separate mounting strategy
- May require PCB cutout or module on opposite side

**Source:** Quectel product page + hardware design docs + FCC filings

---

### 3. ST4SIM-200M (eSIM eUICC)

**Verification Status:** ⚠️ PARTIAL - Exists but with caveats

**Verified Dimensions:**
- Package outline: ~5 × 6mm (VFDFPN8 / MFF2 form factor)
- Height: Not specified in search results (need datasheet)
- **Package:** VFDFPN8 (very thin FPN) / MFF2 micro UICC format

**Critical Notes:**
- ✅ **This IS a real STMicro eSIM SoC** (ST4SIM family confirmed)
- 🚨 **Obsolescence concern:** Some distributor listings show certain PNs obsolete
- ⚠️ **Stock verification needed:** Confirm exact available PN before committing
- ✅ Designed for eSIM use (proper eUICC chip)

**Height Budget Impact:**
- Typical MFF2: ~0.6-0.9mm
- **Status:** ⚠️ LIKELY OK - Needs datasheet confirmation

**Action Required:**
- Verify current stock availability
- Confirm exact PN variant not obsolete
- Get mechanical drawing for height

**Source:** STMicroelectronics product brief + distributor listings

---

### 4. Maxim MAX30102 (PPG Sensor)

**Verification Status:** ✅ CONFIRMED from Analog Devices

**Verified Dimensions:**
- Length × Width × Height: **~5.6 × 3.3 × 1.55mm**
- **Package:** 14-pin optical module (includes LEDs + photodetector + cover glass)

**Critical Notes:**
- ✅ Integrated optical module (not bare die)
- ⚠️ LED drive at 20mA: Note power consumption and heat
- ⚠️ LED supply: 3.3V domain typical
- 🚨 **HEIGHT PROBLEM:** 1.55mm exceeds 1mm budget by 55%
- ⚠️ Optical window alignment with sapphire required
- ⚠️ Window thickness affects sensor distance to skin

**Height Budget Impact:**
- Module height: 1.55mm
- **Status:** 🔴 EXCEEDS BUDGET by 0.55mm

**Power Notes:**
- Datasheet specifies LED forward current limits
- Typical power per LED at 20mA drive needs verification
- Heat dissipation considerations for enclosed design

**Design Implications:**
- Requires flex tail or PCB recess
- Cannot be on same plane as 1mm budget components
- Optical alignment critical

**Source:** Analog Devices (Maxim acquired by ADI) datasheet

---

### 5. TMP102 (Temperature Sensor)

**Verification Status:** ✅ CONFIRMED from TI

**Verified Dimensions:**
- Length × Width: 1.6 × 1.6mm (note: square, not 1.6 × 1.2mm as BOM claimed!)
- Height: **~0.6mm typical**
- **Package:** SOT-563 (very small SMD)

**Critical Notes:**
- 🚨 **DIMENSION ERROR:** BOM claimed 1.6 × 1.2mm, actual is 1.6 × 1.6mm (square!)
- ✅ Supply: 1.4–3.6V
- ✅ Quiescent current: µA range (very low power)
- ✅ **Height OK:** 0.6mm fits 1mm budget with margin

**Height Budget Impact:**
- Height: 0.6mm
- **Status:** ✅ FITS - 0.4mm margin remaining

**Source:** Texas Instruments datasheet

---

### 6. ADXL372 (Accelerometer)

**Verification Status:** ✅ CONFIRMED from Analog Devices

**Verified Dimensions:**
- Length × Width × Height: **3.00 × 3.25 × 1.06mm**
- **Package:** LGA16 (16-pin Land Grid Array)

**Critical Notes:**
- ✅ Ultra-low power high-g accelerometer
- ✅ Datasheet lists supply range and current specs
- 🚨 **HEIGHT PROBLEM:** 1.06mm exceeds 1mm budget by 6%
- ⚠️ May fit with tight tolerances, but no margin

**Height Budget Impact:**
- Height: 1.06mm
- **Status:** ⚠️ MARGINAL - 0.06mm over budget (very tight!)

**Source:** Analog Devices datasheet

---

### 7. MCP1700T-3302E/TT (3.3V LDO)

**Verification Status:** ✅ CONFIRMED from Microchip

**Verified Dimensions:**
- Package: SOT-23-3 (TO-236)
- Dimensions: **~2.9 × 1.3 × 0.95mm**
- Height: 0.95mm

**Critical Notes:**
- ✅ 250mA LDO regulator
- ✅ Quiescent current: few µA
- ✅ **Height OK:** 0.95mm fits 1mm budget
- ✅ /TT suffix confirmed as SMD SOT-23 variant

**Height Budget Impact:**
- Height: 0.95mm
- **Status:** ✅ FITS - 0.05mm margin

**Source:** Mouser product page + Microchip datasheet

---

### 8. MCP73831T-2ACI/OT (Li-Poly Charger)

**Verification Status:** ✅ CONFIRMED from Microchip

**Verified Dimensions:**
- Package: SOT-23-5 (or DFN option available)
- SOT-23 variant: **~3.1 × 1.8 × 1.3mm**
- Height: 1.3mm (SOT-23 variant)

**Critical Notes:**
- ✅ Charge current up to 500mA (variant dependent)
- 🚨 **HEIGHT PROBLEM:** 1.3mm exceeds 1mm budget by 30%
- ✅ **DFN option exists:** Lower profile alternative available
- ⚠️ Check DFN mechanical drawing for exact thickness

**Height Budget Impact:**
- SOT-23 height: 1.3mm
- **Status:** 🔴 EXCEEDS BUDGET by 0.3mm

**Alternative:**
- DFN package may be lower profile
- Need to verify DFN variant height

**Source:** Mouser product page + Microchip datasheet

---

### 9. ST25DV04K-IER8C3 (NFC / I2C EEPROM)

**Verification Status:** ⚠️ PARTIAL - Multiple package variants exist

**Verified Dimensions:**
- UFDFPN8 variant: **~2.0 × 3.0mm** (from mechanical outline)
- Height: Not specified in search results
- **Package:** UFDFPN8 (8-pin ultra-thin FPN)

**Critical Notes:**
- ⚠️ **Multiple variants exist:**
  - UFDFPN8 (8-pin): 2.0 × 3.0mm
  - UFDFPN12 (12-pin): 3.0 × 3.0mm
  - TSSOP/SO8: Larger packages
  - WLCSP: Wafer-level chip scale
- 🚨 **BOM suffix MUST MATCH intended package**
- ⚠️ Different variants have different heights (0.6mm vs 0.85mm)
- ✅ Part family exists and is available

**Height Budget Impact:**
- UFDFPN8: Likely 0.6-0.85mm
- **Status:** ⚠️ NEEDS CLARIFICATION - Which variant?

**Action Required:**
- Confirm exact package suffix (-IER8C3 = which variant?)
- Get mechanical drawing for chosen variant
- Verify height specification

**Source:** STMicroelectronics datasheet (ST25DV family)

---

### 10. DRV2605L (Haptic Driver)

**Verification Status:** ⚠️ PARTIAL - Multiple package options

**Verified Dimensions:**
- Package options: VQFN, VSSOP variants
- Height: Varies by package (not specified in search)

**Critical Notes:**
- ✅ Supports both LRA and ERM motors
- ✅ Can drive 2.0 Grms LRA **if motor specs match driver capability**
- ⚠️ Must confirm motor impedance matches driver recommendations
- ⚠️ Must verify LRA parameters compatibility
- ⚠️ Package height depends on variant chosen

**Height Budget Impact:**
- Typical VQFN: 0.75-0.9mm
- **Status:** ⚠️ LIKELY OK - Needs package confirmation

**Action Required:**
- Choose exact package variant
- Verify Jinlong G1040003D motor electrical specs
- Confirm driver can handle motor parameters

**Source:** Texas Instruments datasheet

---

### 11. Winbond W25Q32JVZPIG (4MB SPI NOR Flash)

**Verification Status:** ⚠️ PARTIAL - Multiple package options

**Verified Dimensions:**
- WSON-8 family: 6 × 5mm variants available
- Height: **~0.75mm** (WSON8 variants)
- **Package:** WSON-8 (8-lead, no leads)

**Critical Notes:**
- ✅ WSON8 at 0.75mm body height likely fits 1mm budget
- ⚠️ **Part suffix matters:** W25Q32JVZPIG vs other suffixes
- ⚠️ Confirm exact suffix maps to WSON-8 package
- ⚠️ Recommended land pattern needed for assembly

**Height Budget Impact:**
- WSON-8 height: 0.75mm
- **Status:** ✅ LIKELY FITS - 0.25mm margin

**Action Required:**
- Verify suffix JVZPIG = WSON-8 package
- Get mechanical drawing
- Confirm land pattern

**Source:** Winbond datasheet

---

## POWER COMPONENTS

### 12. LP301020 (Li-Poly Battery, 50mAh)

**Verification Status:** ⚠️ CONFIRMED with variance

**Verified Dimensions:**
- Nominal: **20 × 10 × 3.0mm** (many vendors list this)
- With PCM/wires: **3.1–3.2mm** (actual pack thickness)

**Critical Notes:**
- 🚨 **THICKNESS VARIANCE:** 3.0mm nominal, but 3.1-3.2mm with PCM/wires
- ⚠️ If enclosure clearance is exactly 3.0mm, this is TIGHT
- ⚠️ Must confirm with actual supplier
- ✅ 50mAh capacity at this size appears standard
- ⚠️ Request mechanical drawing from battery supplier

**Design Impact:**
- Nominal: 3.0mm
- Actual with PCM: 3.1-3.2mm
- **Status:** ⚠️ VERIFY CLEARANCE - May be 0.1-0.2mm larger than expected

**Action Required:**
- Get battery supplier mechanical drawing
- Measure actual samples before finalizing enclosure
- Confirm PCM board thickness included

**Source:** Multiple battery vendors (LiPoly Battery, etc.)

---

### 13. JST SH 1.0mm 2-pin (Battery Connector)

**Verification Status:** ⚠️ NEEDS CLARIFICATION

**Critical Notes:**
- ⚠️ **JST SH family is 1.0mm pitch** (e.g., JST SHR- or SYP variants)
- 🚨 **Ambiguous PN:** Need exact JST part number (S06B? S1B-PH?)
- ⚠️ Board-mount SMT or vertical through-hole? (Different footprints!)
- ⚠️ Orientation matters for connector direction

**Action Required:**
- Specify exact JST PN (e.g., S2B-SH-K or SM02B-SRSS-TB)
- Confirm SMT vs through-hole
- Get datasheet for outline dimensions

**Source:** JST connector catalogs

---

### 14. Mill-Max 0929-7-15-20-77-14-11-0 (Pogo Pins)

**Verification Status:** ⚠️ PARTIAL from Mill-Max specs

**Verified Dimensions:**
- Plunger diameter: ~1.07mm
- Mounting hole: ~0.737mm
- Working height: Varies by variant (e.g., 7.94mm for some)

**Critical Notes:**
- ✅ Mill-Max 0929 series exists
- ⚠️ **Exact suffix determines specifications:**
  - Working height
  - Current rating
  - Travel distance
- ⚠️ Must match exact PN to get correct specs
- ⚠️ Rated contact force and travel in datasheet

**Action Required:**
- Verify exact 0929 variant suffix
- Confirm working height matches design
- Verify current rating (1.5A claimed)

**Source:** Mill-Max product catalog

---

### 15. Jinlong G1040003D (LRA Haptic Motor)

**Verification Status:** ⚠️ PARTIAL - Variant confusion

**Verified Dimensions:**
- Diameter × Height: **∅10 × 4.0mm** (typical 10mm LRA coin motors)

**Critical Notes:**
- ⚠️ **Variant naming confusion:** G1040003D vs VG1040003D
- ⚠️ Typical Grms: **1.5–2.5 depending on vendor/test conditions**
- 🚨 **2.0 Grms claim needs verification** from manufacturer spec
- ⚠️ Many distributors list VG1040003D (note "V" prefix)
- ⚠️ Vendor-specific datasheet required

**Action Required:**
- Confirm exact part number (G1040003D vs VG1040003D)
- Get manufacturer datasheet for Grms rating at rated voltage
- Verify this specific PN exists and is purchasable

**Source:** SparkFun / various distributors

---

### 16. Snaptron 4DT Series (Metal Dome Switch)

**Verification Status:** ✅ CONFIRMED

**Verified Dimensions:**
- Diameter × Thickness: **∅4mm × ~0.3mm**
- **Type:** 4mm metal dome (Snaptron 4DT series)

**Critical Notes:**
- ✅ Standard 4mm metal dome product line
- ✅ Datasheet lists actuation force, travel, thickness
- ⚠️ Confirm exact variant for force specification (varies within series)
- ✅ Height: 0.3mm fits all budgets

**Action Required:**
- Specify exact 4DT variant for actuation force
- Confirm travel and force spec

**Source:** RS Components / Snaptron catalog

---

## PASSIVES & SMALL PARTS

### 32.768 kHz RTC Crystal (SMD)

**Verification Status:** ⚠️ GENERIC - PN needed

**Typical Dimensions:**
- Small SMD packages: **3.2 × 1.5 × 0.8mm** variants common
- Height: ~0.8mm typical

**Critical Notes:**
- ⚠️ Crystals vary significantly by manufacturer
- ⚠️ Must pick exact PN for load capacitance
- ⚠️ Mechanical drawing needed for padstack
- ⚠️ Load capacitance must match MCU requirements

**Action Required:**
- Specify exact crystal PN
- Verify load capacitance (typically 12.5pF for nRF52)
- Get mechanical drawing

---

### BAT60JFILM (Schottky Diode, SOD-323)

**Verification Status:** ✅ CONFIRMED

**Verified Dimensions:**
- Package: SOD-323
- Dimensions: **~1.8 × 1.45 × ~1.07mm**
- Height: 1.07mm

**Critical Notes:**
- ✅ SOD-323 package dimensions confirmed
- 🚨 **HEIGHT PROBLEM:** 1.07mm exceeds 1mm budget by 7%
- ⚠️ May need alternative package (SOD-523 is smaller)

**Height Budget Impact:**
- Height: 1.07mm
- **Status:** ⚠️ MARGINAL - 0.07mm over budget

**Source:** STMicroelectronics datasheet

---

### Everlight 19-337/R6GHBHC-M01/2T (RGB LED)

**Verification Status:** ⚠️ PARTIAL - PN needs confirmation

**Typical Dimensions:**
- Package: 1616 SMD LED
- Dimensions: **~1.6 × 1.6 × ~0.8mm**
- Height: 0.8mm (lens height varies)

**Critical Notes:**
- ⚠️ Exact Everlight PN datasheet needed
- ⚠️ Common cathode vs common anode: Must verify
- ⚠️ Lens height may vary (0.8mm typical)
- ✅ Height: 0.8mm likely fits 1mm budget

**Action Required:**
- Verify exact Everlight PN exists
- Confirm common cathode configuration
- Get datasheet for lens height

---

## MECHANICAL COMPONENTS

### Sapphire Window (PPG) - ∅6 × 0.5mm

**Verification Status:** ✅ AVAILABLE

**Critical Notes:**
- ✅ ∅6mm sapphire windows ARE available from suppliers
- ✅ Thickness options: 0.3–1.0mm commonly available
- ⚠️ Confirm optical specs (AR coatings if needed)
- ⚠️ Supplier quotes include thickness tolerance
- ⚠️ Custom part: Verify with glass/sapphire vendor

**Source:** Various sapphire suppliers

---

### Neodymium N52 Magnets ∅4 × 1mm

**Verification Status:** ✅ AVAILABLE

**Critical Notes:**
- ✅ Small N52 magnets 4×1mm are standard stock
- ✅ Available from K&J Magnetics, Alibaba
- ⚠️ Check plating options (Ni-plated typical)
- ⚠️ Magnetization direction matters

**Source:** K&J Magnetics / various suppliers

---

### Spring Bars (Watch Pins) Ø1.8mm × 25mm

**Verification Status:** ✅ AVAILABLE

**Critical Notes:**
- ✅ Standard watch spring bars exist in 25mm length
- ⚠️ Confirm hole size/diameter compatibility with band lugs
- ⚠️ Verify 1.8mm diameter matches lug holes

**Source:** Watch parts suppliers

---

## CRITICAL ISSUES IDENTIFIED

### 🔴 HEIGHT BUDGET VIOLATIONS (1mm budget)

| Component | Height | Over Budget | Severity |
|-----------|--------|-------------|----------|
| **BG600L-M3** | 2.1mm | +1.1mm (110%) | 🔴 CRITICAL |
| **MAX30102** | 1.55mm | +0.55mm (55%) | 🔴 CRITICAL |
| **MCP73831** | 1.3mm | +0.3mm (30%) | 🟡 HIGH |
| **BAT60JFILM** | 1.07mm | +0.07mm (7%) | 🟡 MEDIUM |
| **ADXL372** | 1.06mm | +0.06mm (6%) | 🟡 MEDIUM |

**Total components violating 1mm budget: 5 out of 15**

### ⚠️ DIMENSION DISCREPANCIES

| Component | BOM Claimed | Actual Found | Discrepancy |
|-----------|-------------|--------------|-------------|
| **TMP102** | 1.6 × 1.2mm | 1.6 × 1.6mm | Width +0.4mm (square, not rectangular!) |

### 🚨 PART EXISTENCE / AVAILABILITY CONCERNS

| Component | Issue | Severity |
|-----------|-------|----------|
| **ST4SIM-200M** | Some SKUs listed as obsolete | 🟡 MEDIUM |
| **Jinlong G1040003D** | Variant naming confusion (G vs VG prefix) | 🟡 MEDIUM |
| **JST SH connector** | Ambiguous PN, need exact variant | 🟢 LOW |

### ⚠️ PACKAGE VARIANT AMBIGUITIES

Multiple parts have variant suffixes that significantly affect dimensions:
- **ST25DV04K:** UFDFPN8 vs UFDFPN12 vs WLCSP (different sizes!)
- **nRF52810:** QFN vs CSP variants (different packages!)
- **DRV2605L:** VQFN vs VSSOP (different heights!)
- **W25Q32:** Multiple WSON/SOIC options (need suffix confirmation)

---

## DESIGN IMPLICATIONS

### Cannot Proceed With Current Design

The 1mm height budget is **fundamentally incompatible** with 5 components:

1. **BG600L-M3 (2.1mm):** MORE THAN DOUBLE the budget
2. **MAX30102 (1.55mm):** 55% over budget
3. **MCP73831 (1.3mm):** 30% over budget
4. **ADXL372 (1.06mm):** 6% over budget (tight)
5. **BAT60JFILM (1.07mm):** 7% over budget (tight)

### Required Design Changes

**Option 1: Abandon 1mm height budget**
- Accept device will be taller
- Recalculate total height with actual component stack
- Current design with these components: ~3-4mm minimum height

**Option 2: Use component recesses**
- BG600L-M3: Recess 1.1mm into housing
- MAX30102: Already planned flex tail (drops 2.5mm below PCB)
- MCP73831: Replace with DFN variant or recess 0.3mm
- Others: Accept tight fit or minor recess

**Option 3: Find alternative components**
- BG600L-M3: Use separate BG95-M3 + MAX-M10S? (But still tall!)
- MCP73831: Use DFN package variant
- BAT60JFILM: Use SOD-523 smaller package
- Keep others (marginal fits)

### Battery Dimension Concern

LP301020 listed as 3.0mm, but **actual with PCM is 3.1-3.2mm**.
- If design assumes exactly 3.0mm clearance: **Won't fit!**
- Need 3.2mm minimum clearance
- Impact on total device height: +0.2mm

---

## CONFIDENCE LEVELS

### ✅ HIGH CONFIDENCE (Likely accurate):
- nRF52810: 6×6mm QFN48
- BG600L-M3: 18.7×16×2.1mm (confirmed from Quectel)
- TMP102: 1.6×1.6mm SOT-563
- ADXL372: 3.0×3.25×1.06mm
- MCP1700: 2.9×1.3×0.95mm SOT-23
- MAX30102: 5.6×3.3×1.55mm
- Mechanical parts: Sapphire, magnets, spring bars available

### ⚠️ MEDIUM CONFIDENCE (Needs datasheet confirmation):
- ST4SIM-200M: Dimensions OK, but check availability
- MCP73831: SOT-23 dimensions, but DFN alternative exists
- W25Q32: WSON-8 likely 0.75mm, confirm suffix
- ST25DV04K: UFDFPN8 variant likely 2×3mm, confirm suffix
- DRV2605L: Package variant determines height
- LP301020: 3.0mm nominal, 3.1-3.2mm actual

### 🟡 LOW CONFIDENCE (Generic specs, need exact PN):
- Jinlong G1040003D: Exists but variant confusion
- JST SH connector: Need exact PN
- 32.768kHz crystal: Generic dimensions
- Everlight RGB: Need exact PN confirmation
- Snaptron 4DT: Series exists, need variant

---

## ACTION ITEMS BY PRIORITY

### 🔴 CRITICAL (Must resolve before proceeding):

1. **Address height budget crisis**
   - Decision: Abandon 1mm budget OR use deep recesses OR find alternatives
   - Recalculate total device height with actual components
   - Update mechanical design accordingly

2. **BG600L-M3 integration strategy**
   - 2.1mm height requires dedicated mounting solution
   - Options: PCB recess, module on opposite side, or separate modules
   - Antenna keepout planning

3. **MAX30102 placement**
   - Already planned flex tail (good!)
   - Confirm optical alignment with sapphire window
   - Verify flex PCB can handle 1.55mm component

### 🟡 HIGH (Resolve soon):

4. **Get actual datasheets for:**
   - BG600L-M3 (power consumption critical for battery life!)
   - MAX30102 (LED power consumption)
   - nRF52810 (Flash/RAM sufficient? Power modes?)
   - LP301020 battery (confirm actual thickness with PCM)

5. **Resolve package variants:**
   - ST25DV04K: Choose UFDFPN8 or UFDFPN12?
   - W25Q32: Confirm JVZPIG = WSON-8
   - MCP73831: SOT-23 or DFN?

6. **Verify part availability:**
   - ST4SIM-200M: Check if specific SKU obsolete
   - Jinlong G1040003D: Confirm exact PN exists

### 🟢 MEDIUM (Can defer slightly):

7. **Specify exact PNs for generic parts:**
   - JST battery connector
   - 32.768kHz crystal
   - Everlight RGB LED
   - Snaptron dome variant

8. **Get mechanical drawings:**
   - All custom mechanical parts
   - Battery with PCM dimensions
   - Connector orientations

---

## NEXT STEPS

1. **User decides on height budget strategy** (abandon 1mm OR use recesses)
2. **Download priority datasheets** (BG600L-M3, MAX30102, nRF52810, LP301020)
3. **Resolve package variant ambiguities** (get exact suffixes)
4. **Update BOM with verified dimensions**
5. **Recalculate PCB layout** with actual component sizes
6. **Recalculate device height** with real components
7. **Verify power consumption** from datasheets (not estimates!)
8. **Check part availability** on Mouser/DigiKey

---

## IMPORTANT NOTES FROM CHATGPT SEARCH

### Module vs IC Confusion
- **BG600L-M3 is a MODULE** (not bare IC) - includes antenna, thicker, needs RF keepouts
- **nRF52810 is bare IC** - different design considerations

### Package Suffix Matters
- Many components have multiple package variants
- **Exact suffix determines footprint and height**
- Must match BOM PN to mechanical drawing precisely

### Height Reality Check
- Several parts are >1mm tall naturally
- 1mm budget may have been based on optimistic/incorrect data
- Real-world designs rarely achieve <1mm component height universally

### Battery Thickness
- Nominal dimensions often exclude PCM board and wires
- **Always add 0.1-0.2mm margin** for actual pack thickness

---

**Report compiled:** November 10, 2025
**Data source:** ChatGPT deep search (preliminary)
**Next:** Obtain actual datasheets for final verification
