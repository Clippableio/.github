# Clippable stack

Every live product lives in the [Clippableio](https://github.com/Clippableio) org. Hosts and secrets are replaceable: swap the capture machine, GPU worker, or Railway service without moving ownership off the org.

Do not put operator names or personal GitHub accounts in descriptions or docs.

## Products

| Repo | What it is | Talks to |
| --- | --- | --- |
| [WebFrontend](https://github.com/Clippableio/WebFrontend) | Public site and customer app — [clippable.io](https://clippable.io) | WebBackend |
| [WebBackend](https://github.com/Clippableio/WebBackend) | API, auth, billing, Clippy, workers for the public app only | WebFrontend, Autoclipper (media jobs) |
| [Fanatics](https://github.com/Clippableio/Fanatics) | Fanatics daily clips — dashboard, API, capture worker, card-pull selector | Autoclipper (library), own Postgres + clip storage |
| [Sony](https://github.com/Clippableio/Sony) | Sony Music clip studio (own frontend + backend) | Autoclipper |
| [Anduril](https://github.com/Clippableio/Anduril) | Anduril clip studio (own frontend + backend) | Autoclipper |
| [Autoclipper](https://github.com/Clippableio/Autoclipper) | Shared clip/edit engine (score, cut, render) | Imported by Fanatics / Sony / Anduril |
| [Clippableios](https://github.com/Clippableio/Clippableios) | iOS app | WebBackend |

WebBackend is **not** the API for Fanatics, Sony, or Anduril.

## Fanatics runtime (replaceable pieces)

```
livestreams
    → capture host (any machine with ffmpeg/streamlink)
    → GPU worker (any CUDA box; Autoclipper + Fanatics/streamclip)
    → Fanatics web on Railway (API, login, Postgres, clip files / object storage)
    → fanatics.clippable.io
```

| Piece | Repo / config | Replace by |
| --- | --- | --- |
| Site + API | `Fanatics/webapp` on Railway | Redeploy the same service |
| Card-pull finder | `Fanatics/streamclip` | Same repo |
| Clip engine | `Autoclipper` (`autoclipper-core`) | Point `AUTOCLIPPER_SRC` at a new checkout |
| Capture host | `Fanatics/worker` env (`CAPTURE_*`) | New machine; same worker scripts |
| GPU worker | `Fanatics/worker` (`detect_puller`, CUDA) | New GPU box or cloud GPU |
| Clip files | Railway volume and/or object storage | New bucket + env vars |
| Search | `Fanatics/webapp` `/api/search` | Text search over already-cut clips |

The public app (WebFrontend + WebBackend) is a separate stack from Fanatics.

## Archived (not products)

| Repo | Why it exists |
| --- | --- |
| `stream-clipper-legacy` | Old unused dump. Live Fanatics is `Fanatics`. |
| `clippable-archive` | Historical worktrees only. |

## Desktop checkouts

Match repo names: `WebFrontend`, `WebBackend`, `Fanatics`, `Anduril`, `Sony`, `Autoclipper`, `Clippableios`.
