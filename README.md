# Video Surfer

*Browser-based video synthesis for riding the standing waves.*

**v1.2**

A web-native experimental video synthesizer in the lineage of analog video tools like the Rutt/Etra Scan Processor, the Sandin Image Processor, and the Paik/Abe Video Synthesizer. Built to bring some of that esoteric corner of video art history within reach of anyone with a phone, laptop, or tablet — no hardware, no install, no signup.

Made by **Slow Cities**.

---

## Try it

Open the deployed version in any modern browser (mobile or desktop):

→ **(https://github.com/slowcities/video-surfer/)**

The whole thing is a single HTML file. Camera, microphone, and audio decoding require an HTTPS context, which means a hosted URL — opening from `file://` will load the synth but those features won't work.

---

## What's inside

**Two oscillators** with sine, triangle, square, and saw waveforms, sweeping along horizontal, vertical, radial, or diagonal axes. Each oscillator has its own hue (ROYGBIV presets plus a continuous hue dial) and its own independent drift rate — letting them scroll past each other at different speeds to produce phasing, beating, and counter-motion that purely time-locked modulation can't. Each oscillator also has its own unique modulator: Osc1 has FM, Osc2 has color drift.

**Cross-modulation (FM) on Osc1** — Osc2 modulates Osc1's phase, which produces the same kind of harmonic spreading and complex textures FM gives you in audio. An FM Amt control sets the depth, and an FM Mod control lets LFO1 wobble that depth over time so the FM texture breathes (independent of whatever else LFO1 is assigned to; at zero it does nothing).

**Color drift on Osc2** — toggles continuous hue cycling for Osc2 only, borrowing one of the oscillators' drift rates to set the speed (Off / O1 / O2 / Both, where Both sums the two rates). A Division selector (1, ½, ¼, 1/10) gears the cycle down for slower color evolution. This keeps Osc1 as a stable color anchor while Osc2's hue wanders, so the overlap zones between them constantly recolor against a fixed reference.

**Two LFOs**, kept as the slow, autonomous foundation layer, with sine, triangle, square, and sample-and-hold shapes. Each owns its matching oscillator plus two feedback parameters: LFO1 routes to Osc1 frequency, Osc1 hue, feedback amount, or feedback hue; LFO2 routes to Osc2 frequency, Osc2 hue, feedback zoom, or feedback rotation. Between them the two LFOs can modulate all four feedback parameters — so the feedback engine can swell, recolor, breathe, and counter-rotate on its own with no hands on the controls. The rate sliders are shaped logarithmically, giving fine control through the slow range where the most useful motion lives (full range roughly 0.01 to 5 Hz, with most of the slider travel devoted to the slow end). They start silent; dial in as needed.

**Rutt/Etra displacement** of the rendered pattern onto a 3D mesh, viewable as wireframe (the classic 1973 scan-line look) or shaded solid, with tilt, rotation, and zoom controls. The original Rutt/Etra used a CRT and a camera angled at it; this is the same idea in shader math. Off by default, so the synth boots showing the flat oscillator pattern — switch it on to fold the image into 3D. A Rot Drift control can continuously rotate the mesh at a rate borrowed from one or both oscillator drift sliders, with a Division selector (1, ½, ¼, 1/10) for gearing the rotation down to meditative speeds.

**Frame feedback** with independent amount, zoom, rotation, and hue shift on the prior frame. Push amount past 0.9 with small zoom and rotation offsets for infinite-tunnel territory. All four feedback parameters are reachable by the LFOs for autonomous evolving motion.

**Burst button** — a momentary trigger that pushes the feedback loop into instability for as long as you hold it. Three styles: White (CRT overload), Color (saturating hue rotation), Geom (resonance amplification of pattern structure). Spacebar works as a keyboard shortcut, and the button can be mapped to a MIDI pad — it auto-detects whether your pad is momentary or toggle-style.

**Video input** from either the device camera or a loaded video file (MP4/H.264 recommended; WebM and MOV work where the browser supports them). Either source can act as a background, a displacement source for the Rutt/Etra mesh, or both simultaneously — point a camera at a candle or drop in a clip of moving water and it becomes terrain the synth flows over. Camera mode offers a device selector (built-in cameras, USB webcams, and HDMI capture devices all appear once permission is granted), front/rear facing for phones, and mirroring; video-file mode offers play/pause, position scrubbing, and looping, with the file's own audio muted by default and an unmute option. Footage with clear light/dark structure and slower movement reads more legibly as displacement than fast-cut, highly detailed video. Because capture devices appear in the selector, you can feed external video — a camcorder, another synth's output, or any HDMI source through a USB capture dongle — straight into the synth as a live texture.

**Audio reactivity** from either a loaded file (MP3, WAV, M4A, OGG, FLAC) or live microphone input. The signal is split into bass, mid, and treble bands, each independently routable to a destination (mesh displacement, oscillator frequency, feedback amount, feedback rotation, brightness) with its own depth. Mic mode is analyzed only — no signal is routed back to your speakers.

**Drag and drop** an audio or video file anywhere onto the window to load it — audio files route to the audio engine, video files to the video engine. This avoids the file-picker focus change that can drop a fullscreen output window. A standard file picker is also available for each.

**MIDI control** of any slider, segment toggle, or the burst button via WebMIDI. Click "Learn," click a control, move a knob on your MIDI device — bound. Pickup mode prevents parameter jumps when bindings recall to different positions, log mapping makes the full knob range musically usable for wide parameters like frequency, and parameter smoothing masks the resolution limits of 7-bit MIDI. Mappings persist across sessions.

**Dual-window output** for performance with an external display. The "Pop Out Visual" button opens a clean visual-only window — drag it to your projector or HDMI monitor, press F for fullscreen, and the main window's UI stays on the laptop while only the visuals go to the display. When popped out, the laptop preview is hidden and rendered at lower resolution to keep GPU costs low.

**Background options:** black for emission, white for ink, chroma green (#00B140) for keying the output into a video mixer or compositor.

---

## Getting started

A few patches to try after you open it:

**Drift duet.** Set Osc1 axis to H, Osc2 axis to V. Give Osc1 a drift of +0.3 and Osc2 a drift of -0.4. Both at amp 0.7. Watch them weave through each other at their own paces — no LFO needed.

**Tunnel.** Turn feedback amount up to 0.93, feedback zoom to 1.005, feedback rotation to 0.008. Add a tiny feedback hue shift. The pattern recursively echoes inward.

**Camera terrain.** Set Video source to Camera, enable it (rear), Mode to Disp, Rutt/Etra mode to Wireframe, Disp around 1.0, Tilt around 0.6. Point at something with strong contrast. Add a touch of FM for surface chaos. Works the same with a video file as the source — drop in footage of water, clouds, or shifting light.

**Voice control.** Switch Audio source to Mic, enable it, set Bass → Disp at amount 0.8, Treble → Feedback at 0.4. Sustained vowels move the mesh; sharp consonants inject feedback bursts.

**Kick-stab burst.** Load a track with strong kicks. Bass → Feedback at amount 1.0. Then tap the Burst button (or spacebar, or your mapped MIDI pad) on the off-beats. Audio drives automatic visual punctuation; you supply manual counter-punctuation.

**Autonomous feedback.** With a feedback patch running (amount around 0.6), set LFO1 → feedback amount at a slow rate and LFO2 → feedback rotation at a different slow rate. The feedback intensity swells and recedes while the whole field slowly counter-rotates — completely hands-free evolving motion you can then play over. Swap LFO1 to feedback hue instead and the echoes cycle color as they build.

**Breathing FM.** Turn on FM (Osc1 panel), set FM Amt around 1.0, give LFO1 a slow rate and some depth, then bring FM Mod up from zero. The harmonic complexity of Osc1 pulses in and out on the LFO's clock without touching anything else.

**Wandering color.** Give Osc2 a small drift, set its Clr Drift to O2 (or O1, or Both), and leave Osc1 on a fixed hue. Osc2's color slowly cycles the spectrum while Osc1 holds steady, so every overlap between them recolors continuously against the anchor.

**Two scales of rotation.** Set Rutt/Etra to Wire mode and give Osc1 a small drift (~0.3). Switch Rot Drift to O1 — the whole mesh turns slowly and meditatively as a foundation. Then route Bass to FBROT and play a kick-heavy track. The mesh keeps its serene slow rotation while the feedback inside it twitches with each kick. Two scales of rotational motion happening at once: foundation and gesture.

**Vinyl reactor.** Place the laptop near a record player. Mic on, all three bands routed to different destinations. Surface noise and groove crackle drive the treble routing; bass hits move the displacement.

## A way to play it

Video Surfer works best when you think of it as two layers of modulation rather than one.

The **foundation layer** is the synth's own internal motion — oscillator drift, the LFOs, FM. Kept slow, this layer never sits still but never demands attention either. It's a bed that breathes and evolves on its own: colors slowly cycling, the tunnel gently pulsing, patterns drifting past each other at their own pace. Set this up and it will keep becoming something without you touching it.

The **expressive layer** is everything that responds to intention in the moment — your hands on the sliders or a MIDI controller, the audio reactivity, the video luminance. This layer rides on top of the foundation and carries the phrasing: the punctuation, the swells, the gestures that answer the music or the room.

The instrument is doing something the moment you turn it on, so playing it becomes a matter of shaping and conversing rather than driving from zero. You're not generating the image from nothing; you're riding a system that already has its own pulse.

Every input layer has a slow/fast dial, so you can decide per performance which layer carries the foundation and which carries the gesture. The LFO rates are shaped to give you fine control in the slow range. The audio reactivity's Smooth control does the same job for sound: high smoothing pushes audio toward the slow organic bed, low smoothing makes it sharp and percussive. Set the foundation slow and organic, leave room above it, and let the performer, the audio, or the video do the talking.

---

## Performance setup

A typical live performance configuration:

- **Laptop** running Video Surfer in Chrome, controls visible on its screen
- **HDMI monitor or projector** attached, popup output dragged to it in fullscreen
- **MIDI controller** mapped to the parameters you sweep continuously (feedback amount, oscillator frequencies, drift rates) and pads bound to the burst button and segment toggles
- **Mic or line-in** capturing the audio source (DJ feed, instrument, room sound)

The hide-UI button (top-right of the controls window) clears the laptop screen entirely when you want clean output to a screen recorder or OBS source.

---

## Tips

- **Backgrounds change the math.** Colors are additive on black, subtractive on white, keyable on chroma green. The blend mode selector adjusts how the two oscillators combine before being composited.
- **Less is often more.** Most of the best-looking patches use modest values for almost everything. The synth rewards subtlety.
- **Audio reactivity stacks with manual controls.** Audio band routings *add to* your manual slider values rather than replacing them, so you can set a baseline and have the music push it from there.
- **MIDI pickup mode** means you have to "find" the parameter when you grab a knob — turn until you cross its current value, then it locks on. Touching a slider with the mouse releases pickup so external moves don't fight you.
- **The Division selectors on the drift controls** (Osc2 Color Drift and Rutt Rot Drift) gear the drift output down without needing to change the underlying Drift slider. This lets you keep oscillator pattern scrolling at a normal pace while pacing color cycling or mesh rotation much more slowly — useful for long-form work where you want different layers of motion happening at very different time scales.

---

## Performance and compatibility

The synth renders at 75% of screen resolution internally and upscales, which is the largest performance lever. The Rutt/Etra mesh is the most expensive single component; switching its mode to Off shows just the flat pattern at full quality if you need to lighten the load.

Tested smoothly on iPhone 12 and newer, recent Android flagships, and any laptop with hardware-accelerated WebGL. WebMIDI requires Chrome, Edge, or Safari 18+. Camera, mic, and audio file loading require HTTPS hosting. Camera device names (for selecting a specific webcam or capture device) appear in the selector only after camera permission has been granted once — a browser privacy rule.

---

## Credits and lineage

Video Surfer wouldn't exist without the pioneers of analog video art: **Steve Rutt and Bill Etra**, whose Scan Processor (1973) inspired the displacement model at the heart of this tool; **Dan Sandin**, whose Image Processor opened the modular video synthesis paradigm; **Nam June Paik and Shuya Abe**, whose Video Synthesizer (1969) showed what was possible when artists built their own instruments. The contemporary scene of analog video synth builders and performers — too many to list — keeps this tradition alive.

The code was written by Claude (Anthropic) through a series of design conversations with Slow Cities. The creative direction, control choices, modulation routing, aesthetic decisions, and testing were Slow Cities'; the implementation was Claude's.

---

## License

**Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**

Copyright © 2026 Slow Cities

You are free to use, share, and adapt Video Surfer for **non-commercial** purposes, with attribution to Slow Cities. You may not use it for commercial purposes without permission.

In plain language, so the intent is clear:

- **Performing with it live is fine — including paid performances, club nights, installations, and gigs.** Using the tool to make your work, even work you're paid for, is exactly what it's for.
- **Using it for teaching, learning, personal projects, and sharing is fine**, including remixing and forking it, as long as you keep the attribution and release your version non-commercially too.
- **Selling it, or bundling it into a product, app, or service that you sell, is not permitted.** Don't take this and turn it into something you charge people for access to.

If you want to use Video Surfer commercially in a way the above doesn't cover, get in touch.

The full license text is available at https://creativecommons.org/licenses/by-nc/4.0/

*Note: Creative Commons licenses are written for creative works rather than software. Video Surfer is released this way deliberately — it is as much an artwork and an instrument as it is code, and the NonCommercial intent matters more here than strict software-license formalism.*
