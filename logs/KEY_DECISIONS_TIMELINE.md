# Key Decisions Timeline

Quick reference for major design decisions chronologically.

---

## October 28, 2025

**Foundation Session:**
- ✅ Logging system established (CONVERSATION_LOG.md + detailed sessions)
- ✅ Working rules defined (PERSONALITY_TRAITS.md with 8 rules)
- ✅ Emergency timing: 5 min → 2 min
- ✅ QR code → NFC tap (ST25DV04K)
- ✅ Battery thresholds: 5%/2%/1% context-aware
- ✅ Team name: **Cortex** 🧠

---

## October 29, 2025

**Component Layout Breakthrough:**
- ✅ Vertical battery rails design (batteries as "rails" on sides)
- ✅ 17mm × 22mm center zone created for RF modules
- ✅ Layer flip: Batteries below, PCB on top (better RF access)
- ✅ PPG on bottom side of flex PCB (reaches sapphire window)

**3-Piece Housing Innovation:**
- ✅ Piece 1 (Base): Stainless steel
- ✅ Piece 2 (Lid): **ABS plastic** (hidden, functional layer)
- ✅ Piece 3 (Cover): Stainless steel (aesthetic)
- ✅ Cost savings: €4.50/unit (32% housing reduction)
- ✅ RF windows: Polycarbonate in plastic lid (better bonding)

---

## October 30, 2025

**Manufacturing Method:**
- ✅ Laser cutting + CD projection welding with M3 threaded studs
- ✅ Factory handles all fabrication (no user equipment investment)
- ✅ Cost: ~€10.50 housing per unit @ 1000qty
- ✅ PCB: 37mm × 20.5mm finalized

**Housing Dimensions:**
- ✅ 40mm × 23mm × 8mm (corrected from 25mm length)
- ✅ User preference noted: Would prefer 35-40mm × 20mm (3mm shorter)

---

## November 4, 2025

**BOM VERIFICATION MISSION (Project-Saving Session):**

**11 Components Corrected:**
1. nRF52810: 4×4mm → **6×6mm**
2. MAX-M10S: 12×16mm → **9.7×10mm**
3. TMP102: DSBGA → **SOT563 1.6×1.2mm**
4. W25Q32: 5×6mm → **5.28×7.9mm**
5. Battery: 2mm → **3mm thick** (LP301020)
6. STSAFE-J100 → **ST4SIM-200M** (correct eSIM chip)
7. MCP1700-3302E/TO → **MCP1700T-3302E/TT** (SMD variant)
8. Jinlong Z4LC1B0001781 → **G1040003D** (verified 2.0 Grms motor)
9. ST25DV04K 3×3mm → **UFDFPN8 2×3mm** (saves space)
10. **Button added:** Snaptron 4DT metal dome (∅4×0.3mm)
11. **RGB LED added:** Everlight 19-337 (1.6×1.6mm)

**Critical Decision: eSIM Strategy**
- ❌ Rejected BG770A-GL iSIM (provider lock-in risk)
- ✅ Confirmed BG95-M3 + ST4SIM-200M + MAX-M10S (€21)
- Rationale: +€6/unit for complete flexibility and safety in medical device

**Rule 9 Added:** External AI input handling (don't adapt blindly)

---

## November 5, 2025

**PCB Cost Breakthrough:**
- ✅ Realistic JLCPCB pricing researched
- ✅ **€7.60/unit production** (was €28 prototype estimate)
- ✅ **Savings: €20.40/unit (-73%)**

**Hybrid Design Concept:**
- ✅ Battery stacking + motor/PPG recess + single double-sided PCB
- ✅ 21×30mm PCB (630mm² per side = 1,260mm² total)
- ✅ All components fit comfortably

**SMD Assembly Education:**
- ✅ Cleared up through-hole vs SMD misunderstanding
- ✅ Components CAN overlap in XY (only height matters)
- ✅ Dual recess design: Cellular UP 1mm, Motor/PPG DOWN 1mm

**Final BOM v3 Cost:**
- ✅ **€78.65/unit @ 1000qty** (down from €102.08)

---

## November 6, 2025

**Material Debate:**
- ✅ SS316L confirmed (€0.50/unit more than SS304, better for sports)
- ✅ **Rule 5 updated:** Debate requirement added (always challenge)
- ⚠️ Metal housing contradictions identified:
  - Dampens haptic 40-60% (user requirement: "haptic needs to be TOP!")
  - Creates Faraday cage (needs RF windows)

**Reality Checks:**
- ⚠️ **All cost estimates are theoretical** (no real supplier quotes)
- ⚠️ Licensing gap identified (Kickstarter → success → can't sell → need €15-30k CE/FCC → no revenue)
- 🚨 **CRITICAL: Design fundamentally broken** - modules naked, no IP67 seal designed, 3mm batteries broke 2mm assumption

**Session Paused:** User needs time to think through fundamental solution

---

## November 7, 2025

**🎉 BREAKTHROUGH SESSION - Design Crisis SOLVED:**

**Final Specifications Locked:**
- ✅ **PCB:** 32×21mm with 11×11mm cutout (haptic motor clearance)
- ✅ **Total height: 9mm** (was >10mm)
- ✅ **Component space:** 1102mm² (vs 815mm² needed = 135% capacity)
- ✅ **Full sapphire bottom:** 40×23mm + dome for PPG

**Layer Stack (Bottom → Top):**
1. 0.5mm - Sapphire glass (full bottom + dome)
2. 0.5mm - SS316L housing (structural + IP67)
3. 3mm - Batteries + motor + hinge
4. 1mm - Bottom PCB component space
5. 0.8mm - PCB (double-sided with cutout)
6. 2.2mm - Top components (cellular + GPS)

**Key Innovations:**
1. ✅ **Flex tail:** PPG + TMP102 drop 2.5mm below PCB (0.5mm from skin)
2. ✅ **10×11mm tall stack:** >1mm components concentrated (77.5% density)
3. ✅ **Sapphire windows:** 1mm under lid + 1mm over = no height penalty
4. ✅ **PCB cutout:** Isolates haptic vibration (motor can't touch PCB)
5. ✅ **Z-space reuse:** Tall stack positioned above flex tail area

**Component Distribution:**
- **TOP (551mm², 99% used):** Cellular (17×19.8mm) + GPS (13.7×14mm) + LED + Button
- **BOTTOM (551mm², 30% used):** <1mm spread freely, >1mm in 10×11mm zone, PPG/temp on flex tail

---

## Cost Summary (as of Nov 7, 2025)

**✅ VERIFIED:**
- Electronics BOM v3: **€78.65/unit @ 1000qty**
- PCB fab+assembly: **€7.60/unit production** (€28 prototype)

**⚠️ THEORETICAL (NO REAL QUOTES):**
- Housing (metal/hybrid): €18.50-55/unit + €1000-2000 tooling
- Rigid-flex PCB: +€0.50-1/unit (estimated)
- Sapphire: €15-24/unit (complete guess)
- **Total Device: €140-167/unit (±50% uncertainty)**

---

## What's Locked In ✅

1. 9mm total height
2. 32×21mm PCB with 11×11mm haptic cutout
3. SS316L 0.5mm housing (debatable but current)
4. Flex tail for PPG + TMP102 (skin contact)
5. 10×11mm tall component zone (77.5% density)
6. Sapphire window recessed design
7. Electronics BOM: €78.65/unit
8. Built-in module antennas (no external)
9. Haptic motor isolation (PCB can't touch)
10. Component space verified (815mm² vs 1102mm²)

---

## What Needs Validation ⚠️

1. Housing manufacturing costs (NO real quotes)
2. Rigid-flex PCB feasibility + real pricing
3. Sapphire costs
4. Kickstarter budget viability (€40-50k uncertain)
5. Licensing gap strategy
6. Final material choice (metal vs hybrid vs polymer)
7. Haptic performance with metal (dampening concern)
8. RF performance with windows (needs testing)
9. Manufacturing partner selection
10. Assembly complexity (9 layers, flex tail, sapphire bonding)

---

## Critical Next Steps

1. **Get REAL quotes** from manufacturers (rigid-flex, sapphire, SS316L)
2. **Validate manufacturing feasibility** with suppliers
3. **Recalculate Kickstarter budget** with real costs
4. **Plan licensing gap strategy**
5. **Design flex tail PCB** (routing, bend radius, attachment)
6. **Design motor mounting** (secure in 3mm layer without PCB contact)
7. **Design sapphire window attachment** (adhesive, gasket, alignment)

---

**Last Updated:** November 10, 2025
**Status:** Design breakthrough complete, ready for detailed CAD and supplier quotes
