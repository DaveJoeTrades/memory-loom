# Memory Loom — how every section fills up

A map of the app: what each screen is for, what puts data into it, and — the part that matters most — **which words are the storyteller's own and which were written by a machine.**

## The two sides

| Side | Who uses it | What it is |
|---|---|---|
| **Storyteller screen** | The person whose life is being recorded | Voice-first, large type, no admin. Biography, Today's journal, I have my own story |
| **Family ledger** | Everyone else | The archive: people, places, tree, stories, review queue, settings |

"Back to start" returns to the storyteller welcome; "Hand to storyteller" does the same from the ledger.

## Provenance: what is real and what is generated

This is the spine of the whole design.

| Kind | Status | Where it appears |
|---|---|---|
| **Audio recording** | **Irreplaceable.** Never edited, never regenerated | Vault on the device; ▶ play in Stories and Journal |
| **Transcript** | The storyteller's own words, as heard | Story detail. Improved by Scribe if a key is set, never rewritten |
| **Entity details** (a person's traits, a place's description) | Quoted or closely paraphrased from a transcript, each carrying its source quote | People, Places, Moments, Things |
| **Follow-up questions** | **Written by Claude** from what was just said | In-session, spoken aloud |
| **Gentle questions** | **Written by Claude** from gaps it noticed | Questions tab, family approves before asking |
| **Gap questions** | Generated from the completeness engine's rules (not a model) | Family tree tab |
| **"Tell me about them"** | **Written by Claude**, strictly from stored transcripts, instructed to invent nothing | Spoken only; never saved into the ledger |
| **Story translation** | **Written by Claude.** Labelled as a reading translation | Story detail, on demand |
| **Sample family stories** | **Entirely invented by Claude** for testing. Tagged as sample, removable in one tap | Everywhere, until removed |
| **Spoken voice** | Synthesized (ElevenLabs or the device voice) unless a family member recorded that question themselves | Every spoken line |

Nothing generated is ever stored as if the storyteller said it. Generated questions are marked as questions; generated narration is spoken, not filed.

## Section by section

### Storyteller — Biography
Serves one question at a time. Priority order:
1. **A family question from the inbox** (one per sitting, skippable — 2 skips parks it until tomorrow)
2. **A gap question** if something important is missing (an unnamed parent outranks a thin chapter)
3. **The life bank** — 48 questions across 12 chapters, rotating per speaker, with kin questions woven in
4. **Dynamic questions** — Claude writes 8 more when a speaker's bank runs low
5. **Evergreen prompts** when everything else is exhausted

Each answer can be extended ("Add a bit more"), corrected by voice ("Change it — tell me how"), or typed if there's no microphone. Saving files the audio in the vault and queues the transcript for extraction.

### Storyteller — Today's journal
A chat, not a form. Eight daily prompts about *them* — sleep, food, where they went, what they made of what they watched. After each answer Claude reacts and asks one deeper question, up to 8 turns per topic. The mic opens by itself after each question and stops after ~3 seconds of quiet. Recall questions drawn from previous days come first — retrieval practice, never scored to their face.

### Storyteller — I have my own story
Skips the question entirely. Free telling, filed under "own telling".

### Ledger — Review
Only fills when the extractor is **unsure**: two names that might be one person, a year that conflicts with an earlier telling, a story with audio but no words. Empty is the normal state.

### Ledger — People / Places / Moments / Things
Filled automatically by extraction after each story. Every entry carries a confidence score and the quote it came from. Expanding one shows **"Told about in"** (the stories it came from, clickable), **"Photos they appear in"**, and **"Tell me about them"**.
Things only shows objects with a photo attached; the rest stay in the data, hidden.

### Ledger — Family tree
A drawn tree around the ★ root, plus:
- **What is still missing** — two progress bars and a priority list (missing parents rank 10, an unnamed person 9, a thin chapter 3), each with "Ask this next"
- Inline relation editing, remove, and add-by-hand
- Relations are always expressed *relative to ★*, which is why merging two devices asks how the two roots relate

### Ledger — Ask
Where the family puts questions in:
- Type one, or **record it in your voice** (played to the storyteller as a real recording, and it can ring like a phone call)
- **Photo album** — select many photos at once, each becomes its own question
- **Bring in a photo scan** — a manifest from the companion scanner
- **Ask in your own voice** — record any of the 48 questions once, and it's you asking forever
- **Family voices** — assign an ElevenLabs voice per person

### Ledger — Journal / Stories / Export
Journal shows entries and recall results. Stories holds every telling with ▶ play, ⬇ save, transcript, and "Read any waiting stories" to retry extraction. Export holds the sample-family tools, the backup pair (**Family archive .json** + **All audio files .zip**), merge, audio re-import, PIN, and journal-audio toggle.

## Backups — the one thing to get right

Everything lives only on the device. Two files together are a complete restore:

| File | Contains |
|---|---|
| **Family archive (.json)** | Graph + every transcript. The only file the merge flow reads |
| **All audio files (.zip)** | Every recording; filenames carry the story ID so re-import re-links them |

The ledger nags after 7 days without an export. The PIN is a curtain, not a lock — data sits unencrypted in browser storage, and the device passcode is the real protection.

## Costs

| Action | Cost |
|---|---|
| A story: follow-up + extraction | ≈ $0.01 |
| 100 generated sample stories | ≈ $1.30 |
| Transcription (Scribe) | $0.22 per hour of audio |
| A spoken line (ElevenLabs) | ~$0.01 per 100 characters — **cached after the first time, so repeats are free** |

Prefetching only warms lines the app is about to say anyway; it doesn't add new spend, it moves the same spend earlier.
