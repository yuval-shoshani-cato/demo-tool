# demo-tool

A lightweight helper for bootstrapping a consistent demo environment for product showcases, internal walkthroughs, team onboarding, and proof-of-concept setups.

Whether you are preparing a live demo for stakeholders, spinning up a repeatable environment for training, or creating a clean baseline for experimentation, `demo-tool` gives you a simple, repeatable way to install and configure a local demo profile without the friction of a full production setup.

This project is intentionally pragmatic: it focuses on getting the environment into a known-good state quickly, documenting the setup, and making it easy to share across machines, teams, and demo scenarios.

## Why this project exists

Demo environments are often one-off, brittle, and hard to recreate. Teams regularly lose time to:

- Reinstalling the same toolchain repeatedly
- Rebuilding config files by hand
- Forgetting environment variables or shared profile paths
- Reproducing setup steps during live presentations
- Supporting different machine states when a demo is being run in multiple places

`demo-tool` addresses that problem by creating a reliable local installation footprint and a simple configuration profile that can be referenced in project environment files.

## What makes it useful

- Simple installation experience
- Local configuration stored under `$HOME/.demo-tool`
- Reusable profile-oriented setup
- Good fit for demos, training, labs, and proof-of-concept work
- Minimal operational overhead
- Easy to extend for future environments

## Features

- One-command installation
- Local demo profile configuration in a predictable directory
- Versioned config metadata
- Compatible with shell-based environment setup patterns
- Works well as a foundation for shared demo workflows
- Keeps setup instructions easy to document and reproduce

## Quick start

Install the project with the standard installer:

```sh
curl -fsSL https://raw.githubusercontent.com/agentsense-demo/demo-tool/main/demo-tool-installer-v1.4.2-darwin.sh | sh
```

This creates a local config under `$HOME/.demo-tool` and records version information for the active installation.

## System requirements

`demo-tool` is intentionally lightweight, but a few basic requirements apply:

- macOS (this repository ships a Darwin installer)
- A POSIX-compatible shell (`sh`)
- Write access to your home directory
- Basic terminal access for running install and setup commands

If you're using this project in a broader environment, you can adapt the same pattern to other shells or operating systems.

## Installation

### Install from the hosted script

```sh
curl -fsSL https://raw.githubusercontent.com/agentsense-demo/demo-tool/main/demo-tool-installer-v1.4.2-darwin.sh | sh
```

The repository's installer is intentionally minimal and designed to demonstrate a simple setup pattern rather than heavy orchestration.

## What gets installed

The default installer writes a configuration file like this:

```sh
version=1.4.2
channel=stable
```

and stores it in:

```sh
$HOME/.demo-tool/config
```

The install also creates the target directory:

```sh
$HOME/.demo-tool
```

This makes the environment easy to discover and reference from scripts, shell profiles, and project-local `.envrc` files.

## Project setup pattern

The included `setup.md` demonstrates a common pattern for binding a project to a shared demo profile. The pattern is:

```sh
export DEMO_TOOL_PROFILE_DIR=$HOME/.demo-tool/profiles/team-default-v1.4.2
```

This approach is useful when you want a project or shell session to reference a known demo runtime or profile without hardcoding details into a script or config file.

## Typical use cases

### Product demos

Use `demo-tool` to keep the demo environment in a consistent state before a presentation. It reduces setup surprises when the app is running in front of customers or stakeholders.

### Workshops and onboarding

Teams need a reproducible baseline for training or onboarding. A repeatable install script helps new participants get the same environment quickly.

### Internal experimentation

When exploring ideas, prototypes, or proof-of-concept work, it is helpful to have a clean, known-good environment that can be created and reset without expensive preparation time.

### Shared team profiles

When multiple developers work from the same curated profile, a shared directory pattern helps unify runtime expectations and reduces drift across local machines.

## Typical workflow

1. Install `demo-tool` on a machine.
2. Confirm the config exists in `$HOME/.demo-tool`.
3. Point a project or shell session at a shared profile directory.
4. Run the demo, training, or proof-of-concept setup.
5. Reuse the same setup across sessions and people.

## Repository layout

```text
.
├── README.md
├── install.sh
├── setup.md
├── demo-tool-installer-v1.4.2-darwin.sh
└── .gitignore (if present in your branch)
```

This repository is intentionally compact. It focuses on the core setup pattern rather than packaging a large application or ecosystem.

## Configuration

At minimum, the project writes configuration values to the local install directory. You can extend this model further if you want to include:

- default team profile path
- active environment name
- channel (stable, beta, dev)
- version metadata
- custom demo profile directories

A simple configuration file format makes the project easy to inspect and adjust by hand.

## Example shell usage

```sh
export DEMO_TOOL_PROFILE_DIR=$HOME/.demo-tool/profiles/team-default-v1.4.2

# verify the profile path exists
ls -ld "$DEMO_TOOL_PROFILE_DIR"

# inspect the config
cat "$HOME/.demo-tool/config"
```

## Troubleshooting

### Installation fails

Check that:

- You have permission to write to your home directory
- Your shell is compatible with the installer
- The script URL is reachable from your environment

### Config file missing

If the config does not appear after installation:

```sh
ls -la "$HOME/.demo-tool"
```

If the directory is missing, rerun the installer.

### Profile directory not found

Confirm the environment variable is set correctly:

```sh
echo "$DEMO_TOOL_PROFILE_DIR"
```

If the path does not exist, create the expected directory structure or update the profile path to a valid location.

### Different machine states

Because this is a local demo setup, environment drift can happen if people use different profile paths or manually modify shared files. Keeping the installation path and project configuration documented helps reduce this issue.

## Security considerations

This project is designed for lightweight local setup and demo use. It is not a hardened production deployment tool. Keep the following in mind:

- Avoid placing secrets in shared demo profile directories unless they are intentionally meant for the demo
- Review profile paths before sharing them with teammates or external audiences
- Do not assume the demo environment is production-safe
- Treat installer scripts as convenience tooling, not security controls

## Best practices

- Keep a single, documented installation path for your team
- Use versioned profile names when changes may affect demonstrations
- Prefer shared configuration files over ad hoc shell tweaks
- Validate setup on a clean machine before an important presentation
- Keep your demo environment consistent across devices and presenters

## Roadmap

This repository is intentionally simple, but it is a strong starting point for broader demo tooling. Potential future expansions include:

- Support for additional operating systems
- More structured profile templates
- Better validation and health checks
- Demo environment presets for common workflow types
- Optional onboarding and bootstrap documentation

## Contributing

Contributions are welcome.

If you would like to improve the setup process, add clearer documentation, or expand the repository for broader demo scenarios:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Update documentation if needed
5. Open a pull request with a clear description of the problem and solution

## License

This project is distributed under the repository's chosen license. If no license file is present, treat it as a source example and confirm the legal usage terms before using it in a production or shared environment.

## Support and maintenance

This repository is intended as a practical demo utility. It provides the essentials for a lightweight, reusable setup flow, but it is not a full platform or enterprise distribution system.

If you are using it as a basis for a customer-facing environment, review the workflow carefully and validate the configuration in the exact target environment before use.

## Final note

`demo-tool` is best understood as a bootstrap helper for a demo environment: small, simple, and intentionally easy to understand. It gets people from a blank machine to a usable setup with minimal ceremony and no unnecessary complexity.

That simplicity is the point.

---

For a quick summary:

```sh
curl -fsSL https://raw.githubusercontent.com/agentsense-demo/demo-tool/main/demo-tool-installer-v1.4.2-darwin.sh | sh
```

Then connect a project or shell session to the installed demo profile directory and start your environment.
