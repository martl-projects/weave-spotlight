# Spotlight

Makes what matters to you stand out: a place where something new waits from a board you care about gets a tint, one where someone close to you wrote gets their sign under the number, and their messages stand out in the chat. It shows nothing until you say who and what (its settings).

A hint service Weave ships (docs/v2-stage20.md): it folds `weave.msg`, `weave.post`, `weave.seen` (what you opened, sealed to you) and `weave.contact` (your address book, sealed to you), and answers for places (tint, sign) and messages (tint, sign). Its settings:

```
{
  "boards":   [{"board": "internal", "space"?: "<id>", "tone": "yellow"}],
  "people":   [{"who": "did:key:…", "name"?: "Lena", "sign"?: "heart", "tone"?: "red"}],
  "contacts": {"tone"?: "blue", "sign"?: "star"}
}
```

- **boards:** a place with a post or message there you haven't opened gets that tone.
- **people:** a place where they wrote what you haven't opened gets their sign; their messages get their tone and sign.
- **contacts:** the same for everyone in your address book who isn't in `people`, on their messages only.

Tones: yellow, green, blue, red, purple. Signs: heart, star, flag, bell.

## Where it lives

This repository is its only source. Weave ships it by pinning one of its releases (Weave's
`packages/shipped/pinned.json`: this repository, a tag and the archive's SHA-256), so what Weave ships and what
its project releases are the same file. A new version: tag it here, release it in its Weave project, then move
the pin in Weave.

## Building and releasing

```
npm install
npm run build              # → spotlight.wasm
```

A tag `v*` builds it on GitHub and attaches `weave-spotlight.tar.gz` (the component, `weave.app.json` and this README) to a
release (`.github/workflows/release.yml`). In Weave, `weave app release <tag> --asset wasm=weave-spotlight.tar.gz -p <project>`
records it in a project, with its SHA-256.

`wit/service.wit` is Weave's service interface (`packages/sdk/wit` in Weave's repository), copied here to build against.
