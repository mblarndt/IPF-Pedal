---
title: IPF-Pedal – Projektübersicht
---

# IPF-Pedal

Willkommen zur Dokumentation des IPF-Pedal-Projekts.  
Dieses Repository enthält eine Sammlung von Pure-Data-Patches, mit denen sich ein mehrteiliges Gitarren‑ bzw. Audio‑Effektpedal realisieren lässt – inklusive:

- Audioeingang und ‑ausgabe
- Effektsektion (Pitch & Delay)
- Synth-Sektion
- GUI-/Frontend-Steuerung
- Hilfs‑ und Utility-Patches

Die Patches sind so aufgebaut, dass sie gemeinsam ein komplettes Setup für Live‑Performance, Experimente mit Gitarren‑/Audioeffekten und Synth-Sounds bilden.

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
  Synthesizer‑Patches (z. B. `OnsetSamplerSynth.pd`, `voice.pd`, `voicemn.pd`) zur Klangerzeugung und ‑manipulation.

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

Aus den GUI‑Elementen in `Project/PedalGUI.pd` und `Project/PedalBackend.pd` ergeben sich folgende Kernkonzepte:

- **Sektionen**
  - **Audio Input**: Eingangssignale (z. B. Gitarre, Mikrofon) werden in das Patch geroutet.
  - **FX Section**: Effekte für Pitch und Delay – einzeln oder kombiniert schaltbar.
  - **Synth Section**: Synthesizer‑Einheit, die über Fußtaster oder MIDI aktiviert werden kann.

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
    - FX3: Kombination aus Pitch & Delay
  - Modi:
    - M1: PitchMode
    - M2: RepeatMode
    - M3: (Platz für weitere Modi/Erweiterungen)

- **Steuerparameter**
  - `knob1`–`knob6`: Drehregler, die u. a. an `guitarinput`, FX‑Parameter und Synth‑Sektionen angebunden sind.
  - `fs1s`, `fs2s`, `tglsw1`–`tglsw3`: Fußschalter‑ und Toggle‑Zustände, die Routing und Effekte beeinflussen.

## Einstieg: Projekt ausführen

Voraussetzungen:

- Installierte Pure‑Data‑Umgebung (z. B. Pd Vanilla, ggf. mit den benötigten Externals wie `else` o. Ä.).
- Audio‑Interface bzw. geeigneter Ein-/Ausgang für das gewünschte Setup (z. B. Gitarre, Line‑In, etc.).

### 1. Haupt-GUI starten

1. Repository klonen oder lokal verfügbar machen.
2. In Pure Data `Project/PedalGUI.pd` öffnen.
3. Sicherstellen, dass die im Patch referenzierten Unterpatches (`../utility/*`, `../project/pedalfrontend`, etc.) im Suchpfad von Pd liegen (standardmäßig genügt meist das Öffnen aus dem Projektverzeichnis).
4. DSP in Pd aktivieren.

Über das GUI können nun Audioeingang, Effekte, Synth und die Fußschaltersteuerung getestet werden.

### 2. Frontend/Backend getrennt verwenden (optional)

Für Debugging oder alternative Setups können auch `PedalFrontend.pd` und `PedalBackend.pd` separat geöffnet werden:

- **Frontend**: Fokus auf Steuerlogik, Eingabegeräte (Footswitches, Regler, MIDI).
- **Backend**: Fokus auf Signalfluss, FX‑Section, Synth‑Section und Audio‑Routing.

## Weiterentwicklung & Anpassung

Mögliche Erweiterungen:

- Weitere FX‑Module in `FX/` hinzufügen und in `PedalBackend.pd` einbinden.
- Zusätzliche Synth‑Engines in `Synth/` ergänzen.
- Mapping der Regler (`knob1`–`knob6`) und Taster anpassen, um eigene Performance‑Setups zu bauen.
- Anbindung an spezifische Hardware‑Controller oder Pedal‑Plattformen (z. B. über MIDI oder spezialisierte Externals).

## Lizenz & Quellen

Die Lizenzinformation befindet sich in `LICENSE`.  
Weitere Hinweise oder Aktualisierungen können in der `README.md` im Projektwurzelverzeichnis ergänzt werden.

