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

On Windows, running `Selene` starts the tray icon. Click it to open a chat console; right-click for chat and exit options. Use `Selene --chat` to open the interactive terminal directly. In chat mode, type questions at `You>` and enter `exit` or `quit` to leave. Search is automatic for likely lookups; add `--search` to always search or `--no-search` to keep every prompt local.

By default Selene uses `qwen2.5-coder:7b`. Set `SELENE_MODEL` to choose another default. When the default is unavailable, Selene uses an installed model whose name includes both `qwen` and `coder`.
