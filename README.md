# MEP Suits — Building Services Mechanical Toolkit

Built by an engineer, for the plant room.

Interactive toolkit for building services mechanical engineering:
- Duct Sizer (Darcy–Weisbach + Haaland, Huebscher equivalent diameter, reverse solver)
- Psychrometrics (Buck saturation, enthalpy, humidity ratio, dew/wet-bulb, density, chart)
- Ventilation to ASHRAE 62.1 (26 space types, Ez, Vbz → Voz)
- Pipe Hydraulics (Darcy + Hazen–Williams cross-check, Sch 40 true ID, pump head/power)
- Water & Coil Loads (Q=ṁcpΔT incl. glycols, COP ↔ EER ↔ kW/ton, coil + condensate)
- Fan Laws & Power (affinity cube law, annual energy/cost)
- Room Cooling Load Estimator (11 editable gains, breakdown, implied flows)
- Unit Converter + property / design reference tables
- 3D System Viewer (Three.js plant-room: AHU, duct run, VAV, elbow, diffuser, CHW pump + pipes, live-linked to Duct + Pipe calculators)

## Use

Open `index.html` in a browser. Single-file build, no backend, no data leaves the browser.
For the hosted version, see the Muse share link in the repo description once published.

## Standards & Compliance Basis

- ASHRAE 62.1 (ventilation)
- ASHRAE Fundamentals / Buck / Stull (psychrometrics)
- Darcy–Weisbach / Haaland / Huebscher (duct + pipe)
- ASME B36.10 (pipe sizes)
- CIBSE AM12 bands (design checks)

Every tool shows its method / formula and checks against published design bands.

## Calculation Record

Use the Calculation Record panel in the app (project, calc ref, prepared-by / checked-by) and Download calculation record (.txt) for the QA file.

## Important — Design Aid

This is a design aid, not a substitute for full engineering judgement or local code compliance.
All results must be verified by a licensed engineer before construction / procurement.
Input limits are enforced in code before calculation; non-finite entries fall back to design defaults.
See in-app Standards & Compliance Basis for details.

## Security

- No backend, no credentials, no secrets in this repo.
- CSP + no-referrer in the page; external loads limited to the two CDNs already used.
- Note: single-file inline scripts require `script-src 'unsafe-inline'` in the CSP; all external origins are restricted.

## License

For Darren Lieu / DarthSandD use. Verify suitability for your project before use.
