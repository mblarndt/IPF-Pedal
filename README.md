# IPF-Pedal

An experimental, IPF-driven guitar & audio pedal in plugdata.
IPF-Pedal is a set of plugdata patches based on **Impulse Pattern Formulation (IPF)** and serves as a **creative playground for experimental effects, live sampling and generative melodies**.  

Instead of just “static” FX, you get a pedal rig that actively responds to your playing – in real time.

## Getting started: Run the project
Requirements:

- Installed **plugdata environment** (with required externals `else`, `cyclone`, `list-abs`).

- Audio interface or suitable input/output for the desired setup (e.g. guitar, line-in, etc.).

1. Clone the repository.

2. Add `/Externals` to the paths in the settings.

3. Open `Project/PedalGUI.pd`.

4. Enable DSP.

## Compatibility

- **Recommended environment: plugdata**  

  IPF-Pedal is primarily developed and tested for **plugdata** (including externals like `else`, `cyclone`).

- **Pure Data (Pd)**  

  Many parts can also be used in Pd Vanilla, **but full functionality is currently not guaranteed**.  

  For the complete experience (including GUI details and externals), **plugdata is strongly recommended**.

## Features
The whole pedal backend (`Project/PedalBackend.pd`) is structured in 3 modular parts which will also work individually.

- **FX-Section**   
   `FX/fx-section.pd`
  
  The effects section consists of 2 effects.
   1. IPF-modulated Pitch-Shifter. `FX/ipitchf.pd`  
   2. IPF-modulated Filter-Delay. `FX/ipfilterdelay.pd`   

  The IPF generates complex patterns that dynamically move the parameters – ranging from subtle movement to completely broken, chaotic textures.


- **Live sampler**  
  `Synth/fx-section.pd`
  
  A central component is the **live sampler synth**:

  - detects the notes you play **in real time**,

  - builds a **set of playable notes**,

  - uses this set to construct a **synthesizer**.

- **IPF-Sequencer**   
   `Synth/sequencer-section.pd`
  
  - Generates continiously **melodies and rhythms** controlled by the IPF
    
  - Outputs it as **MIDI data**
 
  - which will be used as input for the **live sampler** 

  Your playing provides the raw material, the IPF builds new rhythmic and melodic structures from it.

- **Extra: Dynamic tempo adaptation to your playing**  

  A **modified IPF algorithm analyzes your timing** and dynamically adapts the tempo of the synthesizer to your actual playing speed.  `Externals/ipf_taptempo`

  This keeps the system musically “in the groove”, even if you constantly vary tempo and feel.


## Core interaction concepts
<img width="266" height="442" alt="Bildschirmfoto 2026-04-25 um 17 46 07" src="https://github.com/user-attachments/assets/bee68a1f-7ec2-4808-b04e-b75560920cb2" />

- **Footswitches**
    - Left footswitch: toggle FX section
    - Middle footswitch: toggle Synth (long press: freeze groove)
    - Right footswitch: toggle Synth Input Freeze (long press: delete memory)
      
- **Toggleswitches** 
  - FX assignment:
    - FX1: PitchShift
    - FX2: FilterDelay
   
  - Synth Playback:
    - B1: Full Sample
    - B2: Soft Mode (ADSR with long Attack applied)
    - B3: Inverse Mode (ADSR will act inversed to your playing)

  - Modes:
    - M1: PitchMode (Existing Notes will be pitched to desired note)
    - M2: ClosestNote (Only existing notes will be played)
    - M3: (space for further modes/extensions)

- **Knob Controls**
    - Gain In: controls **how extreme** the IPF modulates effect parameters – from subtle movement to complete signal destruction.
    - Chaos:
    - FX-Tempo: determines the **tempo of IPF modulations** and influences both FX rhythms and synth sequencing timing.
    - FX D/W:
    - Notes: controls **how high the threshold for playable notes** is – i.e. when a played note is included in the live sampler synth’s note set.
    - Synth:


## Further development & customization

Possible extensions:

- Add additional FX modules in `FX/` and integrate them into `PedalBackend.pd`.

- Improve Onset Detection and sampling.

- Integration with specific hardware controllers or pedal platforms (e.g. via MIDI or specialized externals).

## License & sources

License information can be found in `LICENSE`.

[1] Linke, S., Bader, R., Mores, R. (2019). The impulse pattern formulation (IPF) as a model of musical instruments—Investigation of stability and limits. In: Chaos: An Interdisciplinary Journal of Nonlinear Science 29(10) https://doi.org/10.1063/1.5092511
