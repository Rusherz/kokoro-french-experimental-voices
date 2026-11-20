# Experimental French Kokoro Voice Packs

Experimental Kokoro-compatible French voice packs. These are plain PyTorch `.pt` tensors and work with Kokoro-FastAPI.

> **Experimental:** These packs are research/test artifacts, not official Kokoro voices. Quality is subjective and unverified — test them before relying on them.

## Included voices

- `fm_tom_experiment`
- `fm_gilleslow_experiment`
- `fm_mlsmedium_experiment`
- `fm_mls1840low_experiment`
- `ff_siwislow_experiment`
- `ff_siwismedium_experiment`
- `ff_upmcmedium_experiment`

## Install into Kokoro-FastAPI

Copy one or more packs into the container's voices directory, then restart it:

```sh
docker cp voices/fm_tom_experiment.pt <container>:/app/api/src/voices/v1_0/
docker restart <container>
```

Or bind-mount each pack in Compose:

```yaml
services:
  kokoro:
    volumes:
      - ./voices/fm_tom_experiment.pt:/app/api/src/voices/v1_0/fm_tom_experiment.pt:ro
```

The API exposes it after startup as `fm_tom_experiment` (the filename without `.pt`). Use that identifier in the web player or speech requests.

Use `fm_` for male-reading French voices and `ff_` for female-reading French voices. The first `f` selects Kokoro's French pipeline. Do not put hyphens in a filename; Kokoro-FastAPI interprets them as voice-mixing separators.

## Layout

- `voices/`: distributable voice-pack files.
- `checksums.sha256`: integrity checksums for voice packs.
