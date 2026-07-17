<div align="center">

# CleanMyMac CLI

**Clean, analyze, and optimize your Mac from the terminal.**

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

- macOS 11 or later
- [Homebrew](https://brew.sh)

## Installation
> The formula lives in our tap — [MacPaw/homebrew-taps](https://github.com/MacPaw/homebrew-taps).


Install it with Homebrew:

```bash
brew install --cask macpaw/taps/cleanmymac-cli
```

Verify that the installation was successful:

```bash
cleanmymac --version
```

View all available commands and options:

```bash
cleanmymac --help
```

View menu:

```bash
cleanmymac
```

## Quick Start

> CleanMyMac CLI scans first and lets you review detected items before anything is removed.
> Both `cmm` and `cleanmymac` run the same tool — this README uses the `cleanmymac` in examples.

### Clean developer junk

> Scan for developer caches, build leftovers, package-manager files, and other removable junk:

```bash
cleanmymac clean
```

Review the results and select what you want to remove.

### Purge project artifacts

> Find removable artifacts across your common project folders:

```bash
cleanmymac purge
```

You can also scan a specific directory:

```bash
cleanmymac purge ~/Projects
```

Artifacts are grouped by project so you can review them before cleanup.

### Analyze disk usage

> Open an interactive disk usage explorer:

```bash
cleanmymac analyze
```

Or analyze a specific directory:

```bash
cleanmymac analyze ~/Projects
```

`analyze` is read-only and does not remove files.

> 💡 Not sure where to begin? Start with `cleanmymac analyze` to understand what is consuming your storage.

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

</details>
> Artifacts older than seven days are preselected. Newer artifacts remain visible but are left unchecked for manual review.

## Safety

CleanMyMac CLI is designed to avoid destructive cleanup actions. By default, every command shows what it will remove and asks for confirmation before deleting. Safety features include:

- Interactive review before deletion (clean, purge)
- Protected system locations are excluded from cleanup.
- An ignore list to permanently protect specific paths from `clean`, `purge`, and `analyze` (`cleanmymac ignore add <path>`)
- During `purge`, only artifacts older than seven days are preselected.
- `analyze` is read-only and never removes files.
- Cleanup detection is based on logic shared with CleanMyMac.

Add a path to the ignore list:

```bash
cleanmymac ignore add ~/Projects/important-project
```

Review ignored paths:

```bash
cleanmymac ignore list
```

> ⚠️ The `--force` flag skips the confirmation prompt and deletes detected items immediately. Use it only when you understand exactly what the command will remove.



## Features in Detail

> CleanMyMac CLI can be used either through its interactive menu or by running commands directly.

Run `cleanmymac` without a subcommand to open the main menu:

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
Prefer direct commands? Use any command without opening the menu:

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

Press `→` to open a category and inspect its contents. Use `Space` to select or deselect individual items.

Nothing is removed until you review the selection and confirm the cleanup.

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

### Configure CleanMyMac CLI

Open the configuration menu to manage CLI preferences, including analytics and cleanup behavior:

```bash
          cleanmymac config
```

Configuration changes persist between sessions.

### Summon a friend

Some maintenance tasks are better with company:

```bash
          cleanmymac cat
```

## Beta

CleanMyMac CLI is in public beta and not yet feature-complete — expect commands and behavior to evolve.


## Prefer a visual interface?

[CleanMyMac Desktop](https://cleanmymac.com) provides broader whole-Mac cleanup, application management, malware protection, and performance tools through a visual review interface.

CleanMyMac CLI is focused on terminal-first developer cleanup and is not intended to replace the desktop app.

## Feedback & Support

We'd love to hear from you. For bugs and feature requests, open an issue on the [issue tracker](https://github.com/macpaw/cleanmymac-cli/issues).

For other questions, contact [MacPaw Support](https://support.macpaw.com).


## Security

For security reporting and supported versions, see our [Security Policy](SECURITY.md).

## License

CleanMyMac CLI is proprietary software owned by MacPaw Way Ltd.

© 2026 MacPaw Way Ltd. All rights reserved.

The use of this software is subject to the terms and conditions set forth in the End User License Agreement [LICENSE](LICENSE) attached to this repository and [Privacy Policy](https://macpaw.com/legal/cleanmymac-privacy-policy) available at https://macpaw.com/legal/cleanmymac-privacy-policy. 

By using this software, you agree to be bound by the terms of that license and the Privacy Policy.

