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
- **Desktop & mobile versions** — optimised interfaces for both screen sizes, with automatic device detection on the landing page
- **Sparse particle graphics** — decorative background layer of slowly drifting particles of random density on a black background, filling unused UI space

## Quick Start

```bash
git clone https://github.com/BrendanJamesLynskey/Synth_Granular.git
cd Synth_Granular
python3 -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) and choose Desktop or Mobile.

Any static file server works — there is no build step or dependency.

## Files

| File | Purpose |
|---|---|
| `index.html` | Landing page with device detection and version selection |
| `desktop.html` | Desktop granular synthesizer with full controls |
| `granular_mobile.html` | Mobile-optimised version with touch-friendly collapsible panels |

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
6. **Particle graphics** — a decorative canvas layer renders sparse, slowly drifting particles of random density on a black background, filling unused space in both desktop and mobile UIs

## History of Granular Synthesis

Granular synthesis is a method of sound synthesis that operates on the microsound time scale. It is based on the same principle as sampling, but the samples are split into small pieces of around 1 to 100 milliseconds in duration. These small pieces are called **grains**. Multiple grains may be layered on top of one another, played at different speeds, phases, volumes, and frequencies, to create complex evolving textures that are far richer than any single waveform could produce.

### Origins and Theory

The theoretical foundation of granular synthesis traces back to the physicist **Dennis Gabor**, who in 1946 proposed that any sound could be decomposed into a family of functions obtained by time and frequency shifts of a single Gaussian-shaped grain. His work on "acoustical quanta" — published in the *Journal of the Institution of Electrical Engineers* — demonstrated that sound could be represented as a combination of elementary acoustic particles, analogous to the quantum theory of light. Gabor was awarded the Nobel Prize in Physics in 1971 for his invention of holography, but his insights into the granular nature of sound laid the conceptual groundwork for what would become an entirely new approach to synthesis.

The Greek-French composer **Iannis Xenakis** independently developed the concept of sound grains in the late 1950s and 1960s. In his landmark 1971 book *Formalized Music*, Xenakis described sound as being composed of elementary sonic particles — a perspective influenced by both quantum physics and probability theory. He proposed that clouds of sound grains, governed by stochastic (probabilistic) distributions, could generate textures ranging from smooth tones to dense noise masses. His compositions *Analogique A-B* (1959) and *Concret PH* (1958) were among the earliest practical explorations of granular sound, using tape-splicing techniques to assemble thousands of tiny sound fragments into sweeping sonic architectures.

### Curtis Roads and the Computer Implementation

**Curtis Roads** is widely regarded as the figure who transformed granular synthesis from a theoretical concept into a practical, computationally implemented technique. Beginning in the late 1970s at the University of California, San Diego, Roads undertook the first systematic computer implementations of granular synthesis, publishing his seminal 1978 paper "Granular Synthesis of Sound" which presented working algorithms for generating and controlling clouds of sound grains in real time.

Roads spent decades refining the technique, exploring the vast parameter space of grain density, duration, pitch, spatial distribution, and envelope shape. His exhaustive 2001 book ***Microsound*** (MIT Press) is the definitive reference on granular and microsound techniques. Spanning over 400 pages, it covers the theory, history, and aesthetics of sound at the microsound time scale — from individual grains through grain streams, clouds, and complex textures. The book examines synchronous, quasi-synchronous, and asynchronous granular synthesis; pitch-synchronous and pitch-asynchronous methods; granulation of sampled sounds; and the psychoacoustic implications of operating at the threshold of temporal perception.

Roads also composed extensively using granular techniques. Works such as *nscor* (1980), *Field* (1981), and *Clang-Tint* (1994) demonstrated the extraordinary range of timbres achievable through granular methods — from ethereal, cloud-like drones to sharp, percussive textures and everything in between. His later pieces including *Pictor Alpha* (2003), *Sculptor* (2001), and *Touche pas* (2009) pushed the boundaries further, combining granular synthesis with other microsound techniques. His compositional work proved that granular synthesis was not merely a technical curiosity but a powerful artistic tool capable of producing sounds with no analogue in the acoustic world.

Beyond his own research, Roads's teaching and writing helped establish granular synthesis as a fundamental technique in computer music. His earlier book *The Computer Music Tutorial* (MIT Press, 1996) introduced a generation of electronic musicians and researchers to granular methods, and his editorial work as founding editor of the *Computer Music Journal* helped disseminate granular synthesis research throughout the academic and artistic communities.

### Barry Truax and Real-Time Granular Synthesis

**Barry Truax**, working at Simon Fraser University in British Columbia, was a pioneer in developing real-time granular synthesis systems. In 1986, he created the first real-time implementation of granular synthesis on a personal computer using the DMX-1000 signal processor. His work distinguished between three fundamental approaches to grain timing:

- **Synchronous** granular synthesis, where grains are spaced at regular intervals, producing amplitude modulation effects
- **Quasi-synchronous** granular synthesis, where grain timing varies slightly around a regular interval, creating richer textures
- **Asynchronous** granular synthesis, where grains are distributed stochastically with no regularity, producing cloud-like sound masses

Truax's compositions *Riverrun* (1986) and *Pacific Fanfare* (1996) are landmark works in the granular repertoire. *Riverrun* in particular demonstrated the technique's ability to create organic, flowing textures that evolve over extended time scales — a quality that has made granular synthesis popular in ambient and experimental electronic music. His research also explored **pitch-synchronous** granular synthesis, where grain envelopes are designed to be synchronous with the waveform frequency, enabling smooth timbral transformations.

### Later Developments

Throughout the 1990s and 2000s, granular synthesis became increasingly accessible. Software implementations appeared in environments like Csound, Max/MSP, SuperCollider, and Pure Data. Commercial synthesizers and plugins — including Native Instruments' Absynth, Robert Henke's Granulator (for Ableton Live), and dedicated instruments like the Tasty Chips GR-1 hardware granular synthesizer — brought the technique to a broader audience of musicians and sound designers.

The rise of the Web Audio API in the 2010s made it possible to implement granular synthesis directly in the browser, requiring no plugins or installations. This synthesizer follows in that tradition, bringing the techniques pioneered by Gabor, Xenakis, Roads, and Truax to anyone with a web browser.

## License

MIT
