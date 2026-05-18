# Changelog: ftw-pki-client

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.0.2a1] - 2026-05-18

### Removed
- **Breaking Change**: Remove the entire combined `programms.py` module and the legacy `prog_client_server_csr` executable entry point.
- Delete obsolete developer guides and automated execution doctests (`get_started_programms.ci.rst`, `get_started_run_programms.ci.rst`).
- Remove deprecated template artifacts (`MERGEMESSAGE.md`, `TAGMESSAGE.md`) from the repository root.

### Changed
- Streamline the Sphinx documentation `index.rst` to remove all entry points tracking the discontinued combined workspace modules.

---

## [0.0.1] - 2026-05-18
- Initial commit and package skeleton for the client workspace.
