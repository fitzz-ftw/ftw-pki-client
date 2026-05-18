# Changelog: ftw-pki-client

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.0.2a1] - 2026-05-18

### Added
- Integrate local `LeafPKIConfig` to handle secure client-level configuration and dynamic path evaluations.
- Replace the generic placeholder docstring for `prog_client_csr` with a comprehensive, Sphinx-compliant English specification.
- Register `user/cli_user` directly within the main Sphinx documentation index tree (`index.rst`).

### Changed
- Shift internal keys location strategy: The internal private keys directory is now inferred dynamically via configuration paths instead of static command-line parameter overrides.
- Enforce secure and explicit `.pem` file extensions (`.key.pem` and `config.ext_public`) for all generated client keypairs.
- Clean up the doctest suites in `get_started_programms.ci.rst` to assert keypair generation against the new secure data and configuration storage locations.

### Removed
- **Breaking Change**: Drop direct `platformdirs` runtime dependency and its unused intersphinx mapping block from the Sphinx documentation setup (`conf.py`).
- Clean up outdated and unused transport encryption `FIXME` architecture placeholders in client workflows.

---

## [0.0.1] - 2026-05-18
- Initial commit and package skeleton for the client workspace, following the structural split from the server modules.
