# CORRECTIONS.md — hl7.fhir.r4.sv

Project: HL7Sweden/hl7.fhir.r4.sv
Base branch analyzed: main
Destination fork: https://github.com/admeduardovieira/hl7.fhir.r4.sv

## Corrections proposed

| ID | Title | Severity | Status | Risk | Files involved |
|----|-------|----------|--------|------|----------------|
| REA-sv-001 | `releaselabel` used instead of `releaseLabel` | P3 | PROPOSING | Low | `hl7.fhir.r4.sv.xml` |
| REA-sv-002 | `translation-princples.md` (typo) duplicated | P3 | PROPOSING | Low | `input/pagecontent/translation-princples.md` |
| REA-sv-003 | `input/resources/` only has place-holder.txt | P3 | PROPOSING | Low | `input/resources/` |

## Details of proposed corrections

### REA-sv-001 — releaselabel vs releaseLabel
**Problem:** `hl7.fhir.r4.sv.xml:46` uses `releaselabel` (lowercase) instead of `releaseLabel` (camelCase).
**Fix:** Change `<code value="releaselabel"/>` to `<code value="releaseLabel"/>`.
**Validation:** Confirm XML parses correctly with SUSHI.

### REA-sv-002 — Typo in pagecontent filename
**Problem:** `input/pagecontent/translation-princples.md` has a typo ("princples" instead of "principles") and duplicates the correct file.
**Fix:** Remove or rename the typo file.
**Validation:** Confirm only `translation-principles.md` exists.

### REA-sv-003 — Only place-holder in resources
**Problem:** `input/resources/` contains only `place-holder.txt`, no real FHIR resources.
**Fix:** Add real FHIR resources or remove the placeholder.
**Validation:** Confirm resources directory contains valid FHIR resources.

## Not implemented
None implemented in this execution; proposals for maintainers.

## Publication plan
- Fork: `admeduardovieira/hl7.fhir.r4.sv` (created).
- No code changes (only audit reports).
- Commit identity: `admeduardovieira <admeduardovieira@users.noreply.github.com>`.
- PR to `HL7Sweden/hl7.fhir.r4.sv` branch `main`.

Переклад технічний, виконаний автоматизовано; рекомендується перегляд носієм мови перед використанням якнормативного посилання.
