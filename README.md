# MEP Suits: HVAC Engineering Calculators

**Live: https://darthsandd.github.io/mep-suits/**

MEP Suits is a browser-based toolkit for building services mechanical engineering, built by an engineer for the plant room. It pairs 8 HVAC calculators with property and reference data, a calculation record for QA, and a 3D System Viewer. It runs as a single page with no backend, and no data leaves the browser.

The interface uses a blueprint-instrument theme: pale blueprint paper, instrument-style readouts, and results presented the way they would be checked on a drawing.

## The 8 calculators

- **Duct Sizer:** Darcy-Weisbach with Haaland, Huebscher equivalent diameter, and a reverse solver
- **Psychrometrics:** Buck saturation, enthalpy, humidity ratio, dew point and wet bulb, density, and a live chart
- **Ventilation:** ASHRAE 62.1, 26 space types, Ez, Vbz to Voz
- **Pipe Hydraulics:** Darcy with a Hazen-Williams cross-check, Schedule 40 true ID, pump head and power
- **Water and Coil Loads:** Q = m cp dT including glycols, COP to EER to kW/ton conversions, coil duty and condensate
- **Fan Laws and Power:** affinity cube law, annual energy and cost
- **Room Cooling Load Estimator:** 11 editable gains, a load breakdown, and implied flows
- **Unit Converter:** plus property and design reference tables

Every tool shows its method and formula in the app, and checks its result against published design bands.

## 3D System Viewer

The viewer renders a plant room in Three.js using real downloaded models, not procedural geometry. All 5 models are CC0 from Poly Haven: an outdoor AC unit, a rectangular duct run, a circular duct run, an industrial pipe run, and a ceiling fan. The duct in the viewer switches shape with the Duct Sizer, round or rectangular. Full provenance for every model, including source, license, and repacking notes, is in [ASSETS.md](ASSETS.md).

## Use

Open the live site above, or open `index.html` in a browser. There is no build step and no backend. Three.js and the GLTF loader are self-hosted in `vendor/`; the only external load is Google Fonts.

## Standards and compliance basis

- ASHRAE 62.1 (ventilation)
- ASHRAE Fundamentals, Buck, Stull (psychrometrics)
- Darcy-Weisbach, Haaland, Huebscher (duct and pipe)
- ASME B36.10 (pipe sizes)
- CIBSE AM12 bands (design checks)

See the in-app Standards and Compliance Basis panel for details.

## Calculation record

Use the Calculation Record panel in the app (project, calc ref, prepared-by and checked-by) and download the calculation record (.txt) for the QA file.

## Important: design aid

MEP Suits is a design aid. It is not a substitute for full engineering judgement or local code compliance. All results must be verified and reviewed by a licensed engineer before construction or procurement. Input limits are enforced in code before calculation; non-finite entries fall back to design defaults.

## Security

- No backend, no accounts, no credentials, no secrets in this repo.
- No data leaves the browser.
- The page sets a Content Security Policy and no-referrer. The only external origin loaded is Google Fonts; scripts and 3D assets are self-hosted.
- Note: the single-file inline scripts require `script-src 'unsafe-inline'` in the CSP.

## License

MIT. See [LICENSE](LICENSE). The 3D models are CC0, see [ASSETS.md](ASSETS.md).
