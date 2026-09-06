# Libra Open Source Compliance

This repository indexes the open-source compliance materials distributed with
Libra. It does not contain the Libra application source code.

## Downloads

Each supported Libra version/build has a matching GitHub Release. Download these
release assets:

- `Libra-<version>-<build>-compliance.zip`
- `Libra-<version>-<build>-compliance.zip.sha256`
- `Libra-<version>-<build>-compliance.manifest.json`

The ZIP contains the complete pinned third-party source archives, patches,
license texts, notices, exact iOS arm64 build recipes, and relink materials for
the statically linked LGPL libraries.

Local artifacts are grouped by version and build:

```text
releases/Libra-<version>-<build>/
  Libra-<version>-<build>-compliance/
  Libra-<version>-<build>-compliance.zip
  Libra-<version>-<build>-compliance.zip.sha256
  Libra-<version>-<build>-compliance.manifest.json
```

## Verification

```sh
shasum -a 256 -c Libra-<version>-<build>-compliance.zip.sha256
unzip Libra-<version>-<build>-compliance.zip
cd Libra-<version>-<build>-compliance
./relink/verify.sh
```

The generated executable is unsigned. Installation requires an independent
valid Apple signing and installation workflow.

## Publishing

Generated files under `releases/` are intentionally ignored by Git. Upload the ZIP, its `.sha256` file, and the standalone manifest as assets on
the matching GitHub Release instead of committing large binaries to repository
history.
