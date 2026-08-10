# 🐢 Turtles Under Care

Daily-operations workflow for Curaçao's sea turtle care program. It pulls turtle intake and check-up records from EarthRanger, filters down to turtles currently housed at a rescue centre or sea aquarium, and produces a dashboard grouped by disposition location or turtle number, so care staff can see at a glance how many turtles are under care, their measurements, and any health flags.

## Dashboard

Three widgets, split into a tab per group (see [Grouping](#-grouping)). Switching tabs filters every widget to that group's data.

**Stat cards**

| | Card | Shows |
|---|------|-------|
| 🐢 | **Total Turtles Under Care** | Count of turtles currently under care |
| 🩺 | **Turtles with FP** | Count of turtles with fibropapillomatosis recorded |

**Summary table** — *Turtles Under Care*, one row per check-up event. Sortable, filterable, downloadable.

| Column |
|---|
| Disposition Location |
| Turtle number |
| Species |
| FP (Y/N) |
| Days in care |
| Weight (kg) |
| Curved Carapace Length (cm) |
| Curved Carapace Width (cm) |
| Straight Carapace Length (cm) |
| Straight Carapace Width (cm) |
| Tail Length (cm) |
| Abnormalities |

## Event types

| Event type | Used? | Notes |
|---|:---:|---|
| Turtle Data Form V2 | ✅ | The only event type fetched. Carries intake measurements, disposition, and health flags for each turtle check-up. |

## Under care definition

"Under care" means the Disposition Location field on the event is Rescue Center or Sea Aquarium. Records with any other disposition (a beach name, released, deceased, or other) are excluded before grouping and display.

## State filter

Filter on event state (Active, Resolved), with multiple values selectable. Defaults to Active. If left empty, events of all states are included.

## 🗂️ Grouping

The dashboard groups by Disposition Location (default) or Turtle Number, selectable via the `groupers` field.

| Group by | Splits the dashboard into |
|---|---|
| Disposition Location | A Rescue Center tab and a Sea Aquarium tab |
| Turtle Number | One tab per turtle, useful for reviewing a single turtle's check-up history in isolation |

## Days in care

Days in care is computed as today minus the date recorded on the Turtle Data Form. "Today" is taken from the workflow's own configured time range (`until`) rather than the real wall-clock date, so a run always classifies days in care consistently with whatever period it was configured to look at, including re-runs against a past window. If the form's date field is empty, the event's own timestamp is used instead.

## ⚙️ Requirements

[pixi](https://pixi.sh) is required for environment and dependency management. You will also need an EarthRanger connection configured for the `curacao` data source.
