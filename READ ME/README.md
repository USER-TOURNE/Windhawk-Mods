# `Tourne'Table` **[Audio Visualizer]**

![Tourne'Table Audio Visualizer](REPLACE_ME_HERO_IMAGE)

> **A real-time audio visualizer that lives on your Windows desktop.**
> Built on the foundation of Salyts' Desktop Audio Visualizer, rebuilt around performance.

Play music. Bars dance on your wallpaper. That's the whole idea.

It listens to **whatever your PC is already playing** — Spotify, YouTube, a game, a call — and draws it behind your desktop icons. No virtual audio cable, no drivers, nothing to configure. It just picks up your system audio.

The original worked, but it ran *hot*. This project rebuilt how it draws itself: **same job, roughly half the CPU, 18 °C cooler**, plus a pile of new shapes, colors and controls.

## ABOUT THIS PROJECT

Built with an emphasis on lower resource consumption, more efficient rendering, better frame pacing, expanded visualization options, dynamic album-art integration, native Windows media info, deeper customization, and power-conscious idle behavior.

The goal is simple:

> **Make the desktop move with the music — without making the CPU move mountains to do it.**

---

## ◈ PERFORMANCE AT A GLANCE

| Metric | Salyts Original | Tourne'Table | Change |
|:--|--:|--:|--:|
| **Total CPU usage** | 13.77 % | **5.95 %** | **−56.8 %** |
| **Peak single-thread** | 78.06 % | **34.86 %** | **−55.3 %** |
| **CPU package power** | 53.09 W | **32.31 W** | **−39.1 %** |
| **CPU package temp** | 57.5 °C | **39.7 °C** | **−17.8 °C** |
| **Peak power draw** | 93.24 W | **40.44 W** | **−53 W** |

**Measured on an Intel Core Ultra 265KF:** CPU package temperature averaged **39.7 °C** *(peak 50 °C)*, with core temperatures averaging **35.4 °C**. The WPA trace puts the mod's own cost at **2.36 % of a single core**. When audio stops, rendering stops — not "slows down," *stops*.

Full methodology, raw numbers and honest caveats are further down.

---

## ◆ VISUAL STYLES

### 8 Shapes

| Shape | What it does |
|:--|:--|
| **Stereo** | Classic equalizer bars. Low notes left, high notes right. |
| **Mountain** | Peaks in the middle, tapers toward both edges. |
| **Mirror** | The opposite — grows from the outside edges inward. |
| **Wave** | Normal bars with a slow ripple rolling through them. |
| **Breathe** | A gentle swell that rises with the music instead of jumping. |
| **Dots** | Stacked dots instead of solid bars — old LED-meter look. |
| **Radial** | Bars shoot outward from a center point, like a sunburst. |
| **Oscilloscope** | A single line tracing the actual sound wave. |

### 9 Color Modes

| Mode | What it does |
|:--|:--|
| **Solid** | One flat color. |
| **Gradient** | Fades between two colors across the bars. |
| **Reactive Gradient** | Shifts toward the second color as things get *louder*. |
| **Windows Accent** | Matches your Windows accent color, updating instantly. |
| **Album Art** | Pulls the dominant color from the playing track's cover. |
| **Dynamic Album** | Gradient between the cover art's two strongest colors. |
| **Acrylic** | Grows more opaque the louder it gets — invisible in silence. |
| **Rainbow Cycle** | Continuously cycling hue, adjustable speed. |
| **Tourne** | Built-in teal → red gradient from my personal palette. |

### Plus

- **2 orientations** — bars grow vertically or horizontally
- **3 anchors** — grow from the Bottom, the Top, or **both directions from the Middle**
- **Peak Hold Caps** — thin markers hang at each bar's recent peak and slowly fall *(classic hardware EQ)*
- **Beat Flash** — bars brighten on detected bass hits, on top of any color mode
- **Multiband Oscilloscope** — the waveform tints toward whichever part of the spectrum is loudest

---

## ♪ NOW PLAYING DISPLAY

Shows the current **artist and title** above the visualizer, pulled from the same Windows media session that powers your volume popup. Works with Spotify, browsers, and most media players.

Fades in on track change, fades out after a configurable delay. Custom color, font family and size.

---

## ◐ THE PALETTE

This project follows my personal theming palette — reflected in the repo screenshots. It can be changed to any hex / RGB / RGBA value you want.

| Name | Hex | RGB |
|:--|:--|:--|
| Green | `#15ffa2` | `21, 255, 162` |
| Red | `#ff8f8f` | `255, 143, 143` |
| Pale Green | `#64aa89` | `100, 170, 137` |
| Alt Pale Green | `#6ba6a0` | `107, 166, 160` |
| Pale Red | `#a95d5d` | `169, 93, 93` |
| Dark Teal *(background)* | `#121c21` | `18, 28, 33` |

The built-in **Tourne** color mode is drawn from these.

---

# ✦ EVERY SETTING, EXPLAINED

**You don't need any of this to use the mod.** The defaults work. This is for when you want to tweak something and you're wondering what a word means.

## Appearance

**Shape** — Which of the 8 styles above to draw.

**Orientation** — *Horizontal* = a row of bars growing up and down. *Vertical* = a column growing left and right.

**Bar Count** — How many bars. More = finer detail, wider visualizer. Range **1–2048** (enough to span a 4K or ultrawide screen).

**Bar Width** — How fat each bar is, in pixels.

**Bar Gap** — Space between bars, in pixels. Set to `0` and they touch.

**Bar Max Size** — How tall a bar gets at full volume. This is the overall height of the visualizer.

**Bar Idle Size** — How tall bars sit in silence. `0` makes them vanish completely; a few pixels leaves a thin resting line.

**Bar Corner Radius** — How rounded the bar corners are. One number rounds all four equally, or give four numbers separated by spaces for individual control: `top-left top-right bottom-right bottom-left`. Example: `5 5 0 0` rounds only the top.

**Color Mode** — Which of the 9 coloring styles above to use.

**Color** — The color used in Solid mode. Format is `#AARRGGBB` or `#RRGGBB` — that's **A**lpha (transparency), then **R**ed, **G**reen, **B**lue in hex. Lower the first two digits to make it see-through.

**Gradient Color 1 / 2** — Start and end colors for the gradient modes.

**Sensitivity** — How hard the bars react. Too low and quiet music barely moves them; too high and everything slams to max. Range 0–300. Turn it down for bass-heavy tracks, up for quiet recordings.

**EQ Preset** — Which frequencies get emphasized *visually*. Doesn't touch your actual audio.
`Default` no adjustment · `Bass` boosts lows · `Rock` boosts mids and highs · `Pop` heavy on highs · `Jazz` warmer, gentler highs · `Electronic` boosts bass and treble, scoops the middle.

**FFT Size** — How finely sound gets analyzed. An FFT is the math that splits audio into separate frequencies — think of it as sorting sound into buckets by pitch. More buckets = finer detail, slightly more CPU.
`1024` fastest, plenty for most · `2048` / `4096` noticeably crisper · `8192` maximum detail.

> **Note — this is an admittedly 'beta' implementation for now.** Everything up to `8192` runs near-flawlessly with almost no overhead, *with the caveat that you're using anything other than the Oscilloscope shape.*
>
> **One more note:** the higher the FFT Size, the more accurate the Sensitivity slider becomes for your specific audio setup. The correlation generally runs: **as FFT Size goes up, your Sensitivity will need to go up too.** For now that means fine-tuning Sensitivity per EQ Preset *and* per FFT Size, for your particular placement, size and personal adjustments.

**Frequency Scale** — How the frequency range spreads across the bars. This matters more than it sounds.
- **Log** — the natural-feeling default. Gives bass and treble roughly equal visual space, matching how humans hear pitch.
- **Linear** — spreads by raw Hz. Since most musical energy lives low, this crams all the action into a sliver on the left and leaves the right mostly dead. Technically accurate, visually dull.
- **Mel** — uses the *mel scale*, built from research on how people actually perceive pitch. Like Log, tuned to human hearing.

**Peak Frequency Readout** — Shows the loudest note as a live number, e.g. `1.2 kHz`.

**Peak Readout Position** — Where that number sits. Horizontal: Left / Center / Right. Vertical: Above / Top / Middle / Bottom / Below.
> **Above** and **Below** place it fully *outside* the bars so it never overlaps the visualization.

**Multiband Oscilloscope Coloring** — Only affects the Oscilloscope shape. The line tints toward whatever part of the spectrum is loudest — warm for bass, green for mids, blue for treble. Overrides Color Mode for that shape.

**Anchor** — Which edge bars grow from. `Bottom` rise upward *(classic)* · `Top` hang downward · `Middle` grow **both directions** from a center line.

**Peak Hold Caps** — Leaves a thin marker floating at each bar's recent peak, which slowly drifts down.

**Beat Flash** + **Intensity** — Flashes bars brighter on bass hits. Intensity controls how hard.

**Rainbow Cycle Speed** — How fast the rainbow rotates. Rainbow mode only.

**Now Playing Text** — Toggles the artist/title display.

**Now Playing Color / Font / Font Size** — Styling for that text. The font must be **installed on your system** — type the exact family name. Windows silently falls back to a default on a typo rather than erroring, so double-check spelling if nothing changes.
> The Peak Frequency Readout shares these same font settings.

**Now Playing Display Seconds** — How long the text stays up after a track change before fading.

## Position

**Horizontal Position** — Left-to-right placement as a percentage. `0` hard left, `50` centered, `100` hard right.

**Vertical Position** — Top-to-bottom, same idea. `0` top, `100` bottom.

**Monitor** — Which screen to draw on. `1` is your first monitor.

## Background

**Enabled** — Draws a panel behind the bars. Turn off for bars floating directly on the wallpaper.

**Color** — Panel color in `#AARRGGBB`. The alpha controls transparency.

**Padding** — Breathing room between the bars and the panel edge.

**Corner Radius** — How rounded the panel corners are. Same one-or-four-value rules as bar radius.

**Blur** — Frosted-glass blur of your wallpaper behind the panel. `0` disables.
> This used to be the single most expensive setting in the mod. It's now computed once and cached, so it's essentially free per frame.

**Border Size / Border Color** — A thin outline around the panel. `0` for none.

## Performance

**Target FPS** — How many times per second it redraws. Higher = smoother, more CPU. Little point exceeding your monitor's refresh rate.

**Pause On Fullscreen** — Stops completely when a fullscreen app runs. Detects both true fullscreen *(games)* and borderless windows. Since the visualizer lives on the desktop it's invisible anyway — this just stops it burning power. Resumes automatically.

**Pause When Silent (seconds)** — After this long without audio, drops to a trickle instead of full speed. `0` disables.

**Auto-Hide When Idle** + **Delay** — Fades out entirely after prolonged silence. Once fully faded it **stops rendering completely** — not just invisible, genuinely doing nothing until audio returns.

**Pause When Covered** — Stops rendering *and* audio capture while fully hidden behind another window.
> **Off by default.** Reliably detecting "am I covered?" on Windows 11 is genuinely tricky — the shell is full of invisible windows that report themselves as visible. The check is deliberately conservative (only a fully-covering, real application window counts), but if the visualizer ever vanishes when it shouldn't, this is the switch to flip.

---

# ▲ WHAT ACTUALLY GOT FIXED

In rough order of measured impact.

### 1. Precision frame pacing — the biggest single win

The original paced itself with `DwmFlush()`, which blocks until the monitor's next refresh. That meant the render thread woke **on every vertical blank, forever** — 60, 144, 240+ times a second — regardless of target FPS, whether anything needed redrawing, or whether the visualizer was even visible.

This barely registers as CPU% in Task Manager, because the thread is blocked, not spinning. But every wake-up drags a core out of deep idle. Do that continuously and the core never settles into its efficient sleep states — which reads as a small, permanent bump in package power and temperature. The classic "low usage, still runs warm" signature.

> **Note:** this becomes exponentially more noticeable on AMD architecture.
>
> **Note:** also exponentially more noticeable if you have **C-States disabled** in your BIOS or elsewhere. Shoutout to Process Lasso, Core Director, Park Control and HWiNFO64 for helping me debug why the hell all my E-cores were sitting at 65–70 °C when they were supposed to be idle during initial testing with Salyts' original mod.

**Fixed with** a high-resolution waitable timer firing only at the configured rate. Plain `Sleep()` wasn't good enough — it's quantized to ~15.6 ms, which would turn a 60 FPS target into stuttery 30–40 FPS.

### 2. Pre-rendered background blur

A Gaussian blur is a full-image convolution — the most expensive thing Direct2D does in this scene. The original recomputed it **from scratch every frame**, despite its input (your wallpaper) never changing.

**Fixed by** computing it exactly once into a cached bitmap, then just copying that each frame. The cache covers only the widget's bounding box, replacing roughly **8 MB of video memory with tens of KB**. It re-bakes automatically if the widget moves or resizes.

### 3. Widget-sized render surface

The render surface spanned the **entire desktop** even though the visualizer occupies a thin strip. Every frame cleared and presented millions of untouched pixels, with two full-desktop buffers parked in VRAM.

**Fixed by** sizing the surface to the widget's bounding box and offsetting the composition layer to position it. Cuts per-frame pixel work and VRAM by roughly an order of magnitude.

### 4. Cached geometry

The background panel and border were rebuilt from scratch every frame — allocating a path geometry, constructing four lines and four arcs by hand, then discarding it. Now rebuilt only when size, padding, radii or border width actually change. In normal use, almost never.

### 5. Cached monitor lookup

Every frame called `EnumDisplayMonitors()` — a real round-trip through the display driver stack — to work out which monitor to draw on. Now resolved once and cached, refreshed on display change.

### 6. Reduced frame latency

DXGI queues up to three frames ahead by default. For a passive widget that's pure latency and power draw with no upside. Capped at **1**.

### 7. Genuine idle shutdown

**Auto-Hide** now stops rendering completely once faded — presents one blank frame, then exits the render path entirely. **Pause When Covered** stops rendering and capture while hidden, checked once per second rather than per frame.

---

# ▦ THE FULL BENCHMARK DATA

Two independent measurement methods, both on an **Intel Core Ultra 265KF**.

## Method 1 — HWiNFO64 sensors

Identical 3-minute runs: 1 min silent → 1 min 30 s audio → 30 s silent.

### Stability — the less obvious win

Averages only tell half the story. The **spikiness** dropped even harder:

| Metric | Before | After |
|:--|--:|--:|
| CPU — median | 11.40 % | **5.50 %** |
| CPU — 95th percentile | 23.97 % | **8.10 %** |
| CPU — maximum | 34.40 % | **12.20 %** |
| CPU — standard deviation | 5.36 | **1.45** |
| Power — 95th percentile | 71.32 W | **36.78 W** |
| Power — maximum | 93.24 W | **40.44 W** |
| Power — standard deviation | 9.85 | **2.57** |

Standard deviation fell ~73 % on CPU and ~74 % on power. The original wasn't just heavier on average — it worked in **bursts**, and bursts are what drive thermal spikes and fan ramping.

That matches the root cause the profiler found: a render thread waking on every vsync, and a full-image blur re-evaluated every frame. Both bursty, repetitive workloads — exactly the profile that produces this variance.

### GPU — unchanged, as expected

| Metric | Before | After |
|:--|--:|--:|
| GPU core load | 7.66 % | 7.92 % |
| GPU D3D usage | 7.41 % | 7.20 % |
| GPU power | 21.81 W | 21.24 W |
| GPU temperature | 35.6 °C | 36.5 °C |

**These differences are inside measurement noise — don't read them as real changes in either direction.** A flat GPU reading is exactly the right outcome here: this workload was never GPU-bound. It sits at 7–8 % in both builds. The blur fix moved work off the CPU-side Direct2D path; it was never going to show as a GPU reduction at this scale.

I'm still working on the GPU side — I'd like both CPU and GPU sitting at a 3 % ceiling. It's already better than these numbers show; `.etl` traces are just enormous and parsing them means fighting a Windows tool currently stranded in a dead preview branch. Forgive me.

### Memory

Sensor logs only report system-wide memory, which includes every other application running — so those totals say nothing useful about this mod and aren't reproduced here.

What *is* known, from the changes themselves: the cached blur dropped from a full-desktop bitmap to a widget-sized one — roughly **8 MB of video memory replaced by tens of KB** at 1080p — and the render surface went from two full-desktop buffers to two widget-sized ones, cutting that allocation by an order of magnitude.

## Method 2 — Windows Performance Analyzer

Same protocol, normalized per second of runtime:

| | Salyts Original | Tourne'Table |
|:--|--:|--:|
| CPU time attributed to mod | 7,736.60 ms | 4,251.18 ms |
| Trace duration | 176.74 s | ~180 s |
| **Normalized cost** | **43.77 ms/sec** | **23.62 ms/sec** |
| As % of one core | 4.38 % | **2.36 %** |
| **Reduction** | — | **−46.0 %** |

### Why −46 % understates it, and how I handicapped myself to show the gains ♥

The two exports came from different WPA tables measuring different things:

- **Salyts'** is the *Sampled* table grouped by Module. It counts only samples where the CPU was executing **inside his DLL itself** — *exclusive* time. It does **not** include time his code spent inside `d2d1.dll` doing the actual drawing.
- **Tourne'Table's** is the *Precise* table with call stacks — *inclusive* time, counting everything downstream, D2D and kernel included.

Since the overwhelming majority of this workload's cost lives inside `d2d1.dll` rather than the mod's own logic, the original's true inclusive cost would be substantially higher than 7,736 ms. **My all-in number is being compared against his self-time-only number, and still comes out 46 % lower.**

### And my build was doing *a lot* more work

I ran an **older build of mine** for these tests — one with unfixed and notably half-implemented features, and considerably fewer optimization passes behind it than the current release.

It was still carrying all of the following, none of which exist in Salyts' original that it was tested against:

- **FFT size 2048** — double the original's fixed 1024, so twice the samples per analysis pass
- **Mel frequency scaling** — extra per-bar warp computation every frame
- **Peak hold caps** — additional per-bar state and draw calls
- **Beat flash** — per-frame transient detection and color modulation
- **Now Playing text** — live DirectWrite text rendering
- **Reactive gradient** vs. the original's flat solid color

Everything else was closely matched: 99 bars, 2 px wide, 1 px gap, middle anchor, ~144 target FPS, blur 33 vs 35, 1 px border, same position. **`pauseWhenObscured` was off**, so the newest optimization contributed nothing here.

### A miss I'll own: Auto-Hide wasn't helping

My test run had Auto-Hide on with a 45-second delay, which fired during both silent stretches. That did **not** give me an unfair advantage — quite the opposite. It was a broken implementation I slapped together on no sleep, and it *cost* me efficiency during my own benchmark. Oops.

The version I benchmarked faded opacity toward zero but **kept rendering the full scene underneath**, plus an extra `PushLayer`/`PopLayer` pair. Once faded it was doing strictly *more* work while showing nothing.

I genuinely missed an obvious optimization before running the comparison. **It's fixed now** — when the scene is fully transparent, rendering is skipped entirely instead of drawn and then hidden. It was built that way originally to shave frame time on scene wake, and I clawed that 0.08 ms back elsewhere.

## Honest caveats

The large deltas are far outside anything noise could explain, but the methodology has real limits:

1. **System-wide, not process-isolated** — HWiNFO measures the whole machine, and the two runs were ~3 minutes apart. The CPU/power/thermal deltas are far too large to be explained this way, but these aren't clean attributions to the mod alone. *(This applies to the HWiNFO numbers only — the WPA traces cover exactly where sensor testing falls short.)*
2. **Small sample size** — ~37 samples per run. Fine for headline effects, not enough to resolve anything under a few percent.
3. **Single run each** — no repeats, so run-to-run variance is unknown.
4. **I handicapped myself on conditions.** Salyts' build was tested on a fully idle system. Mine was tested while screen recording, opening and closing windows, and actively working in applications — which meant Windows 11 did Windows 11 things and spiked clocks via its newer app-launch optimizations.

---

## ♥ CREDITS

**[USER-TOURNE](https://github.com/USER-TOURNE)** — Author and maintainer: performance work, new features, benchmarking and documentation.

**[Salyts](https://github.com/Salyts)** — Original author of Desktop Audio Visualizer. This project exists because the foundation was good enough to be worth optimizing. Author of his own mod and repo; a contributor toward this one.

**[GR0UD](https://github.com/GR0UD)** — Audio visualizer code the original was adapted from. Author of his own work; a contributor toward this one.

### A coincidence worth acknowledging

While I was midway through my initial testing, **NeiZ** (author/maintainer, with **SuperSmile123** contributing) released [Desktop Audio Visualizer Plus](https://github.com/ramensoftware/windhawk-mods/commit/e01d0d0dbd6204804235831fd7f68821e4614028) (`neiz-supersmile-audio-visualizer`). I had planned to publish my own commit that same night — holy coincidence.

His release spurred another round of testing on my end, and I've since gone through roughly twelve more iterations. I didn't want to ship something that essentially achieved what I was already going for, especially if they'd figuratively led me out to pasture to put a bullet in me — aha.

To be explicit about attribution: **I did not borrow from or reference NeiZ or SuperSmile123's work at any point**, other than benchmarking theirs for efficiency to decide whether continuing development was worth it. Thanks to them and their contributors regardless.

---

## ◘ LICENSE

Released under the **MIT License**.

```
MIT License

Copyright (c) 2026 USER-TOURNE

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### In the spirit of the WTFPL

> **0. You just do what the fuck you want to.**
>
> Take it. Fork it. Gut it. Rewrite the parts I got wrong. Ship it. Sell it.
> Learn something from it and never speak to me again.
>
> The only thing MIT actually asks is that the copyright line rides along —
> keep the notice, and we're square.
>
> *(I went with MIT over the real WTFPL for one boring reason: this thing
> injects a DLL into `explorer.exe`, and MIT comes with a warranty disclaimer.
> The WTFPL does not. Same energy, fewer ways for my life to get complicated.)*

### Third-party notices

This project builds on upstream work by **Salyts** and **GR0UD**. Their original
code carries its own license terms — if you redistribute this, carry their notices
along with mine.

---

## ❖ SUPPORT

If this saved you some degrees, some watts, or just made your desktop nicer to
look at, you can throw something in the hat. Entirely optional, genuinely appreciated.

**[ko-fi.com/tourne](https://ko-fi.com/tourne)**
