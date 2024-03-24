# Open-Suno
We aim to form a technical discussion around the challenges around building an impressive music producing system similar to Suno v3. 
Please note that this is not an attempt at reverse-engineering any source code, architecture or training data of Suno. This is a **purely research-oriented discussion** on how a similar level of aweness may be achieved using open-source technologies. This is not a commericial project, and its artifacts will not be used for commericial purposes. On the contrary, we hope to inspire the community in building complex and powerful systems to better assist musicians in their creations.

## Updates
- Mar 24, 2024: Initial assumptions.

## Our assumptions (Last updated: 3/24/2024)
Even with random input, we found that the Suno V3 models seem to have a very strong prior, which forces it to have a song structure. Besides, we notice similar issues with [Bark (Suno's previous autoregressive TTS model)](https://huggingface.co/spaces/suno/bark) that the singer identity shifts sometimes. Therefore, we hypothesis that Suno is not one, but actually four models.

- **Structure Model** is conditioned on lyrics + style prompt (both in natural language), and generates a structure (as well as the lyrics for each structure). This may be achieved by a fine-tuned version of some large language model.
- **Vocal Melody Model** is generating a vocal melody based on the structures and lyrics.
- **Vocal Synthesis Model** is conditioned on lyrics + melody. It could have a singing-frontend + VITS-like backbone structure like many synthesis model; but it's more plausible that they opted for an autoregressive model architecture similar to Bark.
- **Accompanyment Generation Model** is a MusicGen-like model conditioned on discrete learned tokens (similar to EnCodec or SoundStream) that generates accompaniment autoregressively. This model is likely to be conditioned on structure, melody and style.
