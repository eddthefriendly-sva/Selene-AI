# Selene

Selene is a terminal assistant that sends prompts to a local Ollama model. Prompts stay on your machine unless you explicitly enable DuckDuckGo search with `--search`.

## Install on Windows

In PowerShell, from this folder:

```powershell
python -m pip install -e .
```

On first run, Selene checks for its search dependency, Ollama, and the configured model. It installs a missing `ddgs` package with pip, installs Ollama through `winget`, and pulls the model with `ollama pull`. First run therefore needs an internet connection and may download several gigabytes for the model. If `winget` is unavailable, install Ollama from https://ollama.com/download.

If the `Selene` command is not found after installation, add your Python `Scripts` folder to `PATH` and open a new terminal. Selene starts Ollama's local service when needed.

## Use

```powershell
Selene
Selene "Explain this PowerShell error"
Selene --search "What changed in Python 3.14?"
Selene --model qwen2.5-coder:14b "Review this design"
```

Run `Selene` by itself to enter interactive mode. Type questions at the `You>` prompt and enter `exit` or `quit` to leave. Add `--search` when starting Selene to use DuckDuckGo for each interactive question.

By default Selene uses `qwen2.5-coder:7b`. Set `SELENE_MODEL` to choose another default. When the default is unavailable, Selene uses an installed model whose name includes both `qwen` and `coder`.
