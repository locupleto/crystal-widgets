# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Crystal-widgets is a set of macOS desktop system monitoring widgets for the [Übersicht](http://tracesof.net/uebersicht/) widget framework. Supports Apple Silicon and Intel Macs, compatible with macOS Tahoe (26.x) and earlier.

## Architecture

**Data flow:** Übersicht calls a shell script (`widget_runner.sh` or `widget_script.sh`) on a timer → script outputs semicolon-separated values to stdout → CoffeeScript `update()` function parses the string and updates the DOM via jQuery.

**Key components:**
- `crystal_common.sh` — shared configuration (temp dir, bar colors, tool paths for `flock` and `fastfetch`)
- `crystal_htop_runner.sh` — process manager ensuring a single headless `crystal-htop` instance runs via `screen`, using `flock` for mutex. Writes per-CPU, memory, swap, and task metrics to small text files in `$HTOP_TEMP_DIR`
- `crystal_htop_arm64` / `crystal_htop_x86` — custom htop binaries from [crystal-htop](https://github.com/locupleto/crystal-htop) that log metrics to temp files
- Each `.widget/` directory contains `index.coffee` (UI + parsing) and optionally a shell script (data collection)

**Widget pattern (index.coffee):**
```coffeescript
command: "widget-name.widget/widget_runner.sh"   # shell script for data
refreshFrequency: 2000                            # ms between updates
style: """ ... """                                 # CSS/LESS styling
render: -> """ <html> """                          # initial DOM
update: (output, domEl) ->                         # parse output, update DOM with jQuery
```

## Repository vs Installed Widgets

- **This repo** contains `crystal.widget.zip` (the distribution archive) plus README and metadata
- **Installed widgets** live at `/Users/urban/config/ubersicht/` (the Übersicht widgets directory)
- The zip contains a `put_into_widgets_folder/` directory with all widget dirs, shared scripts, and binaries

## Packaging Workflow

There is no build system. To update the distribution after modifying installed widget files:

```bash
# From a temp directory, extract the existing zip, copy in changed files, re-zip:
cd /tmp && mkdir update && cd update
unzip /Volumes/Work/development/projects/git/crystal-widgets/crystal.widget.zip
cp /Users/urban/config/ubersicht/<changed-files> put_into_widgets_folder/
zip -r /Volumes/Work/development/projects/git/crystal-widgets/crystal.widget.zip put_into_widgets_folder/
```

## Dependencies

Required: `flock` (Homebrew), `fastfetch` (Homebrew), `screen` (built-in), `system_profiler` (built-in).

## Known Gotchas

- `system_profiler` on macOS Tahoe (26.x) emits `hw.cpufamily` debug lines to stdout/stderr. Always use `2>/dev/null` when calling it in widget scripts.
- Shell script output must be clean — any stray lines break the semicolon-based parsing in CoffeeScript.
- The `crystal_common.sh` paths (`FLOCK_CMD`, `FASTFETCH_CMD`) are installation-specific and must match the user's Homebrew prefix.
