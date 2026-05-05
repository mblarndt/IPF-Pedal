# IPF-Pedal

An experimental, IPF-driven guitar and audio pedal built in **plugdata**.

IPF-Pedal is a collection of plugdata patches based on **Impulse Pattern Formulation (IPF)**. It serves as a creative playground for experimental effects, live sampling, and generative melodies. Instead of static effects, you get a pedal rig that actively responds to your playing in real time.

---

## Getting Started

### Requirements
- **plugdata environment**: Installed with required externals (`else`, `cyclone`, `list-abs`).
- **Audio Interface**: Or a suitable I/O setup for your instrument (e.g., guitar, line-in).

### Installation & Setup
1. **Clone** the repository to your local machine.
2. **Add** the `/Externals` folder to your paths in the plugdata settings.
3. **Open** `Project/PedalGUI.pd`.
4. **Enable DSP** to start processing audio.

---

## Compatibility

* **Recommended: plugdata** IPF-Pedal is primarily developed and tested for plugdata (utilizing specific GUI elements and externals like `else` and `cyclone`).
* **Pure Data (Pd)** While many components may function in Pd Vanilla, **full functionality is currently not guaranteed**. For the intended experience, plugdata is strongly recommended.

---

## Features

The pedal backend (`Project/PedalBackend.pd`) is structured into three modular sections that can also function independently:

### 1. FX Section
*Path: `FX/fx-section.pd`*

The effects section consists of two primary modules:
1.  **IPF-modulated Pitch-Shifter** (`FX/ipitchf.pd`)
2.  **IPF-modulated Filter-Delay** (`FX/ipfilterdelay.pd`)

The IPF generates complex patterns that dynamically modulate parameters, ranging from subtle movement to completely chaotic, broken textures.

### 2. Live Sampler
*Path: `Synth/fx-section.pd`* (Note: check if path is correct vs. Backend)

A central component that transforms your input into a playable instrument:
* **Real-time detection:** Analyzes the notes you play as you play them.
* **Dynamic Library:** Automatically builds a set of playable notes.
* **Synthesizer Engine:** Uses the captured samples to construct a unique, evolving synthesizer.

### 3. IPF Sequencer
*Path: `Synth/sequencer-section.pd`*

* **Generative Performance:** Continuously generates melodies and rhythms controlled by the IPF.
* **MIDI Workflow:** Outputs MIDI data used as input for the Live Sampler.
* **Reactive Composition:** Your playing provides the raw material, while the IPF constructs new rhythmic and melodic structures from it.

### Extra: Dynamic Tempo Adaptation
*Path: `Externals/ipf_taptempo`*

A modified IPF algorithm analyzes your timing and dynamically adapts the synthesizer's tempo to your actual playing speed. This keeps the generative system "in the groove," even if you vary your tempo or feel.

---

## Core Interaction Concepts

<img width="266" alt="Pedal GUI Interface" src="https://github.com/user-attachments/assets/bee68a1f-7ec2-4808-b04e-b75560920cb2" />

### Hardware Mapping

| Control | Function | Long Press Action |
| :--- | :--- | :--- |
| **Left Footswitch** | Toggle FX Section | - |
| **Middle Footswitch** | Toggle Synth | Freeze Groove |
| **Right Footswitch** | Toggle Synth Input Freeze | Delete Memory |

### Toggle Switches

* **FX Assignment:**
    * **FX1:** PitchShift
    * **FX2:** FilterDelay
* **Synth Playback:**
    * **B1 (Full Sample):** Standard playback.
    * **B2 (Soft Mode):** ADSR with a long attack applied.
    * **B3 (Inverse Mode):** ADSR acts inversely to your playing dynamics.
* **Modes:**
    * **M1 (PitchMode):** Existing samples are pitched to the desired target note.
    * **M2 (ClosestNote):** Only existing (recorded) notes are played.
    * **M3:** Reserved for future extensions.

### Knob Controls

* **Gain:** Controls Input Gain.
* **Chaos:** Determines the intensity of IPF modulation—from subtle shifts to complete signal destruction.
* **FX-Speed:** Sets the tempo/rate of the IPF modulations.
* **FX D/W:** Dry/Wet mix.
* **Notes:** Adjusts the threshold for capturing playable notes.
* **Synth:** Controls the volume of the Live Sampler Synth.

---

## Future Development

* [ ] Add additional FX modules in `FX/` and integrate them into `PedalBackend.pd`.
* [ ] Improve Onset Detection for more precise sampling.
* [ ] Integrate with hardware controllers (e.g., MIDI mapping or specialized externals).

---

## License & Sources

License information is available in the `LICENSE` file.

**Reference:**
[1] Linke, S., Bader, R., Mores, R. (2019). *The impulse pattern formulation (IPF) as a model of musical instruments—Investigation of stability and limits.* In: Chaos: An Interdisciplinary Journal of Nonlinear Science 29(10). [https://doi.org/10.1063/1.5092511](https://doi.org/10.1063/1.5092511)
