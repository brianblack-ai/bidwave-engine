# BidWave Engine - AI Coding Agent Instructions

## Project Overview
BidWave Engine is a spreadsheet-driven AV (Audio Visual) quoting and labor estimation system. The runtime environment is Google Sheets and Google Forms, while this repository serves as the versioned source-of-truth for field mappings, logic specifications, QC rules, and documentation.

**Key Architecture:**
- **Intake Form**: Google Form for client inputs, mapped via `exports/intakeFieldMap.csv`
- **Calculation Sheets**: Google Sheets performing labor/cost calculations using field maps like `exports/universalFieldMap.csv` and `exports/ledWallFieldMap.csv`
- **Data Flow**: Form responses → Intake sheet columns → Calculation logic → Quotes

## Field Mapping Conventions
- **Format**: CSV files with headers like `Field Name,ColumnLetter,Purpose,Example Output,Notes`
- **Naming**: camelCase for field names (e.g., `gearCount`, `setupTimeWindow`)
- **Columns**: Excel-style letters (A-Z, AA-AZ, etc.)
- **Purpose Field**: Describes calculation role and data source (e.g., "Pulled from intake form / Used to scale setup and labor time")
- **Example**: See `exports/universalFieldMap.csv` for comprehensive labor estimation mappings

## Development Workflow
- **Changes**: Edit CSV field maps directly for schema updates
- **Versioning**: Commit changes to GitHub; runtime Sheets import from these CSVs
- **Validation**: No automated tests; manual QC via spreadsheet formulas
- **Deployment**: Manual import/sync to Google Sheets environment

## Key Files
- `exports/intakeFieldMap.csv`: Maps intake form questions to sheet columns
- `exports/universalFieldMap.csv`: Universal calculation fields with detailed purposes
- `exports/ledWallFieldMap.csv`: LED wall-specific calculation fields
- `Readme.md`: High-level project description

## Patterns to Follow
- When adding new gear types, create dedicated field map CSV (e.g., `exports/projectorFieldMap.csv`)
- Include detailed `Purpose` and `Notes` in universal maps for calculation transparency
- Use descriptive field names that match form question labels where possible
- Reference existing maps for consistent column ordering and naming patterns