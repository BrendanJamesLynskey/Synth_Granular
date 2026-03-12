# Granular Synth — Texture Engine

A browser-based granular synthesizer that generates evolving, complex sound textures in real time using the Web Audio API. No samples, no libraries — everything is synthesized from scratch and visualized with audio-reactive WebGL shaders.

**[Launch the app](https://brendanjameslynskey.github.io/Synth_Granular/)**

## Features

- **Granular synthesis** — hundreds of micro-sound grains (5–500ms) are scheduled with timing jitter, each with its own pitch, pan position, and harmonic content
- **6 source types** — Harmonic, Noise, Formant, FM, Choir, Metallic — each with distinct timbral character
- **Continuous evolution** — pitch wander, filter drift, reverb modulation, and chaos-driven interval jumps keep textures alive and shifting
- **8 curated presets** — Celestial, Rainfall, Swarm, Deep Space, Crystals, Aurora, Whispers, Tectonic
- **Audio-reactive WebGL visuals** — full-screen shader with fractal noise fields, flowing nebulae, and sparkle patterns that respond to the audio spectrum
- **Full parameter control** — density, grain size, pitch, spread, shimmer, wander, attack shape, reverb, delay, filter, stereo width, evolution rate/depth, chaos, harmonics

## Quick Start

```bash
git clone https://github.com/BrendanJamesLynskey/Synth_Granular.git
cd Synth_Granular
python3 -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) and tap **Launch Synth**.

Any static file server works — there is no build step or dependency.

## Files

| File | Purpose |
|---|---|
| `index.html` | Landing page with feature overview and launch button |
| `app.html` | Granular synthesizer application |

## Controls

| Parameter | Description |
|---|---|
| **Source** | Select grain waveform type (Harmonic, Noise, Formant, FM, Choir, Metallic) |
| **Density** | Grains per second (1–80) |
| **Size** | Grain duration in milliseconds (5–500ms) |
| **Pitch** | Base frequency in Hz |
| **Spread** | Random pitch variation per grain |
| **Shimmer** | Micro-pitch drift and detune within grains |
| **Wander** | Slow, continuous pitch modulation |
| **Attack** | Grain envelope shape (short = percussive, long = soft pad) |
| **Reverb** | Procedural convolution reverb (3.5s tail with early reflections) |
| **Delay** | Stereo delay with feedback |
| **Filter** | Low-pass filter cutoff frequency |
| **Stereo** | Stereo spread of grain panning |
| **Evolution Rate** | Speed of automatic parameter drift |
| **Evolution Depth** | Intensity of automatic modulation |
| **Chaos** | Probability of octave/interval jumps |
| **Harmonics** | Number of harmonic partials per grain |

## How It Works

The synthesizer uses only native Web Audio API nodes — no external libraries:

1. **Grain scheduling** — a recursive `setTimeout` loop fires grains at the target density with random timing jitter for natural texture
2. **Grain synthesis** — each grain creates short-lived oscillator nodes with a Hann-like amplitude envelope (attack/decay ramp). Source types use different synthesis techniques: additive harmonics, filtered noise, bandpass formant banks, FM operator pairs, detuned choir clusters, or inharmonic metallic partials
3. **Evolution engine** — a 50ms interval modulates filter frequency, reverb mix, and delay time using layered sine LFOs at different rates, creating slow timbral drift
4. **Signal chain** — grains → stereo panner → biquad filter → dry/reverb/delay sends → master gain → analyser → output
5. **Visualisation** — a full-screen WebGL fragment shader reads 8-band FFT data and synthesis parameters, rendering layered simplex noise fields with audio-reactive color, ripple, and sparkle effects. Falls back to a 2D canvas particle system on devices without WebGL

## License

MIT
