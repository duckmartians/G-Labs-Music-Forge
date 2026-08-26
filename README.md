# G-Labs Music Forge

**English** | [Tiếng Việt](README.vi.md)

Desktop app that takes a song (MP3, WAV, M4A, FLAC… or MIDI) and forges it into raw material for composing — **instrumental & stems, melody MIDI, chords/key/tempo, and playable sheet music** — entirely on your machine. Built for the AI-music workflow: keep the track you love, drop the lyrics you don't, and get the musical DNA to write with.

![Main window](docs/screenshots/01-main.png)

## Features

- **Stem split (Demucs)**: vocals / drums / bass / other — and a true **instrumental** made by subtracting vocals from the original, so the backing track keeps full quality
- **Melody → MIDI** (basic-pitch): transcribes the sung melody into a monophonic lead line; a **vocal-energy gate** stops separation bleed from engraving phantom notes in bars where nobody sings
- **Sheet melody source, your pick**: Auto · Vocals · Instrumental · Full mix — plus a **note-detail** dial (Clean / Balanced / Detailed) that trades ornaments for readability
- **Chords, key & tempo**: beat-synced chord progression with a play-along view — the instrumental runs underneath, the **sounding chord lights up**, click any chord to jump there
- **Sheet music that plays**: MusicXML engraved in-app; press play and a piano performs **exactly the engraved notes** while the sounding note lights up and the page follows — with **playback speed** (0.5–1.5×, pitch preserved) and zoom (50–160%)
- **Queue like a downloader**: add many files at once (multi-select, drag & drop), then Start / Pause (soft — the running track finishes) / Stop (cancels it); per-track progress on the app icon's own slider
- **Re-run with today's options**: tick more extractions, press ↻ on any finished track — or sweep-select rows (rubber-band drag, Shift adds, Alt removes) and re-run the whole selection
- **Everything on disk**: per-track results folder with instrumental/stems MP3, `melody.mid`, quantized `sheet.mid`, `sheet.musicxml`, `chords.json` and a piano preview MP3 — drag straight into your DAW
- **Local & private**: analysis runs offline on your machine (Apple Silicon GPU accelerated); nothing is uploaded anywhere
- **App auto-update**: checks GitHub Releases, downloads and installs in-app
- **6 languages**: English, Tiếng Việt, 简体中文, Español, العربية (RTL), Русский

## Screenshots

| Listen — stems with per-stem download | Chords — play along, active chord lit |
|---|---|
| ![Listen](docs/screenshots/02-listen.png) | ![Chords](docs/screenshots/03-chords.png) |

| Sheet music — plays itself, speed & zoom | Queue running |
|---|---|
| ![Sheet](docs/screenshots/04-sheet.png) | ![Queue](docs/screenshots/05-queue-running.png) |

| RTL (العربية) |
|---|
| ![RTL](docs/screenshots/06-rtl-arabic.png) |

## How it works

```
song.mp3 ──► decode ──► chords/key/tempo (chroma + Viterbi)
                 │
                 ├──► Demucs stem split ──► instrumental = original − vocals
                 │
                 └──► basic-pitch (ONNX) ──► melody.mid ──► quantize ──► sheet.musicxml
                                                     └──► piano preview (renders the QUANTIZED
                                                          score, so what you hear is what's engraved)
```

The transcription is a sketch by design — expect a draft to refine in your editor of choice, not a finished score. Rap sections transcribe dense by nature; the **Clean** detail level is your friend there.

## Install

Grab the latest from [Releases](https://github.com/duckmartians/G-Labs-Music-Forge/releases):

- **Windows**: `GLabsMusicForge-<version>-setup.exe`
- **macOS (Apple Silicon)**: `GLabsMusicForge-<version>-arm64.dmg` — unsigned; first open: right-click → Open, or `xattr -dr com.apple.quarantine "/Applications/G-Labs Music Forge.app"`

Settings live in the OS per-user data folder (`%APPDATA%\G-Labs Music Forge` on Windows, `~/Library/Application Support/G-Labs Music Forge` on macOS). Results default to `Documents/G-Labs Music Forge`.

## Development

```bash
npm run install:all          # root + frontend + backend
# Python engine (one-time): see docs/ENGINE-BUILD.md
npm run dev                  # backend :3002 + Vite :5179 — open http://localhost:5179
npm run dev:app              # the same, inside the real Electron window
npm test
```

Build: `./build_mac_arm64.sh` (macOS DMG) · `build-exe.bat` on Windows (NSIS + zip). The Python engine ships as a PyInstaller onedir under `bin/engine/` — instructions in [docs/ENGINE-BUILD.md](docs/ENGINE-BUILD.md).
