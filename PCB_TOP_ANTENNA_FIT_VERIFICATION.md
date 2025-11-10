# PCB Top Antenna Fit Verification

**Date:** November 10, 2025
**Purpose:** Verify cellular + GPS PCB trace antennas fit on PCB top surface

---

## PCB Top Available Area

**Total PCB area:** 32×21mm = **672mm²**

Unlike PCB bottom, there are NO cutouts or obstructions on top surface.
Full 672mm² available for antennas, ground plane, and routing.

---

## BG600L-M3 Antenna Requirements

### Antenna Outputs from Module:
- **Main cellular antenna:** LTE-M / NB-IoT / 2G (700-2200 MHz)
- **GNSS antenna:** GPS/GLONASS/Galileo/BeiDou (1575 MHz)

### Module Placement:
- **BG600L-M3 located:** Below PCB in separate 2.4mm layer
- **Antenna feed points:** Connected via castellated pads through PCB
- **RF traces:** Route from module edge to antenna on PCB top

---

## PCB Trace Antenna Designs

### Option 1: Inverted-F Antenna (IFA) - Most Common for Cellular

**Cellular IFA typical dimensions:**
- **Antenna element:** ~25×8mm to 30×10mm (depends on frequency)
- **Ground plane clearance:** 3-5mm keepout zone around antenna
- **Matching network:** ~5×3mm area for matching capacitors/inductors
- **Total footprint with keepout:** ~35×15mm = **525mm²**

**GPS patch antenna typical dimensions:**
- **Antenna element:** 15×15mm to 20×20mm ceramic patch
- **Ground plane clearance:** 2-3mm keepout
- **Matching network:** ~5×3mm
- **Total footprint with keepout:** ~23×23mm = **529mm²**

**Problem:** 525 + 529 = **1054mm²** > 672mm² available ❌

This doesn't fit!

---

### Option 2: Dual-Band Meandered Monopole (Compact Cellular)

**Meandered monopole for cellular:**
- **Antenna element:** ~20×6mm meandered trace (more compact)
- **Ground plane clearance:** 2-3mm keepout
- **Matching network:** ~5×3mm
- **Total footprint with keepout:** ~27×12mm = **324mm²**

**GPS passive patch antenna:**
- **Antenna element:** 15×15mm ceramic patch
- **Ground plane clearance:** 2-3mm keepout
- **Matching network:** ~5×3mm
- **Total footprint with keepout:** ~20×20mm = **400mm²**

**Problem:** 324 + 400 = **724mm²** > 672mm² available ❌

Still too tight with proper keepout zones!

---

### Option 3: Combined Multiband PCB Antenna (Optimized)

Some designs combine cellular + GPS into shared footprint with careful design.

**Combined multiband antenna:**
- **Shared ground plane:** Both antennas share common ground
- **Interleaved elements:** Cellular and GPS elements physically separated but overlapping keepout zones
- **Estimated footprint:** ~30×20mm = **600mm²**
- **Matching networks (2×):** ~10×3mm = **30mm²**
- **Total:** ~**630mm²**

**Remaining space:** 672 - 630 = **42mm² for routing** ✅

**This works but VERY tight!**

---

## 🔴 CRITICAL ANTENNA DESIGN CHALLENGES

### Challenge 1: Antenna Performance in Compact Space
- **Medical device requirement:** Must maintain reliable connectivity
- **Compact antenna penalty:**
  - Reduced bandwidth
  - Lower gain (potentially -5 to -10dB vs optimal size)
  - Matching network becomes more critical
- **Risk:** Poor cellular/GPS performance in the field

### Challenge 2: Antenna Placement vs Module Location
- **Module below PCB:** 18.7×16mm footprint
- **Antenna feed points:** Must route from module edges to antenna on top
- **Trace routing:** Need to cross PCB vertically (vias)
- **Impedance matching:** 50Ω controlled impedance traces critical

### Challenge 3: Metal Housing Interference
- **Stainless steel housing:** Acts as ground plane and shield
- **RF transparency requirement:**
  - PC windows over antennas (10×10mm each)
  - Windows must align with antenna positions
  - Housing metal affects antenna tuning
- **Concern:** Antenna may need retuning after housing integration

### Challenge 4: GPS Antenna Sensitivity
- **GPS signals are VERY weak:** -130dBm typical
- **Compact antenna challenge:** Limited gain
- **Urban canyon / indoor:** May not acquire satellites reliably
- **Medical device requirement:** GPS must work for emergency location

---

## PCB Top Space Allocation

### Scenario: Combined Multiband Antenna (630mm²)

**Available:** 672mm²
**Antenna + matching:** 630mm²
**Remaining:** 42mm²

**What needs the remaining 42mm²:**
1. **RF traces:** From module to antenna feeds (~10-15mm²)
2. **Test points:** Antenna impedance test pads (~5mm²)
3. **Ground vias:** Stitching vias around antenna perimeter (~10-15mm²)
4. **Edge clearance:** PCB edge to antenna spacing (~10mm²)

**Total overhead:** ~40mm²

**Utilization:** (630+40)/672 = **99.7%** ⚠️

---

## 🚨 ANTENNA DESIGN RED FLAGS

### Red Flag 1: No Space for Tuning Components
- **Matching networks need iteration:** Typically require 2-3 layout revisions
- **Component placement:** Matching caps/inductors need precise positioning
- **Problem:** 99.7% utilization leaves NO room for design iteration

### Red Flag 2: Antenna Performance Unknown
- **Custom antenna design required:** No off-the-shelf solution for 32×21mm
- **Testing required:**
  - VNA (Vector Network Analyzer) for impedance matching
  - Anechoic chamber for radiation pattern
  - Field testing for real-world performance
- **Risk:** May discover antenna doesn't work after PCB fabrication

### Red Flag 3: GPS Antenna Likely Inadequate
- **15×15mm GPS patch antenna:** Marginal performance
- **Typical GPS antenna:** 18×18mm to 25×25mm for good sensitivity
- **Our constraint:** Can't fit larger antenna
- **Result:** GPS may only work outdoors with clear sky view

### Red Flag 4: Cellular Antenna Compromised
- **Meandered monopole in 20×6mm:** Very compact
- **Expected performance:** -8 to -12dB gain (vs -2 to -4dB for optimal size)
- **LTE-M/NB-IoT tolerance:** Can handle poor antenna (~-12dB link budget margin)
- **2G fallback:** May not work indoors with poor antenna

---

## Alternative: External Antenna Connectors

### Option: U.FL Connectors for External Antennas

**Advantages:**
- **Better antenna performance:** Use external cellular + GPS antennas
- **PCB space savings:** U.FL connectors ~3×3mm each = 18mm² total
- **Design flexibility:** Antenna can be in band or housing edge
- **Field-proven:** Medical devices commonly use external antennas

**Disadvantages:**
- **Mechanical complexity:** Antenna cable routing through housing
- **Waterproofing challenge:** U.FL connector must be sealed
- **Cost:** External antennas + connectors + cables = +€3-5/unit
- **Assembly:** More complex manufacturing

**U.FL connector footprint:**
- **2× U.FL connectors:** 3×3mm each = 9mm² × 2 = 18mm²
- **Keepout zones:** 1mm around connectors = 25mm² total
- **RF traces:** From module to connectors = 10mm²
- **Total PCB top usage:** ~35mm²

**Remaining space:** 672 - 35 = **637mm² FREE** ✅

---

## Recommendation

### Option A: PCB Trace Antennas (Current Design)
- **Pros:** No external parts, lower cost, simpler assembly
- **Cons:**
  - 99.7% PCB top utilization (no margin for error)
  - Antenna performance likely marginal (especially GPS)
  - High risk of design iteration required
  - GPS may only work outdoors
- **Feasibility:** Technically possible but HIGH RISK for medical device

### Option B: External Antennas via U.FL Connectors
- **Pros:**
  - Proven antenna performance
  - PCB top mostly free (only 35mm² used)
  - Design flexibility
  - Reliable GPS even indoors (with active external antenna)
- **Cons:**
  - +€3-5/unit cost
  - Mechanical complexity (cable routing, waterproofing)
  - Slightly thicker device (antenna cable routing)
- **Feasibility:** Higher cost but LOWER RISK

---

## Critical Questions for User

1. **Antenna performance requirements:**
   - Does GPS need to work indoors?
   - What cellular signal strength expected (-100dBm? -115dBm?)
   - Is marginal antenna acceptable for medical device?

2. **Cost vs risk tradeoff:**
   - Accept +€3-5/unit for external antennas?
   - Or risk PCB antenna needing 2-3 design iterations?

3. **Housing integration:**
   - Can we enlarge PC windows to 15×20mm for better antenna area?
   - Is there space in housing edge for antenna cable routing?

4. **Time to market:**
   - PCB antenna: Likely 2-3 PCB revisions (6-9 weeks)
   - External antenna: Faster first-pass success but more complex assembly

---

## What We Need to Decide

**PCB TOP SPACE IS VERY TIGHT (99.7% utilization) FOR PCB TRACE ANTENNAS.**

We have three paths:

1. **Keep PCB trace antennas** - accept high risk of marginal performance
2. **Switch to external antennas** - accept +€3-5 cost and mechanical complexity
3. **Increase PCB size** - enlarge from 32×21mm to 35×22mm (if housing allows)

**This is a CRITICAL design decision that affects:**
- Device reliability (especially GPS)
- BOM cost
- Manufacturing complexity
- Time to market

**USER INPUT NEEDED!** 🔴
