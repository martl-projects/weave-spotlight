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

## Building and releasing

```
npm install
npm run build              # → spotlight.wasm
```

A tag `v*` builds it on GitHub and attaches `weave-spotlight.tar.gz` to a release (`.github/workflows/release.yml`). In Weave, `weave app release v1.0 --asset wasm=weave-spotlight.tar.gz -p <project>` records it in a project, with its SHA-256.

Weave also ships this service, built from the same source (`packages/shipped/spotlight` in Weave's repository). Weave's own has the app id `weave-spotlight`, which no project's release may take; this repository's releases are `spotlight-hints`, released in the Weave project Spotlight.
