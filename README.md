# Riyaz — Phrase Looper

A browser-based practice tool for Indian classical music.  
Open an audio file (teacher recording, raga phrase, exercise), mark named sections on the waveform, and loop them — individually or in sequence — while you practice along on harmonium or voice.

Developed by Muneer Ahmed Shaik.

---

## Features

### Sessions
- Sessions are stored as plain JSON files in the `sessions/` folder alongside the app.
- On first load, click **Grant access to riyaz-phrase-looper** once to let the browser read the folder. The permission is remembered across page loads (Chrome only).
- Click any session card to instantly load the associated audio and all its sections — no extra steps.
- If the audio file has moved or been renamed, the app shows an error with a **Locate audio file…** button that updates the session JSON for next time.

### Waveform & Sections
- A full-track waveform is shown at the top for orientation and seeking.
- Click **+ Add Section** to create a new section card. Each card shows a mini waveform of the entire track.
- **Draw a selection** by clicking and dragging anywhere on the mini waveform.
- **Resize** by dragging the left or right edge handle (cursor changes to `↔` near edges). A **magnifier tooltip** appears above the cursor showing a 5× zoomed strip of the waveform around the edge, with a live time label — making it easy to nail the exact cut point.
- **Move** the whole selection by dragging anywhere inside it (cursor changes to `✋`).
- During any drag the selection overlay becomes transparent so the waveform underneath stays readable.
- Sections are colour-coded and the selection is always visible on the waveform.

### Playback
- **Main transport** (top bar) — plays the entire track; click anywhere on the top waveform to seek.
- **Each section** has two play buttons plus a stop:
  - `▶|` **Play from main playhead** — same as the top Play button, reachable from the section row. Useful for auditioning the track to decide what range to drag-select.
  - `▶` **Play selected range** — plays the section's `[start, end]` range. If no range has been drawn yet, it previews the full track so you can hear what's there before dragging.
  - `II` **Pause** — replaces the active play button while it's playing; freezes the playhead at the current position. Pressing again resumes (button shows `▶` with a coloured border).
  - `■` **Stop** — appears once range playback starts or while paused; resets position to the section start.
- **Two playheads** are shown on each section's mini-waveform: a cream line for the section's own playback position and a light-blue line mirroring the main-track position.
- **Loop toggle** per section — switch between looping and single-play.
- **⬇ Download** per section — exports the selected `[start, end]` range as a WAV file named `<audio>__<section>.wav`.
- Only one playback mode is active at a time: starting main playback stops any section/group playback, and starting a section's range playback pauses the main track (resuming the main track continues from where it was).

### Group Practice
- Check the checkbox on two or more sections to create a group.
- A purple **group bar** appears at the bottom showing the sections in chronological order.
- The group plays through the sections in sequence and loops the whole set (configurable).
- The currently-playing section is highlighted with a purple glow.
- The group bar has its own `▶` / `II` / `■` play, pause, and stop controls with the same pause-resume behaviour as individual sections.

### Saving
- Click **↓ Save Session** (or `⌘S`) to write the JSON back directly to `sessions/` (Chrome with folder access) or download it as a file.
- Section names, ranges, colours, and loop state are all saved.
- **Rename a section** inline and press `Enter` to rename and auto-save in one step.

---

## Supported Audio Formats

Verified with `HTMLAudioElement.canPlayType()` in Chrome on macOS:

| Format | Extensions | Status |
|--------|-----------|--------|
| MPEG-4 Audio | `.m4a` `.mp4` | ✅ Supported |
| MP3 | `.mp3` | ✅ Supported |
| AAC | `.aac` | ✅ Supported |
| Ogg Vorbis | `.ogg` `.oga` | ✅ Supported |
| Ogg Opus | `.opus` | ✅ Supported |
| FLAC | `.flac` | ✅ Supported |
| WebM (Vorbis/Opus) | `.webm` `.weba` | ✅ Supported |
| WAV | `.wav` | ✅ Works in practice |
| CAF / AIFF | `.caf` `.aiff` `.aif` | ❌ Not supported in Chrome |

---

## Folder Structure

```
riyaz-phrase-looper/
├── index.html          ← entire app, single file, no build step
├── audio/              ← place audio files here
│   └── Jog-Intro-Alaap.m4a
└── sessions/           ← JSON session files (one per audio file)
    └── Jog-Intro-Alaap.json
```

### Session JSON format

```json
{
  "fileName": "Jog-Intro-Alaap.m4a",
  "audioPath": "audio/Jog-Intro-Alaap.m4a",
  "sections": [
    { "id": 1, "name": "Intro phrase", "start": 0.0, "end": 9.2,
      "color": "#e74c3c", "loop": true },
    { "id": 2, "name": "Sa Re Ga Ma", "start": 8.8, "end": 19.9,
      "color": "#e67e22", "loop": true }
  ]
}
```

`audioPath` is relative to the project root (i.e. relative to `index.html`).

---

## Browser Support

| Browser | Works? | Notes |
|---------|--------|-------|
| Chrome / Chromium | ✅ Full | File System Access API for auto-loading sessions |
| Safari | ⚠️ Partial | Audio works; no folder access — use Browse/drag-drop |
| Firefox | ⚠️ Partial | Audio works; no folder access |

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` | Play / Pause main track |
| `Escape` | Stop all playback |
| `⌘S` / `Ctrl+S` | Save session |
| `Enter` | (in section name) Rename + auto-save |

---

## Getting Started

1. Clone or download the repo.
2. Open `index.html` in Chrome (from disk via `File →` or a local server).
3. Click **Grant access to riyaz-phrase-looper** and select the project folder.
4. Click an existing session card, or drop an audio file to start a new session.
5. Draw sections by dragging on the waveform, name them, and practice!
