# Inkling demo harness

A single-file browser harness for testing [Inkling](https://www.baseten.co/), Thinking Machines Lab's real-time interaction model, served on Baseten Model APIs.

**Live version:** https://anaskar.github.io/inkling-demo/

Hold to talk: your speech is recorded from the mic while webcam snapshots are captured, then sent together as one multimodal turn (16kHz WAV `audio_url` + JPEG `image_url` parts) to the OpenAI-compatible chat completions endpoint. The reply streams into on-screen captions with a time-to-first-token readout — plus a stopwatch and filming mode for clean screen recordings.

Because the model receives raw audio (not a transcript) and synchronized frames, it can react to tone of voice, pacing, and what it sees — not just your words.

## Usage

1. Get a Baseten API key at [app.baseten.co](https://app.baseten.co) (Settings → API keys).
2. Open the page, click ⚙︎, paste your key.
3. Hit **Start session**, allow mic + camera, then **hold Space** (or the talk button) while speaking. Release to send.

Your API key is held in memory only — it is never stored, logged, or sent anywhere except directly to the Baseten endpoint. This repo contains no credentials.

## Controls

- **🎙 Hold to talk / Space** — record a turn; release to send
- **⏱ Start timer** — on-screen stopwatch for timing demos
- **🎬 Filming mode** — hides all controls for clean screen recordings (Esc to exit)
- **Clear chat** — resets captions and conversation history
- **Log** — request/response log for debugging

## Config (⚙︎)

System prompt, frames-per-second and max frames per turn, and conversation history are all adjustable in the settings drawer. Requests are capped at 5 MB by the API, so keep recordings short or lower the frame count for long turns.
