# aud_dsp_stretch

[English](README.md) | Deutsch

[![CI](https://github.com/audaudio/aud_dsp_stretch/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/audaudio/aud_dsp_stretch/actions/workflows/quick_check.yaml)

Time-Stretch- und Pitch-Shift-Node der Audanika Audio Engine auf Signalsmith Stretch.

Teil der Audanika Audio Engine; geplant in [aud_audio_pm](https://github.com/audaudio/aud_audio_pm).

## Motivation

Das Repo gibt es vor seinem Code: Der Paketgraph der Audanika Audio Engine
ist von Anfang an vollständig, damit jedes Paket vom ersten Tag an seinen
Platz, seine Pipeline und seine Version hat. Das Paket ist Schritt
S30 des [Plans der Engine](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/tickets/2026-10-07-17-audanika-audio-engine.md) und wird enthalten:

- ein Time-Stretch- und Pitch-Shift-Node auf Signalsmith Stretch (MIT)
- ein stufenloses Verhältnis und eine Verschiebung in Halbtönen, phasenkohärente Instanzen über eine gemeinsame Blockkonfiguration
- Latenzmeldung, Golden-Renderings gegen einen Pitch-Tracker

Bis dahin trägt es die `package_ffi`-Vorlage, die
[Ticket 41](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/tickets/2026-10-25-41-retire-the-template-api-of-the-stub-packages.md) ausmustert.

## Installation

Das Paket ist nicht auf pub.dev veröffentlicht; eine App löst es über
seine Git-Tags auf:

```yaml
dependencies:
  aud_dsp_stretch:
    git:
      url: git@github.com:audaudio/aud_dsp_stretch.git
      tag_pattern: "{{version}}"
    version: ^0.0.3
```

## Nutzung

Heute exportiert das Paket nur `sum` und `sumAsync` der
`package_ffi`-Vorlage über seine generierten Bindings, die die Tests und
`example/` aufrufen:

```dart
import 'package:aud_dsp_stretch/aud_dsp_stretch.dart';

Future<void> main() async {
  print(sum(1, 2));
  print(await sumAsync(3, 4));
}
```

Es gibt aus:

```text
3
7
```

## Einschränkungen

- Noch kein DSP-Code: Nichts von den geplanten Nodes ist umgesetzt
- Die Vorlagen-API `sum` und `sumAsync` entfällt mit Ticket 41 und ist
  keine Grundlage für eigenen Code

## Dokumentation

- [Der Plan der Audanika Audio Engine](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/tickets/2026-10-07-17-audanika-audio-engine.md),
  Schritt S30
- [Die Architektur der Engine](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/architecture/architecture.md)
  mit dem Paketgraphen und den Plattformen
- [dsp-001](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/concepts/decisions/dsp-001.md):
  DSP-Pakete übernehmen nur Code mit klarer Herkunft
- [Ticket 41](https://github.com/audaudio/aud_audio_pm/blob/main/doc/2026-Q4/tickets/2026-10-25-41-retire-the-template-api-of-the-stub-packages.md):
  die Vorlagen-API der Stub-Pakete ausmustern
- Die Guides in [`doc/guides`](doc/guides)

## Status

Geplant: Schritt S30 des Plans der Engine, noch kein Code. Die
Plattformen des Paketgraphen sind iOS, Android, macOS, Windows, Linux und
das Web. Vor 1.0 — die API kann sich zwischen Minor-Versionen ändern.

## Mitwirken

Gearbeitet wird Ticket für Ticket mit dem `gg`-Workflow; siehe den
[Develop Guide](doc/guides/develop-guide.md) und den
[Review Guide](doc/guides/for-ai/ai-review-guide.md).

## Lizenz

MIT — siehe [LICENSE](LICENSE).
