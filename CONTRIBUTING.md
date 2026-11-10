# Working in Clippable repositories

`main` is the canonical branch. Keep its existing review, protection and release rules.

Use a short-lived branch for a concrete change and open a pull request against `main`. Remove the branch after merging; automatic deletion is enabled on active repositories. A source merge is not permission to deploy every client.

Before retiring unfinished work, preserve its exact commit in an archive tag and a verified Git bundle. Organization cleanup on November 10, 2026 used `archive/2026-11-10/<original-branch>`. Those tags retain the code and its history; unfinished changes were not silently merged into production.

To resume archived work, fetch the tag, create a new short-lived branch from it, and review its changes against current `main`. Closed historical PRs remain available for context. Preserve existing local changes and never commit credentials, runtime databases or client media.
