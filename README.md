# Libra Open Source Software Compliance

This repository publishes the open-source software (OSS) compliance materials distributed
with Libra Media Player. It does not contain Libra application source code.

## Downloads

Each distributed Libra version/build has a matching GitHub Release with these
assets:

- `Libra-<version>-<build>-LGPL-source.zip`
- `Libra-<version>-<build>-LGPL-source.zip.sha256`
- `Libra-<version>-<build>-LGPL-source.manifest.json`

The ZIP contains the complete corresponding FFmpeg and FriBidi source, license
texts, exact iOS arm64 build recipes, checksums, and a framework replacement
helper for that Libra version/build.

Libra loads these LGPL components as separate, replaceable dynamic frameworks:

```text
@rpath/LibraFFmpegBinary.framework/LibraFFmpegBinary
@rpath/LibraFriBidiBinary.framework/LibraFriBidiBinary
```

The package excludes the Libra executable, private bridge code, Swift modules,
application object files, credentials, signing material, and user data.

## Verification

```sh
shasum -a 256 -c Libra-<version>-<build>-LGPL-source.zip.sha256
unzip Libra-<version>-<build>-LGPL-source.zip
cd Libra-<version>-<build>-LGPL-source
shasum -a 256 -c SHA256SUMS
./rebuild-ios-arm64.sh
```

The package also includes `tools/replace-and-resign.sh`. Replacing an embedded
framework changes the app signature; installing the resulting app requires an
appropriate Apple signing identity, provisioning profile, and entitlements.

## Publishing

Generated files under `releases/` are intentionally ignored by Git. The ZIP,
its `.sha256` file, and the standalone manifest are published as assets on the
matching GitHub Release instead of being committed to repository history.

## Licensing

Third-party materials in the Releases are governed by their respective included
licenses. This repository does not contain Libra application source code or grant
an open-source license to the Libra application.
