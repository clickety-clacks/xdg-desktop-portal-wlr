# xdg-desktop-portal-wlr (Gooarchy fork): agent guide

## Branches and releases (Mike, 2026-10-08)

Every agent working in this repository follows this.

- `master` mirrors upstream (emersion/xdg-desktop-portal-wlr) exactly. Never commit to it; only
  fast-forward it from upstream.
- `gooarchy` (the default branch) is an upstream release plus our patches. When upstream releases, rebase
  the patches onto the new release tag and tag `vX.Y.Z-gooarchy.N`.
- Gooarchy and the Scottland Omarchy adapter consume this fork by its `-gooarchy.N` tag only.
- Every patch is also offered upstream in spirit (README policy: AI submissions welcome). When upstream
  carries a fix, drop our patch; when none remain, consumers move back to upstream and the fork retires.
