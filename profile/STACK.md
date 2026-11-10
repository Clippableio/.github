# Clippable source map

| Repository | Purpose |
| --- | --- |
| [WebFrontend](https://github.com/Clippableio/WebFrontend) | clippable.io and the customer app |
| [WebBackend](https://github.com/Clippableio/WebBackend) | Public-app API, authentication, billing and Clippy |
| [Enterprise](https://github.com/Clippableio/Enterprise) | Fanatics and Anduril applications, with independent deployments and data |
| [Autoclipper](https://github.com/Clippableio/Autoclipper) | Clip/edit engine, API/worker services and Ascend full-video moment finder |
| [ClippableTraining](https://github.com/Clippableio/ClippableTraining) | Human review and quality feedback |
| [Clippableios](https://github.com/Clippableio/Clippableios) | iOS app |

WebBackend serves the public product. Enterprise clients retain separate runtime configuration, storage, credentials and releases. Consolidating their source does not combine customer data or trigger a global rollout. Autoclipper's existing package/API paths remain stable; the moment finder lives in `tools/moment-finder`.

The old Fanatics, Anduril, Sony and RCA repositories were retired after consolidation. RCA is no longer an active Enterprise application. `clippable-archive` retains historical work only.

## Branch workflow

Use `main` as the canonical branch. Create a short-lived branch for a concrete change, use the repository's normal review and protection rules, then remove the branch after merging. Retired branch tips are preserved as `archive/2026-11-10/<original-branch>` tags. Archived unfinished PR work is recoverable from those tags; it is not implicitly shipped. Branch cleanup never bypasses protections or changes production code.
