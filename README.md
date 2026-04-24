# landau-config

This repository contains a version-controlled snapshot of selected system configuration files from a Slackware desktop host (`landau`). It serves as a source of truth for system-level configuration, enabling auditability, reproducibility, and controlled evolution of the machine’s state over time.

## Scope

The repository includes curated files from the system tree (primarily under `/etc` and related paths) that define:

* Network configuration
* Service configuration
* Kernel/module behavior
* User environment defaults (where system-wide)
* Miscellaneous system policies

Only files deemed stable, intentional, and relevant to system behavior are tracked. Transient, auto-generated, or host-volatile artifacts are excluded.

## Design Principles

### 1. Transparency over abstraction

This repository is a direct reflection of the system’s configuration files. No templating, indirection, or configuration management DSL is introduced. What you see is what exists on the system.

### 2. Minimalism

Slackware’s design philosophy favors simplicity and explicit control. This repository follows the same principle: it does not attempt to model system state beyond storing canonical file contents.

### 3. Versioned state

All tracked configuration is maintained under Git, providing:

* Change history
* Diff visibility
* Rollback capability
* Peer review (if applicable)

### 4. No orchestration layer

This repository deliberately avoids embedding deployment or orchestration logic. It does not include:

* Configuration management tooling (e.g., push/pull agents)
* Automated provisioning scripts
* State convergence logic

Application of configuration is a manual or externally orchestrated process.

## Usage Model

This repository is intended to be used in one of the following ways:

### Reference / Audit

Inspect configuration history, compare revisions, and understand system changes over time.

### Manual deployment

Apply changes selectively by copying files into place:

```bash
cp path/to/repo/etc/example.conf /etc/example.conf
```

### External orchestration

Integrate with external tooling (e.g., shell scripts, Makefiles, or configuration management systems) that consume this repository as the authoritative config source.

## File Selection Criteria

Files included in this repository generally meet the following criteria:

* Deterministic (not regenerated on boot or by services)
* Human-authored or explicitly modified
* Critical to system behavior or policy
* Portable within the context of the `landau` host

Files typically excluded:

* Runtime state (e.g., `/run`, `/var/run`)
* Logs and caches
* Package-managed files that are unmodified from defaults
* Secrets (unless explicitly managed and secured)

## Host Specificity

This repository is **host-specific** to `landau`. It is not intended to be a generic Slackware configuration baseline.

Assumptions may include:

* Specific hardware (e.g., NICs, storage devices)
* Kernel/module requirements
* Local network topology
* Installed package set

Porting to another system will require careful review and adaptation.

## Safety Considerations

Applying configuration from this repository can affect critical system behavior. It is recommended to:

* Review diffs before applying changes
* Maintain backups of current system state
* Apply changes incrementally
* Validate service behavior after modifications

## Future Extensions (Optional)

While intentionally minimal, this repository can be extended externally with:

* Deployment scripts (`make install`, `rsync`, etc.)
* Host bootstrapping workflows
* Integration with configuration management tools

These concerns are kept out-of-scope by design to preserve clarity and separation of responsibilities.

---

This repository represents a disciplined, low-abstraction approach to system configuration management aligned with Slackware’s operational model.

