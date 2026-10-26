# Windhawk-notification

Windhawk mod fork: **Windows 11 Notification Center Styler – BetterControl11 Unified**.

## Deliverable

- `Version 3.0.cpp` — **current version.** The buggy **Densy** option was removed
  entirely and rebuilt as **Liquid Glass 3.0** (iPhone-style liquid glass):
  1. *One continuous glass sheet* — control center, notification center, calendar
     and toasts share a deep backdrop-blur glass fill (BlurAmount 60, saturated
     theme-aware tint, solid fallback) that adapts to the wallpaper.
  2. *Circular glass buttons* — every quick-action tile is a 64px fully-round
     glass circle with a white glyph (accent fill when checked); split tiles get
     a small 32px chevron circle beside the main circle, so no pill can show a
     clipped or flat edge and no per-name patches are needed.
  3. *Now playing enclosed* — the media module is one self-contained glass card
     (rounded art, white title/artist) with the transport controls redistributed
     as three equal 44px glass circles.
  4. *Liquid capsule sliders* — brightness/volume are 12px fully-round capsules
     with a white fill and hidden thumb; header icons white, centred, unclipped
     (no transforms anywhere in the theme).
  5. *Trimmed labels* — one centred line per tile (`MaxLines=1`, character
     ellipsis), no wrapping or cut-off text.
  6. *Glass footer* — battery pill and settings circle match the tiles.
  The **Oversimplified & Accentuated** and **BetterControl11** options in this
  file are byte-identical to `Version 2.0.cpp` / `Version 1.0.cpp` (verified by
  diff); the default selection is `Liquid Glass 3.0`.
- `Version 2.0.cpp` — Oversimplified & Accentuated apple-style rebuild (2.0.1
  closes the Nearby sharing / Live captions pills), retained unchanged: entire
  panel frosted glass, white scaled-down icons, `$R=20` apple rounding with
  stitched split tiles, and a visible name for every option. Its
  **BetterControl11** option is byte-identical to `Version 1.0.cpp`.
- `Version 1.0.cpp` — BetterControl11 focus, retained unchanged.
  1. *Split tiles closed again* — the chevron half is opaque with the same state fills
     and complementary radius/border as the main half, so Wi‑Fi/Bluetooth read as ONE
     card with the chevron inside (v3's transparent chevron half regressed this).
  2. *White glyphs on checked tiles* — `Foreground@Checked*` = white on both halves of
     the tile (Wi‑Fi, Night light); no other icon is touched.
  3. *Slider icons unclipped* — the brightness/volume header icon rotations carry a
     small in-group translate (`TranslateTransform X="14"`) that lifts them clear of
     the card border.
  4. *Volume-slider crash fixed* — the shell crashed when the volume glyph changed
     state near the top of the range because the mod overrode `RenderTransform` on the
     volume slider's `AnimatedIcon` (AnimatedIcon drives its own transform during glyph
     state transitions). The rotation now sits on the icon's parent ContentPresenter.
  5. *Glassmorphism* — outer panels (control center, notification center, calendar,
     media card, toasts) use a backdrop `WindhawkBlur` glass fill
     (`GlassTint@Dark/#8C17171A`, `@Light`, plus solid `GlassFallback` for battery
     saver / transparency off) that adapts to the wallpaper; tiles, footer, slider card
     and all buttons keep their solid fills, so the glass never alters the buttons.
- `V1.0 beta.cpp` — beta, kept for reference.
  1. *Overlaps removed* — all label-into-card hacks (collapsed text stacks,
     `Margin=0,-36,0,36`, `Height=80`, `Transform3D` pushes) are gone; tiles use the
     native layout (icon card + label directly below), so text can never sit on an icon.
  2. *Uniform radius* — tiles built on the split template but shipped without a chevron
     page (Airplane mode, Energy saver, Night light, Mobile hotspot, Battery saver)
     rendered a flat right edge; per-name overrides close them with the same `$R` radius
     and full border as every other big button. The outer panel rectangles
     (`RootGrid`, `RootContent`, `ControlCenterRegion`) are forced to `$R` as well.
  3. *Music card* — outer radius unified with the buttons (`MediaTransportControls` +
     region at `$R`) and the pill backgrounds behind previous/play/next are removed
     (transparent, borderless) so the icons sit directly on the opaque card.
  4. *Slider icons* — brightness/volume header icons keep the centred in-place rotation;
     the volume L2 button returns to the v1 transform that stayed inside the card.
  5. Keeps what the v2 screenshot proved right: opaque media fill (`MediaBg`), stitched
     split tiles with accent checked state, single unclipped tile page, theme-aware
     `CardFill`/`CardStroke` resources, 60 unique deduplicated targets.
- `windows-11-notification-center-styler-bettercontrol11-unified-v2.wh.cpp` — v2, kept
  for reference. v2 fixes from on-machine screenshot review:
  1. *Transparent music card* — `Grid#MediaTransportControlsRegion` now fills with an
     opaque theme-aware backdrop acrylic (`MediaBg@Dark/@Light`), so the media card no
     longer shows the wallpaper.
  2. *Broken Wi‑Fi/Bluetooth tiles* — split tiles are stitched back into ONE closed
     card: main half gets `$RLeft` radius + `1,1,0,1` border, chevron half `$RRight` +
     `0,1,1,1` with the same fills (complementary sides ⇒ no seam line), and checked
     tiles regain the accent fill through `@CommonStates` backgrounds
     (`Checked`/`CheckedPointerOver`/`CheckedPressed`), so on/off tiles share one palette
     and every tile has the same shape.
  3. *Tile size like the original* — `Height=80` + `Margin=0,0,0,-36` on tile buttons and
     the collapsed-text-stack trick (`Height=0`, `Padding=-48,-8`, `Margin=0,16,0,-16`,
     title pulled up with `Margin=0,-36,0,36`, status collapsed) put the label back
     *inside* the card and restore the first version's bigger cards; grid `Height=375`
     with the pager collapsed keeps all tiles on one unclipped page.
  4. *Slider icons* — the brightness/volume header icon rotations now set
     `RenderTransformOrigin=0.5,0.5` (v1 rotated around 0,0, which displaced the icons),
     so they sit centred under their sliders.
  5. Everything else keeps the v1 rules: single radius `$R=16` everywhere (plus
     `ControlCornerRadius`/`OverlayCornerRadius`), closed cards with consistent gaps,
     theme-aware `CardFill`/`CardStroke` resources, 62 unique deduplicated targets.
- `windows-11-notification-center-styler-bettercontrol11-unified.wh.cpp` — v1, kept for
  reference; a complete,
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
   `Version 3.0.cpp` (current version; defaults to Liquid Glass 3.0 - switch to
   Oversimplified&Accentuated or BetterControl11 in settings for the earlier looks).
2. Compile and enable; the BetterControl11 Unified theme is preselected in settings.
3. Tweak the look via settings → *Style constants* (`R`, `cardBg`, `cardStroke`) or
   *Resource variables* (`CardFill@Dark/@Light`, `CardStroke@Dark/@Light`) without
   touching any target.

## License

GPL-3.0, same as the upstream mod. Original engine © m417z
(https://github.com/m417z/my-windhawk-mods).
