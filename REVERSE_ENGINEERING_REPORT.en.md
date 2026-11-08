# REVERSE_ENGINEERING_REPORT — hl7.fhir.r4.sv

## A. General diagnosis

### Architecture identified
FHIR Implementation Guide (IG) based on SUSHI for Swedish language pack (HL7 Sweden / hl7.fhir.r4.sv). Structure:

- `input/hl7.fhir.r4.sv.xml`: IG definition (id, canonical, version, fhirVersion, pages, parameters)
- `input/translations/*.po`: 16 gettext translation files for CodeSystems
- `input/pagecontent/`: IG pages (index.md, translation-principles.md, etc.)
- `input/resources/`: only `place-holder.txt` (no real resources)
- `ig.ini`: IG publisher configuration
- `.github/workflows/validate-docs.yml`: CI to validate with Sushi and IG Publisher

### Technologies and dependencies
- SUSHI / fsh-sushi
- FHIR R4 (fhirVersion: 4.0.1)
- IG Publisher (Jekyll-based)
- No real FHIR resources (only place-holder.txt)

### Maintenance state
Default branch: main. Repository: https://github.com/HL7Sweden/hl7.fhir.r4.sv. Version 0.1.0.

### Existing testing mechanisms
No automated tests found. CI workflow exists (validate-docs.yml) but does not test FHIR content.

### Investigation limitations
- SUSHI not installed; IG build not executed.
- REA 6.7.0 not operational; static analysis only.

## B. Problems found

| ID | Title | Severity | Status | Location |
|----|-------|----------|--------|----------|
| REA-sv-001 | `hl7.fhir.r4.sv.xml` uses `releaselabel` (lowercase) | P3 | CONFIRMED | `hl7.fhir.r4.sv.xml:46` |
| REA-sv-002 | File `translation-princples.md` (typo) duplicated | P3 | CONFIRMED | `input/pagecontent/translation-princples.md` |
| REA-sv-003 | `input/resources/` contains only `place-holder.txt` | P3 | CONFIRMED | `input/resources/` |

### Details of confirmed problems

**REA-sv-001 (P3, CONFIRMED)**: The IG XML uses parameter `releaselabel` (all lowercase) on line 46. Although some SUSHI versions accept this spelling, the canonical form is `releaseLabel` (camelCase). This may cause compatibility issues with stricter SUSHI versions.

Evidence: `hl7.fhir.r4.sv.xml:46` — `<parameter><code value="releaselabel"/><value value="Working Copy"/>