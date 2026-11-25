# amblight

Personal fork of the `ambient_config` iDrive 7 (MGU22) app, split out on its
own so it doesn't get tangled up with tracking the upstream project's
`idrive7-apps` repo.

Based on [cauliflowermossgrape/idrive7-apps](https://github.com/cauliflowermossgrape/idrive7-apps),
with a couple of personal changes layered on top:

- A **Park lights** strobe pattern (parking/position lights left+right, no
  high beam at all).
- The light-function probe in `strobe.js` is more patient about bus
  contention right after a cold head-unit boot, and gets a second try
  before falling back to the less capable BDC_G05 path.
- A **While driving** toggle next to Lever start, so the strobe can be
  triggered with the flasher lever while rolling (for filming), without
  needing to touch the screen.
- A **Reverse lights** strobe pattern (the reverse lamp flashing on/off,
  nothing else).
- The **Light show**'s length is a Length button (15/30/60 s) instead of
  being fixed at 15 s.
- Fixed a bug where picking "Park lights" and pressing **Start strobe** (or
  starting it with the flasher lever) silently ran the Police pattern
  instead, because the pattern whitelist that feeds the Start button and
  the lever hadn't been updated when Park lights was added.

## Installing

Add this repo as a custom source in the Store (Settings → Sources →
Add), as `jaydrama21-ai/amblight`, branch `main`.

## Layout

Just the one app (`apps/ambient_config`) plus the slice of `kit/` its build
needs - not a mirror of the whole upstream monorepo.
