# Gesture Clip Analyzer — by VIDEOSPACE

**Gesture Clip Analyzer** is a **macOS** desktop app (Python: PySide6 + OpenCV) for analyzing MP4 files and detecting **when a gesture/movement occurs**.  
It exports a structured **`markers.json`** with precise timecodes, labels, and (optionally) durations. This file is then imported into Adobe Premiere Pro via our UXP panel **GestureMarkers_UXP** to place markers and cut clips automatically.

> VIDEOSPACE uses this tool in production for **AI-driven video post-production** (gesture-based editing, voiceover sync, fast rough-cut).

---

## 🎯 Why we built it
Traditional NLEs aren’t optimized to quickly **find & split on gestures**. For AI video workflows (avatars, LipSync, modular tutorials) knowing exact gesture moments is critical.  
GCA automates: detect → label → export → cut at markers in Premiere.

---

## ⚙️ How it works (pipeline)
1. **Load MP4** on macOS.
2. GCA analyzes frames with computer vision (motion/gesture cues).
3. It exports **`markers.json`**:

```json
{
  "version": "1.0",
  "source": "Gesture Clip Analyzer",
  "items": [
    { "t_in": 3.240, "t_out": 4.120, "label": "open_hands", "confidence": 0.87, "color": "yellow" },
    { "t_in": 7.520, "t_out": 8.000, "label": "pointing",   "confidence": 0.81, "color": "red" },
    { "t_in": 12.000, "t_out": 12.600, "label": "neutral", "confidence": 0.72, "color": "green" }
  ]
}
Import markers.json in GestureMarkers_UXP (Premiere Pro).
Panel places color-coded markers on the active sequence and can cut on markers.
✨ Key features
macOS (Apple Silicon) desktop app
Fast MP4 analysis; real-time preview
Export markers.json with labels/timecodes
Seamless Premiere bridge via GestureMarkers_UXP
Built for AI video post-production (avatars, LipSync, modular edits)
🖥️ System requirements (Analyzer)
macOS 13+ (Ventura or newer), Apple Silicon (M1/M2/M3)
Tested with Python runtime packaged into the app bundle (no manual deps needed)
Input: .mp4 (H.264 recommended)
📦 Install & run (Analyzer)
Download the latest GCA .zip from Releases.
Unzip and move Gesture Clip Analyzer.app to /Applications.
If macOS warns about unidentified developer: Right-click → Open → Open.
Launch the app → Load MP4 → Analyze → Export markers.json.
🎛 GestureMarkers_UXP_v0.1.6 (Premiere Pro panel)
GestureMarkers_UXP is a UXP panel for Adobe Premiere Pro that reads markers.json, places timeline markers, and optionally cuts at markers.
✅ Compatibility
Adobe Premiere Pro Beta 25.4 (Build 99) — primary test target
Host: "PPRO" (UXP), minVersion: 24.0 (works on current 2024/2025 lines; Beta recommended)
OS: macOS 13+ (Apple Silicon). Windows 11 should work, but primary QA is on macOS.
📥 Installation (two options)
Option A — Adobe UXP Developer Tool (recommended)
Install Adobe UXP Developer Tool.
Add Plugin → select folder GestureMarkers_UXP_v0.1.6.
Click Load (panel will be sideloaded).
In Premiere: Window → Extensions (or Plugins) → GestureMarkers (VIDEOSPACE).
