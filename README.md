# Quicksave

**Pick up exactly where you left off.**

You are deep in a problem. A meeting pops up, a message pulls you away, the laptop closes for the night. When you come back, the windows are gone and the thread of thought is gone with them. You spend the next twenty minutes rebuilding a mental state you had perfectly a moment ago.

Quicksave gives your work a save point. Press it before you step away and it freezes everything that matters. Come back later, load the save point, and your workspace rebuilds itself in seconds.

## The cost this removes

Research by Gloria Mark at UC Irvine found that interrupted work takes about 23 minutes to resume, usually after drifting through several unrelated tasks first. The expensive part of an interruption is the reconstruction of what you were doing. Quicksave stores that state so the reconstruction is free.

A knowledge worker loses hours every week to this. Quicksave hands those hours back.

## What a save point captures

- **Browser tabs** across every window, so your research context returns intact
- **Terminal directories** for each shell you had open
- **VS Code workspaces**, including open files and unsaved edits through VS Code hot exit
- **Claude Code and Codex sessions**, resumed by their exact session id in the same place they were running
- **Your intent**, one line plus optional notes on what you were about to do next

Everything stays on your machine as small local files. Nothing is uploaded, no account is required, and your work never touches a server.

## How it feels

A meeting starts in two minutes. You press your hotkey, type "reworking the IPCW weights, third column unit looks wrong," and walk away. An hour later you load that save point. Your tabs return, your terminals land back in the right folders, VS Code reopens your project, and your Claude Code conversation continues where it stopped. The note reminds you of the exact thought you had. You are working again inside ten seconds.

## Smart restore

Quicksave restores the difference, so it stays out of your way.

- Only tabs that are gone get reopened. Anything still open stays as it is.
- Terminal directories already in use are left alone.
- AI sessions return to the host they came from. A session that lived in the VS Code integrated terminal reopens there, and a Terminal session goes back to a terminal window.
- Every load ends with a plain report of what reopened, what was already there, and what was skipped.

## Install

```sh
git clone https://github.com/mia-mz/QuickSave.git ~/Projects/quicksave
echo "alias qs='python3 ~/Projects/quicksave/quicksave.py'" >> ~/.zshrc
```

Requires Python 3.9 or newer. Standard library only, so there is nothing else to install.

## Usage

```
qs save -m "title" [-n "notes"] [-p project]   create a save point
qs list                                        list save points
qs load [index]                                restore one
qs ui                                           web panel at 127.0.0.1:7799
qs doctor                                       check macOS permissions
```

On macOS you can bind `qs` to a global hotkey with the Shortcuts app. Add a "Run Shell Script" action containing `python3 ~/Projects/quicksave/quicksave.py` and assign it a keyboard shortcut.

## Platform support

| Capability                 | macOS | Linux    | Windows  |
|----------------------------|:-----:|:--------:|:--------:|
| Browser tabs (capture)     | Yes   | Planned  | Planned  |
| Browser tabs (reopen)      | Yes   | Yes      | Yes      |
| Terminal directories       | Yes   | Yes      | Planned  |
| VS Code workspaces         | Yes   | Yes      | Yes      |
| Claude Code / Codex resume | Yes   | Yes      | Planned  |
| Web panel                  | Yes   | Yes      | Yes      |

macOS has full support today. Linux and Windows cover the core and are open for contributions on the remaining backends.

## Permissions on macOS

Two one time grants unlock the full experience.

- **Automation** lets your terminal control Chrome, Safari, Terminal, and System Events. macOS asks the first time you use it.
- **Accessibility** lets Quicksave type a resume command into the VS Code integrated terminal. Run `qs doctor` to see whether it is on and which app to authorize. Until you grant it, AI sessions still open inside VS Code with the command ready on your clipboard, so one paste finishes the job.

## License

MIT
