# IPF-Pedal

Ein experimentelles, IPF‑gesteuertes Gitarren‑ & Audio‑Pedal in plugdata.

IPF‑Pedal ist ein Set aus plugdata‑Patches, das auf der **Impulse Pattern Formulation (IPF)** basiert und als **kreative Spielwiese für experimentelle Effekte, Live‑Sampling und generative Melodien** dient.  
Statt nur „statischer“ FX bekommst du ein Pedal‑Rig, das aktiv auf dein Spiel reagiert – in Echtzeit.

### Features im Überblick

- **IPF‑modulierte Effekte**  
  Die Effektsektion (Pitch, Delay, Melodiner u. a.) wird direkt durch die IPF moduliert.  
  Die IPF erzeugt komplexe Muster, die Parameter wie Tonhöhenverschiebung, Delay‑Zeit, Feedback oder Mix dynamisch bewegen – von subtiler Bewegung bis hin zu komplett zerlegten, chaotischen Texturen.

- **Experimentelle FX‑Architektur**  
  Statt klassischer „Ein‑Knopf‑Pro‑Effekt“-Logik arbeitet IPF‑Pedal mit **Meta‑Parametern**, die ganze Effektketten modulieren können. Dadurch eignen sich die Patches besonders für **Sounddesign, Improvisation und Live‑Experimente**.

- **Live‑Sampler‑Synth mit IPF‑Melodien**  
  Ein zentraler Baustein ist der **Live‑Sampler‑Synth**:
  - erkennt **in Echtzeit** die von dir gespielten Noten,
  - baut daraus ein **Set spielbarer Noten** auf,
  - nutzt dieses Set, um einen **Synthesizer** aufzubauen, der wiederum **Melodien spielt, die durch die IPF generiert werden**.  
  Dein Spiel liefert also das Rohmaterial, die IPF baut daraus neue rhythmische und melodische Strukturen.

- **Dynamische Tempo‑Anpassung an dein Spiel**  
  Ein **modifizierter IPF‑Algorithmus analysiert dein Timing** und passt das Tempo des Synthesizers dynamisch an dein tatsächliches Spieltempo an.  
  So bleibt das System musikalisch „im Groove“, selbst wenn du Tempo und Feel ständig variierst.

- **Pedal‑optimiertes GUI mit Fußschaltern & 6 Makro‑Reglern**  
  Das GUI bildet ein klassisches Pedal‑Layout nach – mit Fußschaltern, Moditasten und **sechs Makro‑Reglern** für Performance‑Spielereien (inkl. Chaos, Tempo, Notes).

- **Modulare Struktur für eigene Experimente**  
  FX‑Module, Utility‑Patches und Synth‑Sektionen sind sauber getrennt aufgebaut, sodass du problemlos eigene Algorithmen und IPF‑Anwendungen integrieren kannst.

### Kompatibilität

- **Empfohlene Umgebung: plugdata**  
  IPF‑Pedal ist primär für **plugdata** entwickelt und getestet (inkl. Externals wie `else`, `cyclone`, `CEAMMC` etc.).
- **Pure Data (Pd)**  
  Viele Teile lassen sich auch in Pd Vanilla nutzen, **die volle Funktionalität ist dort aktuell aber nicht gewährleistet**.  
  Für das komplette Erlebnis (inkl. GUI‑Details und Externals) wird **plugdata dringend empfohlen**.

## Projektstruktur

Die wichtigsten Ordner im Repository sind:

- `Project/`  
  Enthält die Haupt‑Projektpatches:
  - `PedalGUI.pd`: grafische Oberfläche und zentrales Steuerpatch
  - `PedalFrontend.pd`: Frontend‑Logik, Anbindung von Schaltern, Reglern und Fußtastern
  - `PedalBackend.pd`: Audio‑Routing, FX‑ und Synth‑Sektionen (u. a. „Audio Input“, „FX Section“, „Synth Section“)

- `FX/`  
  Effektpatches wie z. B.:
  - `ipitchf-vanilla.pd` (Pitch‑Effekt)
  - `ipfilterdelay-vanilla.pd` (Delay‑/Filter‑Effekt)
  - `melodiner.pd` (melodische Pitch‑Bearbeitung)

- `Synth/`  
  Sampler-Synthesizer‑Patches (z. B. `OnsetSamplerSynth.pd`, `voice.pd`, `voicemn.pd`) zur Klangerzeugung und ‑manipulation.

- `Utility/`  
  Hilfs‑ und Infrastrukturpatches, z. B.:
  - Audio‑/Gitarreneingang (`audioinput.pd`, `guitarinput.pd`, `AudioControl.pd`)
  - MIDI‑ und Quantisierungs‑Tools (`midiquantizer.pd`, `miditonote.pd`)
  - Sampler und Sample‑Player (`SamplePlayer.pd`, `sampler.pd`, `ipfbeatmaker.pd`)
  - Steuer‑ und Mapping‑Utilities (`ipfcontrol.pd`, `gaincontrol.pd`, `ValueMapper.pd`, `smooth.pd`, `checkscale.pd`, `checkthr.pd`)
  - DSP‑Management (`dsp.pd`)

- `Externals/`  
  Externe/zusätzliche Objekte und deren Hilfepatches (z. B. `momentary2toggle-help.pd`, `ipf~-help.pd`, `ipf-help.pd`), die vom Projekt verwendet werden.

## Zentrale Bedienkonzepte
<img width="222" height="370" alt="IPFPedalGUI" src="https://github.com/user-attachments/assets/d8c7d423-d691-44a2-91f3-fa2edf415a96" />

Aus den GUI‑Elementen in `Project/PedalGUI.pd` und `Project/PedalBackend.pd` ergeben sich folgende Kernkonzepte:

- **Sektionen**
  - **Audio Input**: Eingangssignale (z. B. Gitarre, Mikrofon) werden in das Patch geroutet.
  - **FX Section**: Effekte für Pitch und Delay – einzeln oder kombiniert schaltbar.
  - **Synth Section**: Sample-Synthesizer‑Einheit, die über Fußtaster oder MIDI aktiviert werden kann.

- **Fußschalter & Regler** (Beispiele aus der GUI-Beschriftung)
  - Fußschalter:
    - Linker Fußtaster: Umschalten/Toggeln der FX‑Sektion
    - Rechter Fußtaster: Aufnahme von Audio (Long Press) / Aktivierung des Synth (Short Press)
  - Buttons:
    - B1: 4/4‑Takt
    - B2: 8/8‑Takt
    - B3: 6/8‑Takt
  - FX‑Zuweisung:
    - FX1: Pitch
    - FX2: Delay
    - FX3: Melodiner
  - Modi:
    - M1: PitchMode
    - M2: RepeatMode
    - M3: (Platz für weitere Modi/Erweiterungen)

- **Steuerparameter**
  - `knob1`–`knob6`: Drehregler, die u. a. an `guitarinput`, FX‑Parameter und Synth‑Sektionen angebunden sind.  
    Besonders wichtig sind dabei:
    - **Chaos**: Steuert, **wie extrem** die IPF die Effektparameter moduliert – von subtiler Bewegung bis zur kompletten Zerstörung des Signals.
    - **Tempo**: Bestimmt das **Tempo der IPF‑Modulationen** und beeinflusst damit sowohl die FX‑Rhythmen als auch das Timing des Synth‑Sequencings.
    - **Notes**: Kontrolliert, **wie hoch der Threshold für zu spielende Noten** liegt – also ab wann eine gespielte Note in das Notenset des Live‑Sampler‑Synths übernommen wird.
  - `fs1s`, `fs2s`, `tglsw1`–`tglsw3`: Fußschalter‑ und Toggle‑Zustände, die Routing und Effekte beeinflussen.

### Live‑Sampler‑Synth & IPF‑Tempo‑Tracking

Der Live‑Sampler‑Synth ist das Herzstück der „intelligenten“ Klangerzeugung:

- **Notenerkennung in Echtzeit**: Gespielte Noten werden analysiert und in ein internes Notenset übernommen (abhängig vom `Notes`‑Threshold).
- **Aufbau eines spielbaren Synth‑Sets**: Aus diesen Noten wird ein **dynamischer Synthesizer** gebaut, der mit deinen eigenen Tönen arbeitet.
- **IPF‑generierte Melodien**: Die IPF nutzt dieses Set, um **rhythmisch und melodisch strukturierte Patterns** zu erzeugen, die zwischen harmonischer Ergänzung und kontrolliertem Chaos pendeln können.
- **Dynamische Tempo‑Anpassung**: Ein modifizierter IPF‑Algorithmus passt das Tempo des Synthesizers an dein eigenes Spieltempo an – das System „atmet“ mit dir, statt dich in ein starres Grid zu zwingen.

## Einstieg: Projekt ausführen

Voraussetzungen:
- Installierte **plugdata‑Umgebung** (mit den benötigten Externals `else`, `cyclone`, `CEAMMC` etc.).
- Audio‑Interface bzw. geeigneter Ein-/Ausgang für das gewünschte Setup (z. B. Gitarre, Line‑In, etc.).

1. Repository klonen.
2. Füge `/Externals` in den Einstellungen den Paths hinzu.
3. `Project/PedalBackend.pd` öffnen.
4. `Project/PedalGUI.pd` öffnen.
5. DSP in Pd aktivieren.

Über das GUI können nun Audioeingang, **IPF‑modulierte Effekte**, der **Live‑Sampler‑Synth** sowie Fußschalter‑ und Reglersteuerung getestet werden.


## Weiterentwicklung & Anpassung

Mögliche Erweiterungen:

- Weitere FX‑Module in `FX/` hinzufügen und in `PedalBackend.pd` einbinden.
- Zusätzliche Synth‑Engines in `Synth/` ergänzen.
- Mapping der Regler (`knob1`–`knob6`) und Taster anpassen, um eigene Performance‑Setups zu bauen.
- Anbindung an spezifische Hardware‑Controller oder Pedal‑Plattformen (z. B. über MIDI oder spezialisierte Externals).

## Lizenz & Quellen

Die Lizenzinformation befindet sich in `LICENSE`.  
Weitere Hinweise oder Aktualisierungen können in der `README.md` im Projektwurzelverzeichnis ergänzt werden.

