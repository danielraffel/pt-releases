# pt releases

Repository for PlunderTube release artifacts and the plundertube.com landing page.

## Installation

Download the latest macOS or Windows installer at [plundertube.com](https://plundertube.com/).

## Release conventions

One GitHub release per version, tagged `vX.Y.Z`. When macOS and Windows ship the
same version they share one release. When a platform ships on its own, its
release carries only that platform's files. Assets are never overwritten.

| Platform | File | Purpose |
|----------|------|---------|
| macOS | `PlunderTube.X.Y.Z.pkg` | Notarized full installer (AU, VST3, app, resources) |
| macOS | `PlunderTube.X.Y.Z.dmg` | DMG containing the PKG and the uninstaller |
| macOS | `PlunderTube.X.Y.Z.dmg.zip` | Zipped DMG |
| macOS | `PlunderTube.X.Y.Z.zip` | App-only Sparkle update (EdDSA signed) |
| Windows | `PlunderTube.X.Y.Z-Windows-x64-Setup.exe` | Installer, also the WinSparkle update (EdDSA signed) |
| Windows | `PlunderTube.X.Y.Z-Windows-x64.zip` | Portable build |
| Both | `SHA256SUMS-macos.txt`, `SHA256SUMS-windows.txt` | Checksums |

Older releases used `vX.Y.Z-win` tags and `PlunderTube-vX.Y.Z-Windows-x64-Setup.exe`
names; those remain for history.

## latest.json

`latest.json` is the single source of truth for the download buttons on the landing
page and `docs/latest.html`. It is written only by `scripts/publish_release.py` in the
PlunderTube repo, after a release's assets are uploaded and their public URLs and
checksums verify. Each platform entry is independent:

```json
{
  "schemaVersion": 2,
  "macos":   { "version": "X.Y.Z", "build": "N", "tag": "vX.Y.Z", "url": "…/PlunderTube.X.Y.Z.pkg", "sha256": "…", "size": 0 },
  "windows": { "version": "X.Y.Z", "build": "N", "tag": "vX.Y.Z", "url": "…/PlunderTube.X.Y.Z-Windows-x64-Setup.exe", "sha256": "…", "size": 0 }
}
```

Do not edit download links in `index.html`; publish a release instead.

## Update feeds

- macOS (Sparkle, read by the app): https://raw.githubusercontent.com/danielraffel/pt-appcast/main/appcast-release.xml
- macOS mirrors: `appcast.xml`, `appcast-beta.xml` in the same repo
- Windows (WinSparkle): https://raw.githubusercontent.com/danielraffel/pt-appcast/main/appcast-windows.xml
