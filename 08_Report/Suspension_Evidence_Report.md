# Suspension Evidence Report

Scope: Formula Student tire-suspension evidence package based on existing TTC/PAC2002 outputs and the ninth/final hardpoint sheet. This report does not claim verified Adams simulation results; all kinematic plots marked `Pre-Adams` are analytic geometry checks and must be replaced/validated by Adams/Car exports.

## 1. Project Audit

Design Question: Which files are the authoritative inputs?

Tire Evidence: reused the existing MATLAB tire analysis in `C:\Users\34094\Desktop\Tire_Selection_Analysis`; selected tire table uses Hoosier 43075 16x7.5-10 R20 on 7 in rim.

Suspension Requirement: use the ninth/final sheet from `C:\Users\34094\Desktop\E18_hardpoint_V6a (version 1).xlsx` without moving hardpoints.

Calculation / Adams Evidence: structured hardpoints are saved in `00_Audit/hardpoints_final_structured.csv` and `03_Adams_Model/E18_hardpoint_V6a_ninth_final_for_adams.csv`.

Conclusion: final hardpoint-derived track is 1250 mm front and 1230 mm rear. This differs from the user-recorded 1280/1250 mm, so geometry calculations use the hardpoint-derived tracks.

Limitation: Adams/Car model creation was not completed in this pass.

## 2. Tire Load And Camber Evidence

Design Question: what does the selected tire data say about load transfer and camber?

Tire Evidence: for Hoosier 43075 rim 7, peak |mu_y| decreases from 2.710 at 222 N to 2.432 at 1112 N. This is clear load sensitivity.

Camber data at the selected measured window gives peak |mu_y| 2.488 at IA 0 deg, 2.432 at IA 2 deg, and 2.397 at IA 4 deg.

Conclusion: lateral load transfer distribution matters because moving load to the outside tire loses total axle capacity; camber claims should stay sign-convention-aware because TTC IA is a measured inclination bin, not directly the car's signed dynamic camber.

Limitation: simplified PAC2002 fit is scoped to one operating window only: R2 0.9985, RMSE 82.3 N.

## 3. LLTD = 45% Check

Design Question: is front LLTD 45% reasonable from tire load sensitivity?

Calculation: total left-right load difference at 1.8 g is solved from m*a_y*h = dF_front*t_front + dF_rear*t_rear, with front LLTD = dF_front/(dF_front+dF_rear).

At 45% front LLTD: front axle capacity 2777 N, rear axle capacity 4069 N, total 6846 N, front/rear capacity ratio 0.683.

Within the 35-55% sweep, the maximum total four-tire capacity in this simple load-only model occurs near 35% front LLTD with total capacity 6854 N.

Conclusion: 45% is not proven as a unique optimum. It is a defensible current design target if the desired balance is front capacity lower than rear capacity, but the load-only tire model tends to reward lower front LLTD in this sweep.

Limitation: this LLTD check ignores slip angle distribution, aero, transient effects, and signed camber effects.

## 4. Existing Hardpoints Pre-Adams Kinematics

Design Question: do the final hardpoints create plausible camber and roll-center trends before Adams?

Calculation: a front-view 2D SLA model was solved through +/-30 mm wheel travel. It uses inner pivot midpoints, outer ball joints, wheel center, and fixed upper/lower link lengths. It does not replace Adams.

Front camber gain near static: -0.0143 deg/mm. Rear camber gain near static: -0.0367 deg/mm.

Static roll center estimates: front 9.0 mm, rear 47.1 mm.

Conclusion: these outputs are good enough to prepare Adams inputs and identify expected trends, but not enough for final design-defense claims.

Limitation: Toe vs wheel travel and true motion ratio require Adams/Car or a full 3D constrained model; they are not claimed here.

## 5. 1.8 g Four-Tire Operating State

Design Question: what are the four tire vertical loads at the current 45% LLTD?

- IF: FZ 297.9 N, available lateral force 793.4 N.
- OF: FZ 800.5 N, available lateral force 1983.8 N.
- IR: FZ 516.6 N, available lateral force 1318.5 N.
- OR: FZ 1130.9 N, available lateral force 2750.3 N.

Calculation / Adams Evidence: `Figure_H` combines those loads with a stated 1.5 deg roll reference and the pre-Adams camber curves. This is a framework figure, not a verified Adams result.

Conclusion: outside rear is the highest-load tire and sits slightly above the top measured load bin; the interpolation is clamped at the measured upper load bin and this limitation is recorded here.

Limitation: replace the camber coordinates with Adams dynamic camber after roll analysis.

## 6. Spring And Damper Parameter Study

Design Question: what initial wheel-rate range should be tested?

Calculation: ride-frequency cases from 1.8/2.0 Hz to 2.6/2.8 Hz front/rear produce predicted roll angles from 4.56 deg to 2.28 deg at 1.8 g in this simplified model.

Conclusion: use this as `Parameter Study - not final vehicle hardware specification`. Actual spring rates still need measured motion ratio and chosen spring hardware.

Damper Limitation: found an Ohlins TTX25 MkII dyno PDF under `C:\Users\34094\Desktop\SPEEDUCK`, but no confirmed car-specific measured damper curve or click setting. Do not claim final damping.
