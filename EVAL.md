# Inkling showcase — eval battery & shooting script

A reproducible set of demos for showing what `thinkingmachines/inkling` (raw audio + vision, real-time) does that a transcript-based pipeline can't. Built to be screen-recorded and posted.

**Organizing principle:** *hold the transcript constant, vary only how it's said, show the model's interpretation tracking the delivery.* A transcript+LLM pipeline sees identical text every time — so if Inkling's answer changes, the only possible cause is that it heard the raw audio.

Two rigs:
- **`index.html`** — single-model live harness (hold-to-talk, streaming captions, TTFT, filming mode).
- **`compare.html`** — side-by-side: same words to a transcript-only model (left) vs. raw audio to Inkling (right). The proof rig.

---

## Global recording setup (do this for every test)

In the ⚙︎ drawer:
- Paste your Baseten API key (memory-only; never stored).
- **Turn OFF "Keep conversation history"** — each turn must be judged fresh, or the A/B isn't fair.
- Paste the test's system prompt into **Instruction**.
- **Clear chat** *before* starting a pair (not between the two takes — the caption area keeps the last ~4 captions, so both results stay stacked on screen for the side-by-side money shot).

Per take:
1. Dry-run twice; keep the take where the read is sharpest **and** the TTFT is honestly typical (don't cherry-pick a fluke low number).
2. Hit **🎬 Filming mode** (controls hide; **Space** still works to talk).
3. Screen-record (Screen Studio for polish, or `Cmd+Shift+5` on Mac). Press **Esc** to exit filming mode.

---

## 🏆 Hero test — Contrastive stress ("the 7-word sentence")

One sentence, five times, stressing a different word each time. Words on screen are byte-for-byte identical; the meaning flips every time.

**Line:** `I never said she took the money.`

**System prompt:**
> You are Inkling in a live voice demo. Listen to which word the speaker emphasizes. In one short sentence, state the *subtext* — what they're implying by that emphasis.

| Take | Stress | Expected subtext |
|---|---|---|
| 1 | **I** never said… | someone else said it |
| 2 | I **never** said… | emphatic denial you ever said it |
| 3 | I never **said**… | you implied it but never said it outright |
| 4 | I never said **she**… | someone else took it, not her |
| 5 | …**took** the money | she did something else with it, not took it |

Five identical transcripts → five different answers. Classic linguistics demo, reads as credible.

---

## Test 2 — Sarcasm vs. sincerity

**Line:** `Oh, great. Another meeting.`
- Take A: genuinely pleased. Take B: exact same words, dripping sarcasm.

**System prompt (punchy, bracketed-tag style — best for video):**
> You are Inkling in a live voice demo. You hear the user's raw voice, not a transcript — tone carries the real meaning. Start your reply with a single bracketed tag of the tone you heard — [SINCERE] or [SARCASTIC] — then one short sentence reacting to their true intent, not the literal words.

Expected — A: `[SINCERE] Love the energy — let's make it count.` · B: `[SARCASTIC] Yeah, sounds like a meeting is the last thing you want.`

The bracketed tag is a clean on-screen beat. Two separate hold-Space turns; both tagged results stay stacked on screen.

---

## Test 3 — Intonation (statement vs. question)

**Line:** `You finished the report.`
- Take A: flat, falling tone → treated as a statement/acknowledgement.
- Take B: rising tone → treated as a question and answered.
Same words, no punctuation cue — only pitch contour distinguishes them. Pure prosody.

**System prompt:**
> You are Inkling in a live voice demo. Judge from the speaker's intonation whether they made a statement or asked a question. If it's a statement, acknowledge it in one short sentence; if it's a question, answer it. Do not rely on wording alone.

---

## Test 4 — Non-speech audio (no words at all)

The "there's literally no transcript to work with" mic-drop. A nervous laugh → a sigh → a shaky, hesitant "um… so…". No content, just paralinguistics.

**System prompt:**
> You are Inkling in a live voice demo. There may be few or no real words — describe the speaker's emotional state from the *sounds* you hear (laughter, sighs, hesitation, breathing, tone). One short sentence.

---

## Bonus — Audio + vision fusion

Turn frames **ON** (⚙︎), bump Max frames to ~12. Say, in a shaky voice while visibly fidgeting: `I'm totally fine, everything's great.`

**System prompt:**
> You are Inkling in a live voice demo. Use both what you hear and what you see. In one sentence, say whether the words match the delivery.

Expected: *"Your words say fine, but your voice and body language say otherwise."* Shows both modalities fusing — the thing only Inkling does.

---

## Generic / freeform demo prompt

For live, unscripted demoing:
> You are Inkling, running live on Baseten. You receive the user's raw voice (not a transcript) plus webcam frames captured as they speak. Pay attention to everything the words alone miss — tone, emotion, emphasis, pacing, and what's visible on camera — and let it shape your answer. Reply in one or two short, natural sentences. When how they sound or look adds meaning beyond the words, show that you noticed.

---

## compare.html — split-screen proof

Same model, same words, same answer prompt; the only variable is transcript (left) vs. raw audio (right). Any divergence isolates what hearing the audio buys you. The left side is also honestly slower (extra transcription hop) — visible on the TTFT readouts.

- Default answer prompt (sent to both sides): *"You are in a live voice demo. Reply in ONE short, natural sentence, reacting to how the person actually feels or means it — not just the literal words."*
- Left "text model" defaults to Inkling-in-text-mode (rigorous control). Swap it for another LLM to tell the "Whisper→GPT pipeline" story instead.

---

## Tweet copy

**Hero (lead):**
> Seven words. Same seven words. Five times.
> Only the *emphasis* changes — and Inkling catches a different meaning every single time.
> This is what hearing raw audio instead of a transcript actually buys you.
> On @basetenco Model APIs · first token in ~XXX ms 🎥👇

**Split-screen version:**
> Same model. Same words. One of them heard you.
> Left: only the transcript. Right: the raw audio.
> Say it sarcastically and only Inkling gets the joke.
> Live on @basetenco Model APIs 🎥👇

**Thread reply 2 (tone/intonation clips):** *"It's not just emphasis. Tone. Pitch. Same text, opposite intent."*
**Thread reply 3 (fusion clip):** *"And it's watching too. Words say 'I'm fine.' Voice and face say otherwise. Inkling sees the gap."*

**Honesty guardrails:** put the *real* on-camera TTFT in the copy; keep claims to exactly what's shown ("hears emphasis/tone from raw audio", not "emotion-detection SOTA").
