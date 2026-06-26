# Vessel profile — file format

A vessel profile defines the ship's layout (which bays exist, and each bay's
rows, tiers and deck/hold split). You import it **once** in the app under
**Settings -> Layout -> Import vessel profile**. It is saved on the phone and
synced to other phones that share the same Vessel sync code, so the layout is
set up without entering bays by hand.

Import accepts a JSON file (either form below) or a BAPLIE/EDIFACT file.

## Form A — compact, one entry per bay (recommended, easy to edit)

```json
{
  "vessel": "MUNICH MAERSK",
  "imo": "9778806",
  "bays": [
    {
      "bay": "02",
      "rows": ["00", "01", "02", "03", "04", "05", "06"],
      "deckTiers": [82, 84, 86, 88],
      "holdTiers": [2, 4, 6, 8, 10, 12, 14, 16]
    },
    {
      "bay": "06",
      "rows": ["00", "01", "02", "03", "04"],
      "deckTiers": [82, 84, 86],
      "holdTiers": [2, 4, 6, 8, 10]
    }
  ]
}
```

- `bay` — bay number as text (e.g. "02"). Use the 40 ft / even bay number.
- `rows` — the bay/row numbers present (00 = centre line, odds = starboard,
  evens = port, in normal container numbering).
- `deckTiers` / `holdTiers` — the tier numbers on deck (above the hatch) and in
  the hold (below). If you don't want to split them yourself, put everything in
  one list called `tiers` and the app decides deck vs hold by tier number.

## Form B — one entry per cell (e.g. exported from a planning system)

```json
{
  "vessel": "MUNICH MAERSK",
  "slots": [
    { "bay": "02", "row": "01", "tier": "82" },
    { "bay": "02", "row": "01", "tier": "84" },
    { "bay": "02", "row": "02", "tier": "82" }
  ]
}
```

The app also reads `pos` / `location` style combined codes (e.g. `"020182"` =
bay 02, row 01, tier 82) and many common field-name variants, so most planning
exports work without editing.

## What the app does on import

1. Reads the **vessel name** (if present) and sets it.
2. Collects every cell and works out, per bay: the **rows**, the **tiers**, and
   the **deck/hold split** (deck = tiers at/above the detected threshold,
   usually 80+).
3. Builds the **home bay list** automatically (existing bays keep their status;
   bays not in the file are removed).
4. **Saves** the profile so it persists and syncs to other phones.

## Notes

- A profile only needs the **cells**, not cargo. An "empty" layout file (cells
  with no containers) is exactly what's wanted.
- A normal cargo file (Arrival/Departure) only contains *loaded* slots, so it
  describes the ship only as far as it happens to be filled — fine in a pinch,
  but a full profile is better.
- See `vessel-profile-sample.json` for a complete working example (24 bays).
