# M-VAVE FM1 Resource Hub, Custom Firmwares & MIDI SysEx Protocol Documentation

A curated directory and reference hub for the **M-VAVE FM1** synthesizer (powered by the **JieLi AC791N** processor) — gathering community custom firmwares, documentation, tools, MIDI SysEx protocol details, and the `M-UPGRADE-FM1.app` (macOS) updater.

> [!NOTE]
> **Device Compatibility Notice & SMK-37 Resources:**  
> This repository strictly curates custom firmwares and tools specifically targeted at the **M-VAVE FM-1** synthesizer.  
> If you are looking for custom firmwares, ports, community discussions, and tools for the **M-VAVE SMK-37 / SMK-37 Pro** keyboard controller:
> * **[r/MvaveSmk Subreddit](https://www.reddit.com/r/MvaveSmk/):** Community hub for SMK-37 discussion and mods.
> * **[M-VAVE SMK-37 Custom Firmware Hub](https://genkigenki.github.io/smk37/):** One page for 20+ SMK-37 firmwares, original ones and FM-1 ports, each installed and played on an SMK-37 before it goes up, with a browser installer (Chrome/Edge over USB, the way back to M-VAVE's firmware included), step-by-step help and a repair for a damaged stock key mapping. Updated as new firmwares and ports come out.
> * **[fm1-to-smk37 Port Kit by genkigenki](https://github.com/genkigenki/fm1-to-smk37)** & **[Snoop37](https://github.com/genkigenki/Snoop37)**:
>   * **License:** Open Source (GPL-3.0 for Snoop37 firmware port; CC BY-NC 4.0 for hardware guide & documentation).
>   * **Hardware Relationship:** Both devices share the identical **JieLi AC791N (WL82)** processor, second-stage bootloader, update loader, and chip key, differing primarily in panel wiring (keyboard matrix, 16 RGB pads, 8 encoders, 4 faders, pitch/mod wheels, display pins, and flash partition map).
>   * **Features:** Board Port Patch Series (`smk37-board`), Snoop37 reference port of SLOOP 2.5 on SMK-37 Pro, porting compatibility matrix, and critical flash safety documentation on preserving unique SPI flash regions (`0xC1000` USRTRIM factory calibration `trimdat`, `0xC0000` BTIF, `0xFF000` chip key/MAC).

> [!IMPORTANT]
> **Official Open Source Firmware & SDK (M-VAVE):**  
> In October 2026, M-VAVE officially open-sourced the FM-1 firmware and development toolkit under GPL-3.0:
> * **Repository:** **[m-vave/fm1_open](https://github.com/m-vave/fm1_open)** (8 tracks, 8 sample slots, 16 demo FX, hardware C drivers, and WebAssembly simulator).
> * **Online Web Workbench:** **[open.m-vave.com/fm1-workbench](https://open.m-vave.com/fm1-workbench)** — provides in-browser WebAssembly simulation, testing, and direct USB firmware flashing.
> * **Announcement & Discussion:** **[M-VAVE Official Forum Topic #4](https://forum.m-vave.com/topic/4)**.



---

## 1. Custom & Alternative Firmwares

Community-developed custom firmwares, mods, and experimental firmware projects for the M-VAVE FM-1, clearly divided into sound/groovebox instruments, modular builders, games and non-audio ports, and stock binary patchers:

### 1.1. Sound, Synthesizer & Groovebox Firmwares (Music & Audio)

Community musical firmwares organized by architectural family and lineage — the **Felucca** multi-engine platform, the **SLOOP** live groovebox ecosystem, the **FoMni** chord harp branch, and standalone independent engines:

#### 1.1.1. Felucca Ecosystem (Multi-Engine Platform & Direct Forks)

Firmwares built upon or directly forked from the foundational open-source multi-engine **Felucca** synthesizer core by Hügelton Instruments:

 1. **[Felucca by hugelton](https://github.com/hugelton/Felucca) ([Web Installer](https://hugelton.github.io/Felucca/) | [Web Editor](https://hugelton.github.io/Felucca/webapp/editor/) | [Build Guide](https://github.com/hugelton/Felucca/blob/main/BUILDING.md)):**
   * **License:** Open Source (GPL-3.0-only).
   * **Synthesizer Engines:** 9 distinct sound engines including **ANALOG** (virtual analog, 2 osc, PWM, resonant LPF), **DIGITAL** (4-op FM, 8 algorithms, feedback), **PHASE** (phase distortion), **LOFI** (chiptune, 4-bit wave RAM), **SAMPLE** (multisampled instruments + user slots), **VOICE** (formant/vocal osc), **TRIO** (3 osc with ring mod/sync), **WHEEL** (tonewheel organ with drawbars & rotary speaker), and **GRAIN** (granular textures).
   * **Architecture & Features:** 4 tracks (3 synth parts + 1 GM drum track, 8 shared voices), 64-step sequencer per track with chords/ties/slides and live loop recording, per-track SLICER (16-step tempo-synced gate/stutter), effects (distortion, chorus, delay, reverb sends, master limiter), scales & white-key quantization, and web editor.
   * **Documentation:** [Felucca BUILDING.md Guide](https://github.com/hugelton/Felucca/blob/main/BUILDING.md) — complete build guide for compiling Felucca-family firmwares from source using the JieLi `pi32v2` toolchain.
   * **Video Guides & Demos:** [Complete Guide (v0.9)](https://www.youtube.com/watch?v=UzgbDjsFEpY) | [Engine Tour & Sequencing](https://www.youtube.com/watch?v=EzFknmhtKZk) | [Live Performance Jam](https://www.youtube.com/watch?v=XEK4VhsYwCE).
   * **Installation:** Direct web installer via WebMIDI in Chrome/Edge over standard USB-C cable (no extra hardware needed; stock updater restores official firmware).

 2. **[Felucca [Salt] by Chance Roth (ChanceTheMaker)](https://github.com/ChanceTheMaker/Felucca) ([Web Installer](https://chancethemaker.github.io/Felucca/webapp/installer/) | [Web Studio](https://chancethemaker.github.io/Felucca/webapp/editor/)):**
    * **License:** Open Source (GPL-3.0-only). Enhanced fork of Felucca by Leo Kuroshita (Hügelton Instruments).
    * **Concept:** Multi-engine synthesizer firmware with hardware-inspired browser Studio, hardware TRS MIDI expansion, rich display palettes, and standalone in-browser sound generation.
    * **Features:**
      * **Studio & In-Browser Synthesizer:** Browser Studio can act as an online synthesizer without physical hardware (nine engines, 54 presets, live oscilloscope waveform, 12 hardware themes like Stage Red, Matrix, Vintage DX, Model D, Vaporwave, and on-screen keyboard).
      * **Hardware TRS MIDI Input:** Full expression handling on 3.5 mm TRS MIDI IN alongside USB (sustain pedal, pitch bend, mod-wheel vibrato, MIDI panic/reset).
      * **Flexible Clock Sources:** Internal, USB, or TRS clock sync and MIDI Start/Stop/Continue.
      * **Display Themes & Typography:** 20 on-device screen palettes (including 8 light palettes and light/dark high contrast modes), selectable Terminus Regular/Bold typography.
      * **Preset Management:** Persistent favorite stars, All/Favorites browsing filtering, and live MIDI event/chord monitor.
    * **Installation:** Browser-based WebMIDI installer via USB.

 3. **[Melodee by keremimo](https://github.com/keremimo/melodee) ([Web Installer](https://keremimo.github.io/melodee/) | [Web Editor](https://keremimo.github.io/melodee/webapp/editor/)):**
   * **License:** Open Source (GPL-3.0-only). Modified build based on Felucca.
   * **Features:**
     * **Prophet-5 Engine (New in 0.13):** Native **Sequential Prophet-5 Rev 4** engine replacing ANALOG — two oscillators with hard sync, Poly-Mod, LFO/noise wheel modulation, selectable SSI (Rev 1/2) and Curtis (Rev 3) 4-pole low-pass filters, separate filter/amp envelopes, Vintage knob, glide, unison, and 5 voices per track. Includes **all 200 programs** of Sequential's v1.03 factory bank (128 native user slots P001–P128), 16 device parameter pages, and `.syx` program/bank import and export in the web editor.
     * **Casio CZ-1 Phase Distortion:** Authentic CZ-1 engine with 64 original CZ-1 factory preset tones, 8 CZ device banks with `.syx` import/export, and 38 dedicated editing pages.
     * **FM6 & Microtonal Scales:** 64 DX7/FM6 slots with direct SysEx bank dump support, 70 microtonal tunings across equal divisions, just intonation, historical temperaments, and maqam models.
     * **Advanced Sequencing:** Single unified note editor (`SEQ > NOTES`), reversible timing quantization (`QNT`), and 1,024 recorded notes across 32 pattern banks.
   * **Installation:** Browser WebMIDI installer with built-in backup before installation.

 4. **[ChoralRoot FM-1 by Quixotic7](https://github.com/Quixotic7/ChoralRootFM1) ([Web Installer](https://quixotic7.github.io/ChoralRootFM1/) | [Web Emulator](https://quixotic7.github.io/ChoralRootFM1/emu/)):**
   * **License:** Open Source (GPL-3.0). Based on Felucca (engines/platform) and ChoralRoot (Monome grid chord engine).
   * **Concept:** Telepathic Orchid / Monome-style chord performance instrument.
   * **Features:** Two-handed chord shaping (one hand selects roots, the other shapes voicings), custom key modes, performance bass line, built-in looper, full color UI, and browser sound emulator.
   * **Installation:** Browser WebMIDI installer via USB.
   * **Community Remix / Mod:** [Choralroot-remix on r/MVaveFM1](https://www.reddit.com/r/MVaveFM1/comments/1x3qrqx/choralrootremix/) by Creative_One919 — extended remix incorporating Melodee's 6-voice Prophet-5 engine with 200 factory presets, DUELL-inspired Morph engine, dedicated BASS engine with multi-core rendering, "Rosen" random preset cycling, "Swag voicing" mode, synced BPM gate, and sidechain volume.

 5. **[X0X by Charles Vestal](https://github.com/charlesvestal/fm1-x0x) ([Web Installer](https://charlesvestal.github.io/fm1-x0x/install/) | [Web Emulator](https://charlesvestal.github.io/fm1-x0x/emu/) | [Manual](https://charlesvestal.github.io/fm1-x0x/manual/)):**
    * **License:** Open Source (GPL-3.0). Based on Felucca.
    * **Concept:** Propellerhead ReBirth-inspired techno/acid groovebox machine.
    * **Features:** TR-909, TR-808, two TB-303 synths with an integrated acid line generator, and a breakbeat player all playing simultaneously; includes automation, shared reverb and tape delay sends, and a master compressor.
    * **Installation:** Browser WebMIDI installer via USB (with stock restore option).

 6. **[GHOULBOX 2.0 by Jason Persinger](https://github.com/jasonpersinger/ghoulbox-fm1-dungeon-synth) ([Website & Browser Emulator](https://ghoulbox.messy.quest) | [Web Installer](https://ghoulbox.messy.quest/webapp/installer/)):**
    * **License:** Open Source (GPL-3.0). Based on Felucca.
    * **Concept:** Dungeon synth, dark ambient, and fantasy music groovebox firmware.
    * **Features:** Cathedral-sized HALL reverb, worn-cassette TAPE / CRKL stage, dedicated hurdy-gurdy engine (GURDY with crank clicks and buzzing trompette), drone latching, historical/just temperaments, and 36+ dungeon sounds (crypt pads, monk choirs, lutes, organs) with an old-school RPG UI and skull boot screen.
    * **Interactive Browser Version:** Complete in-browser emulation playable on an interactive virtual FM-1 via keyboard or mouse at [ghoulbox.messy.quest](https://ghoulbox.messy.quest) without flashing hardware first.
    * **Installation:** Browser WebMIDI installer via USB with full backup feature before flashing.

 7. **[Jangada by zednaked](https://github.com/zednaked/jangada) ([Web Installer](https://zednaked.github.io/jangada/) | [Web Studio](https://zednaked.github.io/jangada/webapp/studio/)):**
    * **License:** Open Source (GPL-3.0). Based on Felucca.
    * **Concept:** Dark, industrial, Brazilian-accented groovebox firmware.
    * **Features:** 10 sound engines (including 6-op FM and superwave analog), 4 tracks, modulation matrix, ratchets, drone holding/evolving modes, and dedicated custom drum kits.
    * **Installation:** Browser WebMIDI installer via USB.

 8. **[REDACTED by DJ Redacted](https://fm1-redacted-installer.xrhetor.chatgpt.site/):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Hügelton Instruments.
    * **Concept:** Experimental dark, fractured lo-fi four-track groovebox firmware (`PULSE` · `VOLTAGE` · `STATIC` · `GHOST`).
    * **Features:**
      * **Four Track Engines:** Four distinct sound layers chosen via `ALGORITHM`.
      * **Real-Time Track Shapers:** Four top knobs mapped to dynamic performance parameters: `FRACTURE`, `STATIC`, `CHANCE`, and `MUTATE`.
      * **Startup Artwork:** Custom broken vinyl record splash screen.
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

 9. **[Hortator by DEADACTIVE](https://github.com/DeadActive/hortator) ([Web Emulator & Player](https://deadactive.github.io/hortator/)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca.
    * **Concept:** 8-track drum machine firmware.
    * **Features:** TR-808, TR-909 and Mutable Instruments Plaits drum models, user samples, Mutable Instruments Grids generative rhythm algorithm, pumping master compressor, and acoustic resonators.
    * **Installation:** Browser WebMIDI installer via USB.

10. **[April OS by beashoko](https://github.com/beashoko/april-os) ([Web Installer](https://beashoko.github.io/april-os/)):**
    * **License:** Open Source (MIT). Based on Felucca.
    * **Concept:** Dedicated sampling-focused groovebox firmware.
    * **Features:** 32 sample slots (up to 3 seconds each), 8-track sequencer, built-in sample slice and loop editor, direct audio recording using a connected smartphone or computer microphone.
    * **Installation:** Browser WebMIDI installer via USB.

11. **[WaveLoop FM-1 by ELI7VH](https://github.com/ELI7VH/Felucca) ([Web Installer](https://eli7vh.github.io/Felucca/)):**
    * **License:** Open Source (GPL-3.0). Based on Felucca.
    * **Concept:** Performance firmware specifically mapped for external control via Arturia MiniLab 3.
    * **Features:** Dedicated track fader mappings, follow-the-track encoder integration, DJ filter mode, and momentary punch-in FX pad triggers.
    * **Installation:** Browser WebMIDI installer via USB.

12. **[Rainbow mode by joshbartlettband-web](https://github.com/joshbartlettband-web/felucca-rainbow) ([Web Installer & Emulator](https://joshbartlettband-web.github.io/felucca-rainbow/)):**
    * **License:** Open Source (GPL-3.0). Based on Felucca.
    * **Concept:** Children's musical exploration instrument with rainbow color-coded keys, 40 animal sound effects and rhythms, safe volume limiter, and access to the complete Felucca engine via secret key combination.
    * **Installation:** Browser WebMIDI installer via USB.

13. **[fm1-chord by math0ne](https://github.com/math0ne/fm1-chord):**
    * **License:** Open Source (GPL-3.0). Built on Felucca.
    * **Concept:** Chord composition tool, chord sequencer, rhythm accompanist, and ear-training aid.
    * **Installation:** Python installation script via USB MIDI.

14. **[DUELL by balinthcom](https://github.com/oscillr/DUELL) ([Web Emulator](https://oscillr.github.io/DUELL/emu/)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Hügelton Instruments.
    * **Concept:** Multi-morphing bi-timbral synthesizer firmware for the FM-1: two full simultaneous sound parts, each with its own synthesis engine, patches, effects, EQ, and arpeggiator.
    * **Features:**
      * **Bi-Timbral Modes:** LAYER, SPLIT (keyboard zone), and STEREO (dual mono, part 1 hard-left and part 2 hard-right with isolated audio engines).
      * **Patch Morphing:** Smooth glide between two states of any patch with SMART randomization and per-patch morph amount.
      * **Per-Part Engine Architecture:** Independent arpeggiators, secondary envelopes and LFOs, 8-slot modulation matrix, dedicated EQ, sidechain ducking triggered via MIDI, and ping-pong delay.
      * **Factory Sound Bank:** ~100 sounds across 12 synthesis engines, 16 multi-setups, and 16 patterns.
      * **MIDI Implementation:** Discrete MIDI channel per part, program change, bank select, and clock sync.
    * **Status & Installation:** Available to play via in-browser WebAssembly emulator; hardware flashing in ongoing development.

15. **[MAKU (幕間機) by okumurari2](https://github.com/okumurari2/maku) ([Web Emulator](https://okumurari2.github.io/maku/) | [Releases](https://github.com/okumurari2/maku/releases)):**
    * **License:** Open Source (GPL-3.0-only). Built on Felucca by Hügelton Instruments.
    * **Concept:** Always-on generative ambient machine firmware designed for DJ intermissions and generative soundscapes: power on and an evolving, random, in-key sonic world is immediately playing.
    * **Features:**
      * **Four Continuous Parts:** Pulse (kick/rhythm, DRUM engine), Floor (drone, PHYS physical modeling), Haze (shimmer/textures, GRAIN granular engine), and Voice (arpeggiated melodic phrase, PHYS engine).
      * **Dynamic Generative Evolution:** Every boot generates a unique scale, tempo (70–90 BPM), sounds, and macro states. Holding HOME regenerates a new world.
      * **Taste Memory ("Likes"):** Tapping REC saves preferred worlds (up to 16). Future generated worlds increasingly draw inspiration and mutate from saved favorites.
      * **Verb-Based Interface:** Action buttons perform timed organic changes — FX (sinks depth), SCL (cascades higher intervals), ENV (swells chords), LFO (wobbles filter/pitch), EDIT (lifts brightness/sharpness), GLO (scrambles phrases), and PLAY (toggles DRIFT value wandering).
    * **Installation:** Flash prebuilt `maku-X.Y.fwsc` via `tools/fm1_install.py` or browser WebMIDI updaters.

16. **[Polly by Charles Vestal](https://github.com/charlesvestal/fm1-polly) ([Web Installer & Emulator](https://charlesvestal.github.io/fm1-polly/)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Leo Kuroshita / Hügelton Instruments.
    * **Concept:** Yamaha QY70-inspired 8-track pocket accompaniment arranger and auto-accompaniment workstation for the FM-1.
    * **Features:**
      * **8-Track Arranger Architecture:** Dedicated parts for Drums, Percussion, Bass, and 5 Chord accompaniment tracks powered by the Sonivox EAS General MIDI sound engine.
      * **Interactive Chord Recognition & Follower:** Play chord shapes on the keyboard (or via MIDI IN) to drive realistic live auto-accompaniment transformations.
      * **Style Engine & QY70 Import:** Built-in accompaniment styles with variation switching, fill-ins, intro/outro, and direct import compatibility for Yamaha QY-format style patterns.
      * **In-Browser WebAssembly Simulator:** Full hardware simulation with screen rendering and audio playback running directly in the browser at [charlesvestal.github.io/fm1-polly](https://charlesvestal.github.io/fm1-polly/).
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

17. **[TRIBE (fm1-tribe) by Alexandre Piel (apiel)](https://github.com/apiel/fm1-tribe) ([Site & Web Installer](https://apiel.github.io/fm1-tribe/)):**
    * **License:** Open Source (GPL-3.0-only). Fork of X0X (Charles Vestal) and built on Felucca (Leo Kuroshita / Hügelton Instruments) with kicks and scatter effects from zicBox.
    * **Concept:** Ten-track groovebox firmware where any synthesis or drum engine plays on any track.
    * **Features:**
      * **10 Tracks & 25 Engines:** Freely assignable tracks running two dedicated kick models (`KICK W`, `KICK P`), Roland TR-909 and TR-808 drum voice models (9W9 / 8W8 ports), and TB-303 bassline synthesis (schwung-303 port).
      * **16 Clips per Track:** Launch clips at pattern boundaries or instantly; supports 16, 32, or 64 steps, 6 playback clock rates, 4 playback directions, and shuffle/swing.
      * **Live Performance Scatter FX:** Momentary performance effects triggered directly from keys while playing (beat loops, reverse, rhythmic gating, bitcrush, distortion, ring modulation, and resonant filters).
      * **Dual Master FX & Compressor:** Reverb, delay, drive, distortion, fuzz, wavefolder, bitcrusher, decimator, or ring modulator fed by per-track sends, plus an always-on master compressor.
      * **In-Browser Emulator:** Real firmware compiled to WebAssembly running directly in the browser at [apiel.github.io/fm1-tribe](https://apiel.github.io/fm1-tribe/#emulator).
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

18. **[Golana by Gadlele](https://github.com/Gadlele/Golana) ([Website & Web Installer](https://gadlele.github.io/Golana/) | [Releases](https://github.com/Gadlele/Golana/releases)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Leo Kuroshita / Hügelton Instruments.
    * **Concept:** Korg microKORG-inspired analog-modeling synthesizer firmware for the FM-1 featuring the classic MATRIX editing workflow.
    * **Features:**
      * **MicroKORG Synth Architecture:** 4-voice polyphonic / unison / mono / legato engine with 2 oscillators per voice (saw, pulse with PWM, tri with wavefold, sine with cross-mod from OSC 2, noise, and ring modulation), dual LFOs, and 4 assignable virtual modulation patch routings.
      * **Resonant Multi-Mode Filter:** 24 dB/oct LPF, 12 dB/oct LPF, BPF, HPF, and an aggressive screaming MS-20-style resonant low-pass filter model.
      * **Matrix Interface & Waveform Drawing:** On-device 240 × 240 graphics rendering real-time waveforms for OSC 1/2, dynamic filter response curves, envelope graphs, and live LFO waveforms calculated directly from parameter values.
      * **FX Chain & 16-Step Sequencer:** Integrated arpeggiator, 16-step sequencer with ties/slides per program, modulation FX (chorus, flanger, ensemble, phaser, metal distortion), tempo-synced delay, and reverb with flexible FX routing orders.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site or building/flashing firmware via CLI toolchain (`tools/fm1_install.py`).

19. **[FANTASMA / Pelucco by Gadlele](https://github.com/Gadlele/Pelucco) ([Web Emulator / Artifact](https://claude.ai/artifact/RLDaXqXDuzzfyJZ8ibS5Gk)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Leo Kuroshita / Hügelton Instruments.
    * **Concept:** Generative ambient and drone synthesizer firmware for the FM-1 with dedicated chord-strum and generative "haunted" modes.
    * **Features:**
      * **"Haunted" Generative Ambient Engine:** Pressing `OCT+` on the fourth SEQ page triggers self-generating, evolving ambient music across three independent channels across randomized musical scales (major, minor, dorian, mixolydian, pentatonic, phrygian, lydian) even with the transport stopped; `OCT-` halts the generator.
      * **BELL Generative Loops:** 4 drifting loops of 13/17/23/29 steps (`DENS`, `EVOLVE`, `RANGE`, `SEED`) snapped to the scale on the BELL engine.
      * **Dedicated Ambient Role Split:** 4 channels configured for ambient roles: Pads (automatic chord generator), Lead (key-locked for live manual jamming over drones), FM Bells (generative chime echoes), and Continuous Noise (sea/wind textures).
      * **OMNI Strum Mode:** Omnichord-style performance mode where black keys trigger chords following the active root scale while white keys act as a harp strum plate.
      * **USB Rescue Boot:** Built-in safe recovery mode (`OCT-` held on power-on or two crash loops in a row) launching a minimal updater screen reporting as `FM-1_000` to guarantee web flashing and recover without bricking.
      * **Custom Ambient UI & Reverb:** Expansive long-decay `AMBI` reverb engine, custom ghost splash screen, and high-visibility neon "ECTO" color theme.
    * **Installation:** In-browser WebAssembly simulation and WebMIDI installer via Claude artifact, or build from the [Gadlele/Pelucco repository](https://github.com/Gadlele/Pelucco).

20. **[Skiff by illuminus5](https://github.com/illuminus5/skiff) ([Web Installer](https://illuminus5.github.io/skiff/webapp/installer/) | [Web Editor](https://illuminus5.github.io/skiff/webapp/editor/)):**
    * **License:** Open Source (GPL-3.0). Fork of Felucca by Leo Kuroshita / Hügelton Instruments.
    * **Concept:** 6-track groovebox firmware for the FM-1 with 14 synthesis engines and deep parameter-locking sequencer.
    * **Features:**
      * **6 Tracks & 14 Engines:** Expanded polyphonic tracks hosting virtual analog, FM, wavetable, physical modeling, drums, and noise generators.
      * **Advanced 64-Step Sequencer:** Per-step parameter locks (p-locks), microtiming, ratchets, and trig conditions (probability / iteration logic).
      * **Dual Effects & Mod Matrix:** Flexible send effects and real-time knob modulation assignments.
      * **Web Tooling:** Dedicated browser WebMIDI installer and companion web editor for patch and pattern management.
    * **Installation:** Browser WebMIDI installer via USB directly from the web installer page.

21. **[Felucca 8 Patterns by echoe](https://github.com/echoe/Felucca_8_patterns) ([Releases](https://github.com/echoe/Felucca_8_patterns/releases/tag/1.5.1_and_sequences)):**
    * **License:** Open Source (GPL-3.0). Fork of Felucca 1.5.1.
    * **Concept:** Pattern-chaining and arrangement expansion fork of Felucca.
    * **Features:**
      * **8 Chainable Patterns per Track:** Extends Felucca with 8 independent pattern slots per track that can be chained into song sequences.
      * **Optimized Flash Footprint:** Sample playback assets removed to maximize flash space and code budget for sequence memory and pattern chaining.
    * **Installation:** Prebuilt `.fwsc` firmware releases available on GitHub; flash via WebMIDI or CLI flasher.

22. **[LCD-4 by devrvega](https://github.com/devrvega/LCD-4) ([Website & Hub](https://devrvega.github.io/LCD-4/) | [Web Emulator](https://devrvega.github.io/LCD-4/emu/) | [Web Installer](https://devrvega.github.io/LCD-4/install/) | [Manual](https://devrvega.github.io/LCD-4/manual/)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca by Hügelton Instruments, by way of X0X, AMB-1, and IND-1.
    * **Concept:** Four-track pocket groovebox inspired by pocket calculator synths (Teenage Engineering Pocket Operator style) and vintage Game & Watch LCD games, featuring custom animated LCD game scenes for every sound engine.
    * **Features:**
      * **Four Dedicated Tracks:**
        * **Drums:** 4 kits of 11 parts selectable on black keys (TR-808, TR-909, Arcade console with pulse kicks/zaps/coin, and Vintage Rhythm Box CR-78/606). White keys act as 16-step sequencer lanes as on X0X, featuring Pip the drummer animating on screen.
        * **Basses:** Circuit-modelled Acid (TB-303 with accents/slides and bubbling lab animation), Mono (SH-101), Fat (Minimoog), Boom (808 sub), FM Bass (DX7), and Reese.
        * **Keys:** Poly (Juno-60 with chorus), Brass (Prophet-5 / OB-Xa), E.Piano (DX7), Organ (Korg M1 house organ), Strings (Solina string ensemble), and Bells.
        * **Leads:** Sync, Scream (Korg MS-20), Arcade (NES/Game Boy chip channels with tracker FX), and Arp. (Any synth track can load any sound).
      * **Sequencing & Performance:** 16 patterns with pattern chaining up to 64 steps, 16 chords with chord progression chaining, parameter locks (p-locks), ratchets, slides, swing, 16 punch-in effects, and live/step recording.
    * **Installation:** One-click browser WebMIDI installer (`v0.1.0`), in-browser WebAssembly emulator, or flashing prebuilt `lcd4-0.1.0.fwsc`.

23. **[PIGEON by The Shrimp Blimp](https://github.com/TheShrimpBlimp/pigeon) ([Website](http://theshrimpblimp.com/pigeon) | [Web Installer](http://theshrimpblimp.com/webapp/installer/) | [Web Sample Tool](http://theshrimpblimp.com/webapp/pigeon/) | [Web Emulator](http://theshrimpblimp.com/webapp/emu/)):**
    * **License:** Open Source (GPL-3.0-only). Built upon Felucca (Leo Kuroshita / Hügelton Instruments) with update safeguards and recovery boot stub adapted from ChoralRoot FM-1 (Quixotic7).
    * **Concept:** Old-school hip-hop, boom-bap, and house sampling groovebox inspired by the Roland SP-404 and Teenage Engineering Pocket Operator PO-33, featuring in-browser sample slicing, chop queues, and scratch decks.
    * **Architecture & Memory Model:**
      * **Shared Audio Bank:** 496 KiB flash allocation shared between two song sample tracks (indexed mono MP3, libmad decoder) and a 16-pad drum kit (ADPCM one-shots).
      * **Polyphony:** 8 playback voices shared between Song 1 and Song 2, plus 4 dedicated voices reserved for drum pads (12 voices total).
    * **Features:**
      * **Transient Slicing & Chop Shaping:** Up to 32 chops per song sample with automatic transient detection, editable start/end boundaries, waveform zoom, pitch, envelopes, hold loops, and latching; two independent chop layouts can share the same audio.
      * **FIFO Chop Queue:** Queue mode (`EDIT → ARP`) allows queuing up to 64 waiting chops with live queue manipulation while the current slice plays.
      * **Scratch & Cue Deck:** Dedicated turntable deck (`EDIT → FX`) with jog, brake, reverse playback, level cuts, return-to-cue, and fine cent tuning per song.
      * **Dual-View Sequencer:** Step grid and piano roll views (1–64 steps per track, 4 notes per step, 4 pattern banks, song arrangement sections) with per-note nudge/timing, microtiming, swing, hit probability, repeats, pitch locks, conditional hits, and Euclidean rhythm generation.
      * **Effects Chain:** Resonant filter, tempo-synced tape delay, chorus, reverb, distortion, and independent master compressor.
      * **Accessibility & MIDI:** Built-in screen-reader support across hardware and browser emulator; per-track discrete MIDI channels with incoming-note track selection and MIDI screen wake.
    * **Update Safeguards & Recovery Boot Stub:** Includes installer compatibility checks and recovery boot stub adapted from ChoralRoot FM-1. An interrupted write can safely resume: holding `OCT-` alone on power-on re-enters update mode. Seamlessly interoperates with [TransitFM1](https://quixotic7.github.io/TransitFM1/) as a safe bridge when migrating from other custom firmwares.
    * **Web Tools & Simulation:** Companion web studio for importing, trimming, previewing, and encoding audio banks (`webapp/pigeon/`), alongside a full in-browser WebAssembly hardware emulator (`webapp/emu/`).
    * **Installation:** Browser WebMIDI installer via USB directly from the web installer or flashing prebuilt `.fwsc` firmware packages.

24. **[NOIZ DEMONS by SPIKE the Percussionist](https://github.com/SPIKE-the-Percussionist/noiz_demons) ([Releases](https://github.com/SPIKE-the-Percussionist/noiz_demons/releases)):**
    * **License:** Open Source. Built on Felucca by Hügelton Instruments.
    * **Concept:** Ritualistic noise and sound generator firmware where parameter randomization is framed as occult summoning.
    * **Features:** Generating a sound summons one of 30 demons of the Ars Goetia, rendering the demon's sigil across the 240 × 240 color screen while its demonic rank algorithmically drives the wildness and distortion of the sound synthesis engine.
    * **Installation:** Flashing prebuilt `noiz_demons-v666.fwsc` via WebMIDI or CLI flasher.

25. **[Tuna by delirioux](https://github.com/delirioux/tuna) ([Website & Web Emulator](https://delirioux.github.io/tuna/)):**
    * **License:** Open Source. Built on Felucca by Hügelton Instruments.
    * **Concept:** Generative music synthesizer and composition engine.
    * **Features:** Interactive composer profiles algorithmically generate and evolve musical tracks in real time, with macro controls allowing the performer to steer tonal palettes, tempo, and arrangement.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site.

26. **[X0X-RMX by Mr-Roboto](https://github.com/Mr-Roboto/fm1-x0x-rmx) ([Website](https://mr-roboto.github.io/fm1-x0x-rmx/) | [Web Installer](https://mr-roboto.github.io/fm1-x0x-rmx/install/) | [Web Emulator](https://mr-roboto.github.io/fm1-x0x-rmx/emu/) | [Releases](https://github.com/Mr-Roboto/fm1-x0x-rmx/releases)):**
    * **License:** Open Source (GPL-3.0). Independent fork of X0X by Charles Vestal (built on Felucca).
    * **Concept:** Enhanced ReBirth-style acid and techno groovebox machine expanding the dual drum machines (TR-909 / TR-808), dual TB-303 synthesizers, and breakbeat engine.
    * **Features:**
      * **ORB-Inspired Remix Engine:** 256 step-remapping patterns available independently for the 909, 808, 303A, and 303B lanes.
      * **Enhanced TB-3PO Bassline Generator:** 22 musical scales, motif-based melodic phrase generation, rhythmic call-and-response phrasing, expressive accents/slides, and controlled parameter mutation.
      * **Grids MAP/EUCLID Drum Generation:** Generative Euclidean rhythm and drum patterns with density fill, offset, and chaos probability controls.
      * **Experimental 303 Morph Waveform:** Continuous real-time waveform morphing between Sharkfin, Trapezoid, and Notch-Trapezoid responses.
      * **Performance & Display Polish:** Pattern chaining, saved startup pattern combinations, and six selectable LCD color schemes.
    * **Installation:** Browser WebMIDI installer via USB directly from the project website or flashing prebuilt `v1.0.0` releases.

27. **[DUB-1 by sbegueria](https://github.com/sbegueria/fm1-dub) ([Homepage](https://sbegueria.github.io/fm1-dub/) | [Web Installer](https://sbegueria.github.io/fm1-dub/install/) | [Web Emulator](https://sbegueria.github.io/fm1-dub/emu/) | [Manual](https://sbegueria.github.io/fm1-dub/manual/)):**
    * **License:** Open Source (GPL-3.0). Fork of AMB-1 by Charles Vestal (built on Felucca by Hügelton Instruments).
    * **Concept:** Berlin-style generative dub techno machine ("4 AM in Berlin"): power on and it immediately self-generates deep, evolving dub techno arrangements.
    * **Features:**
      * **Generative Dub Structure:** Chord stabs sent into tape delay, 4 FM ping loops running at independent polymeter lengths, tuned deep sub-bass under a ducking kick, rhythmic shaker, off-beat hi-hat, rimshot, sparse claps, and authentic vinyl crackle.
      * **Self-Arranging 8-Bar Phrases:** Automatically generates evolving arrangements with kick drops, breakdowns, builds, and fills.
      * **Generative & Custom Chord Memory:** Weighted random walks over musical scales that naturally resolve home, voiced as classic Roland/Basic Channel chord-memory stabs, plus 8 user-programmable progression slots.
      * **Performance Dub Controls & Echo Ripples:** Dedicated `REC` dub-hold button to freeze and loop the tape delay buffer infinitely while reverb continues ringing out and dry beats ride over top; real-time echo ripple animations visualising delay throws and loop positions on screen.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site or in-browser WebAssembly simulation.

28. **[Unholy Union by Sparky (actuallysparky)](https://github.com/actuallysparky/FM-1-Unholy-Union-generative-drone-firmware) ([Releases](https://github.com/actuallysparky/FM-1-Unholy-Union-generative-drone-firmware/releases)):**
    * **License:** Open Source (GPL-3.0). Built on Felucca and Jangada.
    * **Concept:** Generative ambient and drone firmware featuring church-themed visuals and atmospheric harmonics.
    * **Features:** A single key press algorithmically generates and rolls a pad, an ambient sequence, a chord arpeggio, and a live-playable lead voice all locked to a shared harmonic key. Includes cathedral reverb algorithms, slow parameter drift, and church-inspired screen aesthetics.
    * **Installation:** Flashing prebuilt `v0.2.3` releases via WebMIDI or CLI updater.

29. **[Melodee (Tess) by Rastapopolix](https://github.com/Rastapopolix/melodee-tess) ([Releases](https://github.com/Rastapopolix/melodee-tess/releases)):**
    * **License:** Open Source (GPL-3.0). Fork of Melodee by Leo Kuroshita.
    * **Concept:** Algorithmic and generative pattern expansion for Melodee's 4-track synthesizer engine.
    * **Features:** Adds four distinct algorithmic note generators across its four tracks: Turing machine shift-register random loops, Euclidean rhythmic distribution, Markov chain note transitions, and Morph phrase mutation. Features dedicated on-device Evolve, Form, and Tweak pages for dynamically mutating melodic phrases and structuring live song sections.
    * **Installation:** Flashing prebuilt `v1.1.0` releases via WebMIDI.

30. **[REGGAE-OS by Kemar Pennant (KemstheSage)](https://github.com/KemstheSage/reggae-os):**
    * **License:** Open Source (GPL-3.0). Derivative of Felucca 1.6.1.
    * **Concept:** Dub and roots reggae performance firmware transforming the FM-1 into a portable reggae sound system.
    * **Features:** Dedicated reggae tonewheel organ and deep sub-bass sound engines, intuitive four-knob dub shaping, and an animated retro sound system UI on the color display.
    * **Installation:** Build and flash via CLI toolchain.

31. **[Glitchbox by Erik de Vos](https://github.com/erikdevos/glitchbox):**
    * **License:** Open Source (GPL-3.0). Fork of Felucca 1.5.1.
    * **Concept:** Harsh, experimental glitch synthesizer and live performance noise box.
    * **Features:** Self-chopping glitch synthesizer engine, a crushed bit-reduced synthesized drum kit, and live punch-in performance effects (beat rolls, rhythmic gating, pitch sweeps, and bitcrush filters) — 100% synthesized in real time without sample playback dependencies.
    * **Installation:** Build and flash via CLI toolchain.

32. **[FM-1 T1 by Tensor-Programming](https://github.com/tensor-programming/fm1-t1):**
    * **License:** Open Source (GPL-3.0). Fork of Felucca 1.6.
    * **Concept:** Torso T-1 style generative algorithmic sequencer firmware for the FM-1.
    * **Features:** Six tracks running algorithmic generative cycles inspired by the Torso T-1 hardware sequencer, featuring Euclidean rhythm generation, pitch mapping, velocity accentuation, and simultaneous MIDI output routing across five tracks.
    * **Installation:** Build and flash via CLI toolchain.

33. **[Patricktronics by gaumondp](https://github.com/gaumondp/patricktronics):**
    * **License:** Open Source (GPL-3.0). Derivative of Felucca.
    * **Concept:** Self-evolving ambient looping synthesizer inspired by Robert Fripp and Brian Eno's tape-delay Frippertronics setup.
    * **Features:** Locks a musical palette of up to five notes played through an FM sound engine, while a bounded random generator continuously rearranges the sequence note order, octave, and timing over time into an endless, evolving ambient soundscape.
    * **Installation:** Build and flash via CLI toolchain.

#### 1.1.2. SLOOP Ecosystem (Groovebox Core & Derived Firmwares)


Firmwares centered around the **SLOOP** 4-track live groovebox workflow and its DX7/sampling expansion forks:

 1. **[SLOOP by isod89](https://github.com/isod89/sloop-fm1) ([Web Installer](https://isod89.github.io/sloop-fm1/) | [Web Editor](https://isod89.github.io/sloop-fm1/webapp/editor/)):**
   * **License:** Open Source (GPL-3.0). Based on Felucca by Hügelton Instruments.
   * **Concept:** Live performance groovebox firmware designed for any music style without mandatory presets or fixed patterns.
   * **Features:** 4 tracks (3 synth tracks + 1 drum machine with 16 sounds across the white keys), 9 synthesis engines, 68 sounds, 37 drum kits, custom sample support, and live-playable song mode. Features USB stereo audio input (class-compliant recording directly into DAWs without drivers), 3.5 mm TRS MIDI IN keyboard input, MIDI clock in/sync, button and note LED illumination modes for dark environments, sample chopping/fitting, and a web editor with full backup/restore.
   * **Installation:** Browser-based installer via WebMIDI in Chrome/Edge, with easy rollback to M-VAVE stock V15.

 2. **[sloopDX by zvenson](https://github.com/zvenson/dxsloop) ([Website & Web Installer](https://dx7.designburgapps.com/) | [Web Editor](https://dx7.designburgapps.com/webapp/editor/) | [Cheat Sheet PDF](https://dx7.designburgapps.com/sloopdx-cheat-sheet.pdf)):**
    * **License:** Open Source (GPL-3.0-only). Built upon SLOOP (isod89), Felucca (Leo Kuroshita), and the `msfa` 6-operator DX7 core of Dexed (Apache-2.0).
    * **Concept:** SLOOP's live groovebox workflow merged with an authentic Yamaha DX7 engine and a fully programmable FM drum machine.
    * **Features:**
      * **6-Operator FM Engine:** Complete 32-algorithm DX7 engine ported directly from Dexed's `msfa` (99% sample-identical to Dexed), featuring full envelope scaling, keyboard level/rate scaling, LFO, and feedback.
      * **Cutoff & Resonance Filter:** Dedicated resonant low-pass filter (CUT and RESO on Knobs 1 & 2) placed behind every DX7 voice, modulatable via envelope and LFO.
      * **On-Device Voice Editing:** Full voice programming on the FM-1 hardware with parameter lists, visual operator box diagrams, and operator solo/mute auditioning, backed by a companion web editor.
      * **256 Sysex Voices:** 8 banks of 32 voices loaded directly from standard DX7 `.syx` bulk dumps (4104 bytes), supplemented with 20 factory modern patches (DEEP SUB, 808 SUB, REESE).
      * **Programmable 16×8 FM Drums:** 16 distinct FM drum sounds across 5 kits (`DX KIT`, `808 FM`, `ELECTRO`, `METAL`, `MY KIT`). Each sound provides 8 on-device macro controls (TUNE, DECAY, SWEEP, BRIGHT, NOISE, LEVEL, PAN, CHOKE) plus a dedicated reverb send, parameter locks per step, kit randomization dice, and kit export/import via `.syx`.
      * **OMNI Chord Harp Mode:** Turn any synth track into an Omnichord-like instrument (black keys trigger chords like F, C, G, Dm, Am, Em, G7, E7, D7, Bb, A7, while white keys act as 16 strum strings; bass tracks can follow chords via `FLW`).
      * **Sequencer & Effects:** Up to 128 steps per track (256 steps shared dynamically across tracks), dedicated per-effect pages (SENDS, DIST with soft/hard/fuzz/crush, CHORUS, DELAY, REVERB), USB audio streaming, and live punch-in FX.
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

 3. **[FM1 Move by Nicodesy06](https://github.com/Nicodesy06/FM1-MOVE) ([Web Simulator](https://nicodesy06.github.io/FM1-MOVE/sim/) | [Device Installer & Manager](https://nicodesy06.github.io/FM1-MOVE/device/) | [Manual / Quick Start](https://nicodesy06.github.io/FM1-MOVE/manual/) | [Source Branch](https://github.com/Nicodesy06/FM1-MOVE/tree/fm1-move/dev)):**
    * **License:** Open Source (GPL-3.0). Built upon SLOOP 2.5 by isod89.
    * **Concept:** Eight-track groovebox firmware for the FM-1 inspired by the Ableton Move workflow, featuring a custom 240 × 240 UI designed for live performance.
    * **Features:**
      * **8 Independent Tracks:** Flexible track assignments (any combination of synth tracks or drum kits).
      * **Clips & Scenes:** Performance-oriented clips and scene launcher replacing traditional linear song arrangers.
      * **Browser Simulator:** Firmware compiled to WebAssembly running directly on a simulated device panel in the browser.
      * **Device Page:** In-browser WebMIDI tool to install/backup firmware, manage presets, kits, FM6 banks, and samples.
      * **Status:** Verified in host simulation and builds cleanly for the JieLi AC791N target compiler (experimental / hardware verification in progress).

 4. **[FM1 Quest by hericdk](https://github.com/hericdk/fm1-quest) ([Web Installer](https://hericdk.github.io/fm1-quest/webapp/installer/) | [Web Emulator](https://hericdk.github.io/fm1-quest/emulator/)):**
   * **License:** Open Source (GPL-3.0-only). Built upon the SLOOP groovebox core.
   * **Concept:** Fantasy RPG sidescroller interface for the groovebox: tracks are represented as party heroes, sequence steps are attacks, BPM drives party walk speed, scales dictate biomes, and recording loops triggers boss fights.
   * **Installation:** Browser WebMIDI installer via USB.

 5. **[JIANT FM by juanjiant-bit](https://github.com/juanjiant-bit/JIANT) ([Online Emulator](https://juanjiant-bit.github.io/JIANT/) | [Web Installer](https://juanjiant-bit.github.io/JIANT/webapp/installer/) | [Web Editor](https://juanjiant-bit.github.io/JIANT/webapp/editor/)):**
    * **License:** Open Source (GPL-3.0-only). Built upon Felucca 1.1.5.1 and SLOOP.
    * **Concept:** Bio-synthetic groovebox & performance synthesizer OS for the FM-1 with a high-contrast "thermal camera" UI theme (ironbow gradient palette and Chakra Petch typography). Treat each sound engine as an organic bio-organism reacting dynamically in real time.
    * **Features:**
      * **6 Multi-Engine Tracks (T1–T6):** Flexible pattern sequencing with compressed song sections (storing 8 songs × 4 sections within the FM-1's flash boundary).
      * **8 Distinct Sound Engines:**
        * `ANALOG`: Dual-oscillator analog synth with hard sync, ring mod, 3-saw supersaw, and per-voice multi-mode filter.
        * `FM6`: 6-operator FM engine (Dexed core) with native `.syx` patch import.
        * `PHASE`: Feedback phase-distortion synthesis engine.
        * `LOFI`: Bytebeat (`BYTE`) and floatbeat (`FLOAT`) algorithmic generator with 32 selectable math formulas, live motion (`MOTN`), pitch bending (`BEND`), and looping (`LOOP`).
        * `VOICE`: Formant/speech synthesis model.
        * `WHEEL`: Tone wheel organ emulation.
        * `NOISE`: Dedicated metallic and noise percussive generator.
        * `DRUM-X`: Bio-percussion kit with colony-morphing X-MOD tempo-synced LFOs.
      * **Bus Slicer (SL BUS):** 16-step mix-bus stutter/repeater and pitch-slicing processor (can be routed post-effects or pre-effects tail).
      * **Technical Visualizer:** Live display curves for envelopes, LFOs, distortion, delay, reverb, and thermal isotherm spectrum.
      * **Live Performance Navigation:** Quick page-jumping by turning the `PRESETS` encoder while holding page navigation buttons.
    * **Installation:** One-click USB browser installer, web-based companion librarian/editor, or in-browser emulator.

 6. **[ORBIT by dspaudio](https://github.com/dspaudio/orbit) ([Web Installer](https://dspaudio.github.io/orbit/) | [Web Emulator](https://dspaudio.github.io/orbit-web-emu/)):**
    * **License:** Open Source (GPL-3.0). Based on SLOOP.
    * **Concept:** Groovebox with visual aesthetic and screen interfaces inspired by the Teenage Engineering OP-1.
    * **Features:** Integrated sample manipulation tools and an event tape mechanism for dynamically shifting and rearranging what the 4 tracks play.
    * **Installation:** In-browser WebMIDI installer via USB directly from the installer page or web emulator.

 7. **[NoteSorcery by catacombius](https://github.com/catacombius/NoteSorcery):**
    * **License:** Open Source (GPL-3.0). Built on SLOOP.
    * **Concept:** OP-1-style 8-track groovebox firmware.
    * **Features:** Live USB audio sampling, project export straight to Ableton Live sets, companion Android controller application.
    * **Installation:** Build and flash via CLI toolchain.

 8. **[SLOOP ALG by shaw-core](https://github.com/shaw-core/Sloop_ALG02):**
    * **License:** Open Source (GPL-3.0-only). Based on SLOOP.
    * **Concept:** Experimental synthesis expansion fork adding Karplus-Strong string synthesis, plucked physical models, additive synthesis, DX7, and VA engines.
    * **Installation:** Web installer and companion editor.

 9. **[FM80S by Floydus (y6zkcqnf5r-hue)](https://github.com/y6zkcqnf5r-hue/fm1-fm80s):**
    * **License:** Open Source (GPL-3.0). Based on SLOOP 2.5 and Felucca.
    * **Concept:** Synthwave-oriented synth-looper firmware for live loop stacking, step sequencing, and song assembly with planned 8-track expansion.
    * **Installation:** Build from source via CLI toolchain.

10. **[SLOOP DX7 Banks by majnikool](https://github.com/majnikool/sloop-fm1):**
    * **License:** Open Source (GPL-3.0). Built on SLOOP by isod89.
    * **Concept:** SLOOP expansion fork supporting up to 12 DX7 voice banks grouped by sound category.
    * **Features:**
      * **12 Categorized DX7 Banks:** Direct flash storage and instant switching across 12 full DX7 voice banks (384 presets) categorized by instrument types (Keys, Bass, Leads, Pads, Strings, Brass, Percussion, FX).
      * **Fast Preset Navigation:** Instant preset category selection without overwriting SLOOP sequencer project states.
    * **Installation:** Build and flash via CLI toolchain (`tools/fm1_install.py`).

11. **[SLOOP Floyd FM by René Bohne](https://github.com/renebohne/sloop-fm1):**
    * **License:** Open Source (GPL-3.0). Fork of SLOOP by isod89.
    * **Concept:** SLOOP fork integrating Floyd Steinberg's 4-operator FM synthesis algorithms and real-time visual envelope feedback.
    * **Features:**
      * **Floyd Steinberg 4-OP FM Engine:** Adds dedicated 4-operator FM sound algorithms with custom modulation matrices and operator wave shaping.
      * **Live Envelope & Scope Display:** Real-time on-device oscilloscope rendering active voice output and ADSR envelope curve response directly on the 240 × 240 screen.
    * **Installation:** Build and flash via CLI toolchain.

12. **[SLICE64-FM by jeymadcat-ops](https://jeymadcat-ops.github.io/SLICE64-FM-web/):**
    * **License:** Open Source (GPL-3.0). Built upon SLOOP / Felucca core.
    * **Concept:** 64-slice sample chopper, beat-slicing, and FM groovebox firmware for the FM-1.
    * **Features:** Deep 64-slice sample mapping across pads/keys, auto-transient detection, slice reversal, pitch pitching per slice, and integrated FM synth accompaniment.
    * **Installation:** Browser WebMIDI installer via USB directly from the web project page.

13. **[winampFM by hericdk](https://github.com/hericdk/winampFM) ([Website & 3D Web Simulator](https://hericdk.github.io/winampFM/)):**
    * **License:** Open Source (GPL-3.0-only). Built upon SLOOP 2.6 (isod89) and Felucca (Leo Kuroshita / Hügelton Instruments).
    * **Concept:** Winamp 2.x-inspired performance synthesizer & groovebox firmware turning the FM-1 interface into classic Winamp windows (main player, equalizer sliders, playlist, and pixel-art visualizers).
    * **Features:**
      * **Winamp 2.x Main Screen & Playlist:** Main home screen styled as Winamp 2.x with time counter, audio spectrum analyzer, BPM, sound marquee, and track buttons. Sound presets browse like a Winamp playlist.
      * **Reel-to-Reel Tape Looping:** Tape deck recording screen with live input VU meter, tape counter, note display, and pass counts. Arming REC starts recording; pressing REC again calculates and locks the loop BPM automatically.
      * **Equalizer Sliders FX & PARTY Mode:** Effects grouped into Winamp equalizer slider bands (SEND, SPACE, MASTER, PARTY, TRACK) controlled via the 4 knobs. Dedicated PARTY performance staging (SOLO, DUEL, TRIAD, AUTOTURN stage cycling, KEEP lead holding, YOYO cross-track stepping).
      * **28 Full-Screen Pixel-Art Visualizers:** Pressing HOME twice unlocks 28 reactive full-screen visualizers responding to played notes, loops, and knobs (Milkdrop-style oscilloscope, spectrum bars, starfield shooter, 80s neon night drive, polygonal chords, doomscrolling feed, dancing raccoon, and lofi study).
      * **Expanded Sound Library & Tapes Carousel:** 157 total sounds (including 153 SLOOP 2.6 sounds plus Brazilian acoustic instruments: Cavaquinho, Berimbau, Agogô Bell, Sanfona, and Brasil drum kits), with a PS1-style 3D cassette tape preview carousel.
      * **Web 3D Simulator & Recorder:** Includes an interactive in-browser 3D model simulator running the real firmware via WebAssembly with audio playback and a Win98-style screen & sound recorder widget.
    * **Installation:** One-click WebMIDI installer via USB directly on the website or flashing `release/winampfm-0.12.fwsc`.

 14. **[No Man Sky FM by hericdk](https://github.com/hericdk/nomanskyFM) ([Website & Web Installer](https://hericdk.github.io/nomanskyFM/) | [3D Web Simulator](https://hericdk.github.io/nomanskyFM/#simulator)):**
     * **License:** Open Source (GPL-3.0). Built upon SLOOP 2.7.1 (isod89) and Felucca (Leo Kuroshita / Hügelton Instruments).
     * **Concept:** Space exploration RPG adventure and live performance groovebox firmware for the FM-1: fly between procedurally generated planetary systems using the rotary knobs while the other hand performs and arranges the live soundtrack.
     * **Features:**
       * **Spaceflight & Planet Exploration:** Pilot a spacecraft across star systems with KNOB 1 (turn/steer) and KNOB 2 (velocity/thrust); land on planetary surfaces, mine mineral resources, fight sentinel robots, warp between stars, and call in your starship via OCT- hold commands.
       * **Interactive Cockpit & Camera Zoom:** KNOB 3 cycles 4 camera perspectives: wide orbit, near flyby, close-up chase, and internal cockpit cabin view.
       * **Live Soundtrack Engine:** Integrated SLOOP 2.7.1 groovebox core allows live sequencing, synth solos, and beat jamming simultaneously while piloting the spacecraft.
       * **Web 3D Simulator & Installer:** Includes an interactive in-browser 3D model simulator running the firmware via WebAssembly with sound output, plus one-click browser WebMIDI installation directly from the project site.
     * **Installation:** One-click WebMIDI installer via USB directly on the website or flashing prebuilt release packages (`.fwsc`).

 15. **[MYCELIUM by Mandalars](https://github.com/megagott/mycelium-fm1) ([Website](https://www.mandalars.org/mandalars/fm1/) | [Releases](https://github.com/megagott/mycelium-fm1/releases)):**
     * **License:** Open Source (GPL-3.0). Built upon Felucca and SLOOP.
     * **Concept:** Psychedelic dance music groovebox firmware dedicated to Forest, Psytrance, Goa, and Hitech production on the FM-1.
     * **Features:** Custom-crafted punchy trance drum kits, alien psychedelic icons and animations, fast rolling 16th-note bassline tools, and four factory demo arrangements.
     * **Installation:** Flashing prebuilt `.fwsc` test releases via WebMIDI or CLI flasher.

#### 1.1.3. FoMni Family (Strumplate & Chord Instruments)

Suzuki Omnichord and Japanese Shigin accompaniment instruments featuring strumplate and chord-shaping workflows:

 1. **[FoMni-1 by charlesvestal](https://github.com/charlesvestal/fm1-fomni) ([Web Installer](https://charlesvestal.github.io/fm1-fomni/)):**
   * **License:** Open Source (GPL-3.0).
   * **Concept:** Suzuki Omnichord-inspired chord harp firmware for the FM-1.
   * **Features:** Strum chords across the white keys like a harp strumplate, select chord roots and types on the black keys, integrated rhythmic accompaniment and arpeggiator modes.
   * **Installation:** Browser WebMIDI installer via USB.

 2. **[FuMi-1 by cartesive](https://github.com/cartesive/fumi-1) ([Web Installer & Emulator](https://cartesive.github.io/fumi-1/)):**
    * **License:** Open Source (GPL-3.0). Fork of FoMni.
    * **Concept:** Traditional Japanese Shigin accompaniment synthesizer inspired by Suikohsha's ST-50.
    * **Features:** Authentic Koto, Sho, Shakuhachi, and Taiko voices tuned to the historical ST-50 just intonation scale system.
    * **Installation:** Browser WebMIDI installer via USB.

 3. **[CoralFlower by FicusFicusov](https://github.com/FicusFicusov/CoralFlower) ([Website & Web Player](https://ficusficusov.github.io/CoralFlower/) | [Releases](https://github.com/FicusFicusov/CoralFlower/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Expressive chord machine inspired by the Torso Electronics T-1 / Orchid chord concepts, tailored specifically to the ergonomics of the FM-1.
    * **Features:** Single-finger chord generation with root and bass note coupling, 27 musical scales, built-in arpeggiator, looper, lush plate reverb, and an evolving pixel flower graphic that grows on the 240 × 240 screen as you play.
    * **Installation:** In-browser WebMIDI player/installer or flashing prebuilt releases (`v0.2`).

#### 1.1.4. Independent & Original Engine Firmwares

Firmwares featuring original sound engines, written-from-scratch architectures, or specialized controller frameworks:

 1. **[baud girl Custom Firmware Mod](https://baudgirl.com/) ([MIDI & SysEx Guide](https://m-vave-fm1-midi-guide.up.railway.app/)):**
   * **License:** Closed Source.
   * **Features:** Comprehensive overhaul and reimagining of the stock firmware ergonomics and controls. Adds Virtual Analog (VA) synthesizer engines and a 64-step sequencer.
   * **Documentation:** [FM-1 MIDI & SysEx Guide](https://m-vave-fm1-midi-guide.up.railway.app/) — exhaustive human-readable documentation of channels, SysEx structure, CC mappings for internal DSP effects, and clock synchronization.
   * **Video Tutorial:** [Baud Girl FM-1+VA Comprehensive Tutorial (NatLife Sounds)](https://www.youtube.com/watch?v=jfuoEBIUsEE) — programming VA engines and the dot-matrix sequencer.
   * **Installation:** Web-based browser installer in a couple of clicks via WebMIDI.

 2. **[Groove OS](https://www.groove-os.com/) ([Web Emulator](https://www.groove-os.com/emu)):**
   * **License:** Commercial / Proprietary ($29).
   * **Concept:** Transforms the FM-1 into a standalone multitrack groovebox without needing any external equipment.
   * **Features:** Up to 8 independent tracks (drums, bass, chords, leads) with independent loop lengths (1 to 8 bars) for evolving polyrhythmic structures, dual sound engine (native 6-op FM + Virtual Analog with ladder filter), up to 20 voices of polyphony (12 FM + 8 VA, max 6 for drums), 64-step sequencer with parameter locks (p-locks), live stage view, curated sound packs, and DX7 SysEx patch reception.
   * **Installation:** Browser-based USB installer via WebMIDI in Chrome/Edge (~2 minutes).

 3. **[Bubba Machine by Erbubar23](https://github.com/Erbubar23/bubba-machine) ([Website](https://erbubar23.github.io/bubba-machine/) | [Web Emulator](https://erbubar23.github.io/bubba-machine/emulador.html) | [Manual](https://github.com/Erbubar23/bubba-machine/blob/main/docs/MANUAL.md)):**
    * **License:** Open Source (GPL-3.0-or-later). Written from scratch in C99.
    * **Concept:** 6-track live performance groovebox firmware for the FM-1 with four gestures per button, dedicated HOME layer, and zero third-party audio dependencies (all factory kits and wavetables synthesized procedurally in C).
    * **Features:**
      * **6 Flexible Tracks:**
        * `T1` TR-Style Drum Machine: 16 instruments with independent polymeter track lengths, accent, ratchets, flam, parameter locks (P-Locks), fill-only steps, and live TR-style roll/erase while running.
        * `T2` Sampler 3.0: 8-slice loop engine reassembled bar-by-bar via algorithmic generator (`TU` programmed row vs `SUENA` played row), integrated sample recorder, take library, slice editor, and 3-band frequency waveform visualization (low/mid/high).
        * `T3` Wavetable Bass: Glide and wavetable synthesis.
        * `T4–T6` Assignable Tracks: Configurable as `SYNTH`, `MONO`, `KIT` (secondary drum machine), or `MIDI`. Per-track arpeggiator, looper, and dedicated musical scale.
      * **Polymeter & Independent Track Timing:** Each track features independent length (1–64 steps) and clock multipliers/dividers (×2 to ×1/4).
      * **Chord Grid:** 16 color-coded chords displaying scale degree and harmonic function.
      * **Live Performance & Safe Flash:** 4 chained scenes, song recording, auto-fills, 16 punch-in FX, track/instrument mutes, and crash-resilient flash saving (CRC, end commit, wear-leveling, and auto-save on stop).
    * **Status & Installation:** Firmware runs in desktop simulation and the in-browser WebAssembly emulator; hardware flasher/installer is in roadmap development.

 4. **[zp12 by Sven Trogus (zvenson)](https://github.com/zvenson/zp12) ([Web Installer & Homepage](https://zp12.designburgapps.com/)):**
    * **License:** Open Source (GPL-3.0-only).
    * **Concept:** Authentic 1980s-style 12-bit sampling drum machine firmware for the FM-1.
    * **Features:**
      * **Lo-Fi 12-Bit Sound Engine:** 32 pads across 4 banks running at 26.04 kHz (or 27.5 kHz). Samples are pitched via pure playback rate skipping without interpolation for authentic gritty 80s aliasing and grain.
      * **8 Filtered Channels:** Independent channel playback where new hits cut previous ones. Channels 1–2 feature a resonant 4-pole low-pass filter closing with decay, channels 3–6 have fixed filters, and knobs act as channel faders.
      * **Performance & Sequencing:** 11 loops triggered on black keys, 4 chained songs, real-time recording with auto-correct and 16-step grid editing, classic MPC-style swing (50–71%), and 4 punch-in FX (beat repeat/roll, reverse, tape stop).
      * **Browser Sample Dropper:** In-browser tool to drop custom user WAVs onto pads and transmit them directly to flash over WebMIDI.
    * **Installation:** Web-based browser installer via WebMIDI in Chrome/Edge.

 5. **[FiMba-1 by J. Adam Sowers (jadamsowers)](https://github.com/jadamsowers/fm1-fimba) ([Web Installer & Emulator](https://jadamsowers.github.io/fm1-fimba/)):**
    * **License:** Open Source (GPL-3.0-only).
    * **Concept:** Thumb piano / kalimba / mbira physical modeling synthesizer firmware for the FM-1.
    * **Features:**
      * **Physical Modeling Engine:** Detailed kalimba acoustic simulation running at 44.1 kHz, featuring modeled tines (material hardness, decay, tone, worn character, tuning, release), resonator bodies (box, gourd, board, buzzers, wah resonance), and built-in effects (space reverb/delay, lo-fi/tape color, chorus, filter, and granular cloud engine).
      * **Keyboard & Key Layouts:** Traditional kalimba *Tine* layout (lowest C4 tine in the center, alternating outwards across white keys) or chromatic *Keyboard* layout. Black keys configurable for thumb-roll chord accompaniment, sharps, or performance modifiers (mute, sound hole covering, freeze, octave shift).
      * **Built-in Sequencer/Arpeggiator:** Mbira pattern generator over chords and live playing.
      * **WebAssembly Browser Emulator:** Complete C sound engine and UI compiled to WebAssembly running in-browser with Web MIDI and preset saving.
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

 6. **[Lunar Modulator by ip2k](https://github.com/ip2k/lunar-modulator):**
   * **License:** Open Source (MIT).
   * **Status:** Research / bench stage.
   * **Features:** *Intergalactic Modulation Station* — alternative firmware based on Mutable Instruments synthesizer engines, a Movy-style sequencer, and an in-browser virtual FM-1 emulator/simulator.

 7. **[AMB-1 by Charles Vestal](https://github.com/charlesvestal/fm1-amb) ([Web Installer & Emulator](https://charlesvestal.github.io/fm1-amb/) | [Manual](https://charlesvestal.github.io/fm1-amb/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Generative ambient synthesizer machine inspired by Brian Eno's *Music for Airports*.
    * **Features:** Self-generating playback immediately from power-on, unsynced tape loops of unequal lengths, gliding bass lines, and generative Euclidean percussion patterns.
    * **Installation:** Browser WebMIDI installer via USB.

 8. **[CTL-1 by Charles Vestal](https://github.com/charlesvestal/fm1-ctl) ([Web Installer](https://charlesvestal.github.io/fm1-ctl/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Dedicated MIDI master controller firmware for the FM-1.
    * **Features:** Turns the FM-1's keys and knobs into a multi-channel USB/TRS MIDI controller while providing internal General MIDI sounds for standalone monitoring.
    * **Installation:** Browser WebMIDI installer via USB.

 9. **[PurpleMonkey FM-1 by Quixotic7](https://github.com/Quixotic7/PurpleMonkeyFM1) ([Web Emulator](https://quixotic7.github.io/PurpleMonkeyFM1/emu/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Simplified toddler music instrument featuring a 5-note pentatonic scale, backing drum beats, and zero menus.
    * **Installation:** Browser WebMIDI installer via USB.

10. **[FM-1 B-Boy Edition by friendsmakenoise-prog](https://github.com/friendsmakenoise-prog/fm1-pocket-sampler):**
    * **License:** Open Source (No license specified in upstream repository).
    * **Concept:** Late-1990s hip-hop chop sampler firmware featuring 3 sample tracks and a dedicated FM bass/lead lane.
    * **Installation:** Web installer via USB.

11. **[fm1-polyseq by NOVALENTI](https://github.com/NOVALENTI/fm1-polyseq):**
    * **License:** Open Source (No license file in repository; source code is publicly accessible).
    * **Concept:** Polyphonic 16-step sequencer and bare-metal hardware abstraction layer (HAL) written in strict C99 for the AC791N's pi32v2 CPU.
    * **Installation:** Compile from source.

12. **[FM-106 by PattF](https://github.com/patttf/fm-106) ([Librarian & SysEx Editor](https://patttf.github.io/fm-106/Librarian.html)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Roland Juno-106 emulation firmware for the FM-1 based on an optimized port of the open-source KR-106 synthesizer engine.
    * **Features:**
      * **Full 6-Voice Polyphony:** Authentic Juno DCO sound generation hitting ~30% CPU load across both JieLi `pi32v2` cores.
      * **Oscilloscope & Real-Time Controls:** Split on-device display showing the live oscilloscope waveform alongside simultaneous filter, envelope, and oscillator parameters.
      * **Juno-106 SysEx Patch Compatibility:** Direct `.syx` patch import and management via companion web Librarian.
      * **Bank Management:** 4 banks (2 factory banks + 2 user banks) selectable via the `ALGORITHM` encoder, with on-device patch naming and saving.
      * **USB-C Audio:** Integrated class-compliant digital stereo audio output over USB-C.
    * **Installation:** Browser WebMIDI installer via USB.

13. **[ETCH by SikkenWorks](https://github.com/SikkenWorks/ETCH) ([Homepage & Web Installer](https://etch.sikkenworks.com/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** "Draw. Morph. Modulate." — waveform drawing and morphing synthesizer firmware.
    * **Features:** 8-voice polyphony, direct on-device single-cycle waveform drawing (Waves A, B, and modulating Wave C), real-time interpolation/morphing between drawn waves, wave library, motion recording, and arpeggiator with generative RIFF mode.
    * **Installation:** Browser WebMIDI installer via USB or flashing prebuilt `.fwsc` image.

14. **[AMBII by MilkBoyG / JalopyMusic](https://github.com/JalopyMusic/fm1-milkboyg-ambii):**
    * **License:** Open Source (GPL-3.0). Built on Melodee and Felucca.
    * **Concept:** Alternative performance and recording interface firmware built on Melodee's real multi-engine C core.
    * **Features:** Four tracks with scoped pattern actions, drum ratchets, parameter automation graphs with undo, shared delay/reverb, and dedicated Galaxy / Dark Matter UI themes.
    * **Status:** In-browser prototype and development preview (no hardware release image yet).

15. **[MC-1 by dspaudio](https://github.com/dspaudio/mc-1) ([Web Hub & Online Player](https://dspaudio.github.io/mc-1-web/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** 4-track groovebox firmware inspired by Roland Linear Arithmetic (LA) synthesis (D-50) and MC-series grooveboxes (MC-101 / MC-303).
    * **Features:**
      * **LA Synthesis Sound Engine:** Combines PCM attack transients with synthesized sustaining partials, driving authentic late-80s digital/analog hybrid timbres.
      * **4 Tracks & Performance Sequencer:** Dedicated lanes for Drums, Bass, Chords, and Lead/Arp with step sequencing and live parameter modulation.
      * **Drum & Acid Generators:** Built-in synthesized TR-style rhythm voices and resonant 303 acid line generator.
      * **Dedicated Web Companion:** Web audio player and patch tool running at `dspaudio.github.io/mc-1-web`.
    * **Installation:** Browser WebMIDI installer via USB directly from the web hub or build from source.

16. **[OberVave by Sven Trogus (zvenson)](https://github.com/zvenson/obervave) ([Webpage & Web Installer](https://fm1.designburgapps.com/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** 8-voice American analog polysynth emulation (Oberheim OB-Xa / OB-8 style, 1979–1984) for the M-VAVE FM-1.
    * **Features:**
      * **Classic 8-Voice Polysynth Architecture:** Dual oscillators per voice with sawtooth and pulse (PWM) waves, hard oscillator sync, cross-modulation, and white noise generator.
      * **Morphing 12/24 dB Resonant Filter:** Continuous morphing between 2-pole (12 dB/oct Oberheim SEM style) and 4-pole (24 dB/oct Curtis/CEM style) low-pass filter responses with dedicated envelope modulation.
      * **Vintage Drift & Unison:** Modeled analog voice circuit drift, polyphonic unison/detune stack, dual LFOs, and vintage chorus/delay spatial effects.
      * **On-Device Graphical Editing:** Real-time filter frequency curve rendering and envelope visualization on the 240 × 240 display.
    * **Installation:** Browser WebMIDI installer via USB directly from the project homepage.

17. **[MONK-1 by Charles Vestal](https://github.com/charlesvestal/fm1-monk) ([Web Emulator](https://charlesvestal.github.io/fm1-monk/emu/) | [Web Installer](https://charlesvestal.github.io/fm1-monk/install/) | [Manual](https://charlesvestal.github.io/fm1-monk/manual/) | [Releases](https://github.com/charlesvestal/fm1-monk/releases)):**
    * **License:** Open Source (GPL-3.0). Free of charge (donations suggested to savetibet.org).
    * **Concept:** Formant vocal synthesizer firmware turning the FM-1 into Jonathan Taylor's **MonkSynth** (homage to AudioNerdz's 2002 *Delay Lama* plug-in) with twelve singing characters (Jerry the monk, Philip the unicorn, Snider, etc.).
    * **Features:**
      * **12 Animated Singing Characters:** Each character sings with its own vocal tract size and voice; mouth animations follow vowels in real-time sprite frames on the color screen.
      * **Native Velocity & Pressure/Aftertouch:** Leverages the FM-1's stock capacitive keys without hardware modifications (via [Velo](https://github.com/charlesvestal/fm1-velocity) sensing algorithms) to control note loudness via strike velocity and vowel morphing/pitch bends via pressure aftertouch.
      * **Dedicated Vocal Controls:** Gliding legato mono voice, Choir/Unison stack (1–10 voices with detune and head size spread), vibrato rate/depth, echo delay, ADSR envelopes, and octave switching.
      * **USB MIDI & Accessibility:** Full USB-MIDI in/out with polyphonic aftertouch and vowel CC controls; integrates with the [FM-1 Screen Reader](https://charlesvestal.github.io/fm1-reader/) to speak aloud on-screen parameters and button actions for visually impaired users.
    * **Installation:** Browser WebMIDI installer via USB, in-browser WebAssembly emulator, or flashing prebuilt releases.

18. **[M-VAVE FM1 Open Firmware (m-vave/fm1_open)](https://github.com/m-vave/fm1_open) ([Releases / V10](https://github.com/m-vave/fm1_open/releases) | [Official Workbench](https://open.m-vave.com/fm1-workbench)):**
    * **License:** Open Source (GPL-3.0-only for application code; includes vendor binary libraries and third-party notices).
    * **Significance:** Official open-source release of the factory FM-1 firmware and SDK directly from the manufacturer (M-VAVE).
    * **Architecture & Features:**
      * **8 Tracks & 8 Sample Slots:** Full multitrack groovebox architecture with 8 audio/synth tracks, 8 sample slots, and 16 built-in demo presets/FX.
      * **Board Drivers & Audio HAL:** Direct hardware C source code for panel controls, 240 × 240 display, encoders, and audio engine rendering (`app/board/`, `app/audio_output.c`) supporting USB/Bluetooth mixing and USB recording.
      * **Complete Toolchain & WebAssembly Workbench:** Complete build scripts (`build.bat`) supporting both native firmware compilation via JieLi PI32v2 Clang 4.0.1 (`FM1_OFFICIAL_OPEN.fwsc`) and WebAssembly compilation via WASI SDK 27 for in-browser workbench simulation.
    * **Installation:** Web workbench flasher via USB (`open.m-vave.com`), official flasher, or building `.fwsc` from source.

19. **[OPN-1 by putchdev](https://github.com/putchdev/opn-1) ([Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x7edf7/mega_drive_genesis_sounds_on_the_fm1/)):**
    * **License:** Open Source.
    * **Concept:** Sega Mega Drive / Genesis sound chip recreation for the M-VAVE FM-1, accurately emulating both the Yamaha **YM2612** 6-channel FM synthesizer and the Texas Instruments **SN76489** 4-channel PSG (Programmable Sound Generator).
    * **Features:**
      * **VGM / VGZ File Player & Patch Converter:** Web companion app converts Sega Genesis/Mega Drive VGM and VGZ music rips into playable patch banks sent directly to the FM-1, or plays the tracks directly through the synthesizer hardware.
      * **Multitimbral Polyphony & Compatibility Modes:** Includes a 6-part monophonic Mega Drive accurate compatibility mode (mapped across individual MIDI channels, with special CH3 multitimbral mode) as well as a modern polyphonic mode where parts can be layered across identical or customized MIDI channels.
      * **Advanced Part Composition & Layering:** Dedicated configuration screen with per-part amplitude scaling, programmable delay stages (parts kick in after a timed delay), and note-off trigger toggles to easily layer transients, sustain bodies, and release tails combining YM2612 FM and PSG voices.
      * **MIDI & On-Device Playback:** Retains the last loaded patch set in memory for standalone play via capacitive keys, USB MIDI, and 3.5 mm TRS MIDI input.
    * **Installation:** Web companion app over WebMIDI USB or building firmware from source.

20. **[CS-1 by twochannels](https://github.com/twochannels/CS-1) ([Website & Web Emulator](https://twochannels.github.io/CS-1/)):**
    * **License:** Open Source.
    * **Concept:** Yamaha CS-80 analog synthesizer emulation in spirit for the FM-1.
    * **Features:** 8 voices consisting of dual independent synthesizer channels, resonant high-pass and low-pass filters in series, ring modulator, expressive touch response modeling, and 22 factory tones faithfully recreated from the original 1977 CS-80 owner's manual.
    * **Installation:** In-browser WebAssembly emulator and WebMIDI flasher.

21. **[Frodhes by Leonardo Mirabal](https://github.com/leonardoMirabal/frodhes) ([Website & Web Emulator](https://leonardomirabal.github.io/frodhes/) | [Releases](https://github.com/leonardoMirabal/frodhes/releases)):**
    * **License:** Open Source. Built on Dinghy.
    * **Concept:** Fender Rhodes electric piano physical modeling synthesizer without sample dependencies.
    * **Features:** 4 physical electric piano models (tines, pickups, hammer character), modeled analog signal chain featuring compressor, drive, stereo tremolo or auto-wah, phaser, chorus, stereo delay, and reverb. Includes tap tempo, MIDI clock sync, musical scale quantization, and patch presets.
    * **Installation:** In-browser WebMIDI installer or flashing prebuilt `frodhes-X.X.X.fwsc`.

22. **[Vector37 by genkigenki](https://github.com/genkigenki/Vector37) ([Web Installer](https://genkigenki.github.io/smk37/#fw-vector37) | [Web Simulator](https://genkigenki.github.io/smk37/vector37-sim/) | [Releases](https://github.com/genkigenki/Vector37/releases) | [Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x8eo32/vector37_update_more_sounds_a_smoother_screen_for/)):**
    * **License:** Open Source (GPL-3.0). Ported from the SMK-37 to FM-1.
    * **Concept:** Orbiting overtone vector synthesizer inspired by the Beetlecrab Vector.
    * **Features:**
      * **Orbiting Overtone Synthesis:** Four corners each hosting two overtone generators, with a central sun moving along an orbital trajectory and an orbiting moon determining crossfade and balance levels between generators, while encoders shape the active planet's synthesis characteristics.
      * **Factory & User Preset Banks:** 32 factory sounds organized into two 16-preset banks (warm strings, ambient pads, choir, vintage organ, electric piano, plucked harp, and an 8-sound drum kit), with user preset saving to a dedicated USER bank via the PATCH button.
      * **Performance & Hardware Features:** Configurable MIDI TRS OUT and USB IN routings via SETUP, plus 60 FPS display rendering optimizations.
    * **Installation:** Browser WebMIDI installer via USB directly from the SMK-37 / FM-1 Hub, in-browser simulator, or flashing prebuilt release packages (`.fwsc`).

23. **[HYP-1 by RedtailWorks](https://github.com/RustyPawz/fm1-HYP1) ([Website & Web Emulator](https://rustypawz.github.io/fm1-HYP1/)):**
    * **License:** Open Source. Forked from AMB-1 by Charles Vestal.
    * **Concept:** Hypnotic techno, acid, and drone groovebox firmware.
    * **Features:** Continuously breathing atmospheric pads, deep sub-bass drones, generative TB-303 acid line generator, and granular textures layered over a hands-on live drum step sequencer with instant bar pattern flipping and breakdown/build-up macro staging.
    * **Installation:** In-browser WebAssembly emulator and WebMIDI installer.

24. **[Tonitor by Nuno Zimas](https://github.com/nzimas/tonitor) ([Website](https://nzimas.github.io/tonitor/)):**
    * **License:** Open Source.
    * **Concept:** 6-track experimental ambient and live looping performance synthesizer.
    * **Features:** 3 distinct synthesis engines, algorithmic sound patch generator, free-length live audio loops supporting up to 10 overdubs per track, real-time granulator, multi-mode filters, and lush ambient reverb.
    * **Installation:** Flashing via WebMIDI or CLI flasher.

25. **[BEETLE by Joppe Sikken (SikkenWorks)](https://github.com/SikkenWorks/BEETLE) ([Website & Web Emulator](https://sikkenworks.github.io/BEETLE/) | [Releases](https://github.com/SikkenWorks/BEETLE/releases)):**
    * **License:** Open Source.
    * **Concept:** Classic vertical tracker firmware for the FM-1.
    * **Features:** Vertical top-to-bottom step tracking interface styled after vintage trackers, featuring dedicated columns for Note, Instrument, Chord, and Effect commands, bringing fast demoscene tracker composition workflows to the FM-1's hardware screen and buttons.
    * **Installation:** Web-based browser emulator/installer or flashing prebuilt release packages (`V1.01d_RC`).

26. **[FOMAJAM by konsumer](https://github.com/konsumer/fomajam) ([Website & Web Emulator](https://konsumer.js.org/fomajam/) | [Releases](https://github.com/konsumer/fomajam/releases)):**
    * **License:** Open Source.
    * **Concept:** Classic step-grid vintage drum machine firmware for the FM-1.
    * **Features:** Faithfully synthesized drum engines inspired by iconic rhythm units: Roland TR-909, TR-808, TR-707, TR-606, Oberheim DMX, and more. Features per-voice machine assignment, step accents, pattern banks, and full browser WebAssembly simulation.
    * **Installation:** In-browser WebMIDI flasher and emulator directly from the project site or flashing prebuilt `fomajam-X.X.X.fwsc`.

27. **[MIN-1 by Reytian](https://github.com/Reytian/fm1-min1) ([Website](https://reytian.github.io/fm1-min1/) | [Web Emulator](https://reytian.github.io/fm1-min1/emu/) | [Releases](https://github.com/Reytian/fm1-min1/releases)):**
    * **License:** Open Source.
    * **Concept:** Minimalist generative ensemble synthesizer firmware inspired by Philip Glass.
    * **Features:** Immediately begins performing intricate generative patterns upon power-up, allowing the player to seamlessly join the performance at any time. Features an EASY mode where every white key triggers harmonically fitting chords, 4 algorithmic models, and 20 built-in minimalist musical pieces.
    * **Installation:** Web-based emulator/installer via USB or flashing prebuilt `min1-X.X.X.fwsc`.

28. **[Pocket GammaWave by ShadowTune (GammaWave Audio)](https://github.com/fvalente/GammaWave-FM1) ([Homepage](https://gammawaveaudio.com/) | [Web Simulator](https://fvalente.github.io/GammaWave-FM1/) | [Web Editor](https://fvalente.github.io/GammaWave-FM1/webapp/editor/?mock=1) | [Releases](https://github.com/fvalente/GammaWave-FM1/releases)):**
    * **License:** Open Source.
    * **Concept:** Companion pocket groovebox and industrial synthesizer for the GammaWave desktop synthesizer.
    * **Features:** Four industrial distortion modes, formant vowel and screaming resonant filters, real-time FFT audio spectrogram visualization, 4-track tape deck style interface, and an automated algorithmic song generator spanning 49 musical genres (including modern Trap, Drill, and industrial soundscapes).
    * **Installation:** In-browser WebAssembly simulator and WebMIDI installer or flashing prebuilt `gammawave-1.0-GW.fwsc`.

29. **[TERKINSTEIN by TerkWerX](https://github.com/TerkWerX/FM1-TERKINSTEIN-Firmware) ([Releases](https://github.com/TerkWerX/FM1-TERKINSTEIN-Firmware/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Dark performance synth and 4-track groovebox with a cybernetic reactive UI.
    * **Features:** 64 curated sounds, 6-operator FM engine, metallic distortion modes, fully synthesized drum kits and pads, reactive neon purple-and-green display animations, and 64-step tracks across 4 pattern banks.
    * **Installation:** Flashing prebuilt `v0.22.0-dev` releases via WebMIDI or CLI updater.

30. **[Niagara Drift by Evan Yerburgh](https://github.com/evanyerburgh/niagara-drift) ([Releases](https://github.com/evanyerburgh/niagara-drift/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Immersive dual-drone synthesizer with slow algorithmic parameter drift.
    * **Features:** Two continuously sounding drones with partner and sub-oscillators, resonant multi-mode filters, dual-waveform LFO, rhythmic swell generator, stereo delay and reverb, 16 pre-programmed sound scenes, and slow continuous automatic drift.
    * **Installation:** Flashing prebuilt `v0.1-beta` releases via WebMIDI or CLI updater.

31. **[MNM-1 by sirpearson](https://github.com/sirpearson/fm-1-monomachine):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Six-track monophonic groovebox inspired by the workflow of the legendary Elektron Monomachine.
    * **Features:** One dedicated drum kit track and five monophonic synth tracks each hosting independent synthesis machines, a 64-step sequencer with parameter locks (p-locks) per step, three assignable LFOs per track, and per-track stereo delay lines.
    * **Installation:** Build and flash via CLI toolchain.

32. **[SIDOU by Denis Sablic (dsablic)](https://github.com/dsablic/sidou):**
    * **License:** Open Source (GPL-3.0-or-later).
    * **Concept:** Commodore 64 SID chip (MOS 6581/8580) emulation instrument for the FM-1.
    * **Features:** Authentic software SID emulation, real-time live performance mode, capacitive key and USB-MIDI input response, with an onboard step sequencer and `.sid` chiptune file playback architecture.
    * **Installation:** Build from source / desktop simulation.

33. **[TripDeck by anonymousacademe](https://github.com/anonymousacademe/FM-1-TripDeck):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Psychedelic synthesizer where every screen page is an interactive full-screen animated graphic driven by the four rotary encoders.
    * **Features:** Sitar, evolving ambient pad, pipe organ, and bell FM voices; spiral echo delay, shimmer reverb, formant vowel filter, musical scale lock, integrated arpeggiator, and step sequencer.
    * **Installation:** Build and flash via CLI toolchain.

34. **[Evander's Music Box by Mike Tsakiroglou (MikeTsak)](https://github.com/MikeTsak/Evanders-Music-Box--FM-1-LARP-firmware) ([Releases](https://github.com/MikeTsak/Evanders-Music-Box--FM-1-LARP-firmware/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Roleplaying-themed firmware transforming the FM-1 into an elven bard's enchanted music box for tabletop and LARP gaming sessions.
    * **Features:** Four-track medieval workshop with a 64-step sequencer, plus an Encounter mode offering 16 instant atmospheric scene soundtracks for live games. Features custom fantasy UI and boot artwork.
    * **Installation:** Flashing prebuilt `v1.3` releases via WebMIDI or CLI updater.

35. **[LOF-1 by RedtailWorks](https://github.com/RustyPawz/fm1-HYP1) ([Website & Web Installer](https://rustypawz.github.io/fm1-HYP1/lof/) | [Web Emulator](https://rustypawz.github.io/fm1-HYP1/lof/emu/) | [Manual](https://rustypawz.github.io/fm1-HYP1/lof/manual/) | [Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x7pbwa/lof1_a_generative_lofi_ambiance_machine_with/)):**
    * **License:** Open Source (GPL-3.0). Built on AMB-1 (Charles Vestal) and Felucca.
    * **Concept:** Generative lo-fi ambience machine and tired jazz band groovebox: you play the lead on the capacitive keys, and an intelligent backing band listens to which chord your notes imply, dynamically following your performance with comp, bass, and drums.
    * **Features:**
      * **Interactive Lead & Tired Jazz Band:** 20 acoustic and FM instruments (Rhodes, Wurli, FM piano, upright pianos, vibes, marimba, kalimba, tenor sax, muted trumpet, clarinet, flute, ocarina, harp, music box).
      * **Comp, Bass & Call-and-Response:** Automatic chord re-voicing on changes (held, stabs, offbeats, arpeggios), walking/dub bass, and an "Answer" engine that dynamically echoes phrases or invents counter-melodies when you pause.
      * **Daydream Mode:** If left untouched, an algorithmic ghost takes over the lead melodies with configurable phrase density until any key is pressed to take back control.
      * **16-Step Drum Sequencer & Drift:** 8 drum lanes across Dusty (samples) and Tape (synthesized) kits with groove swing and automatic pattern drift.
      * **Dust Signal Chain & Old TV Display:** Authentic vinyl crackle, cassette hiss, reel-to-reel saturation, and radio static with wow/flutter and granular smear; vintage CRT scanlines with 5 color themes (Lamp, Matcha, Sakura, Midnight, Sepia).
      * **Live Performance FX Keys:** Hardware keys map to tape stop, backspin, record skip, half-time, stutter, mufflers, and throws.
    * **Installation:** In-browser WebAssembly emulator and WebMIDI installer directly from the project site or flashing prebuilt `lof1-0.0.41.fwsc`.

36. **[ECO-1 by RedtailWorks](https://github.com/RustyPawz/fm1-HYP1/tree/main/eco1) ([Website & Web Installer](https://rustypawz.github.io/fm1-HYP1/eco/) | [Web Emulator](https://rustypawz.github.io/fm1-HYP1/eco/emu/) | [Manual](https://rustypawz.github.io/fm1-HYP1/eco/manual/)):**
    * **License:** Open Source (GPL-3.0). Fork of AMB-1 by Charles Vestal (built on Felucca by Hügelton Instruments). Experimental: tested in the simulator and browser emulator, not yet on a real FM-1.
    * **Concept:** Generative botanical ambient synthesizer turning the FM-1 into an algorithmic musical plant.
    * **Features:**
      * **Leaves & Stem:** Three virtual leaves each accumulate charge from light and water and fire a note when full (8 FM voices: Glass, Wood, Pluck, Chime, Reed, Flute, Swell, Kalimba); firings run down the stem and the other leaves answer. A stem drone underneath (Hum, Organ, Reed, Choir) on the root and a chosen interval.
      * **Sky & Weather:** Day/night cycle (30 s to 30 min) or a fixed Night or Day sky; night mellows the plant rather than silencing it. Rain showers with a synthesized rain track, wind that shakes the leaves, sings a rising whistle and opens the reverb; drought wilts the plant.
      * **Eight Plants:** Fern, Orchid, Moss, Cactus, Willow, Lotus, Ivy and Bamboo, each drawn in its own scene (forest floor, windowsill, desert, pond...) and each reacting to the weather in its own way.
      * **DAW Integration:** MIDI clock in (the day counts in bars, leaves can fire on a 1/4 to 1/16 grid), MIDI out with each leaf and the stem on its own channel plus the plant's signals (charge, water, soil, light, rain, wind) as CCs; the browser emulator outputs eight channels, each voice apart.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site, in-browser WebAssembly emulator, or flashing the prebuilt release package (`eco1-latest.fwsc`).

37. **[P6 by Jonbenderr](https://github.com/Jonbenderr/fm1-p6) ([Web Installer](https://jonbenderr.github.io/fm1-p6/install/) | [Web Emulator](https://jonbenderr.github.io/fm1-p6/emu/) | [Releases](https://github.com/Jonbenderr/fm1-p6/releases)):**
    * **License:** Open Source (GPL-3.0). Built on Dinghy by Charles Vestal.
    * **Concept:** Korg Polysix-inspired 6-voice analog polysynthesizer firmware for the M-VAVE FM-1.
    * **Features:**
      * **6-Voice Analog Architecture:** 6 voices of polyphony, 1 VCO per voice with sub-oscillator (1 or 2 octaves down), pulse width modulation (PWM), and white noise generator.
      * **Resonant 4-Pole VCF & Envelopes:** Modeled SSM2044 24 dB/oct resonant low-pass filter with keyboard tracking and dedicated ADSR envelope generator.
      * **Modulation & Vintage BBD Effects:** Modulation Generator (MG/LFO) with routing to VCO, VCF, and VCA; authentic bucket-brigade style analog Chorus, Phaser, and Ensemble spatial effects.
      * **Key & Voicing Modes:** Polyphonic, Unison (all 6 voices stacked with detune), and Chord Memory modes, plus Key Hold latching and an integrated arpeggiator with up/down/random patterns and sync.
      * **Preset Program Storage:** 32 preset program memories organized as 4 banks of 8 sounds (A-1 through D-8).
    * **Installation:** Browser WebMIDI installer via USB, in-browser WebAssembly emulator, or flashing prebuilt release packages (`.fwsc`).

38. **[Speak37 by genkigenki](https://github.com/genkigenki/Speak37) ([Web Installer](https://genkigenki.github.io/smk37/#fw-speak37) | [Releases](https://github.com/genkigenki/Speak37/releases) | [Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x89f3y/speak37_a_free_talking_synth_firmware_for_the/)):**
    * **License:** Open Source (GPL-3.0). Compatible with both M-VAVE SMK-37 and FM-1.
    * **Concept:** Talking speech synthesizer and singing voice firmware for the FM-1: every keypress speaks or sings the next syllable or word of a sentence at that note's pitch, singing in multi-voice harmony when chords are played.
    * **Features:**
      * **Singing Synthesizer Engine:** 9 distinct speech voices (Classic Chip Robot, Giant, Whisper, Chipmunk, Alien, and more); chords sing in full musical harmony.
      * **Rhythm Section & Fixed-Point 808:** Built-in fixed-point Roland TR-808 rhythm generator with 16 groove styles; pressing the PLAY button automatically speaks words on the beat over drum grooves.
      * **Beatbox Drum Kit:** White and black keys double as vocal beatbox triggers (phonetic kicks, snares, hats, and vocal scratches).
      * **MOPE Mode:** An interactive sullen robot mode that actively monitors your playing, responds with melancholic spoken remarks, and plays sad algorithmic interludes when ignored.
    * **Installation:** Browser WebMIDI installer via USB directly from the SMK-37 / FM-1 Hub, or flashing prebuilt release packages (`.fwsc`).

39. **[FMEL-1 (MEL) by Antonio Altea](https://github.com/AntonioAltea/fmel-1) ([Web Installer](https://antonioaltea.github.io/fmel-1/install/) | [Web Emulator](https://antonioaltea.github.io/fmel-1/) | [Releases](https://github.com/AntonioAltea/fmel-1/releases)):**
    * **License:** Open Source (GPL-3.0). Built on Dinghy by Charles Vestal (SLOOP / Felucca lineage).
    * **Concept:** Mellotron M400 tape keyboard instrument for the FM-1 with authentic tape mechanics, dual-tape blending, and vintage analog signal processing.
    * **Features:**
      * **Four Classic M400S Tapes:** Includes authentic tape recordings of Flute (Strawberry Fields Forever), 8-Voice Choir, Cello, and Vibraphone (digitized by Bernie Kornowicz / Taijiguy).
      * **Tape Blending & Mechanics:** Seamless continuous blending between Tape A and Tape B across the keyboard, complete with authentic 8-second tape run-out physics, key release mechanical click, and half-speed tape motor playback (octave drop).
      * **LOFI Tape Aging Section:** Real-time tape degradation processing featuring wow, flutter, tape hiss, age wear, dropouts, mechanical drift, drive, and lo-fi bitcrush.
      * **Vintage FX & Sequencer:** Vibrato, Leslie rotary speaker, tape echo delay, spring/hall reverb, 2-band EQ, note HOLD latch, integrated arpeggiator, and 16-step pattern sequencer.
      * **Custom Display Art:** Features custom animated tape transport graphics and screen artwork drawn by Javi.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site, in-browser WebAssembly emulator, or flashing prebuilt release packages (`.fwsc`).

40. **[GRAV-1 by RedtailWorks](https://github.com/RustyPawz/fm1-HYP1/tree/main/grav1) ([Website & Web Installer](https://rustypawz.github.io/fm1-HYP1/grav/) | [Web Emulator](https://rustypawz.github.io/fm1-HYP1/grav/emu/) | [Manual](https://rustypawz.github.io/fm1-HYP1/grav/manual/)):**
    * **License:** Open Source (GPL-3.0). Built on AMB-1 by Charles Vestal and Felucca by Hügelton Instruments. Experimental: tested in the simulator and browser emulator, not yet on a real FM-1.
    * **Concept:** Generative dark, spacey ambient firmware that turns the FM-1 into a small solar system: a star and its planets play the music.
    * **Features:**
      * **Star & Planets:** A central star hissing and roaring in eight colours of noise, with up to six orbiting planets, each a voice (16 instruments) playing a short phrase around its orbit, warm and dry near the star, cold and wet far out.
      * **Gravity & Orbits:** A drum sequencer sets each planet's year (and, by Kepler's law, how close it orbits); larger planets swell smaller ones as they pass, and dust clouds, asteroids and comets drift through.
      * **Ten Systems:** Ten preset solar systems, an eclipse hold, and an orbit view that takes over the screen when left untouched.
      * **DAW Integration:** MIDI clock in drives the steps and the orbits; MIDI out sends each planet's notes on its own channel, the drums on another, and the system's signals as CCs; the browser emulator outputs eight channels, each voice apart.
    * **Installation:** Browser WebMIDI installer via USB directly from the project site, in-browser WebAssembly emulator, or flashing the prebuilt release package (`grav1-latest.fwsc`).

41. **[MD-One by d0pe1](https://github.com/d0pe1/md-one):**
    * **License:** Open Source (GPL-3.0-only for firmware, inherited from Dinghy; standalone `dsp/` library is MIT).
    * **Concept:** Mutable Instruments-derived drone machine ("Mutable Droner") for the M-VAVE FM-1.
    * **Features:**
      * **Braids Oscillator Port:** Full port of all 48 synthesis models from Mutable Instruments Braids compiled for the JieLi `pi32v2` CPU core at 44.1 kHz.
      * **Drone Synthesis Engine:** Four always-on Braids voices with detune, tuned comb filters, slow spectral evolution, drift, and key latching to hold notes in and out.
      * **Lightweight DSP Footprint:** Highly optimized fixed-point integer DSP engine consuming ~14.5% of the AC791N audio processing budget.
      * **DAW Integration:** Designed to deliver multichannel drone soundscapes into a DAW over USB audio.
    * **Status & Installation:** Firmware core verified in desktop testing harnesses and the `fm1-emu` emulator; physical hardware release in active development.

### 1.2. Modular Firmware Platforms & Builders

 1. **[fm1-rocket-os by cmlarsen](https://github.com/cmlarsen/fm1-rocket-os):**
    * **License:** Open Source (GPL-3.0). Forked from X0X and Felucca.
    * **Concept:** Clip-launching performance firmware turning the FM-1 into an Ableton Live-style clip launcher and matrix sequencer.
    * **Status:** Work in progress.

 2. **[Optimist by w0ts](https://github.com/w0ts/optimist):**
    * **License:** Open Source (GPL-3.0-only). Derived from SLOOP, Felucca, Melodee, and X0X.
    * **Status:** In active development (tested in emulator).
    * **Concept:** Modular firmware builder and platform allowing users to custom-assemble FM-1 firmware images tailored to flash and RAM budgets.
    * **Features:**
      * **Firmware Builder (`make builder`):** Choose specific synth engines (ANALOG 2, DIGITAL, PHASE, LOFI, SAMPLE, VOICE, TRIO, WHEEL, GRAIN, FM6, SLICE, PHYS, ACID), drum kits, effects (DUST, DUCK, DJ filter, delay, reverb), and sequencer capabilities at compile-time.
      * **Multi-Layer UI & Sequencer:** SLOOP-style live button-held layers, per-track patterns, scenes, snapshots, fills, microtiming, and parameter locks.
      * **SLOOP 2.4 Project Compatibility & Web Editor:** Full project interchangeability and web-based parameters librarian.
    * **Installation:** Build and flash via CLI/Docker toolchain.

 3. **[Dinghy by Sven Trogus (zvenson)](https://github.com/zvenson/dinghy):**
    * **License:** Open Source (GPL-3.0-only).
    * **Concept:** Minimal, clean firmware skeleton for custom developers: 4-voice sine wave synthesizer on top of working display, audio DMA, and button input drivers.
    * **Installation:** Compile and flash via Makefile/CLI.

 4. **[Modular-1 by morgulbrut](https://wiggismodular.github.io/Modular-1/) ([Webapp & Flasher](https://wiggismodular.github.io/Modular-1/)):**
    * **License:** Open Source (GPL-3.0). Built using Felucca HAL and tooling.
    * **Concept:** Nord Modular-inspired modular synthesizer engine and visual web patch editor for the FM-1.
    * **Features:**
      * **Browser Patch Editor:** Interactive visual web environment allowing users to construct modular signal paths, configure modules, and upload patches directly to the FM-1 hardware.
      * **Module Architecture & Matrix:** Modules feature parameter inputs (`p1` and `p2` with attenuverters) alongside an assignable modulation matrix routing global `p1`/`p2` and contextual `k1`–`k4` knob controls per module.
      * **Generative Arpeggiator:** Complex multi-page arpeggiator engine featuring dedicated melody controls (scale, root, speed), Euclidean rhythm sequencing (pulses, rotation, rate), and chaotic generative probability/octave spreading.
    * **Installation:** Browser WebMIDI installer via USB directly under the webapp's Flash tab.

 5. **[Hexagon Console](https://www.reddit.com/r/MVaveFM1/comments/1x5qq7z/coming_soon_hexagon_console/):**
    * **Status:** Upcoming / Teased announcement.
    * **Concept:** Console-style musical environment and custom firmware architecture for the M-VAVE FM-1.
    * **Details:** Teased within the r/MVaveFM1 community ([Coming soon: Hexagon Console](https://www.reddit.com/r/MVaveFM1/comments/1x5qq7z/coming_soon_hexagon_console/)), introducing a modular hexagonal UI paradigm and performance console interface tailored for the FM-1 hardware.

### 1.3. Gaming, Emulators & Non-Audio Ports (Games & Experiments)

 1. **[FM-1 Doom by Sven Trogus (zvenson)](https://github.com/zvenson/fm1doom) ([Web Installer](https://doom.deadlockinteractive.com/) | [Alt Web Installer](https://dx7.designburgapps.com/doom/)):**
    * **License:** Open Source (GPL-2.0-or-later / GPL-3.0; FreeDM game data under BSD-3-Clause). Based on doomgeneric, Chocolate Doom, and the sloopDX / SLOOP / Felucca platform.
    * **Concept:** Port of classic Doom (running a FreeDM arena map) on the M-VAVE FM-1 synthesizer hardware.
    * **Features:**
      * Rendered directly to the FM-1's color screen with health, armor, ammo, and automap overlay.
      * Controls mapped to physical synthesizer keys and knobs: F3/B3 or KNOB 1 to turn, A3/G3 forward/back, OCT−/OCT+ or F#3/G#3 to strafe, C5/PLAY to fire, D5/REC to open/use, E5 to run, C#5/D#5/F#5 weapon selection (fist, pistol, shotgun), ARP for automap, and FX for brightness.
      * Preserves sloopDX projects in flash without overwriting user patch data.
    * **Installation:** Browser WebMIDI installer via USB directly from the project page.

 2. **[FM-1 NES by Keitark](https://github.com/Keitark/fm1-nes) ([App Updates Guide](https://github.com/Keitark/fm1-nes/blob/main/APP_UPDATES.md)):**
    * **License:** Open Source (Apache-2.0).
    * **Status:** Experimental / Source only (reference proof-of-concept).
    * **Concept:** Nintendo Entertainment System (NES) emulator running on the FM-1 hardware.
    * **Features:** Uses the FM-1's 27 keys as the game controller and its color screen as the television display. Developed as a worked example and educational kit for writing bare-metal FM-1 firmware from scratch.
    * **Documentation:** [FM-1 NES APP_UPDATES.md Guide](https://github.com/Keitark/fm1-nes/blob/main/APP_UPDATES.md) — developer guide detailing application-only updates (`app.bin`) that preserve the stock USB bootloader.
    * **Installation:** Compile from source (no web installer or prebuilt release; does not produce audio/music).

 3. **[Mocky by Charles Vestal](https://github.com/charlesvestal/fm1-mocky) ([Web App](https://charlesvestal.github.io/fm1-mocky/)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Display testing firmware and web companion for transmitting and displaying arbitrary bitmap pictures on the FM-1's color screen over WebMIDI.
    * **Installation:** Browser WebMIDI installer via USB.

 4. **[fm1-mdx by Keitark](https://github.com/Keitark/fm1-mdx):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Experimental Sharp X68000 MDX/PDX karaoke music player running a software YM2151 FM chip emulation allowing interactive part muting and live keyboard accompaniment.
    * **Installation:** Research project / computer emulator testing.

 5. **[GameDude by Chance The Maker](https://github.com/ChanceTheMaker/gamedude-fm1-smk) ([Web Simulator & Compiler](https://chancethemaker.github.io/gamedude-fm1-smk/)):**
    * **License:** Open Source (GPL-3.0). Built on Peanut-GB and Felucca.
    * **Concept:** Nintendo Game Boy emulator, browser-based ROM-to-firmware compiler, and interactive web simulator for the M-VAVE FM-1 and SMK-37 controller hardware.
    * **Features:**
      * **Peanut-GB Core Port:** Optimized Game Boy emulator core running at smooth framerates on the JieLi AC791N RISC CPU.
      * **Web ROM Compiler & Simulator:** Drag-and-drop any Game Boy `.gb` ROM into the browser to test it immediately in the WebAssembly simulator and generate a flashable `.fwsc` firmware image in seconds.
      * **Ergonomic Synth-Key Layout:** Physical synth keys mapped intuitively to D-pad (Up/Down/Left/Right), A/B buttons, and Start/Select, with knob controls for volume, display brightness, and color palette cycling (classic DMG pea-soup green, pocket grayscale, neon cyberpunk).
      * **Dual Device Support:** Supports both the FM-1 synthesizer and SMK-37 keyboard controller hardware.
    * **Installation:** Browser WebMIDI installer via USB directly from the web compiler page.

 6. **[Fart Machine One by adamcharleswilsonmusic-code](https://github.com/adamcharleswilsonmusic-code/Fart-Machine-One):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Novelty joke sample-synthesizer and sequencer firmware for the FM-1.
    * **Features:** 11 distinct pitched flatulence sample sounds, integrated 16-step sequencer, dynamic pitch modulation, and onboard stereo delay and reverb effects.
    * **Installation:** Build and flash via CLI toolchain.

 7. **[Trumpagotchi by adamcharleswilsonmusic-code](https://github.com/adamcharleswilsonmusic-code/Trumpagotchi) ([Releases](https://github.com/adamcharleswilsonmusic-code/Trumpagotchi/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Virtual-pet Tamagotchi-style game and mini-instrument for the FM-1 featuring pixel-art animations.
    * **Features:** Four dedicated action keys allow feeding, praising, cleaning, and resting the pet. The white keys play a pentatonic musical instrument, and keeping the pet happy and well-rested unlocks accompanying bongo rhythm tracks.
    * **Installation:** Flashing prebuilt `v1.0.0` releases via WebMIDI or CLI updater.

 8. **[Trireme FM-1 by ignis32](https://github.com/ignis32/trireme_fm1) ([Releases](https://github.com/ignis32/trireme_fm1/releases)):**
    * **License:** Open Source (GPL-3.0).
    * **Concept:** Transforms the FM-1 into a fully programmable USB computer keyboard and macro pad with Vial GUI configuration support.
    * **Features:** Assign any standard keyboard key, multimedia shortcut, or mouse action to each capacitive key, button, and rotary encoder; five distinct layout layers, advanced macros, on-device configuration editor, and instant USB HID compatibility.
    * **Installation:** Flashing prebuilt `v0.1` releases via WebMIDI.

### 1.4. Stock Firmware Patchers & Binary Mods

 1. **[FM-1 Firmware Patcher by Christian Zietz (czietz)](https://github.com/czietz/fm1-firmware-patcher):**
    * **License:** Open Source (Unlicense / Public Domain).
    * **Target:** Stock official **V15** firmware (`FM-1.fwsc`).
    * **Modifications & Bug Fixes:**
      * Fixes the oscillator detune calculation in the stock synth engine to accurately match Dexed / Yamaha DX7 behavior.
      * Disables unhandled MIDI aftertouch messages that cause unwanted heavy vibrato.
      * Modifies the UI colorway: changes the main oscilloscope display to dark blue and the FX selection cursor to green (as visual confirmation of patched firmware).
    * **Usage:** Python patcher script applying precise binary offsets (`python patch_firmware.py FM-1.fwsc FM-1-fixed.fwsc`). Flashed via M-VAVE's M-UPGRADE utility.

 2. **[FM-1 Macropad Patch by smememe](https://github.com/smememe/fm1-macropad-patch) ([Web Patcher](https://smememe.github.io/fm1-macropad-patch/)):**
    * **License:** Open Source (MIT).
    * **Target:** Stock official **V15** firmware (`FM-1.fwsc`).
    * **Concept & Modifications:** Binary patch that transforms the FM-1 into a 55-input MIDI macro pad controller. Modifies the firmware so every physical button, piano key, and rotary knob sends a USB-MIDI note message while turning off all LEDs. Combined with desktop hotkey software, it converts the synthesizer into an external macro pad.
    * **Usage:** Apply patch directly in the browser via WebAssembly/WebMIDI or via Python script (`python3 fm1patch.py FM-1.fwsc`). Flashed via standard update tools.

> [!TIP]
> **Community Flashing Experience & Safe Upgrade Practice:**  
> While not an absolute hard rule, there is a prominent community recommendation to avoid flashing one custom firmware directly over another. To minimize bricking risks, developers recommend either rolling back to the official stock firmware (V15) via M-VAVE's official updater first, or using **[TransitFM1](https://quixotic7.github.io/TransitFM1/)** — a dedicated lightweight bridge firmware by Quixotic7 designed with crash-guarded boot stubs and stock V15 identity emulation to safely transition between custom builds.

---

## 2. Hardware Architecture & Reverse Engineering Reference

All technical deep dives, hardware reverse engineering findings, bootloader memory maps, and protocol specifications are documented in **[REVERSE_ENGINEERING.md](REVERSE_ENGINEERING.md)**:

* **Hardware & Ecosystem Overview:** JieLi AC791N SoC specs, devboard details, PCB characteristics, and teardown instructions.
* **Device Recovery Vectors:**
  * **Plain USB Unbricking:** Soft-brick recovery directly into `WL82 UBOOT1.00` mask-ROM mode via `jl-uboot-tool` and `MvaveFM1Unbricker` without opening the casing.
  * **Hardware `USB_KEY` Mask-ROM Recovery:** Forcing mask-ROM USB download mode on frozen/hard-bricked processors using an external RP2040 dongle ([FM-1 Transporter](https://github.com/kurogedelic/FM-1-transporter)) pulsing the JieLi hardware boot key (`0x16EF` at ~50 kHz) over USB D+/D- lines, with community wiring instructions for Seeed XIAO RP2040 / Raspberry Pi Pico (Green to D6, White to D7, Black to GND).
* **Firmware Container Analysis:** Embedded `.fwsc` firmware extraction from `M-UPGRADE-FM1` (Qt resource layout, `@JMUA` / `JLUFW` signatures).
* **MIDI SysEx OTA Protocol:** Handshake, parameter query behavior, and verified two-step device-pull session flow with 8→7 LSB-first bitstream encoding.
* **Memory Map & Bootloader:** Flash partitions (UBOOT, App, VM), linker script requirements, and critical bootloader re-entry guidelines.
* **Binary References & Offsets:** Magic numbers, Qt container offsets, and symbol references.
* **Firmware Size Boundaries:** SPI flash memory budget, execution model (XIP), and partition limits.
* **Python Firmware Utility:** CLI utility ([`fm1_flasher.py`](fm1_flasher.py)) for extracting firmware images and exploring protocol exchanges.
* **Disassembly & Tooling:** Ghidra processor module ([`ghidra-jieli`](https://github.com/kagaimiq/ghidra-jieli)) and official Pi32v2 toolchain notes.
* **Firmware Security & BadUSB Threat Modeling:** Theoretical risks of unsigned firmware execution (e.g. re-enumerating USB descriptors to standard HID keyboard to inject keystroke payloads) and host security mitigation considerations.

**Read the full documentation:** **[REVERSE_ENGINEERING.md](REVERSE_ENGINEERING.md)**

---

## 3. External References & Resources

Useful open-source tools, documentation, and SDK repositories:

### 3.1. Hardware Recovery, Bootloaders & Firmware Flashers

 1. **[jl-uboot-tool Repository](https://github.com/kagaimiq/jl-uboot-tool):**
    Utility for interacting with JieLi UBOOT bootloaders over USB Mass Storage / SCSI pass-through.

 2. **[Unbricking a Soft-Bricked FM-1 over Plain USB (Reddit Guide by acrawf1)](https://www.reddit.com/r/MVaveFM1/comments/1wz48t7/guide_unbricking_a_softbricked_fm1_black_screen/):**
    Detailed community guide for recovering devices stuck on a black screen in `WL82 UBOOT1.00` mode (`VID_4C4A:PID_8057`) via plain USB cable and `jl-uboot-tool` without extra hardware. Includes the [`fm1_extract_app.py` helper script](https://gist.github.com/Acrawf1/ae2b9930b49231db397568cfc2abc2a8).

 3. **[FM-1 Transporter by Leo Kuroshita (kurogedelic)](https://github.com/kurogedelic/FM-1-transporter) ([Hard Brick Recovery Guide](https://www.reddit.com/r/MVaveFM1/comments/1x5lifu/mvave_fm1_unbricking_after_a_hard_brick_using_a/)):**
    Hardware RP2040-based USB dongle firmware that pulses the JieLi `USB_KEY` pattern (`0x16EF`) to force unresponsive FM-1 devices into mask-ROM USB download mode for emergency flash recovery. See the practical community walkthrough for wiring a Seeed XIAO RP2040 or Raspberry Pi Pico (Green to D6, White to D7, Black to GND) and recovering via `jl-uboot-tool`: [Reddit: Unbricking after a hard brick using a RP2040 and the FM-1 Transporter](https://www.reddit.com/r/MVaveFM1/comments/1x5lifu/mvave_fm1_unbricking_after_a_hard_brick_using_a/).

 4. **[MvaveFM1Unbricker by Quixotic7](https://github.com/Quixotic7/MvaveFM1Unbricker) ([Troubleshooting Guide](https://github.com/Quixotic7/MvaveFM1Unbricker#troubleshooting)):**
    Python-based unbricking toolkit and comprehensive troubleshooting reference for M-VAVE FM-1 recovery. Automates safe backup and restoring via `jl-uboot-tool` (strictly protects the `< 0x4000` boot head, prevents `erasechip`, and verifies flash SHA-256), while providing procedures for forcing unresponsive units into ROM boot (watchdog timeouts, OCT-/OCT+ holds, quick power cycles) and RP2040 Transporter hardware recovery.

 5. **[flipper-fm1-recovery by merthsoft](https://github.com/merthsoft/flipper-fm1-recovery):**
    Firmware flasher and unbricker utility utilizing a **Flipper Zero** to pulse the hardware ROM recovery sequence on the FM-1's USB data pins without requiring an RP2040 dongle or wiring.

 6. **[fm-static by seajaysec](https://github.com/seajaysec/fm-static) ([Web App](https://seajaysec.github.io/fm-static/)):**
    WebMIDI flasher solving the issue where an FM-1's USB-MIDI port identifies under an unusual/renamed descriptor, which causes official updaters to report the synthesizer as missing.

 7. **[fm1-linux-update by fuleo](https://github.com/fuleo/fm1-linux-update):**
    Linux CLI updater tool for flashing and verifying stock V14 to V15 firmware binaries over USB-MIDI.

 8. **[JieLi USB Boot Key Activation (jielie docs)](https://kagaimiq.github.io/jielie/isp/usb/usb-key.html):**
    Documentation on triggering JieLi hardware USB boot loader mode via D+/D- signal patterns and ISP keys.

 9. **[ip2k/mvave-fm1-open-firmware Repository](https://github.com/ip2k/mvave-fm1-open-firmware):**
    Research project towards an open-source firmware for the M-VAVE FM-1. Includes specification, reference implementation, and simulation testbench for an **RP2040-based `USB_KEY` hardware recovery dongle** (`dongle/` directory) that forces the JieLi AC791N SoC into mask-ROM USB download mode (`UBOOT1.00`) via the external USB-C port, enabling low-level flash backup and unbricking.

10. **[Custom Bootloader & Full Flash Backup/Restore Flasher by mobiliakas1](https://www.reddit.com/r/MVaveFM1/comments/1x6xtz1/testers_for_custom_bootloader_needed/):**
    Under-development custom recovery bootloader and cross-platform flasher utility (Windows/macOS/Linux) for FM-1 and SMK-37. Enables full 1 MB SPI flash backup/restore over plain USB and provides standalone recovery without requiring external hardware dongles (RP2040/Transporter) if a bad firmware flash occurs.

11. **[The FM-1 Firmware Hub (Make Firmware, Not War)](https://thefirmwarehub.com/) ([List View](https://thefirmwarehub.com/?view=list)):**
    Web-based firmware manager and one-click WebMIDI installer created by Sven Trogus (zvenson). Allows previewing, installing, and switching between 50+ open-source community firmwares for the M-VAVE FM-1 directly from Chrome/Edge with automatic nightly updates from author repositories and instant rollback to official stock V15 firmware.

12. **[Slipway by Discodave-Glitch](https://github.com/Discodave-Glitch/slipway) ([Releases](https://github.com/Discodave-Glitch/slipway/releases) | [Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x8ec69/slipway_free_fm1_firmware_manager_with_a/)):**
    Windows desktop application that catalogues community FM-1 firmwares, validates downloaded packages against published cryptographic hashes, and installs them through Felucca's flasher engine with a stock-first upgrade safety rule and USB recovery guide.

13. **[FM-SWITCH by Drew Robinson (ocean)](https://github.com/ocean/FM-SWITCH):**
    Native iOS companion app that installs and swaps FM-1 firmwares directly from an iPhone/iPad over USB-C using CoreMIDI, featuring an offline catalogue of community firmwares saved locally on the device for on-the-go flashing without a laptop.

14. **[TransitFM1 by Quixotic7](https://github.com/Quixotic7/TransitFM1) ([Web Installer](https://quixotic7.github.io/TransitFM1/)):**
    * **License:** Open Source (GPL-3.0-only). Built upon Dinghy (zvenson), Felucca's platform as carried by SLOOP, and ChoralRoot FM-1's boot stub. Concept proposed by Melodee author Kerem Kilic.
    * **Concept & Role:** Lightweight intermediate "stopover" bridge firmware for the M-VAVE FM-1 designed to safely transition between different community custom firmwares.
    * **Features & Safety Mechanisms:**
      * **V15 Protocol Identity:** Answers the USB-MIDI update protocol disguised as official stock V15 so that third-party web updaters and installers accept it without version conflicts or compatibility rejections.
      * **Crash-Guarded Write Cycle:** Employs a commit-last write strategy where the first sector of the application area is programmed last, protecting the flash from being left in an unbootable state during an incomplete write.
      * **Power Interruption Recovery:** If a cable is unplugged or battery dies mid-flash, cycling power automatically enters update mode (signaled by 3 short key LED flashes and a black screen). Re-running the installer completes the flashing process without requiring emergency hardware recovery. Holding `OCT-` on power-on manually triggers update mode at any time.
      * **Built-in Safety Checks:** Blocks direct flashing over incompatible older firmwares (such as SLOOP or early Felucca betas) and disallows firmware packages that exceed the standard application partition size (such as Baud Girl, which requires returning to true stock V15 first).
      * **Direct Package Flashing:** Includes browser functionality to inspect the currently installed firmware or upload and flash any raw `.fwsc` package directly (including official stock `FM-1.fwsc`).

### 3.2. Reverse Engineering, Disassembly & Decompilation

 1. **[M-VAVE FM1 Hardware Architecture & Protocol Reference (Local)](REVERSE_ENGINEERING.md):**
    In-depth local technical reverse-engineering documentation: JieLi AC791N hardware overview, UBOOT memory map, Qt container analysis, verified two-step device-pull SysEx OTA protocol, and flasher implementation.

 2. **[AL-255/FM-1-RE Repository](https://github.com/AL-255/FM-1-RE):**
    Reverse-engineering repository for M-VAVE FM-1 firmware. It reveals that the stock FM-1 firmware itself utilizes a Dexed/msfa-derived 6-operator FM synthesis engine, and contains V13/V14 disassembly function maps, XIP flash offset analyses, as well as an experimental custom firmware build.

 3. **[ghidra-jieli Repository](https://github.com/kagaimiq/ghidra-jieli):**
    Ghidra processor extension for disassembling and decompiling JieLi `pi32`, `pi32v2`, and `q32s` CPU binaries.

 4. **[fm1-bootloader by jvitkauskas](https://github.com/jvitkauskas/fm1-bootloader):**
    Readable C source implementation of the stock FM-1 bootloader, reverse-engineered and reconstructed byte-identically from the hardware image.

 5. **[MVAVE-M-UPGRADE-decompiled by entitymar](https://github.com/entitymar/MVAVE-M-UPGRADE-decompiled):**
    Full decompilation and resource extraction of the official M-VAVE M-UPGRADE macOS and Windows updater applications.

 6. **[jl-misctools Repository](https://github.com/kagaimiq/jl-misctools):**
    Utilities for inspecting and converting JieLi firmware containers, key files, and UI resources.

 7. **[M-VAVE SMK-37 PRO Reverse Engineering Gist (by probonopd)](https://gist.github.com/probonopd/18b3ed65a69d0229eb630c47d7e316dc):**
    Research notes on unpacking `.fwsc` firmware files for the M-VAVE SMK-37 PRO (DX7 FM MIDI keyboard) and identifying the underlying JieLi AC791N platform structure using `jl-misctools`.

### 3.3. Vendor SDKs, Architecture & JieLi Community Research

 1. **[JieLi AC79 AIoT SDK (Gitee Repository)](https://gitee.com/Jieli-Tech/fw-AC79_AIoT_SDK):**
    Official C SDK codebase for AC79 series (WL82 / AC791N) microcontrollers, containing board support packages (BSP), linker scripts, and hardware register headers.

 2. **[JieLi AC79 Official Peripheral Documentation](https://doc.zh-jieli.com/AC79/zh-cn/release_v1.0.3/module_example/peripherals/sd.html):**
    Official documentation covering AC79xx series peripheral hardware modules (SD controller, GPIO, UART, SPI, I2S).

 3. **[JieLi SoC Forum Thread (esp8266.ru)](https://esp8266.ru/forum/threads/jl-soc.5500/):**
    Community research thread discussing JieLi SoCs, SDKs, toolchains, flash recovery, and hardware boot modes.

### 3.4. Emulators, Simulators & Virtual Instruments

 1. **[fm1-emulator by Simon Johansson](https://github.com/simonjohansson/fm1-emulator):**
    Rust-based desktop emulator for the M-VAVE FM-1. Executes firmware binaries (`.fwsc`, `.elf`, `.bin`) on desktop operating systems, emulating the JieLi dual-core CPU and peripheral state.

 2. **[m-wave-fm1-browser-emulator by shcherbakov7](https://github.com/shcherbakov7/m-wave-fm1-browser-emulator):**
    Rust/WebAssembly in-browser emulation of the AC791N SoC's two `pi32v2` cores and the FM-1's color display.

 3. **[SLOOP FM-1 Simulator by Chance Roth](https://github.com/chancethemaker/sloop-fm1-sim) ([Web Simulator](https://chancethemaker.github.io/sloop-fm1-sim)):**
    Self-contained in-browser interactive simulator of the SLOOP / Felucca firmware for the FM-1, allowing testing controls, sound engines, and workflow directly in the browser without physical hardware.

 4. **[FM-1 Mobile by hb3p8](https://github.com/hb3p8/fm1-mobile-emu) ([Web App & Mobile Emulator](https://hb3p8.github.io/fm1-mobile-emu/)):**
    * **Platform:** Mobile-first progressive web app (PWA) with full offline support (Add to Home Screen on iOS/Android).
    * **Concept:** Seven real FM-1 C firmware engines compiled to WebAssembly running inside an accurate hardware-simulated touch panel matching the physical FM-1 instrument layout.
    * **Switchable Firmwares:** On-the-fly switching between **X0X** 1.0.6 (acid/TR-style drums & 303), **Felucca** 1.6 (multi-engine synth & 64-step sequencer), **SLOOP** 2.6 (live groovebox), **FiMba-1** 0.6.1 (physical modeling kalimba), **Melodee** 1.4.0-rc.1 (CZ-1, FM6, Prophet-5 & microtonal), **AMB-1** 1.1 (generative ambient), and **MAKU** 0.1 (generative intermission soundscapes).
    * **Features & Architecture:**
      * **AudioWorklet Hardware Clock:** Accurate timing loop where rendering audio advances the device's clock, driving firmware audio interrupts and main loops exactly as on physical hardware.
      * **Display & Graphics:** Real-time 240 × 240 display output drawn via WebGL with optional retro xBR smoothing filter.
      * **Responsive Ergonomics:** Adaptive portrait and landscape touch layouts, multi-touch keys with glides, encoder drag controls, button latching ("Hold" mode for SEL combos), and computer keyboard shortcuts.
      * **Persistent Storage:** Browser local storage isolates and preserves patterns, projects, and custom loops separately across each firmware switch.


 5. **[Virtual-FM-1 by jbschooley](https://github.com/jbschooley/Virtual-FM-1):**
    Software replica of the M-VAVE FM-1: standalone FM synthesizer application and VST3/AU audio plugin featuring bidirectional preset and pattern synchronization with hardware over the Baud Girl (FM-1+VA) firmware.

 6. **[FM1VST by Quixotic7](https://github.com/Quixotic7/FM1VST):**
    DAW plugin host (VST3, AU, and standalone) running Felucca-family firmwares (ChoralRoot, Felucca, Melodee) compiled directly from source and switchable on the fly.

 7. **[fm1-emu by Joakim Eriksson](https://github.com/joakimeriksson/fm1-emu) ([Web Emulator](https://joakimeriksson.github.io/fm1-emu/)):**
    Full hardware emulator for the M-VAVE FM-1 running unmodified firmwares natively and directly in the browser via WebAssembly:
    * **Hardware & CPU Emulation:** Full WebAssembly virtual machine emulating the JieLi AC791N SoC (dual-core 32-bit `pi32v2` CPU), 240 × 240 display, tactile buttons, knobs, and audio synthesis.
    * **Firmware Loading:** Runs community firmwares (Felucca, X0X, FM1 Quest, AMB-1, FM-1 SID, ORBIT, FiMba-1, stock M-VAVE) downloaded on the fly, with support for uploading custom `.fwsc` update packages.
    * **Features:** Configurable emulated clock speed, Web MIDI input routing with channel selection, support for loading Yamaha DX7 32-voice `.syx` banks for stock firmware, and computer keyboard / touch panel controls. Also includes an experimental SMK-37 emulator.

 8. **[FM-1 Studio by thingsapart](https://github.com/thingsapart/fm1-studio):**
    * **License:** Open Source (GPL-3.0).
    * **Platform:** Native Android Application (Java / WebAssembly runtime).
    * **Concept:** Multi-firmware companion environment and touch synthesizer for Android smartphones and tablets.
    * **Features:**
      * Hosts real FM-1 C firmware engines (SLOOP, FM1 MOVE, Felucca, sloopDX) compiled to WebAssembly running directly on Android.
      * Full touch panel simulating the FM-1's 240 × 240 color display, keys, and rotary encoders.
      * Integrated touch piano roll, sound editors, preset management, and USB-MIDI integration to synchronize projects with physical FM-1 hardware.

 9. **[PIGEON WebAssembly Emulator](http://theshrimpblimp.com/webapp/emu/) ([Project Page](http://theshrimpblimp.com/pigeon)):**
    Complete in-browser WebAssembly hardware simulation of the PIGEON sampler firmware. Renders the 240 × 240 interface, loads custom samples, demonstrates transient slicing, sequencing, scratch decks, and audio playback directly in Chrome or Edge without physical hardware.

### 3.5. Web Editors, Patch Librarians & Companion Utilities

 1. **[FM-1 Online Editor & Firmware Directory](https://fm1-editor.com/) ([Firmware Catalog](https://fm1-editor.com/firmware/)):**
    Web-based configuration and patch editor / librarian for the M-VAVE FM1 synthesizer, along with a curated directory and status tracker for community firmwares.

 2. **[FM-1 Utility](https://fm1-utility.pages.dev/):**
    Lightweight, dependency-free WebMIDI parameter editor and diagnostic tool for the FM-1.

 3. **[FM-1 Workbench by thegiantsnail](https://github.com/thegiantsnail/fm1-workbench-public) ([Web App](https://fm1-workbench.web.app)):**
    Multi-platform utility suite (Web app, Android app, VST3/CLAP plugin, and Model Context Protocol MCP server) featuring a DX7 preset library, voice randomizer/mutator, drum sequencer, and MIDI file player.

 4. **[fm1-read-voice by Christian Zietz](https://github.com/czietz/fm1-read-voice):**
    Python utility to request and read the currently active sound patch back from the FM-1 hardware over USB-MIDI SysEx.

 5. **[OpenPatch.es (Yamaha DX7 Patch Utility)](https://openpatch.es/):**
    Web utility for DX7 FM patches allowing WAV upload to recover/match patches, live auditioning, sequencing, modifying, mutating, and exporting patch sets as `.syx` files.

 6. **[DXcompanion](https://dxcompanion.uk/):**
    Browser-based patch and parameter editor for the Yamaha DX synth family featuring experimental M-VAVE FM-1 support.

 7. **[Dexed by asb2m10](https://asb2m10.github.io/dexed/):**
    Open-source DX7 plugin and editor. The FM-1 hardware natively responds to Dexed real-time parameter-change SysEx messages for live DAW sound design.

 8. **[FM-1 Pulses by mene311](https://github.com/mene311/fm1-pulses) ([Web App](https://mene311.github.io/fm1-pulses/)):**
    Browser-based generative MIDI sequencer and pattern generator for the M-VAVE FM-1 (Web MIDI API / PWA, runs on desktop/mobile). Generates reproducible 64-step banks with parameter drift and can freeze them directly into the hardware pattern slots over SysEx (supported on Baud Girl / FM-1+VA firmware), or broadcast live MIDI notes in real time.

 9. **[sloop-fm1-go by jahlib](https://github.com/jahlib/sloop-fm1-go) ([Releases / APK](https://github.com/jahlib/sloop-fm1-go/releases)):**
    * **License:** Open Source (GPL-3.0).
    * Android-native touchscreen companion and project editor for SLOOP custom firmware (based on the SLOOP web editor). Allows editing tracks, synth parameters, samples, and sequence patterns directly from an Android smartphone or tablet over USB-MIDI.

10. **[SLOOP 8-Track Web Workstation by smhulme](https://github.com/smhulme/sloop-web-8trk):**
    Hybrid production environment driving SLOOP's four hardware tracks over WebMIDI while adding four synchronized browser audio tracks alongside them.

11. **[Choppa Lite by WaveLoop](https://waveloop.app/toys/choppa):**
    In-browser, installable sampler web application for the FM-1. Allows recording up to 12 seconds of audio, chopping it into 16 pads, and transferring the sample bank directly to the FM-1 over USB-MIDI. Built for Felucca and SLOOP firmware families (also available for iOS, with Android version planned).

12. **[take-taker by groundstation1](https://github.com/groundstation1/take-taker) ([Releases / APK](https://github.com/groundstation1/take-taker/releases)):**
    * **License:** Open Source (MIT).
    * Android multitrack audio & video recorder designed specifically for USB audio devices.
    * When paired with the **Melodee** firmware on FM-1 (which exposes all 4 audio outputs as discrete USB audio streams), it bypasses Android's default stereo downmixing via raw USB mode to record each channel as an independent track.
    * Exports individual lossless FLAC stems, normalized MP3 mixdowns, or synced video takes (using phone camera footage or rendered live scrolling waveform overlays).

13. **[FM-1 Patch Bank Utility (Soundspirate) by klonecom](https://github.com/klonecom/M-VAVE-FM1-LOADER---):**
    * Single-file, client-side browser Web MIDI tool for transmitting `.syx` patch bank files to the FM-1 with auto-detection and SysEx framing validation.

14. **[FM1 Bank Sender by Leo Maimoni](https://github.com/leomaimoni/fm1-bank-sender):**
    * Android utility app to transmit DX7 sound bank files (`.syx`, 32-voice banks or single patches) to the M-VAVE FM-1 via USB-OTG without entering special receive modes.

15. **[Felucca Editor Skill by hunterxiong2026](https://github.com/hunterxiong2026/fm1-felucca-editor-2026):**
    * **License:** Open Source (MIT).
    * Natural language LLM / Agent skill integration for controlling the M-VAVE FM-1 (running Felucca firmware) over MIDI SysEx for tone design, multi-track arranging, and song playback.

16. **[Oscuro Companion Protocol & File Bridge by kartun83](https://github.com/kartun83/oscuro-companion-protocol):**
    * **License:** Open Source (Apache-2.0).
    * **Concept:** High-speed phone ↔ hardware file bridge and companion communication service over USB (smartphone acts as USB host, device runs as USB peripheral).
    * **Architecture & Features:**
      * Native Android USB-Host app (Kotlin) paired with a lightweight RAM firmware payload (`usbfiles.c` + `usbven.c`) executed on the JieLi AC791N SoC.
      * Fast bidirectional file listing, patch browsing, sample transfer, and remote UI state synchronization on 240 × 240 displays without requiring flash wear.
      * Developed for M-VAVE SMK-37 (under the Oscuro project) and architecturally adaptable to the M-VAVE FM-1 given their shared AC791N SoC and USB stack. Includes desktop Python host mock (`pyusb`) and wire protocol documentation.

17. **[Relay FM-1 Editor, Firmware Database & Manager by Stanley Gurvich (EmeraldMoonLabs)](https://github.com/stanleygurvich/fm1-firmware-database) ([Web Feed](https://stanleygurvich.github.io/fm1-firmware-database/) | [Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x6gg0h/relay_fm1_editor_firmware_database_emulator/)):**
    * **Concept:** Comprehensive FM-1 editor, firmware database, emulator host, and automated release feed service.
    * **Automated Firmware Feed:** Runs a scheduled automated crawler tracking the [FM-1 Resource Hub](https://github.com/aroum/fm1-custom-fw) and upstream GitHub releases every 3 hours. Publishes a unified `feed.json` verifying firmware update packages (`.fwsc` SHA-256, `FELUCCA-LOADER-1` and `FM-1_` package markers, asset sizes, and web installer links) across 60+ projects.
    * **Felucca Web App & Deep Editor:** Includes companion [UplinkFeluccaEditor-WebApp](https://github.com/stanleygurvich/UplinkFeluccaEditor-WebApp) with Web MIDI SysEx parameter control, custom package verification, backup tools, and in-browser mock testing.

18. **[AMÉTRA-001 by Sopozcreations](https://ametra-liard.vercel.app/) ([Reddit Announcement](https://www.reddit.com/r/MVaveFM1/comments/1x89ias/am%C3%A9tra001_a_free_polymetric_sequencer_in_the/)):**
    * **Concept:** Free browser-based polymetric MIDI sequencer and groove generator designed for the M-VAVE FM-1 (and compatible with external MIDI gear and DAWs via Web MIDI).
    * **Features:**
      * **4 Polymetric Loop Lanes:** Four polyrhythmic lanes running completely independent step counts (e.g. 16 vs 7 steps vs triplets) that drift continuously out of phase and realign over time.
      * **Generative Chance & Mutation:** Per-track hit stutter, drift, and random dice-roll probability parameters.
      * **Audio & MIDI Integration:** Supports internal sample playback or live microphone recording alongside Web MIDI transmission, plus direct WAV audio capture and standard MIDI file export.
      * **User Interface:** Clean bilingual (English / French) responsive UI with built-in interactive help tooltips.

19. **[PIGEON Web Sample Tool & Studio](http://theshrimpblimp.com/webapp/pigeon/) ([Documentation](http://theshrimpblimp.com/pigeon)):**
    * In-browser sample preparation, slicing, and backup workstation for the PIGEON sampler firmware.
    * Allows importing custom audio files into Song 1 / Song 2 slots and a 16-pad drum kit, previewing waveforms, automatic transient slicing (up to 32 chops per song), trimming boundaries, offline MP3/ADPCM encoding, and transmitting complete 496 KiB soundbanks to the FM-1 hardware over Web MIDI. Also creates complete session archives and firmware backups before flashing.

### 3.6. Developer Frameworks, UI Designers & Curated Collections


 1. **[MvaveFM1-Designer by Quixotic7](https://github.com/Quixotic7/MvaveFM1-Designer):**
    Visual UI and panel state designer for FM-1 custom developers (mapping key/button LED states, knob functions, and OLED/TFT screen layouts).

 2. **[Schwung by Charles Vestal](https://github.com/charlesvestal/schwung):**
    Open-source music architecture framework for standalone devices. Core synthesis code and models (TR-909, TR-808, TB-303, PSX Verb) are shared with the X0X and Lunar Modulator FM-1 firmwares.

 3. **[awesome-fm-1 by cicloid](https://github.com/cicloid/awesome-fm-1):**
    A curated awesome-list of resources, custom firmwares, tools, and open-source projects for the M-VAVE FM-1 pocket synthesizer.

 4. **[altstrument: M-VAVE FM-1 Directory](https://altstrument.org/devices/m-vave-fm-1):**
    Open-source device registry and custom firmware catalog for the M-VAVE FM-1 tracking 90+ firmwares, companion tools, licenses, release histories, and brick-risk flags.

 5. **[Fluyt by rgrvmusic](https://www.reddit.com/r/LogueSDK/comments/1x3upww/fluyt_felucca_synth_engines_for_drumlogue/):**
    Community port and adaptation of the open-source **Felucca** synthesizer engines from the M-VAVE FM-1 to the **Korg drumlogue** (LogueSDK user synth unit), demonstrating cross-platform portability of Felucca DSP algorithms.

### 3.7. Custom Soundbanks & Preset Collections

Dedicated sound banks, commercial patches, and SysEx preset packs tailored for the M-VAVE FM-1:

 1. **[Ambient & Dreams by NatLife Sounds](https://natlifesounds.com/product/ambient-dreams-for-m-vave-fm-1-fm-synthesizers/):**
    * **Format & Compatibility:** Standard 32-preset SysEx bank (`.syx`) with FM-1 USB installation instructions (cross-compatible with Yamaha DX7/DX7 II, Korg Opsix 2.0, Korg Volca FM/FM2, Dexed, Arturia DX7 V, and NI FM8).
    * **Sound Design:** 32 tailored ambient FM presets designed to showcase soft, harmonic FM textures without harsh digital dissonance — includes 1 AAH vocal preset, 5 bass patches, 2 FX textures, 2 leads, 5 ambient pads, 10 plucks, and 8 melodic synth sounds. Includes video demo walkthroughs and tutorials.

---


## 4. Documentation, Protocols & Guides

Comprehensive technical references and community guides:

1. **[FM-1 SysEx Protocol & Provenance (by KingParamount)](https://github.com/KingParamount/fm1-factory-presets/blob/main/docs/protocol-and-provenance.md):**
   Technical documentation of the FM-1 handshake sequence, 7-bit payload packing, and bulk dump transfers.
2. **[FM-1 OTA Protocol & Architecture Docs (AL-255/FM-1-RE)](https://github.com/AL-255/FM-1-RE/blob/main/docs/io/11-ota-protocol.md):**
   In-depth specifications for the USB-MIDI packet framing, session handshakes, and XIP flash memory layouts.
3. **[FM-1 Easy Guide (by pingywon)](https://pingywon.github.io/fm1-easy-guide/) ([Source](https://github.com/pingywon/fm1-easy-guide)):**
   Beginner-friendly rewrite of the official manual with an interactive step-by-step browser walkthrough.
4. **[fm1-guide (by fuleo)](https://fuleo.github.io/fm1-guide/):**
   Practical operational notes covering sequencer workflows, the V15 reverb bugfix, and Linux flashing procedures.
5. **[FM-1 on Tao of Mac (by Rui Carmo)](https://taoofmac.com/space/com/m-vave/fm-1):**
   Architectural notes, teardown observations, and hackability insights.

---

## 5. Hardware Add-ons & DIY Enhancements

Community hardware companion projects and accessories:

1. **[FM-1 Bonus Box by pfkellogg](https://github.com/pfkellogg/fm1-bonus-box):**
   ESP32-S3 external companion module featuring a rotary preset browser with round color TFT, sustain pedal input, Wi-Fi bank manager, USB-MIDI host, and a sing-on-pitch voice trainer.
2. **[fm1-sustain-footswitch by pfkellogg](https://github.com/pfkellogg/fm1-sustain-footswitch):**
   Arduino-based adapter converting a standard 1/4" sustain pedal into MIDI CC64 over the FM-1's 3.5 mm TRS MIDI input (includes full schematics).
3. **[fm1-midi-voice-tuner by pfkellogg](https://github.com/pfkellogg/fm1-midi-voice-tuner):**
   Passive TRS MIDI splitter box with built-in microphone and OLED pitch display guiding singers on whether they match the FM-1's current note.
4. **[M-VAVE FM-1 3D CAD Model by Zande Creates](https://grabcad.com/library/m-vave-fm-1-1):**
   High-precision 3D CAD model of the M-VAVE FM-1 chassis (accurate within ~0.1 mm) designed for modeling custom 3D-printed faceplates, travel cases, desktop angled stands, and hardware attachments.

---

## 6. Articles, Reviews & Community Analyses

Articles and press coverage detailing community custom firmwares and feature overhauls:

* **[Synth Anatomy: Baud Girl FM-1+VA](https://synthanatomy.com/2026/09/baud-girl-fm-1-va-custom-m-vave-fm-1-firmware.html):** Detailed review of the first community firmware adding Virtual Analog synthesis and 64-step sequencing.
* **[Synth Anatomy: Felucca 1.0 Release](https://synthanatomy.com/2026/10/hugelton-instruments-felucca-custom-m-vave-fm-1-firmware-turns-it-into-a-multi-engine-synth.html):** Coverage of Hügelton Instruments' multi-engine open-source platform.
* **[Synth Anatomy: SLOOP Groovebox](https://synthanatomy.com/2026/10/3dsam-sloop-custom-firmware-turns-m-vave-fm-1-into-a-4-track-groovebox.html):** Feature breakdown of SLOOP 4-track groovebox with USB audio.
* **[Synth Anatomy: X0X Techno Firmware](https://synthanatomy.com/2026/10/charles-vestal-x0x-custom-firmware-turns-the-m-vave-fm-1-into-a-rebirth-like-groovebox.html):** Examination of Charles Vestal's ReBirth-inspired 303/808/909 firmware.
* **[Synth Anatomy: Groove OS](https://synthanatomy.com/2026/10/groove-os-turns-the-m-vave-fm-1-into-an-8-track-groovebox.html):** Coverage of the commercial 8-track groovebox firmware.
* **[Piano & Synth Magazine: Custom Firmware Collection](https://pianoandsynth.com/m-vave-fm-1-custom-firmware-collection/):** Side-by-side comparison matrix of major FM-1 custom firmwares.
* **[Sonicstate: Free Custom Firmware for M-VAVE FM-1](https://sonicstate.com/news/2026/09/29/free-custom-firmware-for-mvave-fm-1-/):** News coverage of third-party firmware development.

---

## 7. Community Hubs & Discussions

Where the M-VAVE FM-1 community discusses reverse engineering, troubleshooting, and new releases:

* **[M-VAVE Official Forum (Topic #4: FM1 Open Firmware Announcement)](https://forum.m-vave.com/topic/4):** The official manufacturer forum and announcement hub (announcement topic #4 was subsequently removed by manufacturer).
* **[Reddit: r/MVaveFM1](https://www.reddit.com/r/MVaveFM1/):** The primary community hub for custom firmware releases, unbricking help, and hardware hacks.
* **[KVR Audio: M-VAVE FM-1 Thread](https://www.kvraudio.com/forum/viewtopic.php?t=632127):** Technical thread where factory preset recovery and early tools were first shared.
* **[Hacker News: FM-1 Reverse-Engineering Discussion](https://news.ycombinator.com/item?id=49994065):** Discussion on the FM-1-RE architecture and JieLi SoC discoveries.
* **[Elektronauts: M-VAVE FM-1 Thread](https://www.elektronauts.com/t/m-vave-fm-1/252170):** Groovebox workflow discussions, firmware releases, and audio demos.
* **[Gearspace: M-VAVE FM-1 Owners Thread](https://gearspace.com/threads/m-vave-fm-1.1465371/):** Hardware impressions, comparison with Yamaha DX-series hardware, and tips.
