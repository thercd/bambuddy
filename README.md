# thercd/bambuddy — homeserver build

This branch only holds the CI that builds the homeserver image. The code comes from [maziggy/bambuddy](https://github.com/maziggy/bambuddy).

- **What it builds:** the latest stable upstream release with the commits from [`feat/remove-purge-line`](../../tree/feat/remove-purge-line) cherry-picked on top. That branch adds the per-model **Remove purge line** toggle ([maziggy/bambuddy#3297](https://github.com/maziggy/bambuddy/issues/3297)).
- **Image:** `ghcr.io/thercd/bambuddy:<version>-hs`, with the version padded to four parts (`1.2.6` becomes `1.2.6.0-hs`). The homeserver's update checker compares tags that have the same suffix and number of parts.
- **When:** daily at 06:17 UTC, or manually from *Actions → Homeserver image → Run workflow*. A tag that already exists is skipped.
- **Failures:** if the patch conflicts with a new release (other than `CHANGELOG.md`), the injection tests fail, or upstream already ships `remove_purge_line`, the run opens or updates the issue *Homeserver image build needs attention*. No image is published, so the homeserver stays on the previous one.
- **Updating the patch:** rebase `feat/remove-purge-line` onto `upstream/dev` and push. The next run picks it up.
- **Retiring the fork:** once upstream ships the feature, point the homeserver back to `ghcr.io/maziggy/bambuddy` and delete this fork.
