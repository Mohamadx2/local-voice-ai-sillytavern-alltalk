# Voice Cloning Guide (Arkham Joker / Batman style)

## Best practices for high-quality clones

1. **Source material**
   - Use clean in-game dialogue clips (5–30 seconds ideal).
   - Prefer sections with minimal background music, SFX, or reverb.
   - Multiple short clips of the same character often work better than one long noisy one.

2. **Audio format**
   - Convert to mono WAV, 22050 Hz or 24000 Hz, 16-bit if possible.
   - Tools: Audacity, FFmpeg.

3. **In AllTalk TTS V2**
   - Use **XTTS** or **F5-TTS** as the main engine.
   - Enable **RVC** (Retrieval-based Voice Conversion) for extra fidelity when available.
   - Test different temperature / speed / exaggeration settings.

4. **Emotion & laughs**
   - For Joker: write character cards that encourage manic energy, sudden laughs, and chaotic phrasing.
   - The LLM decides *when* to laugh; the TTS engine delivers the tone.
   - Some engines support style tags or exaggeration parameters — experiment.

5. **Mapping in SillyTavern**
   - TTS → AllTalk → Voice Map
   - Assign the cloned speaker to the character and optionally a different voice for the Narrator.

## Legal reminder

Only clone voices you have the legal right to use. This project is intended for private, non-commercial, personal use only.
