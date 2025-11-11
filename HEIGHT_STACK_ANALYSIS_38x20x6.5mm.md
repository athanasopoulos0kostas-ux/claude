# Height Stack Analysis - 38×20×6.5mm Constraint

**Date:** November 11, 2025
**New constraint:** 38mm × 20mm × **6.5mm MAX height**

---

## Current BOM Components - Height Requirements

### Layer-by-Layer Stack (Bottom to Top):

```
┌─────────────────────────────────────┐
│  TOP HOUSING                        │  0.8mm
├─────────────────────────────────────┤
│  PCB                                │  0.8mm
├─────────────────────────────────────┤
│  BG600L-M3 MODULE                   │  2.1mm  ⚠️
├─────────────────────────────────────┤
│  BATTERIES (2× LP301020)            │  3.1mm  ⚠️
│  MOTOR (underneath batteries)       │  4.0mm  ⚠️
├─────────────────────────────────────┤
│  BOTTOM HOUSING                     │  0.8mm
└─────────────────────────────────────┘
```

---

## Current Stack Height Calculation:

**WORST CASE (motor location):**
```
Bottom housing:      0.8mm
Motor:               4.0mm
BG600L-M3 module:    2.1mm
PCB:                 0.8mm
Top housing:         0.8mm
━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:               8.5mm  ❌ EXCEEDS 6.5mm by 2.0mm!
```

**BEST CASE (battery location, no motor underneath):**
```
Bottom housing:      0.8mm
Batteries:           3.1mm
BG600L-M3 module:    2.1mm
PCB:                 0.8mm
Top housing:         0.8mm
━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:               7.6mm  ❌ EXCEEDS 6.5mm by 1.1mm!
```

---

## 🚨 CRITICAL PROBLEM: We're 1-2mm TOO TALL!

**Current design does NOT fit in 6.5mm!**

We need to save **1.1-2.0mm** somewhere!

---

## Options to Reduce Height:

### Option 1: Thinner Housing (0.8mm → 0.6mm)
**Savings:** 0.4mm total (0.2mm top + 0.2mm bottom)
**New total:** 7.2mm → **Still 0.7mm too tall** ❌
**Concern:** Structural strength for medical device

### Option 2: Thinner Batteries (3.1mm → 2.5mm)
**Savings:** 0.6mm
**Challenge:** Need to find 2.5mm thick batteries with enough capacity
**Typical LP30xx series:** 2.0mm, 2.5mm, 3.0mm, 3.5mm, 4.0mm available
**New battery:** LP301020 (3.0×10×20mm) → need LP252020 (2.5×10×20mm)
**Capacity loss:** ~300mAh → ~250mAh (-16% capacity)
**New total:** 7.0mm → **Still 0.5mm too tall** ❌

### Option 3: Remove Cellular Module Layer Separation
**Current:** Module in separate 2.4mm layer between batteries and PCB
**New:** Mount module DIRECTLY on PCB bottom (normal SMD placement)
**Savings:** Eliminate 2.4mm layer - (2.1mm module height) = **0.3mm saved**

**BUT:** Module footprint 18.7×16mm = 299mm² now goes ON the PCB bottom
- Reduces available PCB bottom space from 372.8mm² to ~74mm²
- **May not fit all other components!** ⚠️

### Option 4: Side-Mount Motor Instead of Under Batteries
**Current:** Motor underneath batteries (adds 1mm intrusion)
**New:** Motor on device edge/side (like LED and button)
**Savings:** 1.0mm in motor zone
**Challenge:** Motor is **Ø10mm × 4mm** - does it fit on 38mm edge?
**New total:** 7.6mm → 6.6mm → **Still 0.1mm too tall** ❌

### Option 5: Thinner PCB (0.8mm → 0.6mm)
**Savings:** 0.2mm
**Concern:** Structural rigidity, standard PCB thickness is 0.8mm or 1.6mm
**Custom 0.6mm PCB:** More expensive, less common
**New total:** With thinner PCB: 7.4mm → **Still 0.9mm too tall** ❌

---

## 🎯 COMBINATION STRATEGY TO REACH 6.5mm:

### Strategy A: Aggressive Thinning
```
Bottom housing:      0.6mm  (-0.2mm from 0.8mm)
Batteries (new):     2.5mm  (-0.6mm from 3.1mm, use LP252020)
Module on PCB:       2.1mm  (no separate layer)
PCB:                 0.6mm  (-0.2mm from 0.8mm)
Top housing:         0.6mm  (-0.2mm from 0.8mm)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:               6.4mm  ✅ FITS! (with 0.1mm margin)
```

**Compromises:**
- Thinner housing (structural concern)
- 16% battery capacity loss
- Module now on PCB (space problem on PCB bottom)
- Custom 0.6mm PCB (more expensive)

---

### Strategy B: Remove Module Entirely, Use Smaller Alternative

**Check if smaller modules exist:**
- Nordic Semiconductor nRF9160 (10×16×1.0mm) - LTE-M/NB-IoT, NO 2G, NO GPS
- Quectel BG77 (12.5×15.5×2.0mm) - LTE-M/NB-IoT, NO 2G, NO GPS
- SIMCom SIM7070G (16.0×17.0×2.0mm) - LTE-M/NB-IoT + GPS, NO 2G

**Problem:** All lose 2G fallback capability

---

### Strategy C: Eliminate Separate Module Layer + Thinner Batteries

```
Bottom housing:      0.8mm
Batteries (new):     2.5mm  (LP252020, -0.6mm)
Module on PCB:       2.1mm  (mount directly on PCB)
PCB:                 0.8mm
Top housing:         0.8mm
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:               6.0mm  ✅ FITS! (with 0.5mm margin)
```

**Compromises:**
- 16% battery capacity loss (300mAh → 250mAh)
- BG600L-M3 module (299mm²) now occupies PCB bottom
- **Need to verify all components still fit on PCB bottom!**

---

## 🔴 CRITICAL QUESTION: Can Components Fit on PCB Bottom with Module?

**PCB bottom calculation WITH module mounted:**

**Available PCB bottom area:**
- PCB size: 38×20mm = **760mm²** (NEW - larger than 32×21mm!)
- BG600L-M3 footprint: 18.7×16mm = 299mm²
- Remaining: 760 - 299 = **461mm² available** ✅

**Components needed (from previous calculation):**
- Major ICs: 130.1mm²
- Passives: 24.9mm²
- Connectors: 28.8mm²
- Routing overhead: 55mm²
- Keepouts/tolerances: 41mm²
- **Total: 279.8mm²**

**Check:** 279.8mm² < 461mm² ✅ **FITS!**

**Utilization:** 279.8 ÷ 461 = **61%** - Good margin! ✅

---

## 🎯 RECOMMENDED SOLUTION: Strategy C

### Changes Required:

1. **Change PCB dimensions:**
   - OLD: 32×21mm = 672mm²
   - NEW: 38×20mm = 760mm² (+88mm²) ✅

2. **Change batteries:**
   - OLD: 2× LP301020 (3.1×10×20mm, ~150mAh each = 300mAh total)
   - NEW: 2× LP252020 (2.5×10×20mm, ~125mAh each = 250mAh total)
   - **Capacity loss: -50mAh (-16%)** ⚠️

3. **Mount BG600L-M3 on PCB bottom (not separate layer):**
   - Castellated pads or SMD pads
   - Module height 2.1mm fits in 2.4mm budget (above batteries)
   - Frees up the separate module layer

4. **Keep housing at 0.8mm (no thinning):**
   - Maintains structural strength
   - Standard thickness

### New Stack:
```
Bottom housing:      0.8mm
Batteries:           2.5mm  ← THINNER
PCB with module:     2.9mm  (0.8mm PCB + 2.1mm module on bottom)
Top housing:         0.8mm
━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:               6.0mm  ✅ FITS with 0.5mm margin!
```

---

## Height Budget Summary:

| Component | Old Height | New Height | Change |
|-----------|------------|------------|--------|
| Bottom housing | 0.8mm | 0.8mm | - |
| Batteries | 3.1mm | 2.5mm | **-0.6mm** ✅ |
| Module layer | 2.4mm | 0mm | **-2.4mm** ✅ (now on PCB) |
| PCB + module | 0.8mm | 2.9mm | +2.1mm (module on PCB) |
| Top housing | 0.8mm | 0.8mm | - |
| **TOTAL** | **7.9mm** | **6.0mm** | **-1.9mm saved!** ✅ |

---

## Trade-offs:

### ✅ PROS:
- **Fits in 6.5mm!** (6.0mm with 0.5mm margin)
- Larger PCB (38×20mm vs 32×21mm) = more space
- No custom thin housing or PCB needed
- Keeps standard 0.8mm housing thickness

### ⚠️ CONS:
- **Battery capacity reduced 16%** (300mAh → 250mAh)
- Battery life reduced proportionally
- Need LP252020 batteries instead of LP301020

---

## Motor Placement Note:

**Motor (Ø10×4mm) fits in the new 38mm length:**
- Place motor at device end
- Sits above 2.5mm batteries
- Intrudes 1.5mm into PCB layer (4.0mm - 2.5mm = 1.5mm)
- Creates restricted zone on PCB bottom (~100mm² with 0.7mm height limit)

**This is manageable** - we have 461mm² total on PCB bottom, can work around motor zone.

---

## ✅ CONCLUSION:

**YES - we CAN fit everything in 38×20×6.5mm!**

**Required changes:**
1. PCB dimensions: 32×21mm → 38×20mm
2. Batteries: LP301020 (3.1mm) → LP252020 (2.5mm)
3. Mount BG600L-M3 directly on PCB bottom (eliminate separate layer)
4. Accept 16% battery capacity reduction

**Final height: 6.0mm** ✅ (0.5mm under limit)

**USER DECISION NEEDED:**
- Is 16% battery capacity loss acceptable?
- Can we recalculate battery life with 250mAh instead of 300mAh?
