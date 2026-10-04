# Selene

Selene is a terminal assistant that sends prompts to a local Ollama model. It automatically uses DuckDuckGo for likely identity, biography, or current-information questions; those matching queries are sent to DuckDuckGo.

## Install on Windows

In PowerShell, from this folder:

```powershell
python -m pip install -e .
```

On first run, Selene checks for its search dependency, tray libraries, Ollama, and the configured model. It installs missing Python packages with pip, installs Ollama through `winget`, and pulls the model with `ollama pull`. First chat run therefore needs an internet connection and may download several gigabytes for the model. If `winget` is unavailable, install Ollama from https://ollama.com/download.

If the `Selene` command is not found after installation, add your Python `Scripts` folder to `PATH` and open a new terminal. Selene starts Ollama's local service when needed.

## Use

```powershell
Selene
Selene --chat
Selene "Explain this PowerShell error"
Selene "Who is Ada Lovelace?"
Selene --no-search "Who is Ada Lovelace?"
Selene --search "Explain this PowerShell error"
Selene --model qwen2.5-coder:14b "Review this design"
```

On Windows, running `Selene` starts a detached tray process and immediately returns to the terminal or closes the launch window. The tray icon stays active; click it to open a chat console, or right-click and choose **Exit Selene** to stop the background process. Use `Selene --chat` to open the interactive terminal directly. In chat mode, type questions at `You>` and enter `exit` or `quit` to leave. Search is automatic for likely lookups; add `--search` to always search or `--no-search` to keep every prompt local.

By default Selene uses `qwen2.5-coder:7b`. Set `SELENE_MODEL` to choose another default. When the default is unavailable, Selene uses an installed model whose name includes both `qwen` and `coder`.

## Build a Windows executable

Run these commands from PowerShell in the project folder:

```powershell
python -m pip install -e ".[build]"
python build_windows.py
```

The single-file executable is written to `dist\Selene.exe`. It includes Selene, DuckDuckGo search, tray support, and the supplied crystal-style icon. Launching it creates a detached tray process and closes the launch window. Ollama and the Qwen model stay separate and are installed on first chat use; the model is several gigabytes, so it is not bundled into the executable.

To publish a GitHub release automatically, push a version tag such as `v0.1.0`. The Windows workflow builds the executable and attaches it to the release.
