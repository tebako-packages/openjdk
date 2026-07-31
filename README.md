# openjdk feedstock

OpenJDK (Eclipse Temurin JRE) as a tebako toolkit payload — the hermetic
`java` for metanorma's jing/mn2pdf chain (the payload mounts at
`/opt/openjdk`; the tebako-runtime adapters prefer it over PATH).

- **kind:** toolkit (zero-runtime executables `java`, `keytool`)
- **upstream:** Temurin JRE 21.0.12+7 (Adoptium), repacked — no compilation
- **artifacts:** per-triplet `.tfs` images + this registry, on the repo's
  releases (see `tpkg-registry.yaml`)

Consumers declare it in their `requires:` as
`{kind: toolkit, name: openjdk, constraint: ">= 21", mount: /opt/openjdk}`.
