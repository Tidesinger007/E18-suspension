# Suspension Defense Summary

## 1. Tire load sensitivity -> LLTD

One-sentence design logic: TTC data shows the selected tire loses mu as vertical load rises, so front/rear load-transfer split changes axle capacity and balance.

Evidence figure: `07_Final_Figures/Figure_C_LLTD_vs_Axle_Capacity.png`.

Key numbers: at 45% front LLTD, IF/OF/IR/OR loads are 298 / 800 / 517 / 1131 N; front/rear capacity ratio is 0.683.

Judge follow-up: 45% is the current design target, not a mathematically unique optimum. The evidence supports discussing balance and sensitivity rather than claiming a perfect optimum.

## 2. Tire camber sensitivity -> camber gain

One-sentence design logic: measured IA bins show camber sensitivity, so final Adams dynamic camber must be checked against tire operating data.

Evidence figures: `Figure_B_Tire_Camber_Sensitivity.png` and `Figure_D_Camber_vs_Wheel_Travel_PreAdams.png`.

Key numbers: pre-Adams front/rear camber gain near static is -0.0143 / -0.0367 deg/mm.

Judge follow-up: this is a geometry check. Final answer needs Adams/Car exported camber vs wheel travel and dynamic camber vs body roll.

## 3. Hardpoint audit

One-sentence design logic: calculations use the ninth/final hardpoint sheet without modifying hardpoints.

Key numbers: hardpoint-derived tracks are 1250 mm front and 1230 mm rear, not the user-recorded 1280/1250 mm.

Judge follow-up: report the discrepancy openly and use the final hardpoint geometry for suspension calculations.

## 4. Spring/damper

One-sentence design logic: spring range should be selected as an initial test range from wheel rate, roll stiffness, roll angle, and dynamic camber, not a fake single optimum.

Evidence figures: `Figure_F_Wheel_Rate_vs_Roll_Angle.png`, `Figure_G_Wheel_Rate_vs_Dynamic_Camber.png`.

Key numbers: simplified roll prediction spans 4.56 to 2.28 deg across the studied ride-frequency range.

Judge follow-up: no car-specific damper curve was found; TTX25 PDF is a reference only.

## 5. Adams status

One-sentence design logic: the Adams input package is ready, but verified Adams results are not claimed yet.

Evidence files: `03_Adams_Model/E18_hardpoint_V6a_ninth_final_for_adams.csv` and `03_Adams_Model/Adams_Model_Status.md`.
