# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Introduced [internal PackSquash binary
  manifests](https://github.com/ComunidadAylas/PackSquash-action/tree/master/data/packsquash_binary_manifests)
  with machine-parsable instructions for downloading and executing PackSquash
  versions. These manifests are fetched by the action at runtime, decoupling the
  release cycles of the action and PackSquash and enabling backward and forward
  compatibility with different version combinations.
  ([`414ee5c`](https://github.com/ComunidadAylas/PackSquash-action/commit/414ee5cec8f1197f310e5c7e6f68b6efdffc1c66))
  - This means that **from now on it should be less likely to have to upgrade or
    downgrade the action to use a newer or older version of PackSquash**,
    respectively.
- **Windows and macOS runners are now supported**, as long as the PackSquash
  version used by the workflow is distributed in the required way. Currently,
  only the latest unstable builds will work with these operating systems.
  ([`414ee5c`](https://github.com/ComunidadAylas/PackSquash-action/commit/414ee5cec8f1197f310e5c7e6f68b6efdffc1c66))
- Created a **`CHANGELOG.md`** file to make it more comfortable for interested
  parties to track changes to the project.
- Configured **[Husky](https://typicode.github.io/husky/)** to provision project
  developers with a pre-commit Git hook that automatically builds the action
  bundle and stages it for commit. It is possible to opt out of executing this
  hook by using `git commit --no-verify`.
  ([`0c58a3b`](https://github.com/ComunidadAylas/PackSquash-action/commit/0c58a3b43337bd0ce16932f82927cd09c8515b25))

### Changed

- The **`packsquash_version` input parameter is now required**. Also, its
  special value of `latest` now refers to the latest release instead of the
  latest unstable build. A new `latest-unstable` value has been introduced to
  refer to the latest unstable build at the time the workflow is run.
- The **`options_file` input parameter has been renamed to `options`**, and it
  now accepts either a path to a TOML file or an inline TOML string containing
  the [options
  file](https://github.com/ComunidadAylas/PackSquash/wiki/Options-files) to pass
  to PackSquash.
  ([#59](https://github.com/ComunidadAylas/PackSquash-action/pull/59))
- The **`output_file_path` PackSquash option can now be changed**, allowing
  other steps in the workflow to rely on PackSquash to output its ZIP to a
  predictable location. (Related issue:
  [#62](https://github.com/ComunidadAylas/PackSquash-action/issues/62))
- Minor dependency updates.
- Several internal refactors and cleanups.

### Fixed

- Fixed system identifier caching not being handled correctly in some edge
  cases. ([#59](https://github.com/ComunidadAylas/PackSquash-action/pull/59))

### Removed

- The **`path` input has been removed**. A custom `pack_directory` option can be
  set using the new `options` input to achieve the same result.
- As the action does no longer generate options files for PackSquash, the inputs
  that changed the contents of such file were removed: `allow_optifine_mod`,
  `zip_spec_conformance_level`, etc.
- Dropped support for previous major releases from the security policy to allow
  us to focus our development efforts better. If you have a good reason for not
  being able to upgrade to the latest major release, please let us know about
  your case so we can consider providing an upgrade path for you.

[Unreleased]:
    https://github.com/ComunidadAylas/PackSquash-action/compare/v3.0.2...HEAD