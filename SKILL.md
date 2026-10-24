---
name: temporal-pause-breath-architecture
description: Generates exhaustive Temporal, Pause & Breath Architecture reports detailing speech timing, pause duration histograms (ms), pause-to-speech ratio, inhalation acoustics, intra-phrase velocity/acceleration, nPVI rhythm, and filled-pause vowel qualities. Trigger with 'temporal architecture of', 'pause and breath profile for', 'speech timing analysis of', or '/temporal-breath-profile'.
disable-model-invocation: true
---

# Temporal, Pause & Breath Architecture

## Purpose & Scope

This skill models and formalizes the **time domain and respiratory mechanics** of speech. Human listeners identify speakers as much by rhythm, breathing noises, acceleration within clauses, and pause habits as by vocal timbre. This skill translates qualitative timing into concrete millisecond histograms, Pairwise Variability Indices, and acoustic breath profiles.

This skill owns:
- Exact pause duration distributions (micropauses, syntactic pauses, rhetorical pauses)
- Pause-to-speech time ratio and turn-latency constants
- Inhalation acoustics: onset duration (ms), intensity (dB SPL), spectral center, and syntactic placement
- Rhythmic timing metrics: normalized Pairwise Variability Index (nPVI) and stress-timing coefficients
- Intra-phrase velocity: phrase-initial acceleration and phrase-final syllable lengthening
- Acoustic structure of filled pauses (duration, F0 stability, and vowel formant quality)

This skill does **not** own linguistic phoneme realization (owned by `idiolect-phonetic-atlas`) or pitch tunes (owned by `prosodic-grammar-intonation-os`).

---

## Activation Triggers

Activate automatically when:
- User asks for rhythm, pause patterns, breathing profile, or speech timing (e.g., *"temporal architecture of [speaker]"*, *"pause profile for [subject]"*).
- User triggers `/temporal-breath-profile [subject]`.
- Injecting realistic breathing sounds, pauses, and cadence into neural TTS engines (Kokoro, Piper, ElevenLabs).
- Tuning speech synthesis pacing to eliminate robotic isochrony.

---

## Mandatory Report Schema & Structure

### 1. Speaking Rate & Articulatory Velocity
- **Macro Rate:** Words per minute (WPM) and syllables per second (SPS) in conversational baseline vs. performance.
- **Articulation Rate:** Pure phonation rate excluding pauses (syllables per second phonated).
- **Phoneme Duration Distribution:** Mean duration (ms) for vowels, fricatives, stops, and glides.

### 2. Pause Histogram & Architecture
- **Micropauses (50–200 ms):** Articulatory closure pauses and stop transitions.
- **Syntactic / Commatic Pauses (200–600 ms):** Clause-boundary and phrase-separation pauses.
- **Rhetorical / Dramatic Pauses (600–2500+ ms):** Deliberate suspensions for audience reaction or emphasis.
- **Pause-to-Speech Ratio:** Total silence duration divided by total speech time (percentage).

### 3. Inhalation & Respiratory Acoustics
- **Inhalation Duration (ms):** Mean and range of preparatory respiratory intake events.
- **Acoustic Intensity:** Inhalation RMS energy in dB relative to baseline phonation RMS (-12 to -24 dB).
- **Spectral Envelope:** Center of gravity of breath noise (typically 1.2–3.5 kHz); turbulent aspiration texture.
- **Syntactic Breath Placement:** Probability of breathing at clause boundaries vs. unexpected intra-constituent breaks.

### 4. Rhythmic Structure & Isochrony (nPVI)
- **Normalized Pairwise Variability Index (nPVI):** Vowel duration variability score (nPVI > 55 = stress-timed; < 45 = syllable-timed).
- **Stress-Timing Ratio:** Ratio of stressed to unstressed syllable durations.
- **Cadence Regularity:** Degree of metric pulse or syncopation in oratorical delivery.

### 5. Intra-Phrase Dynamics & Final Lengthening
- **Intra-Phrase Velocity:** Velocity curve across a sentence (e.g., rapid initial burst, steady mid-body, terminal slowdown).
- **Phrase-Final Lengthening (PFL):** Duration multiplier on phrase-final syllables (1.2x to 1.8x).

### 6. Filled Pauses & Hesitations
- **Filler Token Quality:** Specific acoustic vowel quality of filled pauses ([əm] vs [ʌː] vs [eː]).
- **Mean Duration (ms):** Average length of hesitation events.
- **F0 Trajectory in Fillers:** Level pitch vs. dipping contours during cognitive holding.

---

## Machine Output Block

```json
{
  "$schema": "https://json-schemas.voice/temporal-architecture.v1.json",
  "speaker_id": "SPEAKER_ID",
  "rate_metrics": {
    "wpm_mean": 145,
    "articulation_rate_sps": 4.6,
    "pause_to_speech_ratio": 0.22
  },
  "pause_distribution_ms": {
    "micropause_mean": 110,
    "syntactic_pause_mean": 420,
    "rhetorical_pause_mean": 1450,
    "rhetorical_pause_max": 2400
  },
  "inhalation_profile": {
    "duration_ms": 480,
    "relative_spl_db": -16.5,
    "spectral_cog_hz": 2100,
    "probability_at_major_clause": 0.88,
    "audible_intake_present": true
  },
  "rhythm_metrics": {
    "npvi_vowel_score": 58.6,
    "timing_class": "STRESS_TIMED",
    "phrase_final_lengthening_multiplier": 1.45
  },
  "filled_pauses": {
    "favored_token": "ʌːm",
    "f1_hz": 520,
    "f2_hz": 1180,
    "mean_dur_ms": 380,
    "f0_flatness_ratio": 0.92
  }
}
```

---

## Biometric & Personality Crosswalk

| Temporal Parameter | Core Biometric Section | Personality Profile Section | Synthesis Compiler Target |
| :--- | :--- | :--- | :--- |
| SPS & WPM | §5 Speaking Rate & Rhythm | §3.1 Sentence Length & MLU | Engine Speed Scalar |
| Pause Histogram | §5 Pause, Phrasing & Timing | §5.1 Turn-Taking Cadence | SSML `<break time="...ms"/>` |
| Inhalation Acoustic Profile | §2 Noise Component | §5.2 Fillers & Hesitations | Audio Sample Injection / Viseme |
| nPVI Score | §5 Stress, Accent & Rhythmic Feel | §2.5 Repetition & "The Groove" | Syllable Duration Scaling |

---

## Calibration Reference Example: Queens Orator Baseline

- **Pause-to-Speech Ratio:** 24.5% during rally speeches; punctuated by signature long rhetorical suspensions (1200–2200 ms) while scanning audience.
- **Inhalation Sound:** Distinct, audible clavicular inhalation (~450 ms duration, -16 dB relative to speech) occurring before major oratorical declarations.
- **Rhythm (nPVI):** High nPVI of 59.2 reflecting aggressive stress-timing; unstressed vowels reduce heavily while nuclear vowels stretch by 1.5x.
- **Acceleration Dynamics:** Accelerates dramatically on parenthetical lists (+30% SPS), then slows to a deliberate, punchy cadence on terminal assertions.

---

## Generation Rules

1. All durations must be stated in milliseconds (ms); all rates in syllables per second (sps) and words per minute (wpm).
2. Quantify rhythm using the normalized Pairwise Variability Index (nPVI).
3. Every profile must output the machine-readable `temporal_architecture.json` block.
