# Battery / Supercapacitor Specification & Data Generation Reference

This document serves as the **technical reference** for battery (supercapacitor) specifications and defines the **ground truth constraints** used for synthetic controller data generation and predictive maintenance modeling.

---

## 1. Electrical Specifications

| Parameter | Unit | Specification | Conditions |
|---------|------|---------------|-----------|
Nominal Capacity | Wh | 90 | Standard charge / discharge |
Nominal Voltage | V | 4.3 DC | — |
Standard Charge Current | A | 21 | Constant current |
Charge Limited Voltage | V | 4.4 | Constant voltage |
Standard Discharge Current | A | 21 | Constant current |
Discharge Cut-off Voltage | V | 2.6 | — |
Max Continuous Charge Current | A | 63 | — |
Max Continuous Discharge Current | A | 63 | — |
Max Peak Charge Current | A | 105 | — |
Max Peak Discharge Current | A | 105 | — |
Internal Resistance | mΩ | ≤ 1.50 | AC, 1 kHz |

---

## 2. Thermal Specifications

| Condition | Temperature Range |
|---------|------------------|
Charge | -36 ℃ to 70 ℃ |
Discharge | -36 ℃ to 70 ℃ |
Standard Test Temperature | 25 ℃ ± 5 ℃ |

---

## 3. Physical Characteristics

| Parameter | Unit | Value |
|--------|------|-------|
Weight | g | 350 ± 10 |
Thickness (T) | mm | 7.4 ± 0.1 |
Width (W) | mm | 210 ± 1.0 |
Height (H) | mm | 128 ± 0.9 |
Terminal Thickness (t) | mm | 0.3 ± 0.05 |
Diameter (D) | mm | 60 ± 1.0 |
Terminal Height (H) | mm | 13.5 ± 0.5 |

---

## 4. Appearance Requirements

The device **must not exhibit**:
- Rift
- Scar
- Breakage
- Rust
- Discoloration
- Leakage
- Deformation

---

## 5. Standard Test Conditions

### 5.1 Environmental Conditions
- Temperature: **25℃ ± 5℃**
- Relative Humidity: **15% – 90%**
- Atmospheric Pressure: **86 – 106 kPa**

### 5.2 Test Sample Conditions
- Capacitor produced within **3 months**
- Measurement accuracy:
  - Voltage: ±0.01 V
  - Current: ±5%
  - Dimensions: ±0.10 mm

---

## 6. Standard Charge & Discharge Definitions

### Standard Charge Procedure
1. Constant current charge at **21 A**
2. Until voltage reaches **4.4 V**
3. Switch to constant voltage mode
4. Terminate when current reduces to **1 A**

### Standard Discharge Procedure
1. Constant current discharge at **21 A**
2. Until voltage reaches **2.60 V**

---

## 7. Performance Test Specifications

| Test | Unit | Requirement |
|----|------|------------|
Rated Capacity | Wh | 90 |
Rated Voltage | V | 4.3 (at 50% SOC) |
Internal Impedance | mΩ | ≤ 1.5 |
Leakage Current (72h) | mA | ≤ 0.5 |

---

## 8. Initial Capacity Determination

Initial capacity is defined as **100–110% of nominal capacity**.

### Test Method
1. Discharge → rest 10 min
2. Charge → rest 10 min
3. Discharge → rest 10 min
4. Repeat steps 2–3 up to 5 cycles
5. If three consecutive results vary <3%, stop early
6. Average of last three values is taken

---

## 9. Environmental Performance Tests

### High Temperature Performance
- Storage: **55℃ for 3 hours**
- Discharge at 55℃
- Capacity ≥ 100% of initial

### Low Temperature Performance
- Storage: **-20℃ for 3 hours**
- Discharge at -20℃
- Capacity ≥ 70% of initial

---

## 10. Fast Charge / Discharge Tests

| Test | Requirement |
|----|------------|
Fast Discharge (42A) | ≥ 90% capacity |
Fast Charge (41A) | ≥ 80% capacity |

---

## 11. Safety & Abuse Tests

| Test | Acceptance Criteria |
|----|--------------------|
External Short Circuit | No fire, no explosion |
Nail Penetration | No fire, no explosion |
Thermal Shock | No leakage, fire, explosion |
Hot & Humid | Capacity ≥ 70%, no deformation |
Drop Test (1.5m) | No fire, leakage |
Overcharge | No fire, no explosion |
Over-discharge | No fire, leakage |

---

## 12. Cycle Life

| Test | Requirement |
|----|------------|
Charge/Discharge Cycles | > 20,000 |
End of Life Criterion | Two successive cycles < 75% capacity |

---

## 13. Relevance to Data Generation

These specifications define **hard constraints** for synthetic data generation:

- Voltage, current, temperature bounds
- Degradation rates (SOH, internal resistance)
- Fault injection thresholds
- Safety violation events
- End-of-life detection

All generated controller data **must remain physically plausible** within these limits.

---

## 14. Usage in This Project

This document is used by:
- `data_generation/` → synthetic BMS signal generation
- `features/` → domain-aware feature extraction
- `models/` → SOH & RUL prediction
- `validation/` → constraint-based sanity checks

---

**Source of Truth:** Manufacturer specification  
**Scope:** Simulation, analytics, predictive maintenance  
**Not for:** Direct hardware certification