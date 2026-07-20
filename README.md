
<div align="center">

# CleanMyMac CLI

**Clean developer caches, project artifacts, and disk clutter. Analyze storage and reclaim space — without leaving the Terminal.**

</div>

<p align="center">
  <img
    width="2172"
    alt="CleanMyMac CLI showing cleanup, disk analysis, and optimization workflows"
    src="https://github.com/user-attachments/assets/d31aa939-cd1e-419c-ba42-d92a49522104"
  />
</p>
<p align="center">
  <em>🩷 Built and used daily by the CleanMyMac team on our own Macs🩷</em>
  
</p>



> Developer storage builds up across Docker, Xcode, package managers, project folders, and AI tools. CleanMyMac CLI brings those leftovers into one place, shows what can be removed, and leaves the final decision to you.

> 💡CleanMyMac CLI is currently in public beta. Commands and behavior may evolve as we improve the experience.

## Features

- **Developer Cleanup**: Clears caches, build artifacts, and system junk across common developer tools (see [Commands](#commands))
- **Artifact Purging**: Removes old build artifacts using age-based selection
- **Disk Analysis**: Reports on disk usage to show what is consuming storage
- **Interactive Review**: Prompts for confirmation before deletion; protected system locations; cleanup logic shared with CleanMyMac
- **Terminal-Based**: Scriptable commands intended for command-line workflows
- **Privacy Controls**: No source code or personal files are uploaded; analytics can be disabled via configuration
- **Optimization**: Runs quick performance tasks from the command line

## Requirements

- macOS 11 or later, [Homebrew](https://brew.sh)

## Installation
> The formula lives in our tap — [MacPaw/homebrew-taps](https://github.com/MacPaw/homebrew-taps)

>  Manual download: Prefer to install without Homebrew? Download the latest build directly: [CleanMyMac-CLI-1.0.0.zip](https://cli.cleanmymac.com/1.0.0/CleanMyMac-CLI-1.0.0.zip)

### The fastest way to install CleanMyMac CLI is with Homebrew:

```bash
brew install --cask macpaw/taps/cleanmymac-cli
```

Verify the installation:

```bash
cleanmymac --version
```

Then launch the interactive interface:

```bash
cleanmymac
```

Or start by analyzing what is taking up space:

```bash
cleanmymac analyze
```

! Both `cleanmymac` and `cmm` run the same tool.


## Quick Start

[Getting Started](https://github.com/MacPaw/cleanmymac-cli/wiki/Getting-Started) ·
[Commands](https://github.com/MacPaw/cleanmymac-cli/wiki/Commands) ·
[Safety & Privacy](https://github.com/MacPaw/cleanmymac-cli/wiki/Safety-and-Privacy) ·
[FAQ](https://github.com/MacPaw/cleanmymac-cli/wiki/FAQ)

---

## What can CleanMyMac CLI do?

### Clean developer caches and system junk

Find removable files created by developer tools, package managers, Xcode, AI tools, and macOS:

```bash
cleanmymac clean
```

Scan a specific cleanup category:

```bash
cleanmymac clean dev
cleanmymac clean junk
cleanmymac clean ai
cleanmymac clean trash
```
CleanMyMac CLI can detect caches and generated files from tools including: Homebrew, npm, Yarn, and pnpm, pip, Poetry, and uv, Xcode DerivedData, Device Support, Module Cache, and other Xcode-related files, supported AI-tool artifacts etc

You review detected items before cleanup.

---

### Remove old project artifacts

Development projects accumulate generated files that can take gigabytes of disk space: `node_modules`, `.next`, `.turbo`, `target`,  `.build` etc

Find them across common project folders:

```bash
cleanmymac purge
```

Or scan a specific directory:

```bash
cleanmymac purge ~/Projects
```
Results are grouped by project so you know what each artifact belongs to.

Artifacts older than seven days are preselected. Newer artifacts remain visible but unchecked for manual review.

> [!TIP]
> Use `clean` for shared caches and tool-generated junk.  
> Use `purge` for removable dependencies and build artifacts stored inside project folders.

---

### Analyze disk usage from Terminal

Not sure where your disk space went?

Open the interactive storage analyzer:

```bash
cleanmymac analyze
```

Or start from a specific folder:

```bash
cleanmymac analyze ~/Projects
```

Navigate through directories by size, explore what is consuming storage, and reveal items in Finder.

Browsing through the analyzer does not modify your files. Any removal action requires an explicit selection and confirmation.

> [!TIP]
> If your Mac is running out of storage and you are not sure what is safe to remove, start with `cleanmymac analyze`.

---

### Optimize your Mac

Run lightweight maintenance tasks directly from Terminal:

```bash
cleanmymac optimize
```

Or run them separately:

```bash
cleanmymac optimize ram
cleanmymac optimize purgeable
```

- `optimize ram` releases inactive memory
- `optimize purgeable` asks macOS to release disk space already marked as purgeable

These commands do not remove project source code or personal documents.

---

## Preview first. Delete only what you approve.

CleanMyMac CLI is designed around transparency and control.

Before cleanup, you can inspect what was detected and decide what should be removed.

Safety features include:

- **Interactive review** before cleanup
- **Protected system locations** excluded from cleanup
- **Project-aware purging** with age-based selection
- **Ignore list** for files and folders you always want protected
- **Explicit confirmation** before removal
- Cleanup detection based on logic shared with CleanMyMac

Protect a path permanently:

```bash
cleanmymac ignore add ~/Projects/important-project
```

View protected paths:

```bash
cleanmymac ignore list
```

Remove a path from the ignore list:

```bash
cleanmymac ignore remove ~/Projects/important-project
```

> [!WARNING]
> `--force` skips interactive confirmation for supported cleanup commands and removes detected items immediately. Run the command without `--force` first and review what it finds.

Learn more: [Safety and Privacy](https://github.com/MacPaw/cleanmymac-cli/wiki/Safety-and-Privacy)

---

## Commands

| Command | Description |
|---|---|
| `clean` | Runs all clean categories at once: system junk, dev-tools junk, and trash |
| `clean ai` | Scans for junk created by AI tools, shows what can be safely removed, and cleans it after your confirmation |
| `clean dev` | Clears cached packages and build files left by developer tools: Homebrew, npm, Yarn, pnpm, pip, Cargo, Go, CocoaPods, Docker, VS Code, JetBrains, Maven, Gradle, Poetry, uv, Bun, Deno, and mise |
| `clean junk` | Clears user logs, Xcode DerivedData, Device Support, Module Cache, Documentation Cache, and other Xcode-related junk |
| `clean trash` | Empties the system trash and mounted-volume trash bins |
| `clean --force` | Deletes immediately, skipping the confirmation prompt |
| `purge` | Scans developer folders (`~/Projects`, `~/Code`, `~/dev`, `~/GitHub`, `~/Workspace`) and lists removable build artifacts grouped by project for review. Detects `node_modules`, `.next`, `.turbo`, `target`, `.build`, `.venv`, `venv`, `pycache`, `Pods`, `DerivedData`, `vendor`, and `cmake-build-*`. Artifacts older than 7 days are preselected; newer ones are shown unchecked |
| `purge <path>` | Scans a specific folder for removable project artifacts |
| `analyze` | Opens an interactive disk usage explorer |
| `analyze <path>` | Explores disk usage within a specific folder |
| `optimize` | Frees RAM and purgeable disk space in one command |
| `optimize ram` | Releases inactive memory (no sudo required) |
| `optimize purgeable` | Clears space macOS has marked as purgeable but not yet released |
| `config` | Opens CLI settings, including the analytics toggle |
| `ignore add <path>` | Adds a path to the ignore list so it never appears in `clean`, `purge`, or `analyze` results |

For detailed examples, see the [Commands documentation](https://github.com/MacPaw/cleanmymac-cli/wiki/Commands).

---
---

## How it works

A typical cleanup takes three steps:

### 1. Scan

```bash
cleanmymac clean/purge
```

CleanMyMac CLI scans supported locations and groups what it finds.

### 2. Review

Inspect categories and paths, then select or deselect what you want to remove.

### 3. Confirm

After cleanup, CleanMyMac CLI shows what was removed and how much disk space was recovered.

---

## Interactive or direct — your choice

Open the interactive interface or run exactly what you need. This makes CleanMyMac CLI useful both as an interactive cleanup tool and as part of command-line workflows.


```bash
cleanmymac
```

```text
        __________
       /    └───   \    CleanMyMac CLI
      /             \   Clean and optimize your Mac safely from the terminal.
     └───────────────┘  v1.0.0 beta
           ▒▒▒▒
           ────

          ▸ Clean       Scan and review junk before removing it
            Purge       Find removable artifacts across your projects
            Analyze     Explore what is taking up disk space
            Optimize    Free RAM and release purgeable disk space
            Config      Manage CLI preferences


      ↑↓ Navigate  ·  Enter Confirm  ·  M More commands  ·  Q Quit
      beta · cleanmymac.com · lovingly crafted by MacPaw
      ```

```
Run:

```
        M
        
        cleanmymac clean                    Scan and review junk on your Mac
        cleanmymac clean junk               Scan and review system junk only
        cleanmymac clean dev                Scan and review developer-tool junk only
        cleanmymac clean ai                 Scan and review ai-tool junk only
        cleanmymac clean trash              Scan and review items in Trash only
          --force                           Skip confirmation and clean immediately
        
        cleanmymac purge                    Find project artifacts in common developer folders
        cleanmymac purge <path>             Scan a specific directory for project artifacts
          --force                           Skip confirmation and clean immediately
        
        cleanmymac analyze                  Explore storage usage in your home directory
        cleanmymac analyze <path>           Explore storage usage inside a specific directory
        
        cleanmymac optimize                 Free RAM and release purgeable disk space
        cleanmymac optimize ram             Release inactive memory
        cleanmymac optimize purgeable       Release purgeable disk space
        
        cleanmymac config                   Manage CLI preferences
        
        cleanmymac ignore list              Show ignored paths
        cleanmymac ignore add <path>        Add a path to the ignore list
        cleanmymac ignore remove <path>     Remove a path from the ignore list
        
        cleanmymac --help                   Show all commands and options
        cleanmymac --version                Show the installed version
        
        cleanmymac cat                      Summon a friend
        
        Esc Back to menu  ·  Q Quit
        beta · cleanmymac.com · lovingly crafted by MacPaw
```
> ⚠️ The `--force` flag skips interactive confirmation for supported cleanup commands. Use it only after reviewing what the command detects without the flag.

---

### Clean developer, system, and AI junk

Use `clean` for leftovers created outside individual project folders: package-manager caches, Xcode files, developer-tool data, AI-tool artifacts, user logs, and Trash.

CleanMyMac CLI scans first and groups the results by category:

```text
          $ cleanmymac clean
          
          ← Back to menu
          23.79 GB of items found
          
          Scan results
          Select items you'd like to remove
          
          ▸ ■ System Junk       631 KB  →
            ■ Dev Tools        23.43 GB →
            □ AI Junk          358.7 MB →
          
          40 items selected (23.43 GB)
          
          ↑↓←→ Navigate  ·  Enter Confirm  ·  Space Toggle  ·  A Select all
          Esc Back to menu  ·  Q Quit
          
          beta · cleanmymac.com · lovingly crafted by MacPaw
```

Press `→` to open a category and inspect its contents. Use `Space` to select or deselect individual items. Nothing is removed until you review the selection and confirm the cleanup.

After cleanup, CleanMyMac CLI shows exactly what was removed and how much space was recovered:

```
          Cleanup complete!
          
          Dev Tools
              ✓ Homebrew       6.61 GB
              ✓ npm            5.03 GB
              ✓ Yarn           3.3 GB
              ✓ pnpm           4.72 GB
              ✓ pip            3.77 GB
          
          AI Junk
              ✓ Claude       358.7 MB
          
          
          ────────────────────────────────────────────────────────────
          
                ____________
               /  23.79 GB  \
              /   cleaned!   \
             └────────────────┘
                    ▒▒▒▒
                    ────
          
          45 items removed
          
          Run cleanmymac ignore add <path> to protect a path
          Run cleanmymac clean --force to clean without confirmation
          
          ────────────────────────────────────────────────────────────
          
          Esc Back to menu  ·  Q Quit
          beta · cleanmymac.com · lovingly crafted by MacPaw
```

Run all cleanup categories together:

```bash
          cleanmymac clean
```

Or scan only one category:

```bash
          cleanmymac clean junk
          cleanmymac clean dev
          cleanmymac clean trash
```

> [!TIP] Use `clean` for shared caches and tool-generated junk. Use `purge` for removable dependencies and build artifacts stored inside your project folders.

---

### Purge project artifacts

Use `purge` to find generated files that accumulate inside development projects, such as `node_modules`, build directories, virtual environments, and compiled dependencies.

By default, it scans common project locations:

        - `~/Projects`
        - `~/Code`
        - `~/dev`
        - `~/GitHub`
        - `~/Workspace`

Results are grouped by project so you can understand what each artifact belongs to before removing it:

```text
          $ cleanmymac purge
          
          Scanning ~/Projects, ~/Code, ~/dev, ~/GitHub, ~/Workspace…
          
          Found 18.5 GB across 8 projects
          
            ☑ my-react-app      3.2 GB   node_modules
            ☑ rust-service      4.1 GB   target
            ☑ django-api        2.3 GB   .venv
            ☑ next-blog         1.9 GB   node_modules
            ☐ current-work      856 MB   node_modules   recent
          
          Artifacts newer than 7 days are shown but left unchecked.
          
          ↑↓ Navigate  ·  Enter Confirm  ·  Space Toggle  ·  A Select all
          Esc Back to menu  ·  Q Quit
          
          beta · cleanmymac.com · lovingly crafted by MacPaw
```

Artifacts older than seven days are preselected. More recent artifacts remain visible but unchecked, reducing the risk of removing files from active projects.

Scan the default project folders:

```bash
          cleanmymac purge
```

Or provide a specific directory:

```bash
          cleanmymac purge ~/Work/client-project
```

> [!NOTE] `purge` removes generated artifacts, not project source code. Review every selected path before confirming, especially when scanning custom directories.

---

### Analyze disk usage

Use `analyze` when you want to understand where your storage has gone before deciding what to clean.

It opens an interactive explorer that sorts directories by size and lets you navigate deeper into the file system:

```text
          $ cleanmymac analyze
          
          252.66 GB of 494.38 GB free
          
          ▸ □ Users          109.08 GB │ 60.3%  ████████████████████░░░░░░░░░░░  →
            □ Library         26.36 GB │ 14.6%  █████░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ System          20.36 GB │ 11.3%  ████░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ Applications    17.35 GB │  9.6%  ███░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ private          6.57 GB │  3.6%  █░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ usr              1.05 GB │  0.6%  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ opt             200.1 MB │  0.1%  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ bin               4.9 MB │  0.0%  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ sbin              2.5 MB │  0.0%  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
            □ Other (10 items) Zero KB │  0.0%  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  →
          
          ↑↓←→ Navigate  ·  ⌫ Delete  ·  Space Toggle  ·  A Select all
          O Reveal in Finder  ·  Esc Back to menu  ·  Q Quit
          
          beta · cleanmymac.com · lovingly crafted by MacPaw
```

Use the arrow keys to navigate through folders, or press `O` to reveal the selected item in Finder.

Removing an item requires an explicit selection and confirmation. Simply browsing through `analyze` does not modify your files.

Analyze your home directory:

```bash
          cleanmymac analyze
```

Or start from a specific path:

```bash
          cleanmymac analyze ~/Projects
```

> [!TIP] Start with `cleanmymac analyze` when you know your disk is full but are not yet sure what is safe or useful to remove.

### Optimize your Mac

Use `optimize` for lightweight maintenance tasks that do not scan project files or developer caches.

Run all available optimization tasks:

```bash
          cleanmymac optimize
```

Or run them separately:

```bash
          cleanmymac optimize ram
          cleanmymac optimize purgeable
```

- `optimize ram` releases inactive memory that macOS can make available to running applications.
- `optimize purgeable` asks macOS to release disk space already marked as purgeable.

These commands do not remove project source code or personal documents.

### Protect important paths

Add folders to the ignore list when they should never appear in CleanMyMac CLI scan results:

```bash
          cleanmymac ignore add ~/Projects/important-project
```

Review all ignored paths:

```bash
          cleanmymac ignore list
```

Remove a path when you want it to appear in scans again:

```bash
          cleanmymac ignore remove ~/Projects/important-project
```

Ignored paths remain excluded until you remove them from the list.

---

### Configure CleanMyMac CLI

Open the configuration menu to manage CLI preferences, including analytics and cleanup behavior:

```bash
          cleanmymac config
```

Configuration changes persist between sessions.

---

### Summon a friend

Some maintenance tasks are better with company:

```bash
          cleanmymac cat
```

---



## Documentation

New to CleanMyMac CLI? [Wiki](https://github.com/MacPaw/cleanmymac-cli/wiki/Getting-Started)

## Built for real developer workflows

CleanMyMac CLI was built around the workflows our own developers face every day. The CleanMyMac team uses it on our own Macs to clean development artifacts, inspect storage, and keep working environments under control.

> 🩷 **We use the same commands we ship to you.**


## Feedback & Support

> CleanMyMac CLI is in public beta and not yet feature-complete — expect commands and behavior to evolve.

We'd love to hear from you. For bugs and feature requests, open an issue on the [issue tracker](https://github.com/macpaw/cleanmymac-cli/issues).

For other questions, contact [MacPaw Support](https://support.macpaw.com).


## Using CleanMyMac CLI?

⭐ **Star this repository** to follow the Public Beta and help other developers discover the project.

💬 [Join GitHub Discussions](https://github.com/MacPaw/cleanmymac-cli/discussions)

📰 [Meet CleanMyMac CLI](https://macpaw.com/news/cleanmymac-cli)

## Prefer a visual interface?

[CleanMyMac Desktop](https://cleanmymac.com) provides broader whole-Mac cleanup, application management, malware protection, and performance tools through a visual review interface.
CleanMyMac CLI focuses on terminal-first developer cleanup and is not intended to replace the desktop app.

## Security

For security reporting and supported versions, see our [Security Policy](SECURITY.md).

## License

CleanMyMac CLI is proprietary software owned by MacPaw Way Ltd.

© 2026 MacPaw Way Ltd. All rights reserved.

The use of this software is subject to the terms and conditions set forth in the End User License Agreement [LICENSE](LICENSE) attached to this repository and [Privacy Policy](https://macpaw.com/legal/cleanmymac-privacy-policy) available at https://macpaw.com/legal/cleanmymac-privacy-policy. 

By using this software, you agree to be bound by the terms of that license and the Privacy Policy.

