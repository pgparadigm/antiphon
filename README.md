# Antiphon

A machine-narrated edition of Jane Austen's *Pride and Prejudice*, produced by Antiphon —
a local multi-voice narration engine. Every character was detected from the text and cast
to a distinct neural voice with no human annotation.

**Listen:** https://pgparadigm.github.io/antiphon/

- Source text: Project Gutenberg #1342 (public domain)
- Voices: Kokoro-82M (Apache-2.0), rendered locally
- Full edition: 63 chapters, 12 h 27 m — see Releases

## The listening key

The page is sealed behind a listening key. The key itself lives only in
`~/.antiphon/listen_key` on the owner's machine; the page carries nothing but its SHA-256.

To rotate it, run this from a clone of this repo (it prompts with hidden input,
re-hashes, updates the page, and stores the new key locally — the key never
appears on screen, in the repo, or in history):

```sh
read -s "K?New listening key: " && echo && \
H=$(printf %s "$K" | shasum -a 256 | cut -d' ' -f1) && \
sed -i '' "s/const KEY_HASH = '[0-9a-f]*'/const KEY_HASH = '$H'/" index.html && \
printf '%s\n' "$K" > ~/.antiphon/listen_key && chmod 600 ~/.antiphon/listen_key && \
unset K H && git commit -am "Rotate the listening key" && git push
```

Rotating the key re-seals every device: visitors must present the new key once.
