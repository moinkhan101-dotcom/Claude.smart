# Claude.smart
## Voice Note Studio

`voice-studio/index.html` is a browser-based voice note editor. Open it in Chrome or Firefox: no install or server is needed. Audio never leaves the browser.

**Repair**
- AI voice isolation with the open-source RNNoise model (`@jitsi/rnnoise-wasm`, loaded from jsDelivr on first use)
- Spectral noise reduction: learns the noise from the quietest 10% of frames, then applies a Wiener filter with decision-directed SNR (Ephraim–Malah) and frequency smoothing, which avoids "musical noise"
- De-hum (auto-detects 50/60 Hz, up to 10 harmonics), noise gate, de-esser, speech leveler

**Voice**
- Pitch shift with formant preservation, so voices stay natural instead of muffled or cartoonish: WSOLA time-stretch, anti-aliased cubic resampling, and a cepstral spectral-envelope correction
- Separate formant control (voice size) for male ↔ female, child and giant voices
- Robot (phase vocoder), whisper, harmonizer/choir, ring modulator, bitcrusher

**Tone, modulation, space**
- Low cut, 4-band EQ, clarity (mud cut, presence, air, harmonic exciter), compressor, distortion
- Chorus, flanger, phaser, tremolo, vibrato, auto-pan
- Echo and reverb (room, booth, plate, hall, cathedral), each with "keep words clear" ducking so the effect drops under speech

**Output**
- Loudness normalization to −16, −14 or −23 LUFS (ITU-R BS.1770 / EBU R128 measurement)
- Look-ahead limiter, fades, reverse
- 16-bit WAV export with TPDF dither
- Before/after background-noise readout and a spectrogram view

**Presets:** Studio enhance, Isolate voice and Remove hiss/hum (Repair presets stack with the others), Male → Female, Female → Male, Child, Giant, Robot, Whisper, Choir, Telephone, Radio, Cathedral, Podcast, ASMR and more.

**Performance:** heavy DSP runs in a Web Worker, and each stage is cached, so changing a reverb setting doesn't re-run noise reduction. All processing runs at 48 kHz.

`voice-studio/studio.html` holds the same page without the document wrapper, which is the version published as an Artifact.
