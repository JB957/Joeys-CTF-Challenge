# Replacing the Adventure secret-room text with a CTF flag

Yes — this is possible in this source tree.

In this disassembly, the secret-room easter egg text is not stored as plain ASCII. It is the sprite/object data under `GfxAuthor` in `adventure.asm`.

## Where to edit

- `GfxAuthor` is the object graphic payload for the hidden text object.
- `AuthorInfo` places that object in room `$1E` (the secret room).
- `AuthorStates` maps object state `FF` to `GfxAuthor`.

So to replace the original message with your CTF flag, you would:

1. Replace the byte pattern under `GfxAuthor` with a new sprite encoding of your desired text.
2. Keep the final terminating `$00` byte.
3. Optionally adjust `AuthorInfo` coordinates if your new glyph width/height needs repositioning.

## Practical note

Because the message is encoded as sprite bytes (not text), you'll need to redraw/re-encode the glyph data for your chosen flag text.
