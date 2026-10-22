# Windhawk-notification

Windhawk mod fork: **Windows 11 Notification Center Styler – BetterControl11 Unified**.

## Deliverable

- `windows-11-notification-center-styler-bettercontrol11-unified.wh.cpp` — a complete,
  installable Windhawk mod (engine based on m417z's upstream
  `windows-11-notification-center-styler` v1.7, which is a superset of the 1.5.2 fork
  code this was reviewed from) with the **BetterControl11** theme rebuilt from scratch.
  The theme is also the mod's default (`theme: BetterControl11`), so installing the mod
  and reloading Explorer/Shell applies it immediately. All other upstream themes remain
  selectable.

## What "better" means here

The pasted BetterControl11 definition styled the same surfaces several times with
conflicting values, stitched surfaces together with half-rounded corners and partial
borders, and hid layout problems behind negative margins and 3D transforms. The rebuild
follows four rules:

1. **Uniform rounded corners** — one radius constant (`R=16`) drives every surface:
   quick-action tiles, slider card, footer (battery/settings) cards, media card,
   notification items, toasts, calendar surfaces, flyouts, jump lists and the
   top-level panels. Native WinUI controls follow the same radius through the
   `ControlCornerRadius` / `OverlayCornerRadius` resource overrides, so tooltips,
   menus and switches match too.
2. **No breaks** — every partial corner radius (`16,0,0,16`, `0,16,16,0`,
   `0,0,18,18`, `18,18,0,0`, `22,22,0,0`, `0,0,27,27`), every partial border
   thickness (`1,0,1,1`, `0,1,1,1`, `1,1,1,0`) and every negative-margin overlap
   used to stitch two surfaces into one was removed. Each surface is now a closed
   card (`cardBg` fill + 1px `cardStroke` border, both theme-aware for dark/light)
   separated from its neighbours by a consistent gap. The chevron half of split
   tiles is transparent and borderless, so a tile reads as one unbroken card.
3. **No page/clipping breaks** — the fixed `Height=375` quick-actions page and the
   pager dots are gone (`Height=Auto` + collapsed `PipsPager`), so all tiles live on
   one page and nothing is clipped; the text-hiding `Transform3D`/`Height=0` hacks
   that clipped tile labels were removed as well.
4. **Clean data** — 52 unique targets (down from ~90 entries with duplicates and
   contradictory repeats such as `Visibility=0` + `Visibility=1` on the same target),
   deep 15-level selector chains shortened with the `*` ancestor wildcard, and all
   visuals sourced from four constants (`R`, `transparent`, `cardBg`, `cardStroke`)
   plus four theme-aware resource variables (`CardFill`, `CardStroke` dark/light,
   `ControlCornerRadius`, `OverlayCornerRadius`).

Layout signatures of BetterControl11 are preserved: two-column quick-action grid,
vertical brightness/volume slider column on the right, battery + settings cards at
the top right, and the compact media card.

## Install

1. In Windhawk, open **New mod → Edit mod code** (or import from file) and paste
   `windows-11-notification-center-styler-bettercontrol11-unified.wh.cpp`.
2. Compile and enable; the BetterControl11 Unified theme is preselected in settings.
3. Tweak the look via settings → *Style constants* (`R`, `cardBg`, `cardStroke`) or
   *Resource variables* (`CardFill@Dark/@Light`, `CardStroke@Dark/@Light`) without
   touching any target.

## License

GPL-3.0, same as the upstream mod. Original engine © m417z
(https://github.com/m417z/my-windhawk-mods).
