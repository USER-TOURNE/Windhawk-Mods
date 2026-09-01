
# `Tourne'Table` **[Audio Visualizer]**
* `Images/GIF WIP`

> A real-time audio spectrum visualizer that displays directly on your Windows desktop.

Captures system audio output and renders frequency bars directly onto the desktop background.

The original **Visualizer Mod** by [Salyts](https://github.com/Salyts) used significant CPU resources by recursively polling the desktop. At idle - with no audio playing - CPU usage could reach **40–65% across multiple cores**.

Under sustained load, every core could be active every cycle, with temperatures reaching **68–71°C** before settling around **63–66°C** on an Ultra 265KF.

This fork aims to add features, improve functionality, and significantly reduce resource usage.

### Performance Improvements

- **Active CPU usage:** Less than 2% on a single E-core while actively rendering
- **Idle behavior:** Rendering stops entirely after silence is detected, eliminating unnecessary CPU/GPU usage
- **Idle temperature:** ~40°C peak, hovering around 36°C
- **Precision frame pacing:** Render thread only wakes as often as the configured target FPS requires

---

## Features

### Visual Styles

**8 Visualizer Shapes**

- **Stereo** - Classic frequency spectrum bars
- **Mountain** - Center-peak spectrum with bars tapering toward the edges
- **Mirror** - Bars grow inward from the edges toward the center
- **Wave** - Bars modulated by a sine wave over time
- **Breathe** - Slow breathing pulse synchronized with audio
- **Dots** - Bar columns constructed from stacked shapes
- **Radial** - Bars radiate outward from a center point like a clock face
- **Oscilloscope** - Traces the live raw waveform as a continuous line

### Color Modes

**9 Color Modes**

- **Solid** - Single flat color
- **Static Gradient** - Fixed color gradient across the visualizer
- **Reactive Gradient** - Gradient shifts toward a secondary color based on audio level
- **Windows Accent Color** - Automatically matches your Windows accent color and updates instantly when it changes
- **Album Art** - Extracts a dominant color from the currently playing track's cover art
- **Dynamic Album** - Creates a gradient from primary to secondary album-art colors, shifting with bar position and audio level
- **Acrylic** - Fixed RGB color with amplitude-driven alpha; nearly transparent at silence and semi-opaque at full volume
- **Rainbow Cycle** - Continuously animated hue rotation across the bars with adjustable speed
- **Tourne** - `Built-in teal-to-red preset gradient per my personal theme`

### Orientation & Animation

- **2 Orientations**
  - **Horizontal** - Bars grow vertically
  - **Vertical** - Bars grow horizontally

- **Vertical Anchor** - Control bar growth direction:
  - Bottom
  - Top
  - Middle

- **Peak Hold Caps** - Thin markers hang at each bar's recent peak and slowly fall, emulating classic hardware EQ displays

- **Beat Flash** - Brightens bars when bass hits are detected, layered on top of any color mode

> Peak Hold Caps are available on bar-based visualizer shapes.

---

## Now Playing Display

Displays the currently playing track's **artist and title** above the visualizer.

Media information is pulled directly from Windows' media session information and works with applications that report now-playing data, including:

- Spotify
- Web browsers
- Media players
- Other Windows Media Session-compatible applications

### Display Behavior

- Fades in when the track changes
- Fades back out after a configurable display duration
- Customizable text color
- Customizable font family
- Customizable font size

---

## Customization

### Bar Configuration

Configure virtually every aspect of the visualizer bars:

- **Bar Count:** 1–1000
- **Thickness**
- **Gap**
- **Maximum Size**
- **Idle Size**
- **Per-Corner Radius**

`Corner radius supports both single-value and individual-corner formats:`

`10`
or: 
`10 10 0 0`

### Position Control

Freely position the visualizer on any monitor using:

- **Horizontal percentage coordinates**
- **Vertical percentage coordinates**

### Background Effects

Optional desktop background panel with:

- **Custom padding**
- **Per-corner radius**
- **Custom border**
- **Custom ARGB hex colors for background and border**
- **Wallpaper blur effect**

---

## Audio Processing

### WASAPI Loopback Capture

Captures **all system audio output in real time** using WASAPI loopback.

### Real-Time FFT

- **7-band frequency spectrum**
- **Hann windowing**
- **Real-time processing**

### EQ Presets

Includes **6 built-in EQ presets**:

- **Balanced**
- **Bass**
- **Rock**
- **Pop**
- **Jazz**
- **Electronic**

### Sensitivity

Adjustable audio sensitivity from:
`**0–300**`

---

## Performance

Performance and resource usage are a major focus of this fork.

### Precision Frame Pacing

Replaced constant per-vsync polling with a **single high-resolution wait per frame**.

The render thread now wakes only as often as required by the configured target FPS instead of continuously polling the desktop.

### Cached Background Geometry

Background panels and borders are only rebuilt when their:

- **Size changes**
- **Shape changes**

They are no longer reconstructed every frame unnecessarily.

### Adjustable Frame Rate

Configure any target FPS value to prioritize either:

- **Maximum visual smoothness**
- **Reduced CPU/GPU usage**
- **Power efficiency**

### Fullscreen Pause

Automatically detects both:

- **Exclusive fullscreen applications**
- **Borderless fullscreen windows**

The visualizer pauses while fullscreen applications are active and automatically resumes when they close or exit fullscreen.

### Silence Detection

After a configurable period of silence, the visualizer reduces its refresh rate to conserve CPU/GPU resources.

Once the idle threshold is reached, **rendering stops entirely** until audio activity resumes.

### Auto-Hide When Idle

`Optionally fades the entire visualizer out during prolonged silence instead of simply leaving it rendered at a reduced refresh rate.`

---

`## Credits`

### [USER-TOURNE](https://github.com/USER-TOURNE)

CPU/render-pacing optimizations and feature additions included in this fork.

### [Salyts](https://github.com/Salyts)

Original author of **Desktop Audio Visualizer**.

### [GR0UD](https://github.com/GR0UD)

Audio visualizer code adapted from their work.

---

## About This Fork

This project builds upon the original Desktop Audio Visualizer with an emphasis on:

- **Lower resource consumption**
- **More efficient rendering**
- **Better frame pacing**
- **Expanded visualization options**
- **Dynamic album-art integration**
- **Windows-native media information**
- **Greater customization**
- **Power-conscious idle behavior**

The goal is simple:

> **Make the desktop move with the music - without making the CPU move mountains to do it.**
