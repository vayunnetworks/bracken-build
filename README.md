# BRACKEN Build

**Build, package, and release the BRACKEN system.**

BRACKEN Build is the product build and release engineering repository. Its intended role is to turn versioned operating-system inputs and BRACKEN components into traceable, deployable artifacts for development, testing, and eventual releases.

> **Project status:** Early-stage project. Build recipes, reproducibility guarantees, supported targets, signing policy, and release cadence remain to be defined.

## Responsibilities

- Orchestrate builds of [bracken-os](https://github.com/vayun-networks/bracken-os) and selected BRACKEN services.
- Pin and record source revisions, toolchains, and external dependencies.
- Package components and assemble configured system profiles.
- Produce installation and virtual-machine images, with cloud or raw images added when supported.
- Generate release manifests and software bills of materials.
- Validate artifact integrity and provide a path for signing and publishing releases.

## Design goals

Builds should be repeatable from declared inputs, produce inspectable logs and manifests, and fail clearly when dependencies or inputs are missing. Profiles should be configuration-driven rather than forks of the operating system. Build outputs should distinguish development artifacts from release candidates and stable releases.

## Scope boundaries

This repository owns build orchestration, packaging integration, image assembly, and release metadata. It does not own the implementation of the kernel, network services, or runtime control plane. Those remain in their component repositories. Deployment after an image is produced belongs in [bracken-deploy](https://github.com/vayun-networks/bracken-deploy).

Potential initial image targets include a bare-metal installer and a QEMU/KVM image. These are planned targets, not current compatibility claims. Additional outputs such as cloud images, upgrade bundles, or firmware packages should be added when their lifecycle and validation are specified.

## Planned workflow

1. Resolve declared source versions and build dependencies.
2. Build packages and the OS base in a controlled environment.
3. Assemble a named product profile.
4. Run image and integration validation.
5. Emit artifacts with checksums, a manifest, and an SBOM.
6. Publish only through a documented release process with artifact provenance.

## Development

Build commands and prerequisites will be added once a first build pipeline is implemented. Contributions should include the exact target, inputs, expected outputs, and a reproducibility or validation note. Never place signing keys, credentials, or private deployment configuration in this repository.

## Related components

- [bracken-os](https://github.com/vayun-networks/bracken-os) — operating system inputs
- [bracken-core](https://github.com/vayun-networks/bracken-core) — shared libraries and contracts
- [bracken-deploy](https://github.com/vayun-networks/bracken-deploy) — installation and rollout automation

## Security and release integrity

A release should be traceable to source revisions and build inputs. Artifact signing and automated vulnerability checks are intended capabilities; until implemented and documented, artifacts should not be treated as verified production releases.