# Audio Logic Spec v0

Rules
- All intake pulls must use intakeFieldMap lookups and INDIRECT into 'Form 1 Raw' using ROW()
- No hardcoded intake column letters
- Use LET() for readability
- Output 0 when audioNeeded is not Yes

Helper function pattern (inline)
LET(
  r, ROW(),
  col, XLOOKUP("fieldName", intakeFieldMap!A:A, intakeFieldMap!B:B),
  INDIRECT("'Form 1 Raw'!" & col & r)
)

FieldMap
- audioFieldMap.csv is the contract. Use its field names.

Task
Generate formulas for:
- micCount
- micComplexityScore
- audioComplexityScore

Assumed intake field names for mics
- micQtyExact
- micQtyRange
- micTypes

Assumed intake field name for audio gating
- audioNeeded

Scoring
- micCount: exact if present, else parse range like "3-6" as midpoint, else parse "6+" as 6, else 0
- micComplexityScore: base 1.0, add 0.25 if headset or earworn, add 0.10 if lav, add 0.05 if handheld
- audioComplexityScore: use drivers already in the row when available, otherwise derive minimally from micCount and micComplexityScore
