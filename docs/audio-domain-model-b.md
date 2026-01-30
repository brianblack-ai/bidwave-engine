Audio Domain Model B
Purpose

This document defines the Audio Domain logic for BidWave using Model B architecture.
Model B separates schedule constraints, labor effort, and pricing presentation to produce quotes that are realistic, scalable, and resistant to double counting.

Audio Model B is designed to:

Be fully fieldMap driven

Avoid hardcoded column references

Scale tech counts based on schedule compression

Preserve labor hours as the source of truth

Support future inference of complete audio packages

Core Design Principles

Time is global, labor response is domain specific
Setup and strike windows are derived once from intake access times.
Each domain reacts independently to the same window.

Rush compresses time, not work
Schedule compression increases tech count.
It does not reduce required labor hours.

Push is logistics, not scope
Push modifiers apply to load-in and load-out only.
Setup and strike are governed by time windows and shortfall.

Labor math is authoritative
All pricing rolls up from tech count multiplied by billed hours per tech.
Display helpers never drive cost.

Inference over enumeration
Phase 1 audio quoting infers packages rather than enumerating every speaker.

Core Driver Fields

The following helpers are drift-safe and derived via field maps.

audioNeeded

audioTechRequested

houseSystemAvailable

zoneCount

playbackCount

monitorCount

micCount

micComplexityScore

livePerformanceFlag

riggingFlag

These fields define audio scope and complexity without embedding pricing assumptions.

Schedule and Pressure Model

Schedule pressure is derived directly from intake access times.

Intake Fields Used

setupAccess

setupCompletion

teardownAccess

teardownCompletion

Derived Helpers

setupTimeWindow

setupTimeShortfall

strikeTimeWindow

strikeTimeShortfall

Time windows represent available clock hours.
Shortfall represents required work exceeding the window.

Shortfall is the sole numeric driver of rush pressure.

Setup Labor Engine

Setup labor is calculated using the following chain:

audioSetupHours
Base hours derived from scope drivers and complexity.

audioSetupTechCount
Scales with setupTimeShortfall to fit work into available window.

audioSetupHoursPerTech
Derived from hours divided by tech count.

audioSetupBilledHoursPerTech
Snapped to industry billing blocks.

audioSetupLaborSubtotal
Tech count multiplied by billed hours multiplied by labor rate.

Setup labor responds to schedule compression by increasing tech count.

Strike Labor Engine

Strike mirrors setup with independent calculations.

audioStrikeHours

audioStrikeTechCount

audioStrikeHoursPerTech

audioStrikeBilledHoursPerTech

audioStrikeLaborSubtotal

Strike responds to teardown windows independently of setup.

Logistics and Push Model

Load-in and load-out are treated as logistics operations.

Push Inputs

setupPushReadable

setupPushModifier

strikePushReadable

strikePushModifier

Logistics Labor

audioLoadinHours

audioLoadoutHours

HoursPerTech and BilledHoursPerTech for each

Corresponding labor subtotals

Push reflects physical constraints such as distance, access, and elevation.
Push does not represent scope or rush.

Labor Rollup

All labor subtotals roll into:

audioLaborCost

This is the authoritative labor cost for the audio domain.

audioDailyRate is intentionally not used as a cost driver.

Rental Cost Strategy

audioRentalCost is designed to be inferred rather than itemized.

Phase 1 strategy:

Use default Gear Keys for inferred packages

Pull prices from gearPricingIndex

Sum inferred components

Planned inferred components:

PA package tier

Console tier

Wireless infrastructure

Stage monitoring package

Rigging adders

This avoids fragile enumeration while producing realistic quotes.

Known Deferrals

The following are intentionally deferred beyond Phase 1:

Detailed speaker counts

Individual amplifier modeling

Per-zone loudspeaker topology

Package level discounting

Presentation layer rounding rules

Summary

Audio Model B produces:

Schedule-aware staffing

Realistic labor pricing

Inference-ready rental costs

Zero hardcoded references

Clear separation of concerns

Audio is quote-complete once rental inference is wired.