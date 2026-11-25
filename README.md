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
- The **Light show**'s length is a Length button (15/30/60 s) instead of
  being fixed at 15 s.
- Fixed a bug where picking "Park lights" and pressing **Start strobe** (or
  starting it with the flasher lever) silently ran the Police pattern
  instead, because the pattern whitelist that feeds the Start button and
  the lever hadn't been updated when Park lights was added.
- The **Light show** no longer touches the park/running lights (aftermarket
  tails that play a startup animation on that circuit would replay it every
  pass through the show).
- **Reverse** and **Reverse + brake ("Tails")** lights, that never touch the
  park/running-light function either.
- Strobe tab layout: Lever start/While driving moved up, and Flash length
  plus Reverse/Tails now sit in the same "Lights" row as All lights/High
  beam, freeing the Pattern row back down to a comfortable width.
- Reverse and Tails are a **Lights** choice, not their own fixed pattern -
  Police, Strobe, In turn and the new **Chase** pattern (every light in the
  current selection, one after another, no pause - the closest thing to
  lights "moving" a one-function-at-a-time body controller can do) all run
  over them too.
- A fifth **Lights** choice, **Indicators** - brake and reverse only have one
  function code for both sides together, so they can't sweep left to right,
  but some aftermarket tails play their own sequential "flowing" animation
  off the turn-signal circuit specifically. Picking Indicators here is how to
  see that, without also flashing the headlights/fog/cornering lights.
- The Strobe panel is wider (900 px) and Light show narrower (636 px), so the
  six-button Lights row (All lights/High beam/flash length/Reverse/Tails/
  Indicators) has room without crowding the Pattern row underneath it.
- A **Lights off** toggle for the running/position lights, which the car
  gives no switch for at all - once it's on, it stays on (parked or not)
  until it's switched off again, re-asserting the lights off every half
  second since the body controller only accepts a function change for a
  limited time at a stretch. Headlights, brake and reverse aren't offered
  here: forcing those off while actually driving would be unsafe and
  illegal, and unlike the park/running lights there's no "off, but only
  while parked" variant of the function to fall back to.
- Police and Chase on Tails no longer flash the actual reverse/brake
  functions - those only have one function code for both sides together,
  so every flash just retriggers the tail light's own built-in sequential
  "coming home" fill animation on both sides at once, and which side looks
  lit at any instant comes down to where that animation happened to be,
  not anything the app is choosing (confirmed on video: the same
  Lights/Pattern recorded two different-looking results). The running
  lights don't have that animation, so Tails now flashes a brief brake
  pulse standing in for "the middle light", then parkR, then parkL - one
  way round (middle, right, left, repeat) rather than bouncing back and
  forth - on Chase that loops with no pause between laps, on Police it
  bursts four of each in turn with a pause at the end, same rhythm as
  every other Police entry. Brake is still the only address for that
  third/center light, so the pulse also flashes the main brake lamps each
  side, not only the middle one. This needs the car actually on (parkL/
  parkR won't do anything otherwise) - Strobe and In turn on Tails are
  unchanged (still reverse/brake) and keep working with the car off.

## Installing

Add this repo as a custom source in the Store (Settings → Sources →
Add), as `jaydrama21-ai/amblight`, branch `main`.

## Layout

Just the one app (`apps/ambient_config`) plus the slice of `kit/` its build
needs - not a mirror of the whole upstream monorepo.
