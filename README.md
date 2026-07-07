[Acoustic_Simulation-README.md](https://github.com/user-attachments/files/29727848/Acoustic_Simulation-README.md)
# 🔊 Acoustic Simulation Suite (AS-V3.1)

**A self-contained, browser-based acoustic privacy and reverberation calculator for room-level noise control design.**

No installs, no servers, no dependencies — a single HTML file that runs entirely client-side in any modern browser.

---

## About

Acoustic Simulation Suite is a front-end engineering tool built to give designers, consultants, and project teams a fast, defensible first-pass estimate of a room's acoustic performance — before a specialist acoustic consultant or lab test gets involved.

It answers two questions for any enclosed space:

1. **Will occupants hear noise they shouldn't?** — modeled as a composite sound transmission loss problem across wall, glazing, and door assemblies, weighted by their real areas, benchmarked against room-type-specific targets drawn from BS 8233:2014.
2. **Will the room sound acoustically comfortable?** — modeled as a reverberation time (RT60) problem using Sabine's equation, applied per surface (wall, ceiling, floor, glazing, doors) rather than a single blended coefficient.

The tool was built to close a common gap in early-stage design: acoustic decisions (wall build-up, glazing spec, ceiling tile selection) are frequently made independently, by different trades, with no single view of how they combine. This suite forces those decisions into one model so the trade-offs are visible before they're built.

## Key Features

- **Tabbed workflow** — Geometry, Envelope, Structure, Finishes, and Noise Sources are organized as separate panels instead of one long form, matching how an acoustic assessment is actually built up.
- **Area-weighted composite transmission loss** — glazing and door area are calculated from real width × height × quantity, then combined with net wall area using logarithmic energy summation:

  ```
  TL_composite = 10·log₁₀( ΣSᵢ / Σ(Sᵢ · 10^(−TLᵢ/10)) )
  ```

  This replaces a fixed ratio approach with a physically correct model that responds to actual glazing-to-wall proportions.

- **Independent Rw / NRC treatment** — wall *construction* (blocks sound, rated in Rw) and wall *finish* (absorbs sound, rated in NRC) are modeled as separate, independent layers, because they are.
- **Room-type-driven compliance targets** — select a room type (Bedroom, Boardroom, Open-Plan Office, Classroom, Hospital Ward, etc.) and the tool applies the correct BS 8233:2014 internal noise target and RT60 comfort band automatically, rather than a single flat pass/fail threshold.
- **Three-tier compliance grading** — Compliant / Marginal (within 3 dB of target) / Non-Compliant, avoiding a false sense of precision at a hard cutoff.
- **Per-surface RT60 calculation** — floor, ceiling, net wall, glazing, and door absorption are summed individually rather than averaged, so hard floors and glazing are correctly modeled as low-absorption surfaces.
- **Logarithmic noise-source summation** — multiple simultaneous noise sources (traffic, HVAC, generators, conversation, etc.) are combined by sound energy, not simple dB addition.
- **Live simulation** — every field recalculates automatically on change; no need to re-trigger a report button.
- **Input validation** — invalid or empty fields are flagged inline (red border) and fall back to a safe default rather than propagating `NaN` through the results.

## Engineering Basis

| Calculation | Method |
|---|---|
| Composite transmission loss | Area-weighted energy summation across wall / glazing / door Rw |
| Reverberation time (RT60) | Sabine's equation, per-surface absorption (`0.161·V / ΣSᵢαᵢ`) |
| Combined noise sources | Logarithmic (energy) summation of incoherent sources |
| Plenum flanking penalty | Linear estimate based on ceiling-to-slab gap — flagged as a heuristic requiring on-site verification |

## Standards Referenced

- **BS 8233:2014** — Guidance on sound insulation and noise reduction for buildings
- **ISO 16283-1:2014** — Field measurement of airborne sound insulation (current standard; supersedes the withdrawn ISO 140 series)
- **ISO 717-1** — Rating of airborne sound insulation (Rw)
- **ASTM E336** — Standard test method for measurement of airborne sound attenuation between rooms

## Tech Stack

- Pure HTML5 / CSS3 / vanilla JavaScript — no build step, no framework
- Google Fonts (Inter, Roboto Mono) loaded via CDN link tag
- Fully self-contained single file — works offline once loaded, identical rendering across Chrome, Edge, and Firefox

## Usage

1. Download `Acoustic_Simulation_AS-V3.1-2026-011.html`
2. Open it in any modern browser — no server or installation required
3. Work through the tabs in order: **Geometry → Envelope → Structure → Finishes → Noise**
4. Select the applicable noise sources for the scenario being assessed
5. Review the Privacy Grade, Internal Level, RT60, and the compliance/treatment recommendations generated in the results panel

## Disclaimer

This tool produces **theoretical, diffuse-field estimates** intended for early-stage design comparison — not certified acoustic test results. Real-world performance depends on workmanship, sealing quality, and flanking paths (ducts, structural connections, unsealed partition heads) that a model cannot fully capture. All compliance-critical designs should be verified by on-site testing per ASTM E336 and confirmed with certified manufacturer laboratory data before submittal.

## Version History

- **V3.1** — Tabbed sidebar navigation (Geometry / Envelope / Structure / Finishes / Noise), live source count badge
- **V3.0** — Rebuilt transmission-loss model to be area-weighted and Rw-driven; added room-type compliance targets; per-surface RT60; live recalculation; input validation
- **V2.9** — Original single-scroll release

## License

Distributed for professional and educational reference use. No warranty of accuracy is expressed or implied — see Disclaimer above.
