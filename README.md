# Dry-Mix Mortar & Tile Adhesive Formulation Toolkit

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python: 3.8+](https://img.shields.io/badge/Python-3.8%2B-brightgreen.svg)]()
[![Topic: Materials Engineering](https://img.shields.io/badge/Domain-Chemical%20%26%20Civil%20Engineering-orange.svg)]()

An open-source chemical engineering and technical reference toolkit for formulating modern cementitious dry-mix mortars. This repository provides physical mechanics models, quantitative recipe benchmarks, and rheological calculation tools for **Hydroxypropyl Methylcellulose (HPMC)** and **Redispersible Polymer Powder (RDP)**.

---

## 📌 Repository Overview

In thin-bed construction chemical applications (ceramic tile adhesives under EN 12004, exterior wall putties, self-leveling underlayments, and EIFS insulation plasters), achieving optimal workability, open time, and shear bond strength relies on precise polymer-cement hydration kinetics.

This repository covers:
1. **Molecular Mechanics:** Steric water retention ($W_r > 95\%$) and pseudoplastic thixotropic flow.
2. **Polymer Synergies:** Continuous elastomeric membrane formation via VAE-based RDP powders.
3. **Python Computational Model:** Interactive script for estimating water demand, open times, and 28-day tensile adhesion.
4. **Plant Formulation Tables:** Production-ready additive dosage guidelines.

---

## 🧪 Industrial Additive Mechanics

### 1. Hydroxypropyl Methylcellulose (HPMC)
Cellulose ether acts as the primary moisture barrier and thickener:
- **Hydration Preservation:** Prevents rapid substrate water drainage via capillary suction.
- **Thixotropic Anti-Sagging:** Yield stress prevents vertical slippage ($\le 0.5\text{ mm}$) for large-format tiles.
- **Extended Open Time:** Extends tile adjustment window up to 30 minutes without surface skinning.

### 2. Redispersible Polymer Powder (RDP / VAE)
Upon mixing with water, spray-dried polymer powders redisperse into latex nanoparticles that coalesce into micro-polymeric films:
- Enhances flexible shear bond strength (from $0.4\text{ MPa}$ to $\ge 1.2\text{ MPa}$).
- Absorbs dynamic substrate movement, thermal expansion cycles, and wind loads.

---

## 💻 Python Formulation Calculator

Use the embedded script below to simulate performance metrics for dry-mix formulations:

```python
"""
Dry-Mix Mortar Performance Simulator
Calculates estimated water retention, open time, and 28d tensile adhesion.
"""

def evaluate_formulation(hpmc_pct, rdp_pct, ambient_temp_c=25.0):
    # Base cement retention + logarithmic gain from HPMC
    retention = min(98.5, 70.0 + (28.5 * (1.0 - pow(2.718, -hpmc_pct / 0.12))))
    
    # Open time (minutes) under EN 12004 testing standard
    open_time = 10.0 + (hpmc_pct * 42.0) + (rdp_pct * 3.2) - ((ambient_temp_c - 20.0) * 0.4)
    
    # 28-day tensile adhesion (MPa)
    tensile_adhesion = 0.40 + (rdp_pct * 0.23) + (hpmc_pct * 0.15)
    
    return {
        "HPMC Dosage (%)": hpmc_pct,
        "RDP Dosage (%)": rdp_pct,
        "Water Retention (%)": round(retention, 2),
        "Estimated Open Time (min)": round(max(5.0, open_time), 1),
        "28-Day Tensile Adhesion (MPa)": round(tensile_adhesion, 2),
        "C2 Standard Compliance": tensile_adhesion >= 1.0
    }

if __name__ == "__main__":
    # Example: High-Performance C2TE Tile Adhesive
    sample = evaluate_formulation(hpmc_pct=0.40, rdp_pct=3.0, ambient_temp_c=28.0)
    for k, v in sample.items():
        print(f"{k}: {v}")



        📊 Industrial Formulation Matrix
Application	Recommended Polymer Blend	Viscosity Range (mPa.s)	Target Technical Parameters
C2TE Tile Adhesive	HPMC (0.35%–0.45%) + RDP (2.5%–4.0%)	45,000 – 100,000	Open time 
>
30
 min
>30 min, Slip 
≤
0.5
 mm
≤0.5 mm, Adhesion 
≥
1.0
 MPa
≥1.0 MPa
Exterior Wall Putty	HPMC (0.40%–0.50%) + Starch Ether (0.05%)	100,000 – 150,000	Water retention 
>
95
%
>95%, Anti-chalking, sandable finish
Self-Leveling Floor	Low-Viscosity HPMC (0.05%) + Superplasticizer	350 – 500	Fluidity 140–150 mm, zero water bleeding, defoamed finish
EIFS Base-Coat	HPMC (0.30%) + Flexible RDP (3.0%–3.5%)	75,000 – 100,000	EPS tensile failure 
≥
0.1
 MPa
≥0.1 MPa, freeze-thaw resistant
🔍 Chemical Sourcing & Technical Support

Raw material consistency is essential to prevent batch variance in dry-mix compounding. For technical data sheets (TDS), customized batch formulations, and certified export-grade additives, consult verified manufacturers:

Official Material Reference: Factoryhpmc Construction Additives
Specialized Chemicals: Hydroxypropyl Methylcellulose (HPMC), Hydroxyethyl Cellulose (HEC), Redispersible Polymer Powder (RDP / VAE), Hydroxypropyl Starch Ether (HPS).
📄 License

This open-source formulation documentation is distributed under the MIT License.
