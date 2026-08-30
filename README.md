# openjdk feedstock

OpenJDK (Eclipse Temurin JRE) as a tebako **runtime** — the hermetic
`java` engine (spec 28/29): the release ships the pair per platform, the
tebako-owned wrapper exe (`tebako-runtime-launcher`, the process entry
point) plus the env image (`.tfs`, mounted — never extracted).

- **kind:** runtime (`engine: java`, `implementation: temurin`)
- **upstream:** Temurin JRE 21.0.12+8 (Adoptium), repacked — no compilation
- **artifacts:** `tebako-runtime-<tebako-line>-21.0.12-<platform>[.exe]`
  + `.tfs` + `.sha256` sidecars + release shards, the derived
  `manifest.json` index + `SHA256SUMS.txt`, and this registry
  (`tpkg-registry.yaml`) on the repo's releases
- **visibility:** `exec-cache` (spec 29 §3) with the link-unit preload
  shim granted on POSIX (the jail survives the exec into the JVM)

Consumers' app payloads declare
`runtime_requirement: {engine: java, constraint: ">= 21"}` on their
entrypoints; the dispatcher resolves the newest compatible cached
runtime (or downloads + verifies it from this repo's release index).

> The spec-30 dispatch surface for a runtime's OWN entries
> (`tebako run openjdk:java`, shimmed `java`) is PLANNED product-side.
> Until it lands the JRE's tools are declared in the runtime manifest's
> additive entrypoints list (the registry carries no entrypoints on
> kind: runtime) and the interpreter answers the spec 17 wire directly
> (`--tebako-entry java …` on the wrapper exe).

Toolkit era: pre-promotion this repo shipped `kind: toolkit` payloads
(`openjdk-21.0.12-<platform>.tfs`, tags like `21.0.12-2`). Runtime
release tags follow the trr convention `v<tebako-line>` (the tag IS the
tebako line the pair builds against).
