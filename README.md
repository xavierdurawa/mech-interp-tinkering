# mech-interp-tinkering

Informal notes and write-ups from poking at language-model internals. Musings
and small experiments — some pan out, most don't; I write up the interesting
ones (including the ones that didn't work). Not peer-reviewed, not exhaustive.
If something turns into a real result, it gets its own repo, linked from the post.

Built with [Quarto](https://quarto.org). Posts live in `posts/`.

## Posts

- **Function vectors steer behavior but don't "read out" in language** — a small
  controlled negative result, and a dissociation between what steers a model and
  what's verbalizable.

## Build

```bash
quarto render          # -> _site/
quarto preview         # local preview
```
