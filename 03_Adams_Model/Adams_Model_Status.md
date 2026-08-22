# Adams Model Status

Adams 2020 command was found at `C:\Program Files\MSC.Software\Adams\2020_711253\bin\adams2020.bat`.

A direct `-help` probe returned `-help is not a valid selection code`, so this pass did not create a verified Adams/Car model or claim Adams simulation results.

Prepared import inputs:

- `E18_hardpoint_V6a_ninth_final_raw_export.csv`: direct data-only export from the ninth/final sheet of `C:\Users\34094\Desktop\E18_hardpoint_V6a (version 1).xlsx`.
- `E18_hardpoint_V6a_ninth_final_for_adams.csv`: structured point table in mm.

Required next manual/automated Adams step: create an Adams/Car SLA front and rear suspension subsystem from these points, run parallel wheel travel +/-30 mm, roll analysis, and export camber/toe/roll-center/motion-ratio CSV. The current figures marked `Pre-Adams` are geometry checks only.
